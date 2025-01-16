---
description: Use Google’s AI Studio to access the Gemini and Gemma models.
coverY: 0
---

# Gemini - AI Studio

#### Authentication <a href="#authentication" id="authentication"></a>

Set your `GOOGLE_API_KEY` environment variable. You can get one [from Google here](https://ai.google.dev/aistudio).

MacWindows

Copy

```
export GOOGLE_API_KEY=***
```

#### [​](https://docs.phidata.com/models/google#example)Example <a href="#example" id="example"></a>

Use `Gemini` with your `Agent`:

agent.py

Copy

```

from phi.agent import Agent, RunResponse
from phi.model.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-1.5-flash"),
    markdown=True,
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/google#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"gemini-1.5-flash"`

The specific Gemini model ID to use.

`name`

`str`

`"Gemini"`

The name of this Gemini model instance.

`provider`

`str`

`"Google"`

The provider of the model.

`function_declarations`

`Optional[List[FunctionDeclaration]]`

`None`

List of function declarations for the model.

`generation_config`

`Optional[Any]`

`None`

Configuration for text generation.

`safety_settings`

`Optional[Any]`

`None`

Safety settings for the model.

`generative_model_kwargs`

`Optional[Dict[str, Any]]`

`None`

Additional keyword arguments for the generative model.

`api_key`

`Optional[str]`

`None`

API key for authentication.

`client_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters for the client.

`client`

`Optional[GenerativeModel]`

`None`

The underlying generative model client.
