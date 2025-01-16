---
description: >-
  The LangchainKnowledgeBase allows us to use a LangChain retriever or vector
  store as a knowledge base.
---

# LangChain Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

Copy

```
pip install langchain
```

langchain\_kb.py

Copy

```
from phi.agent import Agent
from phi.knowledge.langchain import LangChainKnowledgeBase

from langchain.embeddings import OpenAIEmbeddings
from langchain.document_loaders import TextLoader
from langchain.text_splitter import CharacterTextSplitter
from langchain.vectorstores import Chroma

chroma_db_dir = "./chroma_db"


def load_vector_store():
    state_of_the_union = ws_settings.ws_root.joinpath("data/demo/state_of_the_union.txt")
    # -*- Load the document
    raw_documents = TextLoader(str(state_of_the_union)).load()
    # -*- Split it into chunks
    text_splitter = CharacterTextSplitter(chunk_size=1000, chunk_overlap=0)
    documents = text_splitter.split_documents(raw_documents)
    # -*- Embed each chunk and load it into the vector store
    Chroma.from_documents(documents, OpenAIEmbeddings(), persist_directory=str(chroma_db_dir))


# -*- Get the vectordb
db = Chroma(embedding_function=OpenAIEmbeddings(), persist_directory=str(chroma_db_dir))
# -*- Create a retriever from the vector store
retriever = db.as_retriever()

# -*- Create a knowledge base from the vector store
knowledge_base = LangChainKnowledgeBase(retriever=retriever)

agent = Agent(knowledge_base=knowledge_base, add_references_to_prompt=True)
conv.print_response("What did the president say about technology?")
```

#### [​](https://docs.phidata.com/knowledge/langchain#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`retriever`

`Any`

`None`

LangChain retriever.

`vectorstore`

`Any`

`None`

LangChain vector store used to create a retriever.

`search_kwargs`

`dict`

`None`

Search kwargs when creating a retriever using the langchain vector store.

[\
](https://axidata.gitbook.io/axidata/documentation/knowledge/json-knowledge-base)
