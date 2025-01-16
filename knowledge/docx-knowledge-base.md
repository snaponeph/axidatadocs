---
description: >-
  The DocxKnowledgeBase reads local docx files, converts them into vector
  embeddings and loads them to a vector databse.
---

# Docx Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

Copy

```
pip install textract
```

Copy

```
from phi.knowledge.docx import DocxKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = DocxKnowledgeBase(
    path="data/docs",
    # Table name: ai.docx_documents
    vector_db=PgVector(
        table_name="docx_documents",
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

#### [​](https://docs.phidata.com/knowledge/docx#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`path`

`Union[str, Path]`

\-

Path to docx files. Can point to a single docx file or a directory of docx files.

`formats`

`List[str]`

`[".doc", ".docx"]`

Formats accepted by this knowledge base.

`reader`

`DocxReader`

`DocxReader()`

A `DocxReader` that converts the docx files into `Documents` for the vector database.

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
](https://VixData.gitbook.io/VixData/documentation/knowledge/csv-url-knowledge-base)
