# HuggingFace

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `HF_TOKEN` environment. You can get one [from HuggingFace here](https://huggingface.co/settings/tokens).

MacWindows

Copy

```
export HF_TOKEN=***
```

#### [​](https://docs.phidata.com/models/huggingface#example)Example <a href="#example" id="example"></a>

Use `HuggingFace` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.huggingface import HuggingFaceChat

agent = Agent(
    model=HuggingFaceChat(
        id="meta-llama/Meta-Llama-3-8B-Instruct",
        max_tokens=4096,
    ),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/huggingface#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"meta-llama/Meta-Llama-3-8B-Instruct"`

The id of the HuggingFace model to use.

`name`

`str`

`"HuggingFaceChat"`

The name of this chat model instance.

`provider`

`str`

`"HuggingFace"`

The provider of the model.

`store`

`Optional[bool]`

\-

Whether or not to store the output of this chat completion request.

`frequency_penalty`

`Optional[float]`

\-

Penalizes new tokens based on their frequency in the text so far.

`logit_bias`

`Optional[Any]`

\-

Modifies the likelihood of specified tokens appearing in the completion.

`logprobs`

`Optional[bool]`

\-

Include the log probabilities on the logprobs most likely tokens.

`max_tokens`

`Optional[int]`

\-

The maximum number of tokens to generate in the chat completion.

`presence_penalty`

`Optional[float]`

\-

Penalizes new tokens based on whether they appear in the text so far.

`response_format`

`Optional[Any]`

\-

An object specifying the format that the model must output.

`seed`

`Optional[int]`

\-

A seed for deterministic sampling.

`stop`

`Optional[Union[str, List[str]]]`

\-

Up to 4 sequences where the API will stop generating further tokens.

`temperature`

`Optional[float]`

\-

Controls randomness in the model's output.

`top_logprobs`

`Optional[int]`

\-

How many log probability results to return per token.

`top_p`

`Optional[float]`

\-

Controls diversity via nucleus sampling.

`request_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters to include in the request.

`api_key`

`Optional[str]`

\-

The Access Token for authenticating with HuggingFace.

`base_url`

`Optional[Union[str, httpx.URL]]`

\-

The base URL for API requests.

`timeout`

`Optional[float]`

\-

The timeout for API requests.

`max_retries`

`Optional[int]`

\-

The maximum number of retries for failed requests.

`default_headers`

`Optional[Any]`

\-

Default headers to include in all requests.

`default_query`

`Optional[Any]`

\-

Default query parameters to include in all requests.

`http_client`

`Optional[httpx.Client]`

\-

An optional pre-configured HTTP client.

`client_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters for client configuration.

`client`

`Optional[InferenceClient]`

\-

The HuggingFace Hub Inference client instance.

`async_client`

`Optional[AsyncInferenceClient]`

\-

The asynchronous HuggingFace Hub client instance.
