---
description: ExaTools enable an Agent to search the web using Exa.
---

# Exa

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following examples requires the `exa-client` library and an API key which can be obtained from [Exa](https://exa.ai/).

Copy

```
pip install -U exa-client
```

Copy

```
export EXA_API_KEY=***
```

#### [​](https://docs.phidata.com/tools/exa#example)Example <a href="#example" id="example"></a>

The following agent will run seach exa for AAPL news and print the response.

cookbook/tools/exa\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.exa import ExaTools

agent = Agent(tools=[ExaTools(include_domains=["cnbc.com", "reuters.com", "bloomberg.com"])], show_tool_calls=True)
agent.print_response("Search for AAPL news", markdown=True)
```

#### [​](https://docs.phidata.com/tools/exa#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

\-

API key for authentication purposes.

`search`

`bool`

`False`

Determines whether to enable search functionality.

`search_with_contents`

`bool`

`True`

Indicates whether to include contents in the search results.

`show_results`

`bool`

`False`

Controls whether to display search results directly.

#### [​](https://docs.phidata.com/tools/exa#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`search_exa`

Searches Exa for a query.

`search_exa_with_contents`

Searches Exa for a query and returns the contents from the search results.

#### [​](https://docs.phidata.com/tools/exa#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/exa.py)

[\
](https://axidata.gitbook.io/axidata/documentation/tools/email)
