---
description: DeepSeek is a platform for providing endpoints for Large Language models.
---

# DeepSeek

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `DEEPSEEK_API_KEY` environment variable. Get your key from [here](https://platform.deepseek.com/api_keys).

MacWindows

Copy

```
export DEEPSEEK_API_KEY=***
```

#### [​](https://docs.phidata.com/models/deepseek#example)Example <a href="#example" id="example"></a>

Use `DeepSeek` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.deepseek import DeepSeekChat

agent = Agent(model=DeepSeekChat(), markdown=True)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/deepseek#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"deepseek-chat"`

The specific model ID used for generating responses.

`name`

`str`

`"DeepSeekChat"`

The name identifier for the DeepSeek model.

`provider`

`str`

`"DeepSeek"`

The provider of the model.

`api_key`

`Optional[str]`

\-

The API key used for authenticating requests to the DeepSeek service. Retrieved from the environment variable `DEEPSEEK_API_KEY`.

`base_url`

`str`

`"https://api.deepseek.com"`

The base URL for making API requests to the DeepSeek service.

DeepSeek also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
