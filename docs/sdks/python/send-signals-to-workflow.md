---
sidebar_position: 6
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Send Signals to Workflow

This section details the SDK methods for sending signals to control the execution of a running workflow. Explore the capabilities to pause, resume, restart, rerun, and terminate workflows as needed.

## Pause Workflow

To temporarily pause a running workflow, use the following SDK:

```python
workflow_client.pauseWorkflow(workflow_id)
```

Replace **workflow_id** with the workflow ID of the execution to be paused.

## Resume Workflow

To resume a paused workflow, use the following SDK:

```python
workflow_client.resumeWorkflow(workflow_id)
```

Replace **workflow_id** with the workflow ID of the paused execution.

## Restart Workflow

Restart a running workflow using the following SDK:

```python
workflow_client.restartWorkflow(workflow_id, useLatestDef=True)
```
Replace **workflow_id** with the execution ID of the workflow. The **useLatestDef** parameter allows you to restart the workflow with the latest definitions.

## Re-run Workflow

If you want to run a new instance of the workflow with changes to inputs, correlation ID, or task to domain mapping, utilize the rerun option:

```python
WorkflowResourceApi.rerun(self, body, workflow_id, **kwargs)
```

Replace **workflow_id** with the execution ID of the workflow.

## Terminate Workflow

To forcefully terminate a running workflow, use the following SDK with the workflow ID and termination reason as parameters:

```python
workflow_client.terminateWorkflow(workflow_id, "Termination reason")
```

These SDK methods provide flexibility in managing workflow execution, allowing you to adapt and control the flow as needed.