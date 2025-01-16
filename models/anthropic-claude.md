---
description: >-
  Claude is a family of foundational AI models by Anthropic that can be used in
  a variety of applications.
---

# Anthropic Claude

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `ANTHROPIC_API_KEY` environment. You can get one [from Anthropic here](https://anthropic.com/).

MacWindows

Copy

```
export ANTHROPIC_API_KEY=***
```

#### [​](https://docs.phidata.com/models/anthropic#example)Example <a href="#example" id="example"></a>

Use `Claude` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.anthropic import Claude

agent = Agent(
    model=Claude(id="claude-3-5-sonnet-20240620"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/anthropic#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"claude-3-5-sonnet-20240620"`

The id of the Anthropic Claude model to use

`name`

`str`

`"Claude"`

The name of the model

`provider`

`str`

`"Anthropic"`

The provider of the model

`max_tokens`

`Optional[int]`

`1024`

Maximum number of tokens to generate in the chat completion

`temperature`

`Optional[float]`

`None`

Controls randomness in the model's output

`stop_sequences`

`Optional[List[str]]`

`None`

A list of strings that the model should stop generating text at

`top_p`

`Optional[float]`

`None`

Controls diversity via nucleus sampling

`top_k`

`Optional[int]`

`None`

Controls diversity via top-k sampling

`request_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters to include in the request

`api_key`

`Optional[str]`

`None`

The API key for authenticating with Anthropic

`client_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters for client configuration

`client`

`Optional[AnthropicClient]`

`None`

A pre-configured instance of the Anthropic client
