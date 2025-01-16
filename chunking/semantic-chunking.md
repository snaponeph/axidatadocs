# Semantic Chunking

Semantic chunking is a method of splitting documents into smaller chunks by analyzing semantic similarity between text segments using embeddings. It uses the chonkie library to identify natural breakpoints where the semantic meaning changes significantly, based on a configurable similarity threshold. This helps preserve context and meaning better than fixed-size chunking by ensuring semantically related content stays together in the same chunk, while splitting occurs at meaningful topic transitions.

Copy

```
from phi.agent import Agent
from phi.document.chunking.semantic import SemanticChunking
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes_semantic_chunking", db_url=db_url),
    chunking_strategy=SemanticChunking(),
)
knowledge_base.load(recreate=False)  # Comment out after first run

agent = Agent(
    knowledge_base=knowledge_base,
    search_knowledge=True,
)

agent.print_response("How to make Thai curry?", markdown=True)
```

#### [​](https://docs.phidata.com/chunking/semantic-chunking#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`embedder`

`Embedder`

`OpenAIEmbedder`

The embedder to use for semantic chunking.

`chunk_size`

`int`

`5000`

The maximum size of each chunk.

`similarity_threshold`

`float`

`0.5`

The similarity threshold for determining chunk boundaries.
