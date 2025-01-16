# Streaming

Workflows are all about control and flexibility. You have full control over the multi-agent process, how the input is processed, which agents are used and in what order.

You also have full control over how the output is streamed.

#### [​](https://docs.phidata.com/workflows/streaming#streaming)Streaming <a href="#streaming" id="streaming"></a>

To stream the output, yield an `Iterator[RunResponse]` from the `run()` method of your workflow.

news\_report\_generator.py

Copy

```
# Define the workflow
class GenerateNewsReport(Workflow):
    agent_1: Agent = ...

    agent_2: Agent = ...

    agent_3: Agent = ...

    def run(self, ...) -> Iterator[RunResponse]:
        # Run agents and gather the response
        # These can be batch responses, you can also stream intermediate results if you want
        final_agent_input = ...

        # Generate the final response from the writer agent
        agent_3_response_stream: Iterator[RunResponse] = self.agent_3.run(final_agent_input, stream=True)

        # Yield the response
        yield agent_3_response_stream


# Instantiate the workflow
generate_news_report = GenerateNewsReport()

# Run workflow and get the response as an iterator of RunResponse objects
report_stream: Iterator[RunResponse] = generate_news_report.run(...)

# Print the response
pprint_run_response(report_stream, markdown=True)
```

#### [​](https://docs.phidata.com/workflows/streaming#batch)Batch <a href="#batch" id="batch"></a>

Simply return a `RunResponse` object from the `run()` method of your workflow to return a single output.

news\_report\_generator.py

Copy

```
# Define the workflow
class GenerateNewsReport(Workflow):
    agent_1: Agent = ...

    agent_2: Agent = ...

    agent_3: Agent = ...

    def run(self, ...) -> RunResponse:
        # Run agents and gather the response
        final_agent_input = ...

        # Generate the final response from the writer agent
        agent_3_response: RunResponse = self.agent_3.run(final_agent_input)

        # Return the response
        return agent_3_response


# Instantiate the workflow
generate_news_report = GenerateNewsReport()

# Run workflow and get the response as a RunResponse object
report: RunResponse = generate_news_report.run(...)

# Print the response
pprint_run_response(report, markdown=True)
```
