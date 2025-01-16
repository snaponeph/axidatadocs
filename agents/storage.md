---
description: Agents use storage to persist sessions by storing them in a database.
---

# Storage

Agents come with built-in memory, but it only lasts while the session is active. To continue conversations across sessions, we store agent sessions in a database like PostgreSQL.

The general syntax for adding storage to an Agent looks like:

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo
from phi.storage.agent.postgres import PgAgentStorage

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    storage=PgAgentStorage(table_name="agent_sessions", db_url="postgresql+psycopg://ai:ai@localhost:5532/ai"),
    tools=[DuckDuckGo()],
    show_tool_calls=True,
    add_history_to_messages=True,
)
agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")
agent.print_response("Which country are we speaking about?")
```

#### [​](https://docs.phidata.com/agents/storage#example)Example <a href="#example" id="example"></a>

1

Run Postgres

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **Postgres** on port **5532** using:

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

2

Create an Agent with Storage

Create a file `agent_with_storage.py` with the following contents

Copy

```
import typer
from typing import Optional, List
from phi.agent import Agent
from phi.storage.agent.postgres import PgAgentStorage
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    vector_db=PgVector(table_name="recipes", db_url=db_url, search_type=SearchType.hybrid),
)
# Load the knowledge base: Comment after first run
knowledge_base.load(upsert=True)
storage = PgAgentStorage(table_name="pdf_agent", db_url=db_url)

def pdf_agent(new: bool = False, user: str = "user"):
    session_id: Optional[str] = None

    if not new:
        existing_sessions: List[str] = storage.get_all_session_ids(user)
        if len(existing_sessions) > 0:
            session_id = existing_sessions[0]

    agent = Agent(
        session_id=session_id,
        user_id=user,
        knowledge=knowledge_base,
        storage=storage,
        # Show tool calls in the response
        show_tool_calls=True,
        # Enable the agent to read the chat history
        read_chat_history=True,
        # We can also automatically add the chat history to the messages sent to the model
        # But giving the model the chat history is not always useful, so we give it a tool instead
        # to only use when needed.
        # add_history_to_messages=True,
        # Number of historical responses to add to the messages.
        # num_history_responses=3,
    )
    if session_id is None:
        session_id = agent.session_id
        print(f"Started Session: {session_id}\n")
    else:
        print(f"Continuing Session: {session_id}\n")

    # Runs the agent as a cli app
    agent.cli_app(markdown=True)


if __name__ == "__main__":
    typer.run(pdf_agent)
```

3

Run the agent

Install libraries

MacWindows

Copy

```
pip install -U phidata openai pgvector pypdf "psycopg[binary]" sqlalchemy
```

Run the agent

Copy

```
python agent_with_storage.py
```

Now the agent continues across sessions. Ask a question:

Copy

```
How do I make pad thai?
```

Then message `bye` to exit, start the app again and ask:

Copy

```
What was my last message?
```

4

Start a new run

Run the `agent_with_storage.py` file with the `--new` flag to start a new run.

Copy

```
python agent_with_storage.py --new
```

#### [​](https://docs.phidata.com/agents/storage#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`storage`

`Optional[AgentStorage]`

`None`

Storage mechanism for the agent, if applicable.
