---
description: GiphyTools enables an Agent to search for GIFs on GIPHY.
---

# Giphy

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Copy

```
export GIPHY_API_KEY=***
```

#### [​](https://docs.phidata.com/tools/giphy#example)Example <a href="#example" id="example"></a>

The following agent will search GIPHY for a GIF appropriate for a birthday message.

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.giphy import GiphyTools


gif_agent = Agent(
    name="Gif Generator Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[GiphyTools()],
    description="You are an AI agent that can generate gifs using Giphy.",
)

gif_agent.print_response("I want a gif to send to a friend for their birthday.")
```

#### [​](https://docs.phidata.com/tools/giphy#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

`None`

If you want to manually supply the GIPHY API key.

`limit`

`int`

`1`

The number of GIFs to return in a search.

#### [​](https://docs.phidata.com/tools/giphy#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`search_gifs`

Searches GIPHY for a GIF based on the query string.

#### [​](https://docs.phidata.com/tools/giphy#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/giphy.py)

[\
](https://VixData.gitbook.io/VixData/documentation/tools/firecrawl)
