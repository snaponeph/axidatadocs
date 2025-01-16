# Teams

We can combine multiple Agents to form a team and tackle tasks as a cohesive unit. Here’s a simple example that uses a team of agents to write an article about the top stories on hackernews.

hn\_team.py

Copy

```
from phi.agent import Agent
from phi.tools.hackernews import HackerNews
from phi.tools.duckduckgo import DuckDuckGo
from phi.tools.newspaper4k import Newspaper4k

hn_researcher = Agent(
    name="HackerNews Researcher",
    role="Gets top stories from hackernews.",
    tools=[HackerNews()],
)

web_searcher = Agent(
    name="Web Searcher",
    role="Searches the web for information on a topic",
    tools=[DuckDuckGo()],
    add_datetime_to_instructions=True,
)

article_reader = Agent(
    name="Article Reader",
    role="Reads articles from URLs.",
    tools=[Newspaper4k()],
)

hn_team = Agent(
    name="Hackernews Team",
    team=[hn_researcher, web_searcher, article_reader],
    instructions=[
        "First, search hackernews for what the user is asking about.",
        "Then, ask the article reader to read the links for the stories to get more information.",
        "Important: you must provide the article reader with the links to read.",
        "Then, ask the web searcher to search for each story to get more information.",
        "Finally, provide a thoughtful and engaging summary.",
    ],
    show_tool_calls=True,
    markdown=True,
)
hn_team.print_response("Write an article about the top 2 stories on hackernews", stream=True)
```

Run the script to see the output.

Copy

```
pip install -U openai duckduckgo-search newspaper4k lxml_html_clean phidata

python hn_team.py
```

#### [​](https://docs.phidata.com/agents/teams#how-to-build-agent-teams)How to build Agent Teams <a href="#how-to-build-agent-teams" id="how-to-build-agent-teams"></a>

1. Add a `name` and `role` parameter to the member Agents.
2. Create a Team Leader that can delegate tasks to team-members.
3. Use your Agent team just like you would use a regular Agent.

Open-ended Agentic teams are great to play with, but are not reliable for real-world problems that require high reliability.

They need constant oversight and can get confused on very complex tasks. This drawback should improve as models get better (eagerly waiting for gpt-5o).

In our experience, Agent teams work best for simple tasks that require a small number of steps. We highly recommend using Workflows for production applications.
