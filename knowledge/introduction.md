# Introduction

A **knowledge base** is a database of information that an agent can search to improve its responses. This information is stored in a vector database and provides agents with business context, helping them respond in a context-aware manner. The general syntax is:

Copy

```
from phi.agent import Agent, AgentKnowledge

# Create a knowledge base for the Agent
knowledge_base = AgentKnowledge(vector_db=...)

# Add information to the knowledge base
knowledge_base.load_text("The sky is blue")

# Add the knowledge base to the Agent and
# give it a tool to search the knowledge base as needed
agent = Agent(knowledge=knowledge_base, search_knowledge=True)
```

#### [​](https://docs.phidata.com/knowledge/introduction#vector-databases)Vector Databases <a href="#vector-databases" id="vector-databases"></a>

While any type of storage can act as a knowledge base, vector databases offer the best solution for retrieving relevant results from dense information quickly. Here’s how vector databases are used with Agents:

1

Chunk the information

Break down the knowledge into smaller chunks to ensure our search query returns only relevant results.

2

Load the knowledge base

Convert the chunks into embedding vectors and store them in a vector database.

3

Search the knowledge base

When the user sends a message, we convert the input message into an embedding and “search” for nearest neighbors in the vector database.

#### [​](https://docs.phidata.com/knowledge/introduction#loading-the-knowledge-base)Loading the Knowledge Base <a href="#loading-the-knowledge-base" id="loading-the-knowledge-base"></a>

Before you can use a knowledge base, it needs to be loaded with embeddings that will be used for retrieval. Use one of the following knowledge bases to simplify the chunking, loading, searching and optimization process:

* [ArXiv knowledge base](https://docs.phidata.com/knowledge/arxiv): Load ArXiv papers to a knowledge base
* [Combined knowledge base](https://docs.phidata.com/knowledge/combined): Combine multiple knowledge bases into 1
* [CSV knowledge base](https://docs.phidata.com/knowledge/csv): Load CSV files to a knowledge base
* [Document knowledge base](https://docs.phidata.com/knowledge/document): Load local docx files to a knowledge base
* [JSON knowledge base](https://docs.phidata.com/knowledge/json): Load JSON files to a knowledge base
* [LangChain knowledge base](https://docs.phidata.com/knowledge/langchain): Use a Langchain retriever as a knowledge base
* [PDF knowledge base](https://docs.phidata.com/knowledge/pdf): Load local PDF files to a knowledge base
* [PDF URL knowledge base](https://docs.phidata.com/knowledge/pdf-url): Load PDF files from a URL to a knowledge base
* [S3 PDF knowledge base](https://docs.phidata.com/knowledge/s3_pdf): Load PDF files from S3 to a knowledge base
* [S3 Text knowledge base](https://docs.phidata.com/knowledge/s3_text): Load text files from S3 to a knowledge base
* [Text knowledge base](https://docs.phidata.com/knowledge/text): Load text/docx files to a knowledge base
* [Website knowledge base](https://docs.phidata.com/knowledge/website): Load website data to a knowledge base
* [Wikipedia knowledge base](https://docs.phidata.com/knowledge/wikipedia): Load wikipedia articles to a knowledge base
