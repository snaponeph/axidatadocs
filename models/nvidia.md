# Nvidia

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `NVIDIA_API_KEY` environment variable. Get your key [from Nvidia here](https://build.nvidia.com/explore/discover).

MacWindows

Copy

```
export NVIDIA_API_KEY=***
```

#### [​](https://docs.phidata.com/models/nvidia#example)Example <a href="#example" id="example"></a>

Use `Nvidia` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.nvidia import Nvidia

agent = Agent(model=Nvidia(), markdown=True)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story")
```

#### [​](https://docs.phidata.com/models/nvidia#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"nvidia/llama-3.1-nemotron-70b-instruct"`

The specific model ID used for generating responses.

`name`

`str`

`"Nvidia"`

The name identifier for the Nvidia agent.

`provider`

`str`

\-

The provider of the model, combining "Nvidia" with the model ID.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the Nvidia service. Retrieved from the environment variable `NVIDIA_API_KEY`.

`base_url`

`str`

`"https://integrate.api.nvidia.com/v1"`

The base URL for making API requests to the Nvidia service.

Nvidia also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
