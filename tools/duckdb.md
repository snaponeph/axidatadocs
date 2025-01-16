---
description: DuckDbTools enable an Agent to run SQL and analyze data using DuckDb.
---

# DuckDb

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

The following example requires DuckDB library. To install DuckDB, run the following command:

Copy

```
pip install duckdb
```

For more installation options, please refer to [DuckDB documentation](https://duckdb.org/docs/installation).

#### [​](https://docs.phidata.com/tools/duckdb#example)Example <a href="#example" id="example"></a>

The following agent will analyze the movies file using SQL and return the result.

cookbook/tools/duckdb\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.duckdb import DuckDbTools

agent = Agent(
    tools=[DuckDbTools()],
    show_tool_calls=True,
    system_prompt="Use this file for Movies data: https://phidata-public.s3.amazonaws.com/demo_data/IMDB-Movie-Data.csv",
)
agent.print_response("What is the average rating of movies?", markdown=True, stream=False)
```

#### [​](https://docs.phidata.com/tools/duckdb#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`db_path`

`str`

\-

Specifies the path to the database file.

`connection`

`DuckDBPyConnection`

\-

Provides an existing DuckDB connection object.

`init_commands`

`List`

\-

A list of initial SQL commands to run on database connection.

`read_only`

`bool`

`False`

Configures the database connection to be read-only.

`config`

`dict`

\-

Configuration options for the database connection.

`run_queries`

`bool`

`True`

Determines whether to run SQL queries during the operation.

`inspect_queries`

`bool`

`False`

Enables inspection of SQL queries without executing them.

`create_tables`

`bool`

`True`

Allows creation of tables in the database during the operation.

`summarize_tables`

`bool`

`True`

Enables summarization of table data during the operation.

`export_tables`

`bool`

`False`

Allows exporting tables to external formats during the operation.

#### [​](https://docs.phidata.com/tools/duckdb#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`show_tables`

Function to show tables in the database

`describe_table`

Function to describe a table

`inspect_query`

Function to inspect a query and return the query plan. Always inspect your query before running them.

`run_query`

Function that runs a query and returns the result.

`summarize_table`

Function to compute a number of aggregates over a table. The function launches a query that computes a number of aggregates over all columns, including min, max, avg, std and approx\_unique.

`get_table_name_from_path`

Get the table name from a path

`create_table_from_path`

Creates a table from a path

`export_table_to_path`

Save a table in a desired format (default: parquet). If the path is provided, the table will be saved under that path. Eg: If path is /tmp, the table will be saved as /tmp/table.parquet. Otherwise it will be saved in the current directory

`load_local_path_to_table`

Load a local file into duckdb

`load_local_csv_to_table`

Load a local CSV file into duckdb

`load_s3_path_to_table`

Load a file from S3 into duckdb

`load_s3_csv_to_table`

Load a CSV file from S3 into duckdb

`create_fts_index`

Create a full text search index on a table

`full_text_search`

Full text Search in a table column for a specific text/keyword

#### [​](https://docs.phidata.com/tools/duckdb#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/duckdb.py)
