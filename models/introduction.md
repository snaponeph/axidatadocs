---
description: >-
  Introduction Language Models are machine-learning programs that are trained to
  understand natural language and code. They provide reasoning and planning
  capabilities to Agents.
---

# Introduction

Use any `model` with an Agent like:

Copy

```
from phi.agent import Agent
from phi.model.openai import OpenAIChat

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    description="Share 15 minute healthy recipes.",
    markdown=True,
)
agent.print_response("Share a breakfast recipe.", stream=True)
```

Phidata supports the following model providers:

* [OpenAI](https://docs.phidata.com/models/openai)
* [Anthropic](https://docs.phidata.com/models/anthropic)
* [AWS Bedrock](https://docs.phidata.com/models/aws-bedrock)
* [Azure](https://docs.phidata.com/models/azure)
* [Cohere](https://docs.phidata.com/models/cohere)
* [DeepSeek](https://docs.phidata.com/models/deepseek)
* [Fireworks](https://docs.phidata.com/models/fireworks)
* [Google](https://docs.phidata.com/models/google)
* [Groq](https://docs.phidata.com/models/groq)
* [Mistral](https://docs.phidata.com/models/mistral)
* [Ollama](https://docs.phidata.com/models/ollama)
* [OpenAI Like](https://docs.phidata.com/models/openai-like)
* [OpenRouter](https://docs.phidata.com/models/openrouter)
* [Sambanova](https://docs.phidata.com/models/sambanova)
* [Together](https://docs.phidata.com/models/together)
* [VertexAI](https://docs.phidata.com/models/vertexai)

[\
](https://axidata.gitbook.io/axidata/documentation/models)
