---
description: >-
  The WebsiteKnowledgeBase reads websites, converts them into vector embeddings
  and loads them to a vector_db.
---

# Website Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

Copy

```
pip install bs4
```

knowledge\_base.py

Copy

```
from phi.knowledge.website import WebsiteKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = WebsiteKnowledgeBase(
    urls=["https://docs.phidata.com/introduction"],
    # Number of links to follow from the seed URLs
    max_links=10,
    # Table name: ai.website_documents
    vector_db=PgVector(
        table_name="website_documents",
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
    ),
)
```

Then use the `knowledge_base` with an `Agent`:

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

#### [​](https://docs.phidata.com/knowledge/website#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`urls`

`List[str]`

\-

URLs to read

`reader`

`WebsiteReader`

\-

A `WebsiteReader` that reads the urls and converts them into `Documents` for the vector database.

`max_depth`

`int`

`3`

Maximum depth to crawl.

`max_links`

`int`

`10`

Number of links to crawl.

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
](https://axidata.gitbook.io/axidata/documentation/knowledge/text-knowledge-base)
