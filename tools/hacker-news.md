---
description: HackerNews enables an Agent to search Hacker News website.
---

# Hacker News

#### Example <a href="#example" id="example"></a>

The following agent will write an engaging summary of the users with the top 2 stories on hackernews along with the stories.

cookbook/tools/hackernews.py

Copy

```
from phi.agent import Agent
from phi.tools.hackernews import HackerNews

agent = Agent(
    name="Hackernews Team",
    tools=[HackerNews()],
    show_tool_calls=True,
    markdown=True,
)
agent.print_response(
    "Write an engaging summary of the "
    "users with the top 2 stories on hackernews. "
    "Please mention the stories as well.",
)
```

#### [​](https://docs.phidata.com/tools/hackernews#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`get_top_stories`

`bool`

`True`

Enables fetching top stories.

`get_user_details`

`bool`

`True`

Enables fetching user details.

#### [​](https://docs.phidata.com/tools/hackernews#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`get_top_hackernews_stories`

Retrieves the top stories from Hacker News. Parameters include `num_stories` to specify the number of stories to return (default is 10). Returns the top stories in JSON format.

`get_user_details`

Retrieves the details of a Hacker News user by their username. Parameters include `username` to specify the user. Returns the user details in JSON format.

#### [​](https://docs.phidata.com/tools/hackernews#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/hackernews.py)

[\
](https://axidata.gitbook.io/axidata/documentation/tools/google-search)
