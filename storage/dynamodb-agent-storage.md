---
description: >-
  Phidata supports using DynamoDB as a storage backend for Agents using the
  DynamoDbAgentStorage class.
---

# DynamoDB Agent Storage

#### Usage <a href="#usage" id="usage"></a>

You need to provide `aws_access_key_id` and `aws_secret_access_key` parameters to the `DynamoDbAgentStorage` class.

storage.py

Copy

```
from phi.storage.agent.dynamodb import DynamoDbAgentStorage

# AWS Credentials
AWS_ACCESS_KEY_ID = getenv("AWS_ACCESS_KEY_ID")
AWS_SECRET_ACCESS_KEY = getenv("AWS_SECRET_ACCESS_KEY")

storage = DynamoDbAgentStorage(
    # store sessions in the ai.sessions table
    table_name="agent_sessions",
    # region_name: DynamoDB region name
    region_name="us-east-1",
    # aws_access_key_id: AWS access key id
    aws_access_key_id=AWS_ACCESS_KEY_ID,
    # aws_secret_access_key: AWS secret access key
    aws_secret_access_key=AWS_SECRET_ACCESS_KEY,
)

# Add storage to the Agent
agent = Agent(storage=storage)
```

#### [​](https://docs.phidata.com/storage/dynamodb#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`table_name`

`str`

\-

Name of the table to be used.

`region_name`

`Optional[str]`

`None`

Region name of the DynamoDB table.

`aws_access_key_id`

`Optional[str]`

`None`

AWS access key id, if provided.

`aws_secret_access_key`

`Optional[str]`

`None`

AWS secret access key, if provided.

`endpoint_url`

`Optional[str]`

`None`

Endpoint URL, if provided.

`create_table_if_not_exists`

`bool`

`True`

If true, creates the table if it does not exist.
