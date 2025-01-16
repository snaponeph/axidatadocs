# HuggingFace Embedder

The HuggingfaceCustomEmbedder class is used to embed text data into vectors using the Hugging Face API. You can get one from here.

#### Usage <a href="#usage" id="usage"></a>

cookbook/embedders/huggingface\_embedder.py

Copy

```
from phi.agent import AgentKnowledge
from phi.vectordb.pgvector import PgVector
from phi.embedder.huggingface import HuggingfaceCustomEmbedder

embeddings = HuggingfaceCustomEmbedder().get_embedding("The quick brown fox jumps over the lazy dog.")

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge_base = AgentKnowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="huggingface_embeddings",
        embedder=HuggingfaceCustomEmbedder(),
    ),
    num_documents=2,
)
```

#### [​](https://docs.phidata.com/embedder/huggingface#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dimensions`

`int`

\-

The dimensionality of the generated embeddings

`model`

`str`

`all-MiniLM-L6-v2`

The name of the HuggingFace model to use

`api_key`

`str`

\-

The API key used for authenticating requests

`client_params`

`Optional[Dict[str, Any]]`

\-

Optional dictionary of parameters for the HuggingFace client

`huggingface_client`

`Any`

\-

Optional pre-configured HuggingFace client instance
