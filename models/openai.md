---
description: >-
  The GPT models are the best in class LLMs and used as the default LLM by
  Agents.
---

# OpenAI

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `OPENAI_API_KEY` environment variable. You can get one [from OpenAI here](https://platform.openai.com/account/api-keys).

MacWindows

Copy

```
export OPENAI_API_KEY=sk-***
```

#### [​](https://docs.phidata.com/models/openai#example)Example <a href="#example" id="example"></a>

Use `OpenAIChat` with your `Agent`:

agent.py

Copy

```

from phi.agent import Agent, RunResponse
from phi.model.openai import OpenAIChat

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/openai#params)Params <a href="#params" id="params"></a>

For more information, please refer to the [OpenAI docs](https://platform.openai.com/docs/api-reference/chat/create) as well.

NameTypeDefaultDescription

`id`

`str`

`"gpt-4o"`

The id of the OpenAI model to use.

`name`

`str`

`"OpenAIChat"`

The name of this chat model instance.

`provider`

`str`

`"OpenAI " + id`

The provider of the model.

`store`

`Optional[bool]`

`None`

Whether or not to store the output of this chat completion request for use in the model distillation or evals products.

`frequency_penalty`

`Optional[float]`

`None`

Penalizes new tokens based on their frequency in the text so far.

`logit_bias`

`Optional[Any]`

`None`

Modifies the likelihood of specified tokens appearing in the completion.

`logprobs`

`Optional[bool]`

`None`

Include the log probabilities on the logprobs most likely tokens.

`max_tokens`

`Optional[int]`

`None`

The maximum number of tokens to generate in the chat completion.

`presence_penalty`

`Optional[float]`

`None`

Penalizes new tokens based on whether they appear in the text so far.

`response_format`

`Optional[Any]`

`None`

An object specifying the format that the model must output.

`seed`

`Optional[int]`

`None`

A seed for deterministic sampling.

`stop`

`Optional[Union[str, List[str]]]`

`None`

Up to 4 sequences where the API will stop generating further tokens.

`temperature`

`Optional[float]`

`None`

Controls randomness in the model's output.

`top_logprobs`

`Optional[int]`

`None`

How many log probability results to return per token.

`user`

`Optional[str]`

`None`

A unique identifier representing your end-user.

`top_p`

`Optional[float]`

`None`

Controls diversity via nucleus sampling.

`extra_headers`

`Optional[Any]`

`None`

Additional headers to send with the request.

`extra_query`

`Optional[Any]`

`None`

Additional query parameters to send with the request.

`request_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters to include in the request.

`api_key`

`Optional[str]`

`None`

The API key for authenticating with OpenAI.

`organization`

`Optional[str]`

`None`

The organization to use for API requests.

`base_url`

`Optional[Union[str, httpx.URL]]`

`None`

The base URL for API requests.

`timeout`

`Optional[float]`

`None`

The timeout for API requests.

`max_retries`

`Optional[int]`

`None`

The maximum number of retries for failed requests.

`default_headers`

`Optional[Any]`

`None`

Default headers to include in all requests.

`default_query`

`Optional[Any]`

`None`

Default query parameters to include in all requests.

`http_client`

`Optional[httpx.Client]`

`None`

An optional pre-configured HTTP client.

`client_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters for client configuration.

`client`

`Optional[OpenAIClient]`

`None`

The OpenAI client instance.

`async_client`

`Optional[AsyncOpenAIClient]`

`None`

The asynchronous OpenAI client instance.

`structured_outputs`

`bool`

`False`

Whether to use the structured outputs from the Model.

`supports_structured_outputs`

`bool`

`True`

Whether the Model supports structured outputs.

`add_images_to_message_content`

`bool`

`True`

Whether to add images to the message content.

[\
](https://axidata.gitbook.io/axidata/documentation/models/introduction)
