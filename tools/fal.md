---
description: FalTools enable an Agent to perform media generation tasks.
---

# Fal

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `fal_client` library and an API key which can be obtained from [Fal](https://fal.ai/).

Copy

```
pip install -U fal_client
```

Copy

```
export FAL_KEY=***
```

#### [​](https://docs.phidata.com/tools/fal#example)Example <a href="#example" id="example"></a>

The following agent will use FAL to generate any video requested by the user.

cookbook/tools/fal\_tools.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.fal_tools import FalTools

fal_agent = Agent(
    name="Fal Video Generator Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[FalTools("fal-ai/hunyuan-video")],
    description="You are an AI agent that can generate videos using the Fal API.",
    instructions=[
        "When the user asks you to create a video, use the `generate_media` tool to create the video.",
        "Return the URL as raw to the user.",
        "Don't convert video URL to markdown or anything else.",
    ],
    markdown=True,
    debug_mode=True,
    show_tool_calls=True,
)

fal_agent.print_response("Generate video of balloon in the ocean")
```

#### [​](https://docs.phidata.com/tools/fal#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

`None`

API key for authentication purposes.

`model`

`str`

`None`

The model to use for the media generation.

#### [​](https://docs.phidata.com/tools/fal#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`generate_media`

Generate either images or videos depending on the user prompt.

`image_to_image`

Transform an input image based on a text prompt.

#### [​](https://docs.phidata.com/tools/fal#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/fal_tools.py)
