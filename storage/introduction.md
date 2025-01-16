# Introduction

Agents come with built-in memory but it only lasts while the session is active. To continue conversations across sessions, we store Agent sessions in a database like PostgreSQL.

Storage is a necessary component when building user facing AI products as any production application will require users to be able to “continue” their conversation with the Agent.

The general syntax for adding storage to an Agent looks like:

storage.py

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

The following databases are supported as a storage backend:

* [PostgreSQL](https://docs.phidata.com/storage/postgres)
* [Sqlite](https://docs.phidata.com/storage/sqlite)
* [SingleStore](https://docs.phidata.com/storage/singlestore)
* [DynamoDB](https://docs.phidata.com/storage/dynamodb)
* [MongoDB](https://docs.phidata.com/storage/mongodb)
