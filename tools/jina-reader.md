---
description: JinaReaderTools enable an Agent to perform web search tasks using Jina.
---

# Jina Reader

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `jina` library.

Copy

```
pip install -U jina
```

#### [​](https://docs.phidata.com/tools/jina_reader#example)Example <a href="#example" id="example"></a>

The following agent will use Jina API to summarize the content of [https://github.com/phidatahq](https://github.com/phidatahq)

cookbook/tools/jinareader\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.jina_tools import JinaReaderTools

agent = Agent(tools=[JinaReaderTools()])
agent.print_response("Summarize: https://github.com/phidatahq")
```

#### [​](https://docs.phidata.com/tools/jina_reader#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

\-

The API key for authentication purposes, retrieved from the configuration.

`base_url`

`str`

\-

The base URL of the API, retrieved from the configuration.

`search_url`

`str`

\-

The URL used for search queries, retrieved from the configuration.

`max_content_length`

`int`

\-

The maximum length of content allowed, retrieved from the configuration.

#### [​](https://docs.phidata.com/tools/jina_reader#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`read_url`

Reads the content of a specified URL using Jina Reader API. Parameters include `url` for the URL to read. Returns the truncated content or an error message if the request fails.

`search_query`

Performs a web search using Jina Reader API based on a specified query. Parameters include `query` for the search term. Returns the truncated search results or an error message if the request fails.

#### [​](https://docs.phidata.com/tools/jina_reader#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/jina_tools.py)
