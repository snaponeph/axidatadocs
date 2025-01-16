---
description: GoogleSearch enables an Agent to perform web crawling and scraping tasks.
---

# Google Search

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following examples requires the `googlesearch` and `pycountry` libraries.

Copy

```
pip install -U googlesearch-python pycountry
```

#### [​](https://docs.phidata.com/tools/googlesearch#example)Example <a href="#example" id="example"></a>

The following agent will search Google for the latest news about “Mistral AI”:

cookbook/tools/googlesearch\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.googlesearch import GoogleSearch

agent = Agent(
    tools=[GoogleSearch()],
    description="You are a news agent that helps users find the latest news.",
    instructions=[
        "Given a topic by the user, respond with 4 latest news items about that topic.",
        "Search for 10 news items and select the top 4 unique items.",
        "Search in English and in French.",
    ],
    show_tool_calls=True,
    debug_mode=True,
)
agent.print_response("Mistral AI", markdown=True)
```

#### [​](https://docs.phidata.com/tools/googlesearch#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`fixed_max_results`

`int`

`None`

Optional fixed maximum number of results to return.

`fixed_language`

`str`

`None`

Optional fixed language for the requests.

`headers`

`Any`

`None`

Optional headers to include in the requests.

`proxy`

`str`

`None`

Optional proxy to be used for the requests.

`timeout`

`int`

`None`

Optional timeout for the requests, in seconds.

#### [​](https://docs.phidata.com/tools/googlesearch#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`google_search`

Searches Google for a specified query. Parameters include `query` for the search term, `max_results` for the maximum number of results (default is 5), and `language` for the language of the search results (default is “en”). Returns the search results as a JSON formatted string.

#### [​](https://docs.phidata.com/tools/googlesearch#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/googlesearch.py)
