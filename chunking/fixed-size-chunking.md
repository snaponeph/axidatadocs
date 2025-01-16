# Fixed Size Chunking

Fixed size chunking is a method of splitting documents into smaller chunks of a specified size, with optional overlap between chunks. This is useful when you want to process large documents in smaller, manageable pieces.



#### Usage <a href="#usage" id="usage"></a>

Copy

```
from phi.agent import Agent
from phi.document.chunking.fixed import FixedSizeChunking
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes_fixed_size_chunking", db_url=db_url),
    chunking_strategy=FixedSizeChunking(),
)
knowledge_base.load(recreate=False)  # Comment out after first run

agent = Agent(
    knowledge_base=knowledge_base,
    search_knowledge=True,
)

agent.print_response("How to make Thai curry?", markdown=True)
```

#### [​](https://docs.phidata.com/chunking/fixed-size-chunking#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`chunk_size`

`int`

`5000`

The maximum size of each chunk.

`overlap`

`int`

`0`

The number of characters to overlap between chunks.
