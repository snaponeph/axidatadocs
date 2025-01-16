---
description: Use AWS Bedrock to access the Claude models.
---

# AWS Bedrock Claude

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` and `AWS_DEFAULT_REGION` environment variables. Get your keys from [here](https://us-west-2.console.aws.amazon.com/bedrock/home?region=us-west-2#/models).

MacWindows

Copy

```
export AWS_ACCESS_KEY_ID=***
export AWS_SECRET_ACCESS_KEY=***
export AWS_DEFAULT_REGION=***
```

#### [​](https://docs.phidata.com/models/aws-bedrock#example)Example <a href="#example" id="example"></a>

Use `AWS BedrockClaude` with your `Agent`:

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.aws.claude import Claude

agent = Agent(
    model=Claude(id="anthropic.claude-3-5-sonnet-20240620-v1:0"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/aws-bedrock#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"anthropic.claude-3-sonnet-20240229-v1:0"`

The specific model ID used for generating responses.

`name`

`str`

`"AwsBedrockAnthropicClaude"`

The name identifier for the Claude agent.

`provider`

`str`

`"AwsBedrock"`

The provider of the model.

`max_tokens`

`int`

`4096`

The maximum number of tokens to generate in the response.

`temperature`

`Optional[float]`

\-

The sampling temperature to use, between 0 and 2. Higher values like 0.8 make the output more random, while lower values like 0.2 make it more focused and deterministic.

`top_p`

`Optional[float]`

\-

The nucleus sampling parameter. The model considers the results of the tokens with top\_p probability mass.

`top_k`

`Optional[int]`

\-

The number of highest probability vocabulary tokens to keep for top-k-filtering.

`stop_sequences`

`Optional[List[str]]`

\-

A list of sequences where the API will stop generating further tokens.

`anthropic_version`

`str`

`"bedrock-2023-05-31"`

The version of the Anthropic API to use.

`request_params`

`Optional[Dict[str, Any]]`

\-

Additional parameters for the request, provided as a dictionary.

`client_params`

`Optional[Dict[str, Any]]`

\-

Additional client parameters for initializing the `AwsBedrock` client, provided as a dictionary.

