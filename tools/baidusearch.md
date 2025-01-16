# BaiduSearch

BaiduSearch enables an Agent to search the web for information using the Baidu search engine.

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `baidusearch` library. To install BaiduSearch, run the following command:

Copy

```
pip install -U baidusearch
```

#### [​](https://docs.phidata.com/tools/baidusearch#example)Example <a href="#example" id="example"></a>

cookbook/tools/baidusearch\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.baidusearch import BaiduSearch

agent = Agent(
    tools=[BaiduSearch()],
    description="You are a search agent that helps users find the most relevant information using Baidu.",
    instructions=[
        "Given a topic by the user, respond with the 3 most relevant search results about that topic.",
        "Search for 5 results and select the top 3 unique items.",
        "Search in both English and Chinese.",
    ],
    show_tool_calls=True,
)
agent.print_response("What are the latest advancements in AI?", markdown=True)
```

#### [​](https://docs.phidata.com/tools/baidusearch#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`fixed_max_results`

`int`

\-

Sets a fixed number of maximum results to return. No default is provided, must be specified if used.

`fixed_language`

`str`

\-

Set the fixed language for the results.

`headers`

`Any`

\-

Headers to be used in the search request.

`proxy`

`str`

\-

Specifies a single proxy address as a string to be used for the HTTP requests.

`timeout`

`int`

`10`

Sets the timeout for HTTP requests, in seconds.

#### [​](https://docs.phidata.com/tools/baidusearch#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`baidu_search`

Use this function to search Baidu for a query.

#### [​](https://docs.phidata.com/tools/baidusearch#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/baidusearch.py)
