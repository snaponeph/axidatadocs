# Introduction

Vector databases enable us to store information as embeddings and search for “results similar” to our input query using cosine similarity or full text search. These results are then provided to the Agent as context so it can respond in a context-aware manner using Retrieval Augmented Generation (**RAG**).

Here’s how vector databases are used with Agents:

1

Chunk the information

Break down the knowledge into smaller chunks to ensure our search query returns only relevant results.

2

Load the knowledge base

Convert the chunks into embedding vectors and store them in a vector database.

3

Search the knowledge base

When the user sends a message, we convert the input message into an embedding and “search” for nearest neighbors in the vector database.

Many vector databases also support hybrid search, which combines the power of vector similarity search with traditional keyword-based search. This approach can significantly improve the relevance and accuracy of search results, especially for complex queries or when dealing with diverse types of data.

Hybrid search typically works by:

1. Performing a vector similarity search to find semantically similar content.
2. Conducting a keyword-based search to identify exact or close matches.
3. Combining the results using a weighted approach to provide the most relevant information.

This capability allows for more flexible and powerful querying, often yielding better results than either method alone.

The following VectorDb are currently supported:

* [PgVector](https://docs.phidata.com/vectordb/pgvector)\*
* [LanceDb](https://docs.phidata.com/vectordb/lancedb)\*
* [Pinecone](https://docs.phidata.com/vectordb/pinecone)\*
* [Qdrant](https://docs.phidata.com/vectordb/qdrant)

\*hybrid search supported

Each of these databases has its own strengths and features, including varying levels of support for hybrid search. Be sure to check the specific documentation for each to understand how to best leverage their capabilities in your projects.
