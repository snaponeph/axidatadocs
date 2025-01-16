---
description: >-
  The WikipediaKnowledgeBase reads wikipedia topics, converts them into vector
  embeddings and loads them to a vector databse.
---

# Wikipedia KnowledgeBase

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](http://localhost:3333/vectordb/pgvector)

Copy

```
pip install wikipedia
```

knowledge\_base.py

Copy

```
from phi.knowledge.wikipedia import WikipediaKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = WikipediaKnowledgeBase(
    topics=["Manchester United", "Real Madrid"],
    # Table name: ai.wikipedia_documents
    vector_db=PgVector(
        table_name="wikipedia_documents",
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

#### [​](https://docs.phidata.com/knowledge/wikipedia#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`topics`

`List[str]`

\-

Topics to read

`vector_db`

`VectorDb`

\-

Vector Database for the Knowledge Base.

`reader`

`Reader`

\-

A `Reader` that reads the topics and converts them into `Documents` for the vector database.

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
](https://axidata.gitbook.io/axidata/documentation/knowledge/website-knowledge-base)
