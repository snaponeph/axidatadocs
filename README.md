---
description: Introduction
---

# Introduction

**Build agents and workflows to automate intelligent work.**

#### [​](https://docs.phidata.com/introduction#what-is-phidata)What is VixData? <a href="#what-is-phidata" id="what-is-phidata"></a>

VixData **is a framework for building multi-modal agents and workflows.**

* **Build agents with memory, knowledge, tools and reasoning.**
* **Build teams of agents that can work together to solve problems.**
* **Interact with your agents and workflows using a beautiful Agent UI.**

#### [​](https://docs.phidata.com/introduction#key-features)Key Features <a href="#key-features" id="key-features"></a>

* [Simple & Elegant](https://VixData.gitbook.io/VixData#simple-and-elegant)
* [Powerful & Flexible](https://VixData.gitbook.io/VixData#powerful-and-flexible)
* [Multi-Modal by default](https://VixData.gitbook.io/VixData#multi-modal-by-default)
* [Multi-Agent orchestration](https://VixData.gitbook.io/VixData#multi-agent-orchestration)
* [A beautiful Agent UI to chat with your agents](https://VixData.gitbook.io/VixData/agent-ui)
* [Agentic RAG built-in](https://VixData.gitbook.io/VixData/examples#agentic-rag)
* [Structured outputs](https://VixData.gitbook.io/VixData/examples#structured-outputs)
* [Reasoning built-in](https://VixData.gitbook.io/VixData/examples#reasoning-agent)
* [Monitoring & Debugging built-in](https://VixData.gitbook.io/VixData/monitoring)

#### [​](https://docs.phidata.com/introduction#install)Install <a href="#install" id="install"></a>

Copy

```
pip install -U VixData
```

#### [​](https://docs.phidata.com/introduction#simple-and-elegant)Simple & Elegant <a href="#simple-and-elegant" id="simple-and-elegant"></a>

VixData Agents are simple and elegant, resulting in minimal, beautiful code.

For example, you can create a web search agent in 10 lines of code.

web\_search.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo

web_agent = Agent(
    name="Web Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGo()],
    instructions=["Always include sources"],
    show_tool_calls=True,
    markdown=True,
)
web_agent.print_response("Tell me about OpenAI Sora?", stream=True)
```

[**​**](https://docs.phidata.com/introduction#setup)**Setup**

1

Setup your virtual environment

MacWindows

Copy

```
python3 -m venv ~/.venvs/aienv
source ~/.venvs/aienv/bin/activate
```

2

Install libraries

MacWindows

Copy

```
pip install -U VixData openai duckduckgo-search
```

3

Export your OpenAI key

VixData works with most model providers but for these examples let’s use OpenAI.

MacWindows

Copy

```
export OPENAI_API_KEY=sk-***
```

You can get an API key from [here](https://platform.openai.com/account/api-keys).

4

Run the agent

Copy

```
python web_search.py
```

#### [​](https://docs.phidata.com/introduction#powerful-and-flexible)Powerful & Flexible <a href="#powerful-and-flexible" id="powerful-and-flexible"></a>

Phidata agents can use multiple tools and follow instructions to achieve complex tasks.

For example, you can create a finance agent with tools to query financial data.

1

Create a finance agent

finance\_agent.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.yfinance import YFinanceTools

finance_agent = Agent(
    name="Finance Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
    instructions=["Use tables to display data"],
    show_tool_calls=True,
    markdown=True,
)
finance_agent.print_response("Summarize analyst recommendations for NVDA", stream=True)
```

2

Run the agent

Install libraries

Copy

```
pip install yfinance
```

Run the agent

Copy

```
python finance_agent.py
```

#### [​](https://docs.phidata.com/introduction#multi-modal-by-default)Multi-Modal by default <a href="#multi-modal-by-default" id="multi-modal-by-default"></a>

Phidata agents support text, images, audio and video.

For example, you can create an image agent that can understand images and make tool calls as needed

1

Create an image agent

image\_agent.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGo()],
    markdown=True,
)

agent.print_response(
    "Tell me about this image and give me the latest news about it.",
    images=["https://upload.wikimedia.org/wikipedia/commons/b/bf/Krakow_-_Kosciol_Mariacki.jpg"],
    stream=True,
)
```

2

Run the agent

Copy

```
python image_agent.py
```

#### [​](https://docs.phidata.com/introduction#multi-agent-orchestration)Multi-Agent orchestration <a href="#multi-agent-orchestration" id="multi-agent-orchestration"></a>

Phidata agents can work together as a team to achieve complex tasks.

1

Create an agent team

agent\_team.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo
from phi.tools.yfinance import YFinanceTools

web_agent = Agent(
    name="Web Agent",
    role="Search the web for information",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGo()],
    instructions=["Always include sources"],
    show_tool_calls=True,
    markdown=True,
)

finance_agent = Agent(
    name="Finance Agent",
    role="Get financial data",
    model=OpenAIChat(id="gpt-4o"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True)],
    instructions=["Use tables to display data"],
    show_tool_calls=True,
    markdown=True,
)

agent_team = Agent(
    team=[web_agent, finance_agent],
    instructions=["Always include sources", "Use tables to display data"],
    show_tool_calls=True,
    markdown=True,
)

agent_team.print_response("Summarize analyst recommendations and share the latest news for NVDA", stream=True)
```

2

Run the agent team

Run the agent team

Copy

```
python agent_team.py
```

#### [​](https://docs.phidata.com/introduction#continue-reading)Continue reading <a href="#continue-reading" id="continue-reading"></a>

* Chat with your Agents using a beautiful [Agent UI](https://docs.phidata.com/agent-ui).
* [More examples](https://docs.phidata.com/more-examples)
* [Monitoring & Debugging](https://docs.phidata.com/monitoring)
