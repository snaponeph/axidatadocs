# Singlestore Agent Storage

#### Usage <a href="#usage" id="usage"></a>

Obtain the credentials for Singlestore from [here](https://portal.singlestore.com/)

storage.py

Copy

```
from phi.storage.agent.singlestore import S2AgentStorage

# SingleStore Configuration
USERNAME = getenv("SINGLESTORE_USERNAME")
PASSWORD = getenv("SINGLESTORE_PASSWORD")
HOST = getenv("SINGLESTORE_HOST")
PORT = getenv("SINGLESTORE_PORT")
DATABASE = getenv("SINGLESTORE_DATABASE")
SSL_CERT = getenv("SINGLESTORE_SSL_CERT", None)

# SingleStore DB URL
db_url = f"mysql+pymysql://{USERNAME}:{PASSWORD}@{HOST}:{PORT}/{DATABASE}?charset=utf8mb4"
if SSL_CERT:
    db_url += f"&ssl_ca={SSL_CERT}&ssl_verify_cert=true"

# Create a database engine
db_engine = create_engine(db_url)

# Create a storage backend using the Singlestore database
storage = S2AgentStorage(
    # store sessions in the ai.sessions table
    table_name="agent_sessions",
    # db_engine: Singlestore database engine
    db_engine=db_engine,
    # schema: Singlestore schema
    schema=DATABASE,
)

# Add storage to the Agent
agent = Agent(storage=storage)
```

#### [​](https://docs.phidata.com/storage/singlestore#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`table_name`

`str`

\-

Name of the table to be used.

`schema`

`Optional[str]`

`"ai"`

Schema name.

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

Version of the schema.

`auto_upgrade_schema`

`bool`

`False`

If `true`, automatically upgrades the schema when necessary.
