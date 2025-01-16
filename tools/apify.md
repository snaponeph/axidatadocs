# Apify

ApifyTools enable an Agent to access the Apify API and run actors.

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `apify-client` library and an API token which can be obtained from [Apify](https://apify.com/).

Copy

```
pip install -U apify-client
```

Copy

```
export MY_APIFY_TOKEN=***
```

#### [​](https://docs.phidata.com/tools/apify#example)Example <a href="#example" id="example"></a>

The following agent will use Apify to crawl the webpage: [https://docs.phidata.com/introduction](https://docs.phidata.com/introduction) and summarize it.

cookbook/tools/apify\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.apify import ApifyTools

agent = Agent(tools=[ApifyTools()], show_tool_calls=True)
agent.print_response("Tell me about https://docs.phidata.com/introduction", markdown=True)
```

#### [​](https://docs.phidata.com/tools/apify#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`api_key`

`str`

\-

API key for authentication purposes.

`website_content_crawler`

`bool`

`True`

Enables the functionality to crawl a website using website-content-crawler actor.

`web_scraper`

`bool`

`False`

Enables the functionality to crawl a website using web\_scraper actor.

#### [​](https://docs.phidata.com/tools/apify#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`website_content_crawler`

Crawls a website using Apify’s website-content-crawler actor.

`web_scrapper`

Scrapes a website using Apify’s web-scraper actor.

#### [​](https://docs.phidata.com/tools/apify#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/apify.py)
