---
description: >-
  ComposioTools enable an Agent to work with tools like Gmail, Salesforce,
  Github, etc.
---

# Composio

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `composio-phidata` library.

Copy

```
pip install composio-phidata
composio add github # Login into Github
```

#### [​](https://docs.phidata.com/tools/composio#example)Example <a href="#example" id="example"></a>

The following agent will use Github Tool from Composio Toolkit to star a repo.

cookbook/tools/composio\_tools.py

Copy

```
from phi.agent import Agent
from composio_phidata import Action, ComposioToolSet


toolset = ComposioToolSet()
composio_tools = toolset.get_tools(
  actions=[Action.GITHUB_STAR_A_REPOSITORY_FOR_THE_AUTHENTICATED_USER]
)

agent = Agent(tools=composio_tools, show_tool_calls=True)
agent.print_response("Can you star phidatahq/phidata repo?")
```

#### [​](https://docs.phidata.com/tools/composio#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

The following parameters are used when calling the GitHub star repository action:

ParameterTypeDefaultDescription

`owner`

`str`

\-

The owner of the repository to star.

`repo`

`str`

\-

The name of the repository to star.

#### [​](https://docs.phidata.com/tools/composio#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

Composio Toolkit provides 1000+ functions to connect to different software tools. Open this [link](https://composio.dev/tools) to view the complete list of functions.

[\
](https://VixData.gitbook.io/VixData/documentation/tools/cal.com)
