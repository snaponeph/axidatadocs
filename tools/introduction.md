# Introduction

Tools are **functions** that an Agent can run like searching the web, running SQL, sending an email or calling APIs. Use tools integrate Agents with external systems. You can use any python function as a tool or use a pre-built **toolkit**. The general syntax is:

Copy

```
from phi.agent import Agent

agent = Agent(
    # Add functions or Toolkits
    tools=[...],
    # Show tool calls in the Agent response
    show_tool_calls=True
```
