# Pinecone Agent Knowledge

#### Setup <a href="#setup" id="setup"></a>

Follow the instructions in the [Pinecone Setup Guide](https://docs.pinecone.io/guides/get-started/quickstart) to get started quickly with Pinecone.

#### [​](https://docs.phidata.com/vectordb/pinecone#example)Example <a href="#example" id="example"></a>

agent\_with\_knowledge.py

Copy

```
import os
import typer
from typing import Optional
from rich.prompt import Prompt

from phi.agent import Agent
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pineconedb import PineconeDB

api_key = os.getenv("PINECONE_API_KEY")
index_name = "thai-recipe-hybrid-search"

vector_db = PineconeDB(
    name=index_name,
    dimension=1536,
    metric="cosine",
    spec={"serverless": {"cloud": "aws", "region": "us-east-1"}},
    api_key=api_key,
    use_hybrid_search=True,
    hybrid_alpha=0.5,
)

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=vector_db,
)

# Comment out after first run
knowledge_base.load(recreate=True, upsert=True)


def pinecone_agent(user: str = "user"):
    run_id: Optional[str] = None

    agent = Agent(
        run_id=run_id,
        user_id=user,
        knowledge=knowledge_base,
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
    typer.run(pinecone_agent)

```

#### [​](https://docs.phidata.com/vectordb/pinecone#pineconedb-params)PineconeDB Params <a href="#pineconedb-params" id="pineconedb-params"></a>

ParameterTypeDefaultDescription

`name`

`str`

\-

The name of the Pinecone index

`dimension`

`int`

\-

The dimension of the embeddings

`spec`

`Union[Dict, ServerlessSpec, PodSpec]`

\-

The index spec

`embedder`

`Optional[Embedder]`

`None`

Embedder instance for creating embeddings (defaults to OpenAIEmbedder if not provided)

`metric`

`Optional[str]`

`"cosine"`

The metric used for similarity search

`additional_headers`

`Optional[Dict[str, str]]`

`None`

Additional headers to pass to the Pinecone client

`pool_threads`

`Optional[int]`

`1`

The number of threads to use for the Pinecone client

`namespace`

`Optional[str]`

`None`

The namespace for the Pinecone index

`timeout`

`Optional[int]`

`None`

The timeout for Pinecone operations

`index_api`

`Optional[Any]`

`None`

The Index API object

`api_key`

`Optional[str]`

`None`

The Pinecone API key

`host`

`Optional[str]`

`None`

The Pinecone host

`config`

`Optional[Config]`

`None`

The Pinecone config

`use_hybrid_search`

`bool`

`False`

Whether to use hybrid search

`hybrid_alpha`

`float`

`0.5`

The alpha value for hybrid search
