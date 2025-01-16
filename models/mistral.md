---
description: Mistral is a platform for providing endpoints for Large Language models.
---

# Mistral

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `MISTRAL_API_KEY` environment variable. Get your key from [here](https://console.mistral.ai/api-keys/).

MacWindows

Copy

```
export MISTRAL_API_KEY=***
```

#### [​](https://docs.phidata.com/models/mistral#example)Example <a href="#example" id="example"></a>

Use `Mistral` with your `Agent`:

agent.py

Copy

```
import os

from phi.agent import Agent, RunResponse
from phi.model.mistral import MistralChat

mistral_api_key = os.getenv("MISTRAL_API_KEY")

agent = Agent(
    model=MistralChat(
        id="mistral-large-latest",
        api_key=mistral_api_key,
    ),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/mistral#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"mistral-large-latest"`

The ID of the model.

`name`

`str`

`"MistralChat"`

The name of the model.

`provider`

`str`

`"Mistral"`

The provider of the model.

`temperature`

`Optional[float]`

`None`

Controls randomness in output generation.

`max_tokens`

`Optional[int]`

`None`

Maximum number of tokens to generate.

`top_p`

`Optional[float]`

`None`

Controls diversity of output generation.

`random_seed`

`Optional[int]`

`None`

Seed for random number generation.

`safe_mode`

`bool`

`False`

Enables content filtering.

`safe_prompt`

`bool`

`False`

Applies content filtering to prompts.

`response_format`

`Optional[Union[Dict[str, Any], ChatCompletionResponse]]`

`None`

Specifies the desired response format.

`request_params`

`Optional[Dict[str, Any]]`

`None`

Additional request parameters.

`api_key`

`Optional[str]`

`None`

Your Mistral API key.

`endpoint`

`Optional[str]`

`None`

Custom API endpoint URL.

`max_retries`

`Optional[int]`

`None`

Maximum number of API call retries.

`timeout`

`Optional[int]`

`None`

Timeout for API calls in seconds.

`client_params`

`Optional[Dict[str, Any]]`

`None`

Additional client parameters.

`mistral_client`

`Optional[Mistral]`

`None`

Custom Mistral client instance.
