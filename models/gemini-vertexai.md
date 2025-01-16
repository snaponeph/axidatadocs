---
description: >-
  VertexAI is Google’s cloud platform for building, training, and deploying
  machine learning models.
---

# Gemini - VertexAI



#### &#x20;Authentication <a href="#authentication" id="authentication"></a>

[Authenticate with Gcloud](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal)

#### [​](https://docs.phidata.com/models/vertexai#example)Example <a href="#example" id="example"></a>

Use `Gemini` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.vertexai import Gemini

agent = Agent(
    model=Gemini(id="gemini-1.5-flash"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/vertexai#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"claude-3-5-sonnet-20240620"`

The specific model ID used for generating responses.

`name`

`str`

`"Claude"`

The name identifier for the agent.

`provider`

`str`

`"Anthropic"`

The provider of the model.

`max_tokens`

`Optional[int]`

`1024`

The maximum number of tokens to generate in the response.

`temperature`

`Optional[float]`

\-

The sampling temperature to use, between 0 and 2. Higher values like 0.8 make the output more random, while lower values like 0.2 make it more focused and deterministic.

`stop_sequences`

`Optional[List[str]]`

\-

A list of sequences where the API will stop generating further tokens.

`top_p`

`Optional[float]`

\-

Nucleus sampling parameter. The model considers the results of the tokens with top\_p probability mass.

`top_k`

`Optional[int]`

\-

The number of highest probability vocabulary tokens to keep for top-k-filtering.

`request_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters to include in the request.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the service.

`client_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters for client configuration.

`client`

`Optional[AnthropicClient]`

\-

A pre-configured instance of the Anthropic client.
