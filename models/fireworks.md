---
description: Fireworks is a platform for providing endpoints for Large Language models.
---

# Fireworks

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `FIREWORKS_API_KEY` environment variable. Get your key from [here](https://fireworks.ai/account/api-keys).

MacWindows

Copy

```
export FIREWORKS_API_KEY=***
```

#### [​](https://docs.phidata.com/models/fireworks#example)Example <a href="#example" id="example"></a>

Use `Fireworks` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.fireworks import Fireworks

agent = Agent(
    model=Fireworks(id="accounts/fireworks/models/firefunction-v2"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/fireworks#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"accounts/fireworks/models/firefunction-v2"`

The specific model ID used for generating responses.

`name`

`str`

`"Fireworks: {id}"`

The name identifier for the agent. Defaults to "Fireworks: " followed by the model ID.

`provider`

`str`

`"Fireworks"`

The provider of the model.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the service. Retrieved from the environment variable FIREWORKS\_API\_KEY.

`base_url`

`str`

`"https://api.fireworks.ai/inference/v1"`

The base URL for making API requests to the Fireworks service.

Fireworks also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
