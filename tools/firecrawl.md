---
description: FirecrawlTools enable an Agent to perform web crawling and scraping tasks.
---

# Firecrawl

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `firecrawl-py` library and an API key which can be obtained from [Firecrawl](https://firecrawl.dev/).

Copy

```
pip install -U firecrawl-py
```

Copy

```
export FIRECRAWL_API_KEY=***
```

#### [​](https://docs.phidata.com/tools/firecrawl#example)Example <a href="#example" id="example"></a>

The following agent will scrape the content from [https://finance.yahoo.com/](https://finance.yahoo.com/) and return a summary of the content:

cookbook/tools/firecrawl\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.firecrawl import FirecrawlTools

agent = Agent(tools=[FirecrawlTools(scrape=False, crawl=True)], show_tool_calls=True, markdown=True)
agent.print_response("Summarize this https://finance.yahoo.com/")
```

#### [​](https://docs.phidata.com/tools/firecrawl#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

`None`

Optional API key for authentication purposes.

`formats`

`List[str]`

`None`

Optional list of formats to be used for the operation.

`limit`

`int`

`10`

Maximum number of items to retrieve. The default value is 10.

`scrape`

`bool`

`True`

Enables the scraping functionality. Default is True.

`crawl`

`bool`

`False`

Enables the crawling functionality. Default is False.

#### [​](https://docs.phidata.com/tools/firecrawl#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`scrape_website`

Scrapes a website using Firecrawl. Parameters include `url` to specify the URL to scrape. The function supports optional formats if specified. Returns the results of the scraping in JSON format.

`crawl_website`

Crawls a website using Firecrawl. Parameters include `url` to specify the URL to crawl, and an optional `limit` to define the maximum number of pages to crawl. The function supports optional formats and returns the crawling results in JSON format.

#### [​](https://docs.phidata.com/tools/firecrawl#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/firecrawl.py)
