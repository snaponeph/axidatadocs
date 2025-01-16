---
description: >-
  One of our favorite features is using Agents to generate structured data (i.e.
  a pydantic model). Use this feature to extract features, classify data,
  produce fake data etc. The best part is that they
---

# Structured Output

#### Example <a href="#example" id="example"></a>

Let’s create an Movie Agent to write a `MovieScript` for us.

movie\_agent.py

Copy

```
from typing import List
from rich.pretty import pprint
from pydantic import BaseModel, Field
from phi.agent import Agent, RunResponse
from phi.model.openai import OpenAIChat


class MovieScript(BaseModel):
    setting: str = Field(..., description="Provide a nice setting for a blockbuster movie.")
    ending: str = Field(..., description="Ending of the movie. If not available, provide a happy ending.")
    genre: str = Field(
        ..., description="Genre of the movie. If not available, select action, thriller or romantic comedy."
    )
    name: str = Field(..., description="Give a name to this movie")
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(..., description="3 sentence storyline for the movie. Make it exciting!")


# Agent that uses JSON mode
json_mode_agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    description="You write movie scripts.",
    response_model=MovieScript,
)
# Agent that uses structured outputs
structured_output_agent = Agent(
    model=OpenAIChat(id="gpt-4o-2024-08-06"),
    description="You write movie scripts.",
    response_model=MovieScript,
    structured_outputs=True,
)


# Get the response in a variable
# json_mode_response: RunResponse = json_mode_agent.run("New York")
# pprint(json_mode_response.content)
# structured_output_response: RunResponse = structured_output_agent.run("New York")
# pprint(structured_output_response.content)

json_mode_agent.print_response("New York")
structured_output_agent.print_response("New York")
```

Run the script to see the output.

Copy

```
pip install -U phidata openai

python movie_agent.py
```

The output is an object of the `MovieScript` class, here’s how it looks:

Copy

```
# Using JSON mode
MovieScript(
│   setting='The bustling streets of New York City, filled with skyscrapers, secret alleyways, and hidden underground passages.',
│   ending='The protagonist manages to thwart an international conspiracy, clearing his name and winning the love of his life back.',
│   genre='Thriller',
│   name='Shadows in the City',
│   characters=['Alex Monroe', 'Eva Parker', 'Detective Rodriguez', 'Mysterious Mr. Black'],
│   storyline="When Alex Monroe, an ex-CIA operative, is framed for a crime he didn't commit, he must navigate the dangerous streets of New York to clear his name. As he uncovers a labyrinth of deceit involving the city's most notorious crime syndicate, he enlists the help of an old flame, Eva Parker. Together, they race against time to expose the true villain before it's too late."
)

# Use the structured output
MovieScript(
│   setting='In the bustling streets and iconic skyline of New York City.',
│   ending='Isabella and Alex, having narrowly escaped the clutches of the Syndicate, find themselves standing at the top of the Empire State Building. As the glow of the setting sun bathes the city, they share a victorious kiss. Newly emboldened and as an unstoppable duo, they vow to keep NYC safe from any future threats.',
│   genre='Action Thriller',
│   name='The NYC Chronicles',
│   characters=['Isabella Grant', 'Alex Chen', 'Marcus Kane', 'Detective Ellie Monroe', 'Victor Sinclair'],
│   storyline='Isabella Grant, a fearless investigative journalist, uncovers a massive conspiracy involving a powerful syndicate plotting to control New York City. Teaming up with renegade cop Alex Chen, they must race against time to expose the culprits before the city descends into chaos. Dodging danger at every turn, they fight to protect the city they love from imminent destruction.'
)
```

[\
](https://axidata.gitbook.io/axidata/documentation/agents/storage)
