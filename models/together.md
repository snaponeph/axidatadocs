---
description: Together is a platform for providing endpoints for Large Language models.
---

# Together

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `TOGETHER_API_KEY` environment variable. Get your key [from Together here](https://api.together.xyz/settings/api-keys).

MacWindows

Copy

```
export TOGETHER_API_KEY=***
```

#### [​](https://docs.phidata.com/models/together#example)Example <a href="#example" id="example"></a>

Use `Together` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.together import Together

agent = Agent(
    model=Together(id="meta-llama/Meta-Llama-3.1-8B-Instruct-Turbo"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/together#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"mistralai/Mixtral-8x7B-Instruct-v0.1"`

The id of the Together model to use.

`name`

`str`

`"Together"`

The name of this chat model instance.

`provider`

`str`

`"Together " + id`

The provider of the model.

`api_key`

`Optional[str]`

`None`

The API key to authorize requests to Together. Defaults to environment variable TOGETHER\_API\_KEY.

`base_url`

`str`

`"https://api.together.xyz/v1"`

The base URL for API requests.

`monkey_patch`

`bool`

`False`

Whether to apply monkey patching.

Together also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
