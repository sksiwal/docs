---
sidebar_position: 6
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Send Signals to Workflow

The workflow is now running. Let's explore the SDKs for sending signals to control the execution of the workflow.

## Pause Workflow

To pause your running worklow, use the following SDK:

```python
WorkflowResourceApi.pause_workflow1(self, workflow_id, **kwargs)
```

Replace **workflow_id** with the workflow ID of the execution to be paused.

## Resume Workflow

To resume your paused worklow, use the following SDK:

```python
WorkflowResourceApi.resume_workflow1(self, workflow_id, **kwargs)
```

Replace **workflow_id** with the workflow ID of the paused execution.

## Restart Workflow

Use the following SDK to restart your running workflow:

```python
WorkflowResourceApi.restart1(self, workflow_id, **kwargs)
```
Replace **workflow_id** with the execution ID of the workflow.

## Re-run Workflow

The restart option restarts the workflow with either the current or latest definitions. However, if you want to run a new instance of the workflow by making changes to the workflow inputs, correlation ID, or task to domain mapping, you can utilize the rerun option.

```python
WorkflowResourceApi.rerun(self, body, workflow_id, **kwargs)
```

Replace **workflow_id** with the execution ID of the workflow.

## Terminate Workflow

Use the following SDK with the workflowId as the parameter to terminate your running workflow:

```python
TaskResourceApi.log(body, task_id, **kwargs)
```