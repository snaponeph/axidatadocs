---
description: >-
  The LlamaIndexKnowledgeBase allows us to use a LlamaIndex retriever or vector
  store as a knowledge base.
---

# LlamaIndex Knowledge Base

#### Usage <a href="#usage" id="usage"></a>

Copy

```
pip install llama-index-core llama-index-readers-file llama-index-embeddings-openai
```

llamaindex\_kb.py

Copy

```

from pathlib import Path
from shutil import rmtree

import httpx
from phi.agent import Agent
from phi.knowledge.llamaindex import LlamaIndexKnowledgeBase
from llama_index.core import (
    SimpleDirectoryReader,
    StorageContext,
    VectorStoreIndex,
)
from llama_index.core.retrievers import VectorIndexRetriever
from llama_index.core.node_parser import SentenceSplitter


data_dir = Path(__file__).parent.parent.parent.joinpath("wip", "data", "paul_graham")
if data_dir.is_dir():
    rmtree(path=data_dir, ignore_errors=True)
data_dir.mkdir(parents=True, exist_ok=True)

url = "https://raw.githubusercontent.com/run-llama/llama_index/main/docs/docs/examples/data/paul_graham/paul_graham_essay.txt"
file_path = data_dir.joinpath("paul_graham_essay.txt")
response = httpx.get(url)
if response.status_code == 200:
    with open(file_path, "wb") as file:
        file.write(response.content)
    print(f"File downloaded and saved as {file_path}")
else:
    print("Failed to download the file")


documents = SimpleDirectoryReader(str(data_dir)).load_data()

splitter = SentenceSplitter(chunk_size=1024)

nodes = splitter.get_nodes_from_documents(documents)

storage_context = StorageContext.from_defaults()

index = VectorStoreIndex(nodes=nodes, storage_context=storage_context)

retriever = VectorIndexRetriever(index)

# Create a knowledge base from the vector store
knowledge_base = LlamaIndexKnowledgeBase(retriever=retriever)

# Create an agent with the knowledge base
agent = Agent(knowledge_base=knowledge_base, search_knowledge=True, debug_mode=True, show_tool_calls=True)

# Use the agent to ask a question and print a response.
agent.print_response("Explain what this text means: low end eats the high end", markdown=True)
```

#### [​](https://docs.phidata.com/knowledge/llamaindex#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`retriever`

`BaseRetriever`

`None`

LlamaIndex retriever used for querying the knowledge base.

`loader`

`Optional[Callable]`

`None`

Optional callable function to load documents into the knowledge base.

[\
](https://VixData.gitbook.io/VixData/documentation/knowledge/langchain-knowledge-base)
