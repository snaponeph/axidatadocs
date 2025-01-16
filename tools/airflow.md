# Airflow

#### Example <a href="#example" id="example"></a>

The following agent will use Airflow to save and read a DAG file.

cookbook/tools/airflow\_tools.py

Copy

```
from phi.agent import Agent
from phi.tools.airflow import AirflowToolkit

agent = Agent(
    tools=[AirflowToolkit(dags_dir="dags", save_dag=True, read_dag=True)], show_tool_calls=True, markdown=True
)


dag_content = """
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime, timedelta
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2024, 1, 1),
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}
# Using 'schedule' instead of deprecated 'schedule_interval'
with DAG(
    'example_dag',
    default_args=default_args,
    description='A simple example DAG',
    schedule='@daily',  # Changed from schedule_interval
    catchup=False
) as dag:
    def print_hello():
        print("Hello from Airflow!")
        return "Hello task completed"
    task = PythonOperator(
        task_id='hello_task',
        python_callable=print_hello,
        dag=dag,
    )
"""

agent.run(f"Save this DAG file as 'example_dag.py': {dag_content}")


agent.print_response("Read the contents of 'example_dag.py'")
```

#### [​](https://docs.phidata.com/tools/airflow#toolkit-params)Toolkit Params <a href="#toolkit-params" id="toolkit-params"></a>

ParameterTypeDefaultDescription

`dags_dir`

`Path` or `str`

`Path.cwd()`

Directory for DAG files

`save_dag`

`bool`

`True`

Whether to register the save\_dag\_file function

`read_dag`

`bool`

`True`

Whether to register the read\_dag\_file function

`name`

`str`

`"AirflowTools"`

The name of the tool

#### [​](https://docs.phidata.com/tools/airflow#toolkit-functions)Toolkit Functions <a href="#toolkit-functions" id="toolkit-functions"></a>

FunctionDescription

`save_dag_file`

Saves python code for an Airflow DAG to a file

`read_dag_file`

Reads an Airflow DAG file and returns the contents

#### [​](https://docs.phidata.com/tools/airflow#information)Information <a href="#information" id="information"></a>

* View on [Github](https://github.com/phidatahq/phidata/blob/main/phi/tools/airflow.py)
