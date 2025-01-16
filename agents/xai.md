---
description: xAI is a platform for providing endpoints for Large Language models.
---

# xAI

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `XAI_API_KEY` environment variable. You can get one [from xAI here](https://console.x.ai/).

MacWindows

Copy

```
export XAI_API_KEY=sk-***
```

#### [​](https://docs.phidata.com/models/xai#example)Example <a href="#example" id="example"></a>

Use `xAI` with your `Agent`:

agent.py

Copy

```

from phi.agent import Agent, RunResponse
from phi.model.xai import xAI

agent = Agent(
    model=xAI(id="grok-beta"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/xai#params)Params <a href="#params" id="params"></a>

For more information, please refer to the [xAI docs](https://docs.x.ai/docs) as well.

#### [​](https://docs.phidata.com/models/xai#params-2)Params <a href="#params-2" id="params-2"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"grok-beta"`

The specific model ID used for generating responses.

`name`

`str`

`"xAI"`

The name identifier for the xAI agent.

`provider`

`str`

`"xAI"`

The provider of the model, combining "xAI" with the model ID.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the xAI service. Retrieved from the environment variable `XAI_API_KEY`.

`base_url`

`str`

`"https://api.xai.xyz/v1"`

The base URL for making API requests to the xAI service.

xAI also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
