---
description: >-
  Sambanova is a platform for providing endpoints for Large Language models.
  Note that Sambanova currently does not support function calling.
---

# Sambanova

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `SAMBANOVA_API_KEY` environment variable. Get your key from [here](https://cloud.sambanova.ai/apis).

MacWindows

Copy

```
export SAMBANOVA_API_KEY=***
```

#### [​](https://docs.phidata.com/models/sambanova#example)Example <a href="#example" id="example"></a>

Use `Sambanova` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.sambanova import Sambanova

agent = Agent(model=Sambanova(), markdown=True)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/sambanova#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"Meta-Llama-3.1-8B-Instruct"`

The id of the Sambanova model to use

`name`

`str`

`"Sambanova"`

The name of this chat model instance

`provider`

`str`

`"Sambanova"`

The provider of the model

`api_key`

`Optional[str]`

`None`

The API key for authenticating with Sambanova (defaults to environment variable SAMBANOVA\_API\_KEY)

`base_url`

`str`

`"https://api.sambanova.ai/v1"`

The base URL for API requests

Sambanova also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
