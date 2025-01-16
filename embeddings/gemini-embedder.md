---
description: >-
  The GeminiEmbedder class is used to embed text data into vectors using the
  Gemini API. You can get one from here.
---

# Gemini Embedder

#### Usage <a href="#usage" id="usage"></a>

cookbook/embedders/gemini\_embedder.py

Copy

```
from phi.agent import AgentKnowledge
from phi.vectordb.pgvector import PgVector
from phi.embedder.google import GeminiEmbedder

embeddings = GeminiEmbedder().get_embedding("The quick brown fox jumps over the lazy dog.")

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge_base = AgentKnowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="gemini_embeddings",
        embedder=GeminiEmbedder(),
    ),
    num_documents=2,
)
```

#### [​](https://docs.phidata.com/embedder/gemini#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dimensions`

`int`

`768`

The dimensionality of the generated embeddings

`model`

`str`

`models/text-embedding-004`

The name of the Gemini model to use

`task_type`

`str`

\-

The type of task for which embeddings are being generated

`title`

`str`

\-

Optional title for the embedding task

`api_key`

`str`

\-

The API key used for authenticating requests.

`request_params`

`Optional[Dict[str, Any]]`

\-

Optional dictionary of parameters for the embedding request

`client_params`

`Optional[Dict[str, Any]]`

\-

Optional dictionary of parameters for the Gemini client

`gemini_client`

`Optional[Client]`

\-

Optional pre-configured Gemini client instance
