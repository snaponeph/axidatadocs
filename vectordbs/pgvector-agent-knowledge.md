# PgVector Agent Knowledge

#### Setup <a href="#setup" id="setup"></a>

Copy

```
docker run -d \
  -e POSTGRES_DB=ai \
  -e POSTGRES_USER=ai \
  -e POSTGRES_PASSWORD=ai \
  -e PGDATA=/var/lib/postgresql/data/pgdata \
  -v pgvolume:/var/lib/postgresql/data \
  -p 5532:5432 \
  --name pgvector \
  phidata/pgvector:16
```

#### [​](https://docs.phidata.com/vectordb/pgvector#example)Example <a href="#example" id="example"></a>

agent\_with\_knowledge.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes", db_url=db_url, search_type=SearchType.hybrid),
)
# Load the knowledge base: Comment out after first run
knowledge_base.load(recreate=True, upsert=True)

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    knowledge=knowledge_base,
    # Add a tool to read chat history.
    read_chat_history=True,
    show_tool_calls=True,
    markdown=True,
    # debug_mode=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup", stream=True)
agent.print_response("What was my last question?", stream=True)
```

#### [​](https://docs.phidata.com/vectordb/pgvector#pgvector-params)PgVector Params <a href="#pgvector-params" id="pgvector-params"></a>

ParameterTypeDefaultDescription

`table_name`

`str`

\-

The name of the table to use.

`schema`

`str`

\-

The schema to use.

`db_url`

`str`

\-

The database URL to connect to.

`db_engine`

`Engine`

\-

The database engine to use.

`embedder`

`Embedder`

\-

The embedder to use.

`search_type`

`SearchType`

vector

The search type to use.

`vector_index`

`Union[Ivfflat, HNSW]`

\-

The vector index to use.

`distance`

`Distance`

cosine

The distance to use.

`prefix_match`

`bool`

\-

Whether to use prefix matching.

`vector_score_weight`

`float`

0.5

Weight for vector similarity in hybrid search. Must be between 0 and 1.

`content_language`

`str`

\-

The content language to use.

`schema_version`

`int`

\-

The schema version to use.

`auto_upgrade_schema`

`bool`

\-

Whether to auto upgrade the schema.
