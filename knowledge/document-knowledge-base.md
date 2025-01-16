---
description: >-
  The DocumentKnowledgeBase reads local docs files, converts them into vector
  embeddings and loads them to a vector databse.
---

# Document Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

Copy

```
pip install textract
```

Copy

```
from phi.knowledge.document import DocumentKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = DocumentKnowledgeBase(
    path="data/docs",
    # Table name: ai.documents
    vector_db=PgVector(
        table_name="documents",
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
    ),
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

agent.print_response("Ask me about something from the knowledge base")
```

#### [​](https://docs.phidata.com/knowledge/document#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`documents`

`List[Document]`

\-

List of documents to load into the vector database.

`vector_db`

`VectorDb`

\-

Vector Database for the Knowledge Base.

`reader`

`Reader`

\-

A `Reader` that converts the content of the documents into `Documents` for the vector database.

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

Was this page helpful?

YesNo[Suggest edits](https://github.com/phidatahq/phidata-docs/edit/main/knowledge/document.mdx)[Docx](https://docs.phidata.com/knowledge/docx)[JSON](https://docs.phidata.com/knowledge/json)[x](https://x.com/phidatahq)[github](https://github.com/phidatahq/phidata)[discord](https://phidata.link/discord)[youtube](https://phidata.link/youtube)[website](https://phidata.com/)[Powered by Mintlify](https://mintlify.com/preview-request?utm_campaign=poweredBy\&utm_medium=docs\&utm_source=docs.phidata.com)

[\
](https://axidata.gitbook.io/axidata/documentation/knowledge/docx-knowledge-base)
