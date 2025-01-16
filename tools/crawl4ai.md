---
description: >-
  Crawl4aiTools enable an Agent to perform web crawling and scraping tasks using
  the Crawl4ai library.
---

# Crawl4AI

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `crawl4ai` library.

Copy

```
pip install -U crawl4ai
```

#### [​](https://docs.phidata.com/tools/crawl4ai#example)Example <a href="#example" id="example"></a>

The following agent will scrape the content from the [https://github.com/phidatahq/phidata](https://github.com/phidatahq/phidata) webpage:

cookbook/tools/crawl4ai\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.crawl4ai_tools import Crawl4aiTools

agent = Agent(tools=[Crawl4aiTools(max_length=None)], show_tool_calls=True)
agent.print_response("Tell me about https://github.com/phidatahq/phidata.")
```

#### [​](https://docs.phidata.com/tools/crawl4ai#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`max_length`

`int`

`1000`

Specifies the maximum length of the text from the webpage to be returned.

#### [​](https://docs.phidata.com/tools/crawl4ai#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`web_crawler`

Crawls a website using crawl4ai’s WebCrawler. Parameters include ‘url’ for the URL to crawl and an optional ‘max\_length’ to limit the length of extracted content. The default value for ‘max\_length’ is 1000.

#### [​](https://docs.phidata.com/tools/crawl4ai#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/crawl4ai_tools.py)
