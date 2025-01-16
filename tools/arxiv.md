# Arxiv

ArxivTools enable an Agent to search for publications on Arxiv.

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `arxiv` and `pypdf` libraries.

Copy

```
pip install -U arxiv pypdf
```

#### [​](https://docs.phidata.com/tools/arxiv#example)Example <a href="#example" id="example"></a>

The following agent will run seach arXiv for “language models” and print the response.

cookbook/tools/arxiv\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.arxiv_toolkit import ArxivToolkit

agent = Agent(tools=[ArxivToolkit()], show_tool_calls=True)
agent.print_response("Search arxiv for 'language models'", markdown=True)
```

#### [​](https://docs.phidata.com/tools/arxiv#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`search_arxiv`

`bool`

`True`

Enables the functionality to search the arXiv database.

`read_arxiv_papers`

`bool`

`True`

Allows reading of arXiv papers directly.

`download_dir`

`Path`

\-

Specifies the directory path where downloaded files will be saved.

#### [​](https://docs.phidata.com/tools/arxiv#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`search_arxiv_and_update_knowledge_base`

This function searches arXiv for a topic, adds the results to the knowledge base and returns them.

`search_arxiv`

Searches arXiv for a query.

#### [​](https://docs.phidata.com/tools/arxiv#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/arxiv_toolkit.py)
