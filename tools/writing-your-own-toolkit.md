# Writing your own Toolkit

Many advanced use-cases will require writing custom Toolkits. Here’s the general flow:

1. Create a class inheriting the `phi.tools.Toolkit` class.
2. Add your functions to the class.
3. **Important:** Register the functions using `self.register(function_name)`

Now your Toolkit is ready to use with an Agent. For example:

shell\_toolkit.py

Copy

```
from typing import List

from phi.tools import Toolkit
from phi.utils.log import logger


class ShellTools(Toolkit):
    def __init__(self):
        super().__init__(name="shell_tools")
        self.register(self.run_shell_command)

    def run_shell_command(self, args: List[str], tail: int = 100) -> str:
        """Runs a shell command and returns the output or error.

        Args:
            args (List[str]): The command to run as a list of strings.
            tail (int): The number of lines to return from the output.
        Returns:
            str: The output of the command.
        """
        import subprocess

        logger.info(f"Running shell command: {args}")
        try:
            logger.info(f"Running shell command: {args}")
            result = subprocess.run(args, capture_output=True, text=True)
            logger.debug(f"Result: {result}")
            logger.debug(f"Return code: {result.returncode}")
            if result.returncode != 0:
                return f"Error: {result.stderr}"
            # return only the last n lines of the output
            return "\n".join(result.stdout.split("\n")[-tail:])
        except Exception as e:
            logger.warning(f"Failed to run shell command: {e}")
            return f"Error: {e}"
```
