---
description: Agents use knowledge to supplement their training data with domain expertise.
---

# Knowledge

Knowledge is stored in a vector database and provides agents with business context at query time, helping them respond in a context-aware manner. The general syntax is:

Copy

```
from phi.agent import Agent, AgentKnowledge

# Create a knowledge base for the Agent
knowledge_base = AgentKnowledge(vector_db=...)

# Add information to the knowledge base
knowledge_base.load_text("The sky is blue")

# Add the knowledge base to the Agent and
# give it a tool to search the knowledge base as needed
agent = Agent(knowledge=knowledge_base, search_knowledge=True)
```

#### [​](https://docs.phidata.com/agents/knowledge#vector-databases)Vector Databases <a href="#vector-databases" id="vector-databases"></a>

While any type of storage can act as a knowledge base, vector databases offer the best solution for retrieving relevant results from dense information quickly. Here’s how vector databases are used with Agents:

1

Chunk the information

Break down the knowledge into smaller chunks to ensure our search query returns only relevant results.

2

Load the knowledge base

Convert the chunks into embedding vectors and store them in a vector database.

3

Search the knowledge base

When the user sends a message, we convert the input message into an embedding and “search” for nearest neighbors in the vector database.

#### [​](https://docs.phidata.com/agents/knowledge#example-rag-agent-with-a-pdf-knowledge-base)Example: RAG Agent with a PDF Knowledge Base <a href="#example-rag-agent-with-a-pdf-knowledge-base" id="example-rag-agent-with-a-pdf-knowledge-base"></a>

Let’s build a **RAG Agent** that answers questions from a PDF.

[**​**](https://docs.phidata.com/agents/knowledge#step-1-run-pgvector)**Step 1: Run PgVector**

Let’s use `PgVector` as our vector db as it can also provide storage for our Agents.

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **PgVector** on port **5532** using:

Copy

```
docker run -d \
  -e POSTGRES_DB=ai \
  -e POSTGRES_USER=ai \
  -e POSTGRES_PASSWORD=ai \
  -e PGDATA=/var/lib/postgresql/data/pgdata \
  -v pgvolume:/var/lib/postgresql/data \
  -p 5532:5432 \
  --name pgvector \
  phidata/pgvector:16
```

[**​**](https://docs.phidata.com/agents/knowledge#step-2-traditional-rag)**Step 2: Traditional RAG**

Retrieval Augmented Generation (RAG) means **“stuffing the prompt with relevant information”** to improve the model’s response. This is a 2 step process:

1. Retrieve relevant information from the knowledge base.
2. Augment the prompt to provide context to the model.

Let’s build a **traditional RAG** Agent that answers questions from a PDF of recipes.

1

Install libraries

Install the required libraries using pip

MacWindows

Copy

```
pip install -U pgvector pypdf "psycopg[binary]" sqlalchemy
```

2

Create a Traditional RAG Agent

Create a file `traditional_rag.py` with the following contents

traditional\_rag.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
knowledge_base = PDFUrlKnowledgeBase(
    # Read PDF from this URL
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    # Store embeddings in the `ai.recipes` table
    vector_db=PgVector(table_name="recipes", db_url=db_url, search_type=SearchType.hybrid),
)
# Load the knowledge base: Comment after first run
knowledge_base.load(upsert=True)

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    knowledge=knowledge_base,
    # Enable RAG by adding references from AgentKnowledge to the user prompt.
    add_context=True,
    # Set as False because Agents default to `search_knowledge=True`
    search_knowledge=False,
    markdown=True,
    # debug_mode=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup")
```

3

Run the agent

Run the agent (it takes a few seconds to load the knowledge base).

MacWindows

Copy

```
python traditional_rag.py
```

How to use local PDFs

[**​**](https://docs.phidata.com/agents/knowledge#step-3-agentic-rag)**Step 3: Agentic RAG**

With traditional RAG above, `add_context=True` always adds information from the knowledge base to the prompt, regardless of whether it is relevant to the question or helpful.

With Agentic RAG, we let the Agent decide **if** it needs to access the knowledge base and what search parameters it needs to query the knowledge base.

Set `search_knowledge=True` and `read_chat_history=True`, giving the Agent tools to search its knowledge and chat history on demand.

1

Create an Agentic RAG Agent

Create a file `agentic_rag.py` with the following contents

agentic\_rag.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes", db_url=db_url, search_type=SearchType.hybrid),
)
# Load the knowledge base: Comment out after first run
knowledge_base.load(upsert=True)

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    knowledge=knowledge_base,
    # Add a tool to search the knowledge base which enables agentic RAG.
    search_knowledge=True,
    # Add a tool to read chat history.
    read_chat_history=True,
    show_tool_calls=True,
    markdown=True,
    # debug_mode=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup", stream=True)
agent.print_response("What was my last question?", markdown=True)
```

2

Run the agent

Run the agent

MacWindows

Copy

```
python agentic_rag.py
```

Notice how it searches the knowledge base and chat history when needed

#### [​](https://docs.phidata.com/agents/knowledge#attributes)Attributes <a href="#attributes" id="attributes"></a>

ParameterTypeDefaultDescription

`knowledge`

`AgentKnowledge`

`None`

Provides the knowledge base used by the agent.

`search_knowledge`

`bool`

`True`

Adds a tool that allows the Model to search the knowledge base (aka Agentic RAG). Enabled by default when `knowledge` is provided.

`add_context`

`bool`

`False`

Enable RAG by adding references from AgentKnowledge to the user prompt.

`retriever`

`Callable[..., Optional[list[dict]]]`

`None`

Function to get context to add to the user message. This function is called when add\_context is True.

`context_format`

`Literal['json', 'yaml']`

`json`

Specifies the format for RAG, either “json” or “yaml”.

`add_context_instructions`

`bool`

`False`

If True, add instructions for using the context to the system prompt (if knowledge is also provided). For example: add an instruction to prefer information from the knowledge base over its training data.
