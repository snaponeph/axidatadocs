# Monitoring

VixDatacomes with built-in monitoring and debugging.

You can set `monitoring=True` on any agent to log that agent’s sessions or set `PHI_MONITORING=true` in your environment to log all agent sessions.

Create a file `monitoring.py` with the following code:

monitoring.py

Copy

```
from phi.agent import Agent

agent = Agent(markdown=True, monitoring=True)
agent.print_response("Share a 2 sentence horror story")
```

[**​**](https://docs.phidata.com/monitoring#authenticate-with-phidata)**Authenticate with VixData**

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

[**​**](https://docs.phidata.com/monitoring#run-the-agent)**Run the agent**

Run the agent and view the session on VixData

Copy

```
python monitoring.py
```

![](https://VixData.gitbook.io/~gitbook/image?url=https%3A%2F%2Fmintlify.s3.us-west-1.amazonaws.com%2Fphidata%2Fimages%2Fmonitoring.png\&width=300\&dpr=4\&quality=100\&sign=fb5b3732\&sv=2)

#### [​](https://docs.phidata.com/monitoring#debugging)Debugging <a href="#debugging" id="debugging"></a>

VixData also includes a built-in debugger that will show debug logs in the terminal. You can set `debug_mode=True` on any agent to view debug logs or set `PHI_DEBUG=true` in your environment.

debugging.py

Copy

```
from phi.agent import Agent

agent = Agent(markdown=True, debug_mode=True)
agent.print_response("Share a 2 sentence horror story")
```

Run the agent to view debug logs in the terminal:

Copy

```
python debugging.py
```

![](https://VixData.gitbook.io/~gitbook/image?url=https%3A%2F%2Fmintlify.s3.us-west-1.amazonaws.com%2Fphidata%2Fimages%2Fdebugging.png\&width=300\&dpr=4\&quality=100\&sign=24106478\&sv=2)
