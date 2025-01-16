---
description: >-
  The TextKnowledgeBase reads local txt files, converts them into vector
  embeddings and loads them to a vector databse.
---

# Text Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

We are using a local PgVector database for this example. [Make sure it’s running](https://docs.phidata.com/vectordb/pgvector)

knowledge\_base.py

Copy

```
from phi.knowledge.text import TextKnowledgeBase
from phi.vectordb.pgvector import PgVector

knowledge_base = TextKnowledgeBase(
    path="data/txt_files",
    # Table name: ai.text_documents
    vector_db=PgVector(
        table_name="text_documents",
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
    knowledge_base=knowledge_base,
    search_knowledge=True,
)
agent.knowledge.load(recreate=False)

agent.print_response("Ask me about something from the knowledge base")
```

#### [​](https://docs.phidata.com/knowledge/text#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`path`

`Union[str, Path]`

\-

Path to text files. Can point to a single txt file or a directory of txt files.

`formats`

`List[str]`

`[".txt"]`

Formats accepted by this knowledge base.

`reader`

`TextReader`

`TextReader()`

A `TextReader` that converts the text files into `Documents` for the vector database.

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
](https://VixData.gitbook.io/VixData/documentation/knowledge/s3-text-knowledge-base)
