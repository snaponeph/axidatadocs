# Prompts

We prompt Agents using `description` and `instructions` and a number of other settings. These settings are used to build the **system** prompt that is sent to the language model.

Understanding how these prompts are created will help you build better Agents.

The 2 key parameters are:

1. **Description**: A description that guides the overall behaviour of the agent.
2. **Instructions**: A list of precise, task-specific instructions on how to achieve its goal.

Description and instructions only provide a formatting benefit, we do not alter or abstract any information and you can always use `system_prompt` to provide your own system prompt.

#### [​](https://docs.phidata.com/agents/prompts#system-message)System message <a href="#system-message" id="system-message"></a>

The system message is created using `description`, `instructions` and a number of other settings. The `description` is added to the start of the system message and `instructions` are added as a list after `## Instructions`. For example:

instructions.py

Copy

```
from phi.agent import Agent

agent = Agent(
    description="You are a famous short story writer asked to write for a magazine",
    instructions=["You are a pilot on a plane flying from Hawaii to Japan."],
    markdown=True,
    debug_mode=True,
)
agent.print_response("Tell me a 2 sentence horror story.", stream=True)
```

Will translate to (set `debug_mode=True` to view the logs):

Copy

```
DEBUG    ============== system ==============
DEBUG    You are a famous short story writer asked to write for a magazine

         ## Instructions
         - You are a pilot on a plane flying from Hawaii to Japan.
         - Use markdown to format your answers.
DEBUG    ============== user ==============
DEBUG    Tell me a 2 sentence horror story.
DEBUG    ============== assistant ==============
DEBUG    As the autopilot disengaged inexplicably mid-flight over the Pacific, the pilot glanced at the copilot's seat
         only to find it empty despite his every recall of a full crew boarding. Hands trembling, he looked into the
         cockpit's rearview mirror and found his own reflection grinning back with blood-red eyes, whispering,
         "There's no escape, not at 30,000 feet."
DEBUG    **************** METRICS START ****************
DEBUG    * Time to first token:         0.4518s
DEBUG    * Time to generate response:   1.2594s
DEBUG    * Tokens per second:           63.5243 tokens/s
DEBUG    * Input tokens:                59
DEBUG    * Output tokens:               80
DEBUG    * Total tokens:                139
DEBUG    * Prompt tokens details:       {'cached_tokens': 0}
DEBUG    * Completion tokens details:   {'reasoning_tokens': 0}
DEBUG    **************** METRICS END ******************
```

#### [​](https://docs.phidata.com/agents/prompts#set-the-system-message-directly)Set the system message directly <a href="#set-the-system-message-directly" id="set-the-system-message-directly"></a>

You can manually set the system message using the `system_prompt` parameter.

Copy

```
from phi.agent import Agent

agent = Agent(system_prompt="Share a 2 sentence story about")
agent.print_response("Love in the year 12000.")
```

#### [​](https://docs.phidata.com/agents/prompts#user-message)User message <a href="#user-message" id="user-message"></a>

The input `message` sent to the `Agent.run()` or `Agent.print_response()` functions is used as the user message.

[**​**](https://docs.phidata.com/agents/prompts#user-message-when-enable-rag-true)**User message when `enable_rag=True`**

If the Agent is provided `knowledge`, and the `enable_rag=True`, the user message is set to:

Copy

```
user_prompt += f"""Use the following information from the knowledge base if it helps:"

## Context
{context}
"""
```

#### [​](https://docs.phidata.com/agents/prompts#default-system-message)Default system message <a href="#default-system-message" id="default-system-message"></a>

The Agent creates a default system message that can be customized using the following parameters:

ParameterTypeDefaultDescription

`description`

`str`

`None`

A description of the Agent that is added to the start of the system message.

`task`

`str`

`None`

Describe the task the agent should achieve.

`instructions`

`List[str]`

`None`

List of instructions added to the system prompt in `<instructions>` tags. Default instructions are also created depending on values for `markdown`, `output_model` etc.

`additional_context`

`str`

`None`

Additional context added to the end of the system message.

`expected_output`

`str`

`None`

Provide the expected output from the Agent. This is added to the end of the system message.

`extra_instructions`

`List[str]`

`None`

List of extra instructions added to the default system prompt. Use these when you want to add some extra instructions at the end of the default instructions.

`prevent_hallucinations`

`bool`

`False`

If True, add instructions to return “I don’t know” when the agent does not know the answer.

`prevent_prompt_injection`

`bool`

`False`

If True, add instructions to prevent prompt injection attacks.

`limit_tool_access`

`bool`

`False`

If True, add instructions for limiting tool access to the default system prompt if tools are provided

`markdown`

`bool`

`False`

Add an instruction to format the output using markdown.

`add_datetime_to_instructions`

`bool`

`False`

If True, add the current datetime to the prompt to give the agent a sense of time. This allows for relative times like “tomorrow” to be used in the prompt

`system_prompt`

`str`

`None`

System prompt: provide the system prompt as a string

`system_prompt_template`

`PromptTemplate`

`None`

Provide the system prompt as a PromptTemplate.

`use_default_system_message`

`bool`

`True`

If True, build a default system message using agent settings and use that.

`system_message_role`

`str`

`system`

Role for the system message.

Disable the default system message by setting `use_default_system_message=False`.

#### [​](https://docs.phidata.com/agents/prompts#default-user-message)Default user message <a href="#default-user-message" id="default-user-message"></a>

The Agent creates a default user message, which is either the input message or a message with the `context` if `enable_rag=True`. The default user message can be customized using:

ParameterTypeDefaultDescription

`enable_rag`

`bool`

`False`

Enable RAG by adding references from the knowledge base to the prompt.

`add_rag_instructions`

`bool`

`False`

If True, adds instructions for using the RAG to the system prompt (if knowledge is also provided). For example: add an instruction to prefer information from the knowledge base over its training data.

`add_history_to_messages`

`bool`

`False`

If true, adds the chat history to the messages sent to the Model.

`num_history_responses`

`int`

`3`

Number of historical responses to add to the messages.

`user_prompt`

`Union[List, Dict, str]`

`None`

Provide the user prompt as a string. Note: this will ignore the message sent to the run function.

`user_prompt_template`

`PromptTemplate`

`None`

Provide the user prompt as a PromptTemplate.

`use_default_user_message`

`bool`

`True`

If True, build a default user prompt using references and chat history.

`user_message_role`

`str`

`user`

Role for the user message.

Disable the default user message by setting `use_default_user_message=False`.
