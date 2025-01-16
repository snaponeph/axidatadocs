---
description: >-
  The S3TextKnowledgeBase reads text files from an S3 bucket, converts them into
  vector embeddings and loads them to a vector databse.
---

# S3 Text Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

Copy

```
pip install textract
```

Copy

```
from phi.knowledge.s3.text import S3TextKnowledgeBase
from phi.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = S3TextKnowledgeBase(
    bucket_name="phi-public",
    key="recipes/recipes.docx",
    vector_db=PgVector(table_name="recipes", db_url=db_url),
)
```

Then use the `knowledge_base` with an `Agent`:

Copy

```
from phi.agent import Agent
from knowledge_base import knowledge_base

agent = Agent(
    knowledge=knowledge_base,
    search_knowledge=True,
)
agent.knowledge.load(recreate=False)

agent.print_response("How to make Hummus?")
```

#### [​](https://docs.phidata.com/knowledge/s3_text#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`formats`

`List[str]`

`[".doc", ".docx"]`

Formats accepted by this knowledge base.

`reader`

`S3TextReader`

`S3TextReader()`

A `S3TextReader` that converts the `Text` files into `Documents` for the vector database.

`vector_db`

`VectorDb`

\-

Vector Database for the Knowledge Base.

`num_documents`

`int`

`5`

Number of documents to return on search.

`optimize_on`

`int`

\-

Number of documents to optimize the vector db on.

`chunking_strategy`

`ChunkingStrategy`

`FixedSizeChunking`

The chunking strategy to use.

[\
](https://VixData.gitbook.io/VixData/documentation/knowledge/s3-pdf-knowledge-base)
