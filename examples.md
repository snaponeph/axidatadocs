---
description: Research Agent
---

# Examples

Let’s build a research agent to generate a report using Exa.

1

Create a research agent

research\_agent.py

Copy

```
from textwrap import dedent
from datetime import datetime

from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.exa import ExaTools

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    tools=[ExaTools(start_published_date=datetime.now().strftime("%Y-%m-%d"), type="keyword")],
    description="You are an advanced AI researcher writing a report on a topic.",
    instructions=[
        "For the provided topic, run 3 different searches.",
        "Read the results carefully and prepare a NYT worthy report.",
        "Focus on facts and make sure to provide references.",
    ],
    expected_output=dedent("""\
    An engaging, informative, and well-structured report in markdown format:

    ## Engaging Report Title

    ### Overview
    {give a brief introduction of the report and why the user should read this report}
    {make this section engaging and create a hook for the reader}

    ### Section 1
    {break the report into sections}
    {provide details/facts/processes in this section}

    ... more sections as necessary...

    ### Takeaways
    {provide key takeaways from the article}

    ### References
    - [Reference 1](link)
    - [Reference 2](link)
    - [Reference 3](link)

    - published on {date} in dd/mm/yyyy
    """),
    markdown=True,
    show_tool_calls=True,
    add_datetime_to_instructions=True,
    save_response_to_file="tmp/{message}.md",
)
agent.print_response("Simulation theory", stream=True)
```

2

Run the agent

Install libraries

Copy

```
pip install openai exa-py AxiData
```

Run the agent

Copy

```
python research_agent.py
```

View the report

Copy

```
cat tmp/Simulation theory.md
```

#### [​](https://docs.phidata.com/more-examples#agentic-rag)Agentic RAG <a href="#agentic-rag" id="agentic-rag"></a>

We were the first to pioneer Agentic RAG using our Auto-RAG paradigm. With Agentic RAG (or auto-rag), the Agent can search its knowledge base (vector db) for the specific information it needs to achieve its task, instead of always inserting the “context” into the prompt.

This saves tokens and improves response quality.

1

Create a RAG agent

rag\_agent.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.embedder.openai import OpenAIEmbedder
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.lancedb import LanceDb, SearchType

# Create a knowledge base from a PDF
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    # Use LanceDB as the vector database
    vector_db=LanceDb(
        table_name="recipes",
        uri="tmp/lancedb",
        search_type=SearchType.vector,
        embedder=OpenAIEmbedder(model="text-embedding-3-small"),
    ),
)
# Comment out after first run as the knowledge base is loaded
knowledge_base.load()

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    # Add the knowledge base to the agent
    knowledge=knowledge_base,
    show_tool_calls=True,
    markdown=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup", stream=True)
```

2

Run the agent

Install libraries

Copy

```
pip install lancedb tantivy pypdf sqlalchemy
```

Run the agent

Copy

```
python rag_agent.py
```

#### [​](https://docs.phidata.com/more-examples#structured-outputs)Structured Outputs <a href="#structured-outputs" id="structured-outputs"></a>

Agents can return their output in a structured format as a Pydantic model.

Create a file `structured_output.py`

1

Create a structured output agent

structured\_output.py

Copy

```
from typing import List
from pydantic import BaseModel, Field
from phi.agent import Agent
from phi.model.openai import OpenAIChat

# Define a Pydantic model to enforce the structure of the output
class MovieScript(BaseModel):
    setting: str = Field(..., description="Provide a nice setting for a blockbuster movie.")
    ending: str = Field(..., description="Ending of the movie. If not available, provide a happy ending.")
    genre: str = Field(..., description="Genre of the movie. If not available, select action, thriller or romantic comedy.")
    name: str = Field(..., description="Give a name to this movie")
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(..., description="3 sentence storyline for the movie. Make it exciting!")

# Agent that uses JSON mode
json_mode_agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    description="You write movie scripts.",
    response_model=MovieScript,
)
# Agent that uses structured outputs
structured_output_agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    description="You write movie scripts.",
    response_model=MovieScript,
    structured_outputs=True,
)

json_mode_agent.print_response("New York")
structured_output_agent.print_response("New York")
```

2

Run the agent

Copy

```
python structured_output.py
```

#### [​](https://docs.phidata.com/more-examples#reasoning-agent)Reasoning Agent <a href="#reasoning-agent" id="reasoning-agent"></a>

Reasoning is an experimental feature that helps agents work through a problem step-by-step, backtracking and correcting as needed.

1

Create a reasoning agent

reasoning\_agent.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = (
    "Three missionaries and three cannibals need to cross a river. "
    "They have a boat that can carry up to two people at a time. "
    "If, at any time, the cannibals outnumber the missionaries on either side of the river, the cannibals will eat the missionaries. "
    "How can all six people get across the river safely? Provide a step-by-step solution and show the solutions as an ascii diagram"
)

reasoning_agent = Agent(model=OpenAIChat(id="gpt-4o"), reasoning=True, markdown=True, structured_outputs=True)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

2

Run the reasoning agent

Copy

```
python reasoning_agent.py
```

Reasoning is an experimental feature and will break \~20% of the time. **It is not a replacement for o1.** It is an experiment that combines COT and tool use. Set your expectations very low for this initial release. For example: It will not be able to count ‘r’s in ‘strawberry’.

[\
](https://axidata.gitbook.io/axidata/agent-ui)
