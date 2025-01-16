---
description: >-
  The FastEmbedEmbedder class is used to embed text data into vectors using the
  FastEmbed.
---

# Qdrant FastEmbed Embedder

#### Usage <a href="#usage" id="usage"></a>

cookbook/embedders/qdrant\_fastembed.py

Copy

```
from phi.agent import AgentKnowledge
from phi.vectordb.pgvector import PgVector
from phi.embedder.fastembed import FastEmbedEmbedder

embeddings = FastEmbedEmbedder().get_embedding("The quick brown fox jumps over the lazy dog.")

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge_base = AgentKnowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="qdrant_embeddings",
        embedder=FastEmbedEmbedder(),
    ),
    num_documents=2,
)
```

#### [​](https://docs.phidata.com/embedder/qdrant_fastembed#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dimensions`

`int`

\-

The dimensionality of the generated embeddings

`model`

`str`

`BAAI/bge-small-en-v1.5`

The name of the qdrant\_fastembed model to use
