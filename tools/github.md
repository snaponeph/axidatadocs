---
description: >-
  GithubTools enables an Agent to access Github repositories and perform tasks
  such as listing open pull requests, issues and more.
---

# Github

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following examples requires the `PyGithub` library and a Github access token which can be obtained from [here](https://github.com/settings/tokens).

Copy

```
pip install -U PyGithub
```

Copy

```
export GITHUB_ACCESS_TOKEN=***
```

#### [​](https://docs.phidata.com/tools/github#example)Example <a href="#example" id="example"></a>

The following agent will search Google for the latest news about “Mistral AI”:

cookbook/tools/github\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.github import GithubTools

agent = Agent(
    instructions=[
        "Use your tools to answer questions about the repo: phidatahq/phidata",
        "Do not create any issues or pull requests unless explicitly asked to do so",
    ],
    tools=[GithubTools()],
    show_tool_calls=True,
)
agent.print_response("List open pull requests", markdown=True)
```

#### [​](https://docs.phidata.com/tools/github#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`access_token`

`str`

`None`

Github access token for authentication. If not provided, will use GITHUB\_ACCESS\_TOKEN environment variable.

`base_url`

`str`

`None`

Optional base URL for Github Enterprise installations.

`search_repositories`

`bool`

`True`

Enable searching Github repositories.

`list_repositories`

`bool`

`True`

Enable listing repositories for a user/organization.

`get_repository`

`bool`

`True`

Enable getting repository details.

`list_pull_requests`

`bool`

`True`

Enable listing pull requests for a repository.

`get_pull_request`

`bool`

`True`

Enable getting pull request details.

`get_pull_request_changes`

`bool`

`True`

Enable getting pull request file changes.

`create_issue`

`bool`

`True`

Enable creating issues in repositories.

#### [​](https://docs.phidata.com/tools/github#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`search_repositories`

Searches Github repositories based on a query.

`list_repositories`

Lists repositories for a given user or organization.

`get_repository`

Gets details about a specific repository.

`list_pull_requests`

Lists pull requests for a repository.

`get_pull_request`

Gets details about a specific pull request.

`get_pull_request_changes`

Gets the file changes in a pull request.

`create_issue`

Creates a new issue in a repository.

#### [​](https://docs.phidata.com/tools/github#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/github.py)
