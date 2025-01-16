---
description: FileTools enable an Agent to read and write files on the local file system.
---

# File

#### Example <a href="#example" id="example"></a>

The following agent will generate an answer and save it in a file.

cookbook/tools/file\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.file import FileTools

agent = Agent(tools=[FileTools()], show_tool_calls=True)
agent.print_response("What is the most advanced LLM currently? Save the answer to a file.", markdown=True)
```

#### [​](https://docs.phidata.com/tools/file#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

NameTypeDefaultDescription

`base_dir`

`Path`

\-

Specifies the base directory path for file operations.

`save_files`

`bool`

`True`

Determines whether files should be saved during the operation.

`read_files`

`bool`

`True`

Allows reading from files during the operation.

`list_files`

`bool`

`True`

Enables listing of files in the specified directory.

#### [​](https://docs.phidata.com/tools/file#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

NameDescription

`save_file`

Saves the contents to a file called `file_name` and returns the file name if successful.

`read_file`

Reads the contents of the file `file_name` and returns the contents if successful.

`list_files`

Returns a list of files in the base directory

#### [​](https://docs.phidata.com/tools/file#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/file.py)
