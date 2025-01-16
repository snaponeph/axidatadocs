# Reasoning

Reasoning is an **experimental feature** that enables an `Agent` to think through a problem step-by-step before jumping into a response. The Agent works through different ideas, validating and correcting as needed. Once it reaches a final answer, it will validate and provide a response. Let’s give it a try. Create a file `reasoning_agent.py`

reasoning\_agent.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = (
    "Three missionaries and three cannibals need to cross a river. "
    "They have a boat that can carry up to two people at a time. "
    "If, at any time, the cannibals outnumber the missionaries on either side of the river, the cannibals will eat the missionaries. "
    "How can all six people get across the river safely? Provide a step-by-step solution and show the solutions as an ascii diagram"
)

reasoning_agent = Agent(model=OpenAIChat(id="gpt-4o"), reasoning=True, markdown=True, structured_outputs=True)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the Reasoning Agent:

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python reasoning_agent.py
```

Reasoning is currently limited to OpenAI models and will break about 20% of the time. **It is not a replacement for o1.**

It is an experiment fueled by curiosity, combining COT and tool use. Set your expectations very low for this initial release. For example: It will not be able to count ‘r’s in ‘strawberry’.

#### [​](https://docs.phidata.com/agents/reasoning#how-to-use-reasoning)How to use reasoning <a href="#how-to-use-reasoning" id="how-to-use-reasoning"></a>

To add reasoning, set `reasoning=True`. When using reasoning with tools, do not use `structured_outputs=True` as gpt-4o cannot use tools with structured outputs.

Copy

```
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"),
    reasoning=True,
    markdown=True,
    structured_outputs=True,
)
reasoning_agent.print_response("How many 'r' are in the word 'supercalifragilisticexpialidocious'?", stream=True, show_full_reasoning=True)
```

#### [​](https://docs.phidata.com/agents/reasoning#reasoning-with-tools)Reasoning with tools <a href="#reasoning-with-tools" id="reasoning-with-tools"></a>

You can also use tools with a reasoning agent, but do not use `structured_outputs=True` as gpt-4o cannot use tools with structured outputs. Lets create a finance agent that can reason.

Reasoning with tools is currently limited to OpenAI models and will break about 20% of the time.

finance\_reasoning.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.yfinance import YFinanceTools

reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
    instructions=["Use tables to show data"],
    show_tool_calls=True,
    markdown=True,
    reasoning=True,
)
reasoning_agent.print_response("Write a report comparing NVDA to TSLA", stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai yfinance

export OPENAI_API_KEY=***

python finance_reasoning.py
```

#### [​](https://docs.phidata.com/agents/reasoning#more-reasoning-examples)More reasoning examples <a href="#more-reasoning-examples" id="more-reasoning-examples"></a>

[**​**](https://docs.phidata.com/agents/reasoning#logical-puzzles)**Logical puzzles**

logical\_puzzle.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = (
    "Three missionaries and three cannibals need to cross a river. "
    "They have a boat that can carry up to two people at a time. "
    "If, at any time, the cannibals outnumber the missionaries on either side of the river, the cannibals will eat the missionaries. "
    "How can all six people get across the river safely? Provide a step-by-step solution and show the solutions as an ascii diagram"
)
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python logical_puzzle.py
```

[**​**](https://docs.phidata.com/agents/reasoning#mathematical-proofs)**Mathematical proofs**

mathematical\_proof.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = "Prove that for any positive integer n, the sum of the first n odd numbers is equal to n squared. Provide a detailed proof."
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python mathematical_proof.py
```

[**​**](https://docs.phidata.com/agents/reasoning#scientific-research)**Scientific research**

scientific\_research.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = (
    "Read the following abstract of a scientific paper and provide a critical evaluation of its methodology,"
    "results, conclusions, and any potential biases or flaws:\n\n"
    "Abstract: This study examines the effect of a new teaching method on student performance in mathematics. "
    "A sample of 30 students was selected from a single school and taught using the new method over one semester. "
    "The results showed a 15% increase in test scores compared to the previous semester. "
    "The study concludes that the new teaching method is effective in improving mathematical performance among high school students."
)
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python scientific_research.py
```

[**​**](https://docs.phidata.com/agents/reasoning#ethical-dilemma)**Ethical dilemma**

ethical\_dilemma.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = (
    "You are a train conductor faced with an emergency: the brakes have failed, and the train is heading towards "
    "five people tied on the track. You can divert the train onto another track, but there is one person tied there. "
    "Do you divert the train, sacrificing one to save five? Provide a well-reasoned answer considering utilitarian "
    "and deontological ethical frameworks. "
    "Provide your answer also as an ascii art diagram."
)
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python ethical_dilemma.py
```

[**​**](https://docs.phidata.com/agents/reasoning#planning-an-itinerary)**Planning an itinerary**

planning\_itinerary.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = "Plan an itinerary from Los Angeles to Las Vegas"
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python planning_itinerary.py
```

[**​**](https://docs.phidata.com/agents/reasoning#creative-writing)**Creative writing**

creative\_writing.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

task = "Write a short story about life in 5000000 years"
reasoning_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"), reasoning=True, markdown=True, structured_outputs=True
)
reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

export OPENAI_API_KEY=***

python creative_writing.py
```
