---
description: >-
  Phidata supports using Sqlite as a storage backend for Agents using the
  SqlAgentStorage class.
---

# Sqlite Agent Storage

#### Usage <a href="#usage" id="usage"></a>

You need to provide either `db_url`, `db_file` or `db_engine`. The following example uses `db_file`.

storage.py

Copy

```
from phi.storage.agent.sqlite import SqlAgentStorage

# Create a storage backend using the Sqlite database
storage = SqlAgentStorage(
    # store sessions in the ai.sessions table
    table_name="agent_sessions",
    # db_file: Sqlite database file
    db_file="tmp/data.db",
)

# Add storage to the Agent
agent = Agent(storage=storage)
```

#### [​](https://docs.phidata.com/storage/sqlite#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`table_name`

`str`

\-

Name of the table to be used.

`schema`

`Optional[str]`

`"ai"`

Schema name, default is "ai".

`db_url`

`Optional[str]`

`None`

Database URL, if provided.

`db_engine`

`Optional[Engine]`

`None`

Database engine to be used.

`schema_version`

`int`

`1`

Version of the schema, default is 1.

`auto_upgrade_schema`

`bool`

`False`

If true, automatically upgrades the schema when necessary.
