# Introduction

An Embedder converts complex information into vector representations, allowing it to be stored in a vector database. By transforming data into embeddings, the embedder enables efficient searching and retrieval of contextually relevant information. This process enhances the responses of language models by providing them with the necessary business context, ensuring they are context-aware. Phidata uses `OpenAIEmbedder` as the default embedder, but other embedders are supported as well. Here is an example:

Copy

```
from phi.agent import Agent, AgentKnowledge
from phi.vectordb.pgvector import PgVector
from phi.embedder.openai import OpenAIEmbedder

# Create knowledge base
knowledge_base=AgentKnowledge(
    vector_db=PgVector(
        db_url=db_url,
        table_name=embeddings_table,
        embedder=OpenAIEmbedder(),
    ),
    # 2 references are added to the prompt
    num_documents=2,
),

# Add information to the knowledge base
knowledge_base.load_text("The sky is blue")

# Add the knowledge base to the Agent
agent = Agent(knowledge_base=knowledge_base)
```

The following embedders are supported:

* [OpenAI](https://docs.phidata.com/embedder/openai)
* [Gemini](https://docs.phidata.com/embedder/gemini)
* [Ollama](https://docs.phidata.com/embedder/ollama)
* [Voyage AI](https://docs.phidata.com/embedder/voyageai)
* [Azure OpenAI](https://docs.phidata.com/embedder/azure_openai)
* [Mistral](https://docs.phidata.com/embedder/mistral)
* [Fireworks](https://docs.phidata.com/embedder/fireworks)
* [Together](https://docs.phidata.com/embedder/together)
* [HuggingFace](https://docs.phidata.com/embedder/huggingface)
* [Qdrant FastEmbed](https://docs.phidata.com/embedder/qdrant_fastembed)
