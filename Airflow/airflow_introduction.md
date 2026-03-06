# Apache Airflow

## Introduction
- Apache Airflow is an open-source platform for developing, scheduling, and monitoring batch-oriented workflows.
- Airflow's extensible python framework enables you to build workflows that can connect with almost any technology.
- A web-based UI helps with visualizing, managing, and debugging workflows.
- Airflow is used by data engineers for orchestrating workflows or pipelines.
- A data pipeline's dependencies, progress, log, code, triggered tasks, and success criteria can be easily monitored using airflow.
- Workflows as Code:
  - Airflow workflows are defined entirely in python. This approach brings several advantages:
    - Dynamic - Pipelines are defined as code, enabling dynamic DAG generation and parametrization.
    - Extensible - The airflow framework includes a wide range of built-in operators and can be extended to fit your needs.
    - Flexible - Airflow leverages Jinja templating engine, allowing for rich customizations.
- Use Cases:
  - Airflow is mainly used for orchestration of batch workflows. It offers a flexible framework with a wide range of built-in operators and makes it easy to integrate with other technologies.
  - Workflows that have a clear start point, end point, and schedule are ideal for being managed using airflow.
- Benefits:
  - Version Control - Track changes and rollback to previous versions if needed.
  - Team Collaboration - Multiple developers can work on the same workflow codebase.
  - Testing - Validate pipeline functionality with unit and integration tests.
  - Extensibility - Customize workflows using a large ecosystem of existing components, or build your own.
- Disadvantages:
  - Airflow is only designed to handle finite, **batch-oriented** workflows.
  - While DAGs can be triggered using the CLI or REST API, airflow is **not intended** for continuously-running, event-driven, or streaming workflows.
  - Works better as an "infrastructure as code" solution than an interactive UI or CLI.
  - Some amount of coding is always required even if you use the UI or CLI.

## Architecture
- Airflow's architecture is designed for flexibility, scalability, and reliability. The architecture consists of a web server, scheduler, executor, and metadata database.
- Web Server:
  - This is the UI of airflow that can be used to get an overview of the overall health of a DAG and visualize different components and states of each component. The UI also provides access to useful logs and metrics related to a DAG and its components.
  - The UI allows you to view the underlying code used to build the DAG.
  - The UI, through the use of REST APIs, allows you to perform tasks such as triggering DAGs and tasks or getting the status of each task.
  - The UI provides options to manage configurations such as variables and connections.
  - The web server provides the ability to manage users, roles, and different configurations of the airflow setup.
  - The web server provides options to enabled role-based access control (RBAC), providing the ability to manage user permissions, including a user's ability to trigger or view a DAG.
- Scheduler:
  - The primary function of the scheduler is to continuously monitor the DAGs directory to identify and schedule tasks based on their dependencies and specified time intervals.
  - The scheduler is responsible for determining which tasks to execute and when. It interacts with the metadata database to store and retrieve task state and execution information.
- Executor:
  - The executor is responsible for allocating resources and running tasks on the specified worker nodes. The two types of executors in airflow are:
    - Sequential Executor - Sequentially executes tasks on a single worker node. Useful for testing and local development purposes, where parallelism is not a requirement.
    - Distributed Executor - Airflow supports distributed executors like Celery and Kubernetes Executors, which distribute execution of tasks across multiple worker nodes or containers. This enables parallel processing of tasks.
- Metadata Database:
  - Stores all of the configuration details, task states, and execution metadata.
  - Provides persistence and ensures airflow can recover gracefully from failures and resume tasks in their last known state.
  - Serves as a central repository for managing and monitoring task execution.

## Directed Acyclic Graphs (DAGs)
- A DAG is a mathematical structure consisting of nodes and edges. In airflow, a DAG represents a data pipeline or workflow with a clear start and end.
- The mathematical properties of DAGs make them useful for building data pipelines:
  - Directed - There is a clear direction of flow between tasks. A task can be either upstream, downstream, or parallel to another task.
  - Acyclic - There are no circular dependencies in a DAG. This means a task cannot depend on itself or depend on a task that depends on it.
  - Graph - A DAG is a structure consisting of nodes and edges. Nodes are tasks and edges are dependencies between tasks. Defining workflows as graphs helps visualize the entire workflow in a way that's easy to navigate and conceptualize.
- Each task in a DAG performs one unit of work, ranging from a simple python function to complex data transformation or calling an external resource.
- A DAG run is an instance of a DAG running at a specific point in time. A task instance is an instance of a task running at a specific point in time. Each DAG instance has a unique `run_id` and consists of one or more task instances.
- The history of previous DAG runs is stored in the airflow metadata database.
- DAG Run Properties:
  - A DAG run graph in the airflow UI contains information about the run, as well as the status of each task instance in the run. The different elements of a graph include:
    - `dag_id` - The unique identifier of the DAG.
    - `logical_date` - The point in time after which the DAG can be executed. Not necessarily the same as the time the DAG is actually executed.
    - `task_id` - Unique identifier of the task.
    - `task_state` - The status of the task instance in the DAG run. Possible states include `running`, `success`, `failed`, `skipped`, `restarting`, `up_for_retry`, `upstream_failed`, `queued`, `none`, `removed`, `deferred`, and `up_for_reschedule`. Each of these states causes the border of a node to be colored differently in the UI.
- DAG Statuses:
  - Queued - The time after which the DAG run can be created, but the scheduler has not created task instances for it yet.
  - Running - The DAG run is eligible to have task instances scheduled.
  - Success - All task instances are in a terminal state (`success`, `skipped`, `failed`, or `upstream_failed`) and all leaf tasks (tasks with no downstream tasks) are either in the state `success` or `skipped`. The duration bar of a successful DAG run is green.
  - Failed - All task instances are in a terminal state and at least one leaf task is either in the state `failed` or `upstream_failed`. The duration bar of a failed DAG run is red.
- Triggering a DAG:
  - Backfill - Mechanism by which you can create several DAG runs for dates in the past. Backfilled DAG runs include a curved arrow in their duration bar.
  - Scheduled - Triggered based on a DAG's schedule (daily, weekly, monthly, etc.). These DAG runs are managed by the airflow scheduler. The DAG run duration bar does not have an additional icon.
  - Manual - Triggered manually using the UI, CLI, or API. Manually triggered DAG runs include a play button in their duration bar.
  - Asset Triggered - Scheduled using data-aware scheduling. This means the DAG runs as soon as one or more airflow assets is updated. These updates can come from tasks in the same airflow instance, a call to the REST API, manually using the UI, or based on messages in a message queue. The DAG run duration bar includes an asset icon.
- Writing a DAG:
  - A DAG can be defined with a python file placed in an airflow project's DAG bundle. When using the Astro CLI with default settings, this is your `dags` folder. Airflow automatically parses all files in this folder every 5 minutes to check for new DAGs and parses existing DAGs to check for code changes every 30 seconds.
  - A DAG can be created in python by instantiating a DAG context using the DAG class and defining tasks within that context:
    ```
    # Import all packages needed at the top level of the DAG
    from airflow.sdk import DAG
    from airflow.providers.standard.operators.python import PythonOperator
    from pendulum import datetime

    def my_task_1_func():
        import time  # import packages only needed in the task function
        time.sleep(5)
        print(1)

    # Instantiate the DAG
    with DAG(
        dag_id="traditional_syntax_dag",
        start_date=datetime(2025, 4, 1),
        schedule="@daily",

    ):
        # Instantiate tasks within the DAG context
        my_task_1 = PythonOperator(
            task_id="my_task_1",
            python_callable=my_task_1_func,
        )
      
        my_task_2 = PythonOperator(
            task_id="my_task_2",
            python_callable=lambda: print(2),
        )

        # Define dependencies
        my_task_1 >> my_task_2 # Ensures task 2 runs after task 1.
    ```
- DAG-Level Parameters:
  - Airflow allows you to configure when and how a DAG runs by setting parameters in the DAG object. DAG-level parameters affect how the _entire_ DAG behaves, as opposed to task-level parameters that only affect a single task. Basic DAG-level parameters include:
    - `dag_id` - The name of the DAG, which must be unique for each DAG in the airflow environment. When using the `@dag` decorator without specifying the `dag_id`, the function name is used as the `dag_id`.
    - `start_date` - The date and time after which the DAG starts being scheduled.
    - `schedule` - The schedule for the DAG. There are many different ways to schedule a DAG. The default schedule is `None`, which means the DAG must be run manually.