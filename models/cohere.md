---
description: Leverage Cohere’s powerful command models and more.
---

# Cohere

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `CO_API_KEY` environment variable. Get your key from [here](https://dashboard.cohere.com/api-keys).

MacWindows

Copy

```
export CO_API_KEY=***
```

#### [​](https://docs.phidata.com/models/cohere#example)Example <a href="#example" id="example"></a>

Use `CohereChat` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.cohere import CohereChat

agent = Agent(
    model=CohereChat(id="command-r-08-2024"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/cohere#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"command-r-08-2024"`

The specific model ID used for generating responses.

`name`

`str`

`"CohereChat"`

The name identifier for the agent.

`provider`

`str`

`"Cohere"`

The provider of the model.

`temperature`

`Optional[float]`

\-

The sampling temperature to use, between 0 and 2. Higher values like 0.8 make the output more random, while lower values like 0.2 make it more focused and deterministic.

`max_tokens`

`Optional[int]`

\-

The maximum number of tokens to generate in the response.

`top_k`

`Optional[int]`

\-

The number of highest probability vocabulary tokens to keep for top-k-filtering.

`top_p`

`Optional[float]`

\-

Nucleus sampling parameter. The model considers the results of the tokens with top\_p probability mass.

`frequency_penalty`

`Optional[float]`

\-

Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.

`presence_penalty`

`Optional[float]`

\-

Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.

`request_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters to include in the request.

`add_chat_history`

`bool`

`False`

Whether to add chat history to the Cohere messages instead of using the conversation\_id.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the Cohere service.

`client_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters for client configuration.

`cohere_client`

`Optional[CohereClient]`

\-

A pre-configured instance of the Cohere client.

[\
](https://axidata.gitbook.io/axidata/documentation/models/azure)
