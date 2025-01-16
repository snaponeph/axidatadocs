# AWS Lambda

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires the `boto3` library.

Copy

```
pip install openai boto3
```

#### [​](https://docs.phidata.com/tools/aws_lambda#example)Example <a href="#example" id="example"></a>

The following agent will use AWS Lambda to list all Lambda functions in our AWS account and invoke a specific Lambda function.

cookbook/tools/aws\_lambda\_tools.py

Copy

```

from phi.agent import Agent
from phi.tools.aws_lambda import AWSLambdaTool


# Create an Agent with the AWSLambdaTool
agent = Agent(
    tools=[AWSLambdaTool(region_name="us-east-1")],
    name="AWS Lambda Agent",
    show_tool_calls=True,
)

# Example 1: List all Lambda functions
agent.print_response("List all Lambda functions in our AWS account", markdown=True)

# Example 2: Invoke a specific Lambda function
agent.print_response("Invoke the 'hello-world' Lambda function with an empty payload", markdown=True)
```

#### [​](https://docs.phidata.com/tools/aws_lambda#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`region_name`

`str`

`"us-east-1"`

AWS region name where Lambda functions are located.

#### [​](https://docs.phidata.com/tools/aws_lambda#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`list_functions`

Lists all Lambda functions available in the AWS account.

`invoke_function`

Invokes a specific Lambda function with an optional payload. Takes `function_name` and optional `payload` parameters.

#### [​](https://docs.phidata.com/tools/aws_lambda#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/aws_lambda.py)
