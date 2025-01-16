---
description: >-
  The SentenceTransformerEmbedder class is used to embed text data into vectors
  using the SentenceTransformers library.
---

# SentenceTransformers Embedder

#### Usage <a href="#usage" id="usage"></a>

cookbook/embedders/sentence\_transformer\_embedder.py

Copy

```
from phi.agent import AgentKnowledge
from phi.vectordb.pgvector import PgVector
from phi.embedder.sentence_transformer import SentenceTransformerEmbedder

embeddings = SentenceTransformerEmbedder().get_embedding("The quick brown fox jumps over the lazy dog.")

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge_base = AgentKnowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="sentence_transformer_embeddings",
        embedder=SentenceTransformerEmbedder(),
    ),
    num_documents=2,
)
```

#### [​](https://docs.phidata.com/embedder/sentencetransformers#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dimensions`

`int`

\-

The dimensionality of the generated embeddings

`model`

`str`

`all-mpnet-base-v2`

The name of the SentenceTransformers model to use

`sentence_transformer_client`

`Optional[Client]`

\-

Optional pre-configured SentenceTransformers client instance
