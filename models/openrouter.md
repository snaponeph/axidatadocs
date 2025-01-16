---
description: OpenRouter is a platform for providing endpoints for Large Language models.
---

# OpenRouter

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `OPENROUTER_API_KEY` environment variable. Get your key from [here](https://openrouter.ai/settings/keys).

MacWindows

Copy

```
export OPENROUTER_API_KEY=***
```

#### [​](https://docs.phidata.com/models/openrouter#example)Example <a href="#example" id="example"></a>

Use `OpenRouter` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.openrouter import OpenRouter

agent = Agent(
    model=OpenRouter(id="gpt-4o"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/openrouter#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"gpt-4o"`

The specific model ID used for generating responses.

`name`

`str`

`"OpenRouter"`

The name identifier for the OpenRouter agent.

`provider`

`str`

\-

The provider of the model, combining "OpenRouter" with the model ID.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the OpenRouter service. Retrieved from the environment variable `OPENROUTER_API_KEY`.

`base_url`

`str`

`"https://openrouter.ai/api/v1"`

The base URL for making API requests to the OpenRouter service.

`max_tokens`

`int`

`1024`

The maximum number of tokens to generate in the response.

OpenRouter also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
