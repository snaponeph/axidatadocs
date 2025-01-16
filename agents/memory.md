# Memory

Phidata provides 3 types of memories for building a great Agent experience (AX):

1. **Chat History:** previous messages from the conversation, we recommend sending the last 3-5 messages to the model.
2. **User Memories:** notes and insights about the user, this helps the model personalize the response to the user.
3. **Summaries:** a summary of the conversation, which is added to the prompt when chat history gets too long.

Before we dive in, let’s understand the terminology:

* **Session:** Each conversation with an Agent is called a **session**. Sessions are identified by a `session_id`.
* **Run:** Every interaction (i.e. chat) within a session is called a **run**. Runs are identified by a `run_id`.
* **Messages:** are the individual messages sent to and received from the model. They have a `role` (`system`, `user` or `assistant`) and `content`.

**Sessions** are equivalent to **threads** in the OpenAI Assistant API.

#### [​](https://docs.phidata.com/agents/memory#built-in-memory)Built-in Memory <a href="#built-in-memory" id="built-in-memory"></a>

Every Agent comes with built-in memory that can be used to access the historical **runs** and **messages**. Access it using `agent.memory`

Show AgentMemory

[**​**](https://docs.phidata.com/agents/memory#example)**Example**

agent\_memory.py

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from rich.pretty import pprint


agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    # Set add_history_to_messages=true to add the previous chat history to the messages sent to the Model.
    add_history_to_messages=True,
    # Number of historical responses to add to the messages.
    num_history_responses=3,
    description="You are a helpful assistant that always responds in a polite, upbeat and positive manner.",
)

# -*- Create a run
agent.print_response("Share a 2 sentence horror story", stream=True)
# -*- Print the messages in the memory
pprint([m.model_dump(include={"role", "content"}) for m in agent.memory.messages])

# -*- Ask a follow up question that continues the conversation
agent.print_response("What was my first message?", stream=True)
# -*- Print the messages in the memory
pprint([m.model_dump(include={"role", "content"}) for m in agent.memory.messages])
```

#### [​](https://docs.phidata.com/agents/memory#persistent-memory)Persistent Memory <a href="#persistent-memory" id="persistent-memory"></a>

The built-in memory only lasts while the session is active. To persist memory across sessions, we can store Agent sessions in a database using `AgentStorage`.

Storage is a necessary component when building user facing AI products as any production application will require users to be able to “continue” their conversation with the Agent.

Let’s test this out, create a file `persistent_memory.py` with the following code:

persistent\_memory.py

Copy

```
import json

from rich.console import Console
from rich.panel import Panel
from rich.json import JSON

from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.storage.agent.sqlite import SqlAgentStorage


agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    # Store agent sessions in a database
    storage=SqlAgentStorage(table_name="agent_sessions", db_file="tmp/agent_storage.db"),
    # Set add_history_to_messages=true to add the previous chat history to the messages sent to the Model.
    add_history_to_messages=True,
    # Number of historical responses to add to the messages.
    num_history_responses=3,
    # The session_id is used to identify the session in the database
    # You can resume any session by providing a session_id
    # session_id="xxxx-xxxx-xxxx-xxxx",
    # Description creates a system prompt for the agent
    description="You are a helpful assistant that always responds in a polite, upbeat and positive manner.",
)

console = Console()


def print_chat_history(agent):
    # -*- Print history
    console.print(
        Panel(
            JSON(json.dumps([m.model_dump(include={"role", "content"}) for m in agent.memory.messages]), indent=4),
            title=f"Chat History for session_id: {agent.session_id}",
            expand=True,
        )
    )


# -*- Create a run
agent.print_response("Share a 2 sentence horror story", stream=True)
# -*- Print the chat history
print_chat_history(agent)

# -*- Ask a follow up question that continues the conversation
agent.print_response("What was my first message?", stream=True)
# -*- Print the chat history
print_chat_history(agent)
```

[**​**](https://docs.phidata.com/agents/memory#run-the-agent)**Run the agent**

Install dependencies and run the agent:

Copy

```
pip install openai sqlalchemy phidata

python persistent_memory.py
```

You can view the agent sessions in the sqlite database and continue any conversation by providing the same `session_id`.

Read more in the [storage](https://docs.phidata.com/agents/storage) section.

#### [​](https://docs.phidata.com/agents/memory#user-preferences-and-conversation-summaries)User preferences and conversation summaries <a href="#user-preferences-and-conversation-summaries" id="user-preferences-and-conversation-summaries"></a>

Along with storing chat history and run messages, `AgentMemory` can be extended to automatically classify and store user preferences and conversation summaries.

To do this, add a `db` to `AgentMemory` and set `create_user_memories=True` and `create_session_summary=True`

User memories are stored in the `AgentMemory` whereas session summaries are stored in the `AgentStorage` table with the rest of the session information.

User preferences and conversation summaries are currently only compatible with `OpenAI` and `OpenAILike` models. While Persistent Memory is compatible with all model providers.

#### [​](https://docs.phidata.com/agents/memory#example-2)Example <a href="#example-2" id="example-2"></a>

personalized\_memories\_and\_summaries.py

Copy

```
from rich.pretty import pprint

from phi.agent import Agent, AgentMemory
from phi.model.openai import OpenAIChat
from phi.memory.db.postgres import PgMemoryDb
from phi.storage.agent.postgres import PgAgentStorage

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    # Store the memories and summary in a database
    memory=AgentMemory(
        db=PgMemoryDb(table_name="agent_memory", db_url=db_url), create_user_memories=True, create_session_summary=True
    ),
    # Store agent sessions in a database
    storage=PgAgentStorage(table_name="personalized_agent_sessions", db_url=db_url),
    # Show debug logs so you can see the memory being created
    # debug_mode=True,
)

# -*- Share personal information
agent.print_response("My name is john billings?", stream=True)
# -*- Print memories
pprint(agent.memory.memories)
# -*- Print summary
pprint(agent.memory.summary)

# -*- Share personal information
agent.print_response("I live in nyc?", stream=True)
# -*- Print memories
pprint(agent.memory.memories)
# -*- Print summary
pprint(agent.memory.summary)

# -*- Share personal information
agent.print_response("I'm going to a concert tomorrow?", stream=True)
# -*- Print memories
pprint(agent.memory.memories)
# -*- Print summary
pprint(agent.memory.summary)

# Ask about the conversation
agent.print_response("What have we been talking about, do you know my name?", stream=True)
```

#### [​](https://docs.phidata.com/agents/memory#attributes)Attributes <a href="#attributes" id="attributes"></a>

ParameterTypeDefaultDescription

`memory`

`AgentMemory`

`AgentMemory()`

Agent’s memory object used for storing and retrieving information.

`add_history_to_messages`

`bool`

`False`

If true, adds the chat history to the messages sent to the Model. Also known as `add_chat_history_to_messages`.

`num_history_responses`

`int`

`3`

Number of historical responses to add to the messages.

`create_user_memories`

`bool`

`False`

If true, create and store personalized memories for the user.

`update_user_memories_after_run`

`bool`

`True`

If true, update memories for the user after each run.

`create_session_summary`

`bool`

`False`

If true, create and store session summaries.

`update_session_summary_after_run`

`bool`

`True`

If true, update session summaries after each run.
