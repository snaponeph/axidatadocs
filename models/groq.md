---
description: Groq offers blazing-fast API endpoints for large language models
---

# Groq

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `GROQ_API_KEY` environment variable. Get your key from [here](https://console.groq.com/keys).

MacWindows

Copy

```
export GROQ_API_KEY=***
```

#### [​](https://docs.phidata.com/models/groq#example)Example <a href="#example" id="example"></a>

Use `Groq` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.groq import Groq

agent = Agent(
    model=Groq(id="llama3-groq-70b-8192-tool-use-preview"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/groq#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"llama3-groq-70b-8192-tool-use-preview"`

The specific model ID used for generating responses.

`name`

`str`

`"Groq"`

The name identifier for the agent.

`provider`

`str`

`"Groq"`

The provider of the model.

`frequency_penalty`

`Optional[float]`

\-

A number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.

`logit_bias`

`Optional[Any]`

\-

A JSON object that modifies the likelihood of specified tokens appearing in the completion by mapping token IDs to bias values between -100 and 100.

`logprobs`

`Optional[bool]`

\-

Whether to return log probabilities of the output tokens.

`max_tokens`

`Optional[int]`

\-

The maximum number of tokens to generate in the chat completion.

`presence_penalty`

`Optional[float]`

\-

A number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.

`response_format`

`Optional[Dict[str, Any]]`

\-

Specifies the format that the model must output. Setting to `{ "type": "json_object" }` enables JSON mode, ensuring the message generated is valid JSON.

`seed`

`Optional[int]`

\-

A seed value for deterministic sampling, ensuring repeated requests with the same seed and parameters return the same result.

`stop`

`Optional[Union[str, List[str]]]`

\-

Up to 4 sequences where the API will stop generating further tokens.

`temperature`

`Optional[float]`

\-

The sampling temperature to use, between 0 and 2. Higher values like 0.8 make the output more random, while lower values like 0.2 make it more focused and deterministic.

`top_logprobs`

`Optional[int]`

\-

The number of top log probabilities to return for each generated token.

`top_p`

`Optional[float]`

\-

Nucleus sampling parameter. The model considers the results of the tokens with top\_p probability mass.

`user`

`Optional[str]`

\-

A unique identifier representing your end-user, helping to monitor and detect abuse.

`request_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters to include in the request.

`api_key`

`Optional[str]`

\-

The API key for authenticating requests to the service.

`base_url`

`Optional[Union[str, httpx.URL]]`

\-

The base URL for making API requests to the service.

`timeout`

`Optional[int]`

\-

The timeout duration for requests, specified in seconds.

`max_retries`

`Optional[int]`

\-

The maximum number of retry attempts for failed requests.

`client_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters for client configuration.

`groq_client`

`Optional[GroqClient]`

\-

An instance of GroqClient provided for making API requests.
