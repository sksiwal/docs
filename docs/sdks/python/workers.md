---
sidebar_position: 8
---

# Workers (Simple Tasks)

This section provides guidance on writing Python workers for simple tasks in three different styles: as a function, as a class, or as an annotation. Additionally, it covers running these workers using the TaskHandler and provides examples for each style.

## Worker as a Function

A Python worker can be implemented as a function using the following signature:

```python
ExecuteTaskFunction = Callable[
    [
        Union[Task, object]
    ],
    Union[TaskResult, object]
]
```

In other words:
* Input must be either a `Task` or an `object`
    * If it isn't a `Task`, the assumption is - you're expecting to receive the `Task.input_data` as the object
* Output must be either a `TaskResult` or an `object`
    * If it isn't a `TaskResult`, the assumption is - you're expecting to use the object as the `TaskResult.output_data`

**Example:**

```python
from conductor.client.http.models import Task, TaskResult
from conductor.client.http.models.task_result_status import TaskResultStatus

def execute(task: Task) -> TaskResult:
    task_result = TaskResult(
        task_id=task.task_id,
        workflow_instance_id=task.workflow_instance_id,
        worker_id='your_custom_id'
    )
    task_result.add_output_data('worker_style', 'function')
    task_result.status = TaskResultStatus.COMPLETED
    return task_result
```

If you like more details, you can look at all possible combinations of workers [here](https://github.com/conductor-sdk/conductor-python/blob/main/tests/integration/resources/worker/python/python_worker.py).

## Worker as a Class

Implement a worker as a class by extending the `WorkerInterface` class and providing the required `execute` method.

**Example:**

```python
from conductor.client.http.models import Task, TaskResult
from conductor.client.http.models.task_result_status import TaskResultStatus
from conductor.client.worker.worker_interface import WorkerInterface

class SimplePythonWorker(WorkerInterface):
    def execute(self, task: Task) -> TaskResult:
        task_result = self.get_task_result_from_task(task)
        task_result.add_output_data('worker_style', 'class')
        task_result.add_output_data('secret_number', 1234)
        task_result.add_output_data('is_it_true', False)
        task_result.status = TaskResultStatus.COMPLETED
        return task_result

    def get_polling_interval_in_seconds(self) -> float:
        # poll every 500ms
        return 0.5
```

## Worker as an Annotation

A worker can also be invoked by adding a `WorkerTask` decorator. Annotated workers are picked up by the `TaskHandler` during execution.

The arguments that can be passed when defining the decorated worker are:
1. **task_definition_name**: The definition of the conductor task that needs to be polled for.
2. **domain**: Optional routing domain of the worker to execute tasks with a specific domain
3. **worker_id**: An optional worker id used to identify the polling worker
4. **poll_interval**: Polling interval in seconds. Defaulted to 1 second if not passed.

**Example:**

```python
from conductor.client.worker.worker_task import WorkerTask

@WorkerTask(task_definition_name='python_annotated_task', domain='cool', worker_id='decorated', poll_interval=2.0)
def python_annotated_task(input) -> object:
    return {'message': 'python is so cool :)'}
```

## Run Workers

To run the workers, use the `TaskHandler` and configure it with the necessary settings.

```python
from conductor.client.configuration.settings.authentication_settings import AuthenticationSettings
from conductor.client.configuration.configuration import Configuration
from conductor.client.automator.task_handler import TaskHandler
from conductor.client.worker.worker import Worker

#### Add these lines if running on a Mac####
from multiprocessing import set_start_method
set_start_method('fork')
############################################

SERVER_API_URL = 'http://localhost:8080/api'
KEY_ID = '<KEY_ID>'
KEY_SECRET = '<KEY_SECRET>'

configuration = Configuration(
    server_api_url=SERVER_API_URL,
    debug=True,
    authentication_settings=AuthenticationSettings(
        key_id=KEY_ID,
        key_secret=KEY_SECRET
    ),
)

workers = [
    SimplePythonWorker(
        task_definition_name='python_task_example'
    ),
    Worker(
        task_definition_name='python_execute_example',
        execute_function=execute,
        poll_interval=0.25,
    )
]

# If there are decorated workers in your application, scan_for_annotated_workers should be set
# default value of scan_for_annotated_workers is False
with TaskHandler(workers, configuration, scan_for_annotated_workers=True) as task_handler:
    task_handler.start_processes()
    task_handler.join_processes()
```

To launch the workers, create a file (e.g., `main.py`) and run:

```shell
python3 main.py
```

For better performance with multiple workers of the same type, append more instances of the same worker to the workers list like this:

```python
workers = [
    SimplePythonWorker(
        task_definition_name='python_task_example'
    ),
    SimplePythonWorker(
        task_definition_name='python_task_example'
    ),
    SimplePythonWorker(
        task_definition_name='python_task_example'
    ),
    ...
]
```

```python
workers = [
    Worker(
        task_definition_name='python_task_example',
        execute_function=execute,
        poll_interval=0.25,
    ),
    Worker(
        task_definition_name='python_task_example',
        execute_function=execute,
        poll_interval=0.25,
    ),
    Worker(
        task_definition_name='python_task_example',
        execute_function=execute,
        poll_interval=0.25,
    )
    ...
]
```