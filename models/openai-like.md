---
description: >-
  Many providers like Together, Groq, Sambanova, etc support the OpenAI API
  format. Use the OpenAILike model to access them by replacing the base_url.
---

# OpenAI Like

#### Example <a href="#example" id="example"></a>

agent.py

Copy

```
from os import getenv
from phi.agent import Agent, RunResponse
from phi.model.openai.like import OpenAILike

agent = Agent(
    model=OpenAILike(
        id="mistralai/Mixtral-8x7B-Instruct-v0.1",
        api_key=getenv("TOGETHER_API_KEY"),
        base_url="https://api.together.xyz/v1",
    )
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/openai-like#params)Params <a href="#params" id="params"></a>

`OpenAILike` also support all the params of [OpenAIChat](https://docs.phidata.com/models/openai)

[\
](https://VixData.gitbook.io/VixData/documentation/models/openai)
