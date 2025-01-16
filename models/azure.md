---
description: Use the best in class GPT models using Azure’s OpenAI API.
---

# Azure

#### Authentication <a href="#authentication" id="authentication"></a>

Set your environment variables.

MacWindows

Copy

```
export AZURE_OPENAI_API_KEY=***
export AZURE_OPENAI_ENDPOINT=***
export AZURE_OPENAI_MODEL_NAME=***
export AZURE_OPENAI_DEPLOYMENT=***
# Optional:
# export AZURE_OPENAI_API_VERSION=***
```

#### [​](https://docs.phidata.com/models/azure#example)Example <a href="#example" id="example"></a>

Use `AzureOpenAIChat` with your `Agent`:

agent.py

Copy

```
import os
from typing import Iterator

from phi.agent import Agent, RunResponse
from phi.model.azure import AzureOpenAIChat

azure_model = AzureOpenAIChat(
    id=os.getenv("AZURE_OPENAI_MODEL_NAME"),
    api_key=os.getenv("AZURE_OPENAI_API_KEY"),
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    azure_deployment=os.getenv("AZURE_OPENAI_DEPLOYMENT"),
)

agent = Agent(
    model=azure_model,
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/azure#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

\-

The specific model ID used for generating responses. This field is required.

`name`

`str`

`"AzureOpenAIChat"`

The name identifier for the agent.

`provider`

`str`

`"Azure"`

The provider of the model.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the Azure OpenAI service.

`api_version`

`str`

`"2024-02-01"`

The version of the Azure OpenAI API to use.

`azure_endpoint`

`Optional[str]`

\-

The endpoint URL for the Azure OpenAI service.

`azure_deployment`

`Optional[str]`

\-

The deployment name or ID in Azure.

`base_url`

`Optional[str]`

\-

The base URL for making API requests to the Azure OpenAI service.

`azure_ad_token`

`Optional[str]`

\-

The Azure Active Directory token for authenticating requests.

`azure_ad_token_provider`

`Optional[Any]`

\-

The provider for obtaining Azure Active Directory tokens.

`organization`

`Optional[str]`

\-

The organization associated with the API requests.

`openai_client`

`Optional[AzureOpenAIClient]`

\-

An instance of AzureOpenAIClient provided for making API requests.

Azure also supports the params of [OpenAI](https://docs.phidata.com/models/openai).
