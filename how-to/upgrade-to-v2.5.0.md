# Upgrade to v2.5.0

## Upgrade to v2.5.0

#### Key Changes <a href="#key-changes" id="key-changes"></a>

1. Constructor: `Assistant()` -> `Agent()`
2. LLM/Model: `llm` -> `model`
3. Knowledge Base: `knowledge_base` -> `knowledge`
4. RunResponse: Pydantic model for string response
5. Structured Output: Changes in how structured output is handled

#### [​](https://docs.phidata.com/migration/2-5-0#detailed-migration-steps)Detailed Migration Steps <a href="#detailed-migration-steps" id="detailed-migration-steps"></a>

[**​**](https://docs.phidata.com/migration/2-5-0#1-update-import-statements)**1. Update Import Statements**

Copy

```
# Version < 2.5.0
from phi.assistant import Assistant
from phi.llm.openai import OpenAIChat
from phi.storage.assistant.postgres import PgAssistantStorage

# Version >= 2.5.0
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.storage.agent.postgres import PgAgentStorage
```

[**​**](https://docs.phidata.com/migration/2-5-0#2-update-arguments)**2. Update Arguments**

Replace `llm` with `model` and `model` with `id`.

Copy

```
# Version < 2.5.0
from phi.assistant import Assistant
from phi.llm.openai import OpenAIChat

assistant = Assistant(
    llm=OpenAIChat(model="gpt-4o"),
)

# Version >= 2.5.0
from phi.agent import Agent
from phi.model.openai import OpenAIChat

agent = Agent(
    # Note: 'llm' is now 'model' and 'model' is now 'id'
    model=OpenAIChat(id="gpt-4o"),
)
```

[**​**](https://docs.phidata.com/migration/2-5-0#3-update-knowledge-base)**3. Update Knowledge Base**

Replace `knowledge_base` with `knowledge`.

Copy

```
# Version < 2.5.0
from phi.assistant import Assistant
from phi.storage.assistant.postgres import PgAssistantStorage
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector2
from phi.llm.openai import OpenAIChat

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector2(collection="recipes", db_url=db_url),
)

# Comment out after first run
knowledge_base.load()

storage = PgAssistantStorage(table_name="pdf_assistant", db_url=db_url)

assistant = Assistant(
    llm=OpenAIChat(model="gpt-4o"),
    knowledge_base=knowledge_base,
    search_knowledge=True, # enables agent to search knowledge base
    storage=storage,
)

res = assistant.run("What is the recipe for chicken curry?")


# Version >= 2.5.0
from phi.agent import Agent, RunResponse
from phi.storage.agent.postgres import PgAgentStorage
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector, SearchType
from phi.model.openai import OpenAIChat

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes", db_url=db_url, search_type=SearchType.hybrid),
)

# Comment out after first run
knowledge_base.load()

storage = PgAgentStorage(table_name="pdf_agent", db_url=db_url)

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    knowledge=knowledge_base,
    storage=storage,
)

response: RunResponse = agent.run("What is the recipe for chicken curry?")
res = response.content
```

[**​**](https://docs.phidata.com/migration/2-5-0#4-output-model-response-as-a-string)**4. Output model response as a string**

Copy

```
# Version < 2.5.0
from phi.assistant import Assistant
from phi.llm.openai import OpenAIChat

assistant = Assistant(
    llm=OpenAIChat(model="gpt-4o"),
)

res = assistant.run("What is the recipe for chicken curry?")

# Version >= 2.5.0
from phi.agent import Agent, RunResponse
from phi.model.openai import OpenAIChat

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
)

response: RunResponse = agent.run("What is the recipe for chicken curry?")
res = response.content
```

[**​**](https://docs.phidata.com/migration/2-5-0#5-handle-structured-outputs)**5. Handle structured outputs**

Replace `output_model` with `response_model`.

If you are using OpenAI models, you can set `structured_outputs=True` to get a structured output.

Copy

```
# Version < 2.5.0
from typing import List
from pydantic import BaseModel, Field
from rich.pretty import pprint
from phi.assistant import Assistant
from phi.llm.openai import OpenAIChat


class MovieScript(BaseModel):
    setting: str = Field(..., description="Provide a nice setting for a blockbuster movie.")
    ending: str = Field(..., description="Ending of the movie. If not available, provide a happy ending.")
    genre: str = Field(
        ..., description="Genre of the movie. If not available, select action, thriller or romantic comedy."
    )
    name: str = Field(..., description="Give a name to this movie")
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(..., description="3 sentence storyline for the movie. Make it exciting!")


movie_assistant = Assistant(
    llm=OpenAIChat(model="gpt-4-turbo-preview"),
    description="You help people write movie ideas.",
    output_model=MovieScript,
)

pprint(movie_assistant.run("New York"))

# Version >= 2.5.0
from typing import List
from rich.pretty import pprint
from pydantic import BaseModel, Field
from phi.agent import Agent, RunResponse
from phi.model.openai import OpenAIChat


class MovieScript(BaseModel):
    setting: str = Field(..., description="Provide a nice setting for a blockbuster movie.")
    ending: str = Field(..., description="Ending of the movie. If not available, provide a happy ending.")
    genre: str = Field(
        ..., description="Genre of the movie. If not available, select action, thriller or romantic comedy."
    )
    name: str = Field(..., description="Give a name to this movie")
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(..., description="3 sentence storyline for the movie. Make it exciting!")


# Agent that uses JSON mode
json_mode_agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    description="You write movie scripts.",
    response_model=MovieScript,
)

# Print the response
json_mode_agent.print_response("New York")

# Get the response in a variable
json_mode_response: RunResponse = json_mode_agent.run("New York")
pprint(json_mode_response.content)


# Agent that uses structured outputs
# Note: `structured_output` only works with OpenAI models
structured_output_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"),
    description="You write movie scripts.",
    response_model=MovieScript,
    structured_outputs=True,
)

# Print the response
structured_output_agent.print_response("New York")

# Get the response in a variable
structured_output_response: RunResponse = structured_output_agent.run("New York")
pprint(structured_output_response.content)
```
