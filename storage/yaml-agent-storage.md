# YAML Agent Storage

#### Usage <a href="#usage" id="usage"></a>

storage.py

Copy

```
from phi.agent import Agent
from phi.tools.duckduckgo import DuckDuckGo
from phi.storage.agent.yaml import YamlFileAgentStorage

agent = Agent(
    storage=YamlFileAgentStorage(path="tmp/agent_sessions_yaml"),
    tools=[DuckDuckGo()],
    add_history_to_messages=True,
)

agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")
```

#### [​](https://docs.phidata.com/storage/yaml#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`dir_path`

`str`

\-

Path to the folder to be used to store the YAML files.
