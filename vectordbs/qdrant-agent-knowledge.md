# Qdrant Agent Knowledge

#### Setup <a href="#setup" id="setup"></a>

Follow the instructions in the [Qdrant Setup Guide](https://qdrant.tech/documentation/guides/installation/) to install Qdrant locally. Here is a guide to get API keys: [Qdrant API Keys](https://qdrant.tech/documentation/cloud/authentication/).

#### [​](https://docs.phidata.com/vectordb/qdrant#example)Example <a href="#example" id="example"></a>

agent\_with\_knowledge.py

Copy

```
import os
import typer
from typing import Optional
from rich.prompt import Prompt

from phi.agent import Agent
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.qdrant import Qdrant

api_key = os.getenv("QDRANT_API_KEY")
qdrant_url = os.getenv("QDRANT_URL")
collection_name = "thai-recipe-index"

vector_db = Qdrant(
    collection=collection_name,
    url=qdrant_url,
    api_key=api_key,
)

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=vector_db,
)

# Comment out after first run
knowledge_base.load(recreate=True, upsert=True)


def qdrant_agent(user: str = "user"):
    run_id: Optional[str] = None

    agent = Agent(
        run_id=run_id,
        user_id=user,
        knowledge=knowledge_base,
        tool_calls=True,
        use_tools=True,
        show_tool_calls=True,
        debug_mode=True,
    )

    if run_id is None:
        run_id = agent.run_id
        print(f"Started Run: {run_id}\n")
    else:
        print(f"Continuing Run: {run_id}\n")

    while True:
        message = Prompt.ask(f"[bold] :sunglasses: {user} [/bold]")
        if message in ("exit", "bye"):
            break
        agent.print_response(message)


if __name__ == "__main__":
    typer.run(qdrant_agent)
```

#### [​](https://docs.phidata.com/vectordb/qdrant#qdrant-params)Qdrant Params <a href="#qdrant-params" id="qdrant-params"></a>

NameTypeDefaultDescription

`collection`

`str`

\-

Name of the Qdrant collection

`embedder`

`Embedder`

`OpenAIEmbedder()`

Embedder for embedding the document contents

`distance`

`Distance`

`Distance.cosine`

Distance metric for similarity search

`location`

`Optional[str]`

`None`

Location of the Qdrant database

`url`

`Optional[str]`

`None`

URL of the Qdrant server

`port`

`Optional[int]`

`6333`

Port number for the Qdrant server

`grpc_port`

`int`

`6334`

gRPC port number for the Qdrant server

`prefer_grpc`

`bool`

`False`

Whether to prefer gRPC over HTTP

`https`

`Optional[bool]`

`None`

Whether to use HTTPS

`api_key`

`Optional[str]`

`None`

API key for authentication

`prefix`

`Optional[str]`

`None`

Prefix for the Qdrant API

`timeout`

`Optional[float]`

`None`

Timeout for Qdrant operations

`host`

`Optional[str]`

`None`

Host address for the Qdrant server

`path`

`Optional[str]`

`None`

Path to the Qdrant database
