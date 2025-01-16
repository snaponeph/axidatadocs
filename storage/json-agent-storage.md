---
description: >-
  Phidata supports using local JSON files as a storage backend for Agents using
  the JsonFileAgentStorage class.
---

# JSON Agent Storage

#### Usage <a href="#usage" id="usage"></a>

storage.py

Copy

```
from phi.agent import Agent
from phi.tools.duckduckgo import DuckDuckGo
from phi.storage.agent.json import JsonFileAgentStorage

agent = Agent(
    storage=JsonFileAgentStorage(path="tmp/agent_sessions_json"),
    tools=[DuckDuckGo()],
    add_history_to_messages=True,
)

agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")
```

#### [​](https://docs.phidata.com/storage/json#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dir_path`

`str`

\-

Path to the folder to be used to store the JSON files.
