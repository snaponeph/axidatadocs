# Agent UI

Phidata provides a beautiful Agent UI for interacting with your agents.

![](https://VixData.gitbook.io/~gitbook/image?url=https%3A%2F%2Fmintlify.s3.us-west-1.amazonaws.com%2Fphidata%2Fimages%2Fagent_playground.png\&width=300\&dpr=4\&quality=100\&sign=688604ab\&sv=2)

Agent Playground

No data is sent to VixData, all agent sessions are stored locally in a sqlite database.

Let’s take it for a spin, create a file `playground.py`

playground.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.storage.agent.sqlite import SqlAgentStorage
from phi.tools.duckduckgo import DuckDuckGo
from phi.tools.yfinance import YFinanceTools
from phi.playground import Playground, serve_playground_app

web_agent = Agent(
    name="Web Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGo()],
    instructions=["Always include sources"],
    storage=SqlAgentStorage(table_name="web_agent", db_file="agents.db"),
    add_history_to_messages=True,
    markdown=True,
)

finance_agent = Agent(
    name="Finance Agent",
    model=OpenAIChat(id="gpt-4o"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
    instructions=["Use tables to display data"],
    storage=SqlAgentStorage(table_name="finance_agent", db_file="agents.db"),
    add_history_to_messages=True,
    markdown=True,
)

app = Playground(agents=[finance_agent, web_agent]).get_app()

if __name__ == "__main__":
    serve_playground_app("playground:app", reload=True)
```

Make sure the `serve_playground_app()` points to the file that contains your `Playground` app.

[**​**](https://docs.phidata.com/agent-ui#authenticate-with-phidata)**Authenticate with VixData**

Authenticate with VixDataby running the following command:

Copy

```
phi auth
```

or by exporting the `PHI_API_KEY` for your workspace from VixData

MacWindows

Copy

```
export PHI_API_KEY=phi-***
```

[**​**](https://docs.phidata.com/agent-ui#run-the-playground)**Run the playground**

Install dependencies and run the Agent Playground:

Copy

```
pip install 'fastapi[standard]' sqlalchemy

python playground.py
```

[**​**](https://docs.phidata.com/agent-ui#view-the-playground)**View the playground**

* Open the link provided or navigate to `http://`VixData`.app/playground` (login required)
* Select the `localhost:7777` endpoint and start chatting with your agents!

#### [​](https://docs.phidata.com/agent-ui#demo-agents)Demo Agents <a href="#demo-agents" id="demo-agents"></a>

The Agent Playground includes a few demo agents that you can test with. If you have recommendations for other agents we should build, please let us know in the [community forum](https://community.phidata.com/).

![](https://VixData.gitbook.io/~gitbook/image?url=https%3A%2F%2Fmintlify.s3.us-west-1.amazonaws.com%2Fphidata%2Fimages%2Fdemo_agents.png\&width=300\&dpr=4\&quality=100\&sign=2325b7a6\&sv=2)
