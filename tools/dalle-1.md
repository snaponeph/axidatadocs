# Dalle

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

You need to install the `openai` library.

Copy

```
pip install openai
```

Set the `OPENAI_API_KEY` environment variable.

Copy

```
export OPENAI_API_KEY=****
```

#### [​](https://docs.phidata.com/tools/dalle#example)Example <a href="#example" id="example"></a>

The following agent will use DALL-E to generate an image based on a text prompt.

cookbook/tools/dalle\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.dalle import Dalle

# Create an Agent with the DALL-E tool
agent = Agent(tools=[Dalle()], name="DALL-E Image Generator")

# Example 1: Generate a basic image with default settings
agent.print_response("Generate an image of a futuristic city with flying cars and tall skyscrapers", markdown=True)

# Example 2: Generate an image with custom settings
custom_dalle = Dalle(model="dall-e-3", size="1792x1024", quality="hd", style="natural")

agent_custom = Agent(
    tools=[custom_dalle],
    name="Custom DALL-E Generator",
    show_tool_calls=True,
)

agent_custom.print_response("Create a panoramic nature scene showing a peaceful mountain lake at sunset", markdown=True)
```

#### [​](https://docs.phidata.com/tools/dalle#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`model`

`str`

`"dall-e-3"`

The DALL-E model to use

`n`

`int`

`1`

Number of images to generate

`size`

`str`

`"1024x1024"`

Image size (256x256, 512x512, 1024x1024, 1792x1024, or 1024x1792)

`quality`

`str`

`"standard"`

Image quality (standard or hd)

`style`

`str`

`"vivid"`

Image style (vivid or natural)

`api_key`

`str`

`None`

The OpenAI API key for authentication

#### [​](https://docs.phidata.com/tools/dalle#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`generate_image`

Generates an image based on a text prompt

#### [​](https://docs.phidata.com/tools/dalle#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/dalle.py)

[\
](https://axidata.gitbook.io/axidata/documentation/tools/csv)
