# Ollama

Run Large Language Models locally with Ollama

[Ollama](https://ollama.com/) is a fantastic tool for running models locally. Install [ollama](https://ollama.com/) and run a model using

run modelserve

Copy

```
ollama run llama3.1
```

After you have the local model running, use the `Ollama` model to access them

#### [​](https://docs.phidata.com/models/ollama#example)Example <a href="#example" id="example"></a>

agent.py

Copy

```
from phi.agent import Agent, RunResponse
from phi.model.ollama import Ollama

agent = Agent(
    model=Ollama(id="llama3.1"),
    markdown=True
)

# Get the response in a variable
# run: RunResponse = agent.run("Share a 2 sentence horror story.")
# print(run.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story.")
```

#### [​](https://docs.phidata.com/models/ollama#params)Params <a href="#params" id="params"></a>

ParameterTypeDefaultDescription

`id`

`str`

`"llama3.2"`

The ID of the model to use.

`name`

`str`

`"Ollama"`

The name of the model.

`provider`

`str`

`"Ollama llama3.2"`

The provider of the model.

`format`

`Optional[str]`

`None`

The format of the response.

`options`

`Optional[Any]`

`None`

Additional options to pass to the model.

`keep_alive`

`Optional[Union[float, str]]`

`None`

The keep alive time for the model.

`request_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters to pass to the request.

`host`

`Optional[str]`

`None`

The host to connect to.

`timeout`

`Optional[Any]`

`None`

The timeout for the connection.

`client_params`

`Optional[Dict[str, Any]]`

`None`

Additional parameters to pass to the client.

`client`

`Optional[OllamaClient]`

`None`

A pre-configured instance of the Ollama client.

`async_client`

`Optional[AsyncOllamaClient]`

`None`

A pre-configured instance of the asynchronous Ollama client.
