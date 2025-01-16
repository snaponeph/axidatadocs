---
description: DuckDuckGo enables an Agent to search the web for information.
---

# DuckDuckGo

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `duckduckgo-search` library. To install DuckDuckGo, run the following command:

Copy

```
pip install -U duckduckgo-search
```

#### [​](https://docs.phidata.com/tools/duckduckgo#example)Example <a href="#example" id="example"></a>

cookbook/tools/duckduckgo.py

Copy

```
from phi.agent import Agent
from phi.tools.duckduckgo import DuckDuckGo

agent = Agent(tools=[DuckDuckGo()], show_tool_calls=True)
agent.print_response("Whats happening in France?", markdown=True)
```

#### [​](https://docs.phidata.com/tools/duckduckgo#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`search`

`bool`

`True`

Enables the use of the `duckduckgo_search` function to search DuckDuckGo for a query.

`news`

`bool`

`True`

Enables the use of the `duckduckgo_news` function to fetch the latest news via DuckDuckGo.

`fixed_max_results`

`int`

\-

Sets a fixed number of maximum results to return. No default is provided, must be specified if used.

`headers`

`Any`

\-

Accepts any type of header values to be sent with HTTP requests.

`proxy`

`str`

\-

Specifies a single proxy address as a string to be used for the HTTP requests.

`proxies`

`Any`

\-

Accepts a dictionary of proxies to be used for HTTP requests.

`timeout`

`int`

`10`

Sets the timeout for HTTP requests, in seconds.

#### [​](https://docs.phidata.com/tools/duckduckgo#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`duckduckgo_search`

Use this function to search DuckDuckGo for a query.

`duckduckgo_news`

Use this function to get the latest news from DuckDuckGo.

#### [​](https://docs.phidata.com/tools/duckduckgo#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/duckduckgo.py)

[\
](https://VixData.gitbook.io/VixData/documentation/tools/duckdb)
