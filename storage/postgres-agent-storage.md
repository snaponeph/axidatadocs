---
description: >-
  Phidata supports using PostgreSQL as a storage backend for Agents using the
  PgAgentStorage class.
---

# Postgres Agent Storage

#### Usage <a href="#usage" id="usage"></a>

#### [​](https://docs.phidata.com/storage/postgres#run-pgvector)Run PgVector <a href="#run-pgvector" id="run-pgvector"></a>

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **PgVector** on port **5532** using:

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

storage.py

Copy

```
from phi.storage.agent.postgres import PgAgentStorage

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

# Create a storage backend using the Postgres database
storage = PgAgentStorage(
    # store sessions in the ai.sessions table
    table_name="agent_sessions",
    # db_url: Postgres database URL
    db_url=db_url,
)

# Add storage to the Agent
agent = Agent(storage=storage)
```

#### [​](https://docs.phidata.com/storage/postgres#params)Params <a href="#params" id="params"></a>

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
