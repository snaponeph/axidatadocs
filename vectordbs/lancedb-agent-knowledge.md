# LanceDB Agent Knowledge

#### Setup <a href="#setup" id="setup"></a>

Copy

```
pip install lancedb
```

#### [​](https://docs.phidata.com/vectordb/lancedb#example)Example <a href="#example" id="example"></a>

agent\_with\_knowledge.py

Copy

```
import typer
from typing import Optional
from rich.prompt import Prompt

from phi.agent import Agent
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.lancedb import LanceDb
from phi.vectordb.search import SearchType

# LanceDB Vector DB
vector_db = LanceDb(
    table_name="recipes",
    uri="/tmp/lancedb",
    search_type=SearchType.keyword,
)

# Knowledge Base
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=vector_db,
)

# Comment out after first run
knowledge_base.load(recreate=True)


def lancedb_agent(user: str = "user"):
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
    typer.run(lancedb_agent)
```

#### [​](https://docs.phidata.com/vectordb/lancedb#lancedb-params)LanceDb Params <a href="#lancedb-params" id="lancedb-params"></a>

ParameterTypeDefaultDescription

`uri`

`str`

\-

The URI to connect to.

`table`

`LanceTable`

\-

The Lance table to use.

`table_name`

`str`

\-

The name of the table to use.

`connection`

`DBConnection`

\-

The database connection to use.

`api_key`

`str`

\-

The API key to use.

`embedder`

`Embedder`

\-

The embedder to use.

`search_type`

`SearchType`

vector

The search type to use.

`distance`

`Distance`

cosine

The distance to use.

`nprobes`

`int`

\-

The number of probes to use. [More Info](https://lancedb.github.io/lancedb/ann_indexes/#use-gpu-to-build-vector-index)

`reranker`

`Reranker`

\-

The reranker to use. [More Info](https://lancedb.github.io/lancedb/hybrid_search/eval/)

`use_tantivy`

`bool`

\-

Whether to use tantivy.
