---
description: Agents use tools to take actions and interact with external systems.
---

# Tools

Tools are functions that an Agent can run to achieve tasks. For example: searching the web, running SQL, sending an email or calling APIs. You can use any python function as a tool or use a pre-built **toolkit**. The general syntax is:

Copy

```
from phi.agent import Agent

agent = Agent(
    # Add functions or Toolkits
    tools=[...],
    # Show tool calls in the Agent response
    show_tool_calls=True
)
```

#### [​](https://docs.phidata.com/agents/tools#using-a-toolkit)Using a Toolkit <a href="#using-a-toolkit" id="using-a-toolkit"></a>

Phidata provides many pre-built **toolkits** that you can add to your Agents. For example, let’s use the DuckDuckGo toolkit to search the web.

You can find more toolkits in the [Toolkits](https://docs.phidata.com/tools/toolkits) guide.1

Create Web Search Agent

Create a file `web_search.py`

web\_search.py

Copy

```
from phi.agent import Agent
from phi.tools.duckduckgo import DuckDuckGo

agent = Agent(tools=[DuckDuckGo()], show_tool_calls=True, markdown=True)
agent.print_response("Whats happening in France?", stream=True)
```

2

Run the agent

Install libraries

Copy

```
pip install openai duckduckgo-search phidata
```

Run the agent

Copy

```
python web_search.py
```

#### [​](https://docs.phidata.com/agents/tools#writing-your-own-tools)Writing your own Tools <a href="#writing-your-own-tools" id="writing-your-own-tools"></a>

For more control, write your own python functions and add them as tools to an Agent. For example, here’s how to add a `get_top_hackernews_stories` tool to an Agent.

hn\_agent.py

Copy

```
import json
import httpx

from phi.agent import Agent


def get_top_hackernews_stories(num_stories: int = 10) -> str:
    """Use this function to get top stories from Hacker News.

    Args:
        num_stories (int): Number of stories to return. Defaults to 10.

    Returns:
        str: JSON string of top stories.
    """

    # Fetch top story IDs
    response = httpx.get('https://hacker-news.firebaseio.com/v0/topstories.json')
    story_ids = response.json()

    # Fetch story details
    stories = []
    for story_id in story_ids[:num_stories]:
        story_response = httpx.get(f'https://hacker-news.firebaseio.com/v0/item/{story_id}.json')
        story = story_response.json()
        if "text" in story:
            story.pop("text", None)
        stories.append(story)
    return json.dumps(stories)

agent = Agent(tools=[get_top_hackernews_stories], show_tool_calls=True, markdown=True)
agent.print_response("Summarize the top 5 stories on hackernews?", stream=True)
```

Read more about:

* [Available toolkits](https://docs.phidata.com/tools/toolkits)
* [Using functions as tools](https://docs.phidata.com/tools/functions)

#### [​](https://docs.phidata.com/agents/tools#attributes)Attributes <a href="#attributes" id="attributes"></a>

The following attributes allow an `Agent` to use tools

ParameterTypeDefaultDescription

`tools`

`List[Union[Tool, Toolkit, Callable, Dict, Function]]`

\-

A list of tools provided to the Model. Tools are functions the model may generate JSON inputs for.

`show_tool_calls`

`bool`

`False`

Print the signature of the tool calls in the Model response.

`tool_call_limit`

`int`

\-

Maximum number of tool calls allowed.

`tool_choice`

`Union[str, Dict[str, Any]]`

\-

Controls which (if any) tool is called by the model. “none” means the model will not call a tool and instead generates a message. “auto” means the model can pick between generating a message or calling a tool. Specifying a particular function via `{"type": "function", "function": {"name": "my_function"}}` forces the model to call that tool. “none” is the default when no tools are present. “auto” is the default if tools are present.

`read_chat_history`

`bool`

`False`

Add a tool that allows the Model to read the chat history.

`search_knowledge`

`bool`

`False`

Add a tool that allows the Model to search the knowledge base (aka Agentic RAG).

`update_knowledge`

`bool`

`False`

Add a tool that allows the Model to update the knowledge base.

`read_tool_call_history`

`bool`

`False`

Add a tool that allows the Model to get the tool call history.
