---
description: >-
  The CSVUrlKnowledgeBase reads CSVs from urls, converts them into vector
  embeddings and loads them to a vector database.
---

# CSV URL Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

knowledge\_base.py

Copy

```
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = CSVUrlKnowledgeBase(
    urls=["csv_url"],
    # Table name: ai.csv_documents
    vector_db=PgVector(
        table_name="csv_documents",
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
    ),
)
```

Then use the `knowledge_base` with an Agent:

agent.py

Copy

```
from phi.agent import Agent
from knowledge_base import knowledge_base

agent = Agent(
    knowledge=knowledge_base,
    search_knowledge=True,
)
agent.knowledge.load(recreate=False)

agent.print_response("Ask me about something from the knowledge base")
```

#### [​](https://docs.phidata.com/knowledge/csv-url#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`urls`

`List[str]`

\-

URLs for `PDF` files.

`reader`

`CSVUrlReader`

`CSVUrlReader()`

A `CSVUrlReader` that converts the `CSVs` into `Documents` for the vector database.

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
](https://VixData.gitbook.io/VixData/documentation/knowledge/csv-knowledge-base)
