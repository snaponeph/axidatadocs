# Agentic Chunking

Agentic chunking is an intelligent method of splitting documents into smaller chunks by using an LLM to determine natural breakpoints in the text. Rather than splitting text at fixed character counts,

#### Usage <a href="#usage" id="usage"></a>

Copy

```
from phi.agent import Agent
from phi.document.chunking.agentic import AgenticChunking
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes_agentic_chunking", db_url=db_url),
    chunking_strategy=AgenticChunking(),
)
knowledge_base.load(recreate=False)  # Comment out after first run

agent = Agent(
    knowledge_base=knowledge_base,
    search_knowledge=True,
)

agent.print_response("How to make Thai curry?", markdown=True)
```

#### [​](https://docs.phidata.com/chunking/agentic-chunking#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`model`

`Model`

`OpenAIChat`

The model to use for chunking.

`max_chunk_size`

`int`

`5000`

The maximum size of each chunk.
