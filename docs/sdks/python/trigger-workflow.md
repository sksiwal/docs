---
sidebar_position: 4
---

# Trigger a workflow

## Trigger asynchronously

### Start using StartWorkflowRequest

```python
workflow = ConductorWorkflow(
    executor=self.workflow_executor,
    name="WORKFLOW_NAME",
    description='Test Create Workflow',
    version=1
)
workflow.input_parameters(["a", "b"])
workflow >> SimpleTask("simple_task", "simple_task_ref")
workflowDef = workflow.to_workflow_def()

startWorkflowRequest = StartWorkflowRequest(
    name="WORKFLOW_NAME",
    version=1,
    workflow_def=workflowDef,
    input={ "a" : 15, "b": 3 }
)
workflow_id = workflow_client.startWorkflow(startWorkflowRequest)
```

### Start using Workflow Name

```python
wfInput = { "a" : 5, "b": "+", "c" : [7, 8] }
workflow_id = workflow_client.startWorkflowByName("WORKFLOW_NAME", wfInput)
```

## Trigger synchronous

The following command starts a workflow and waits until the workflow completes or the *waitUntilTask* completes.

```python
wfInput = { "a" : 5, "b": "+", "c" : [7, 8] }
requestId = "request_id"
version = 1
waitUntilTaskRef = "task_ref_name" # Optional
workflow_id = workflow_client.executeWorkflow(
    startWorkflowRequest, requestId, "WORKFLOW_NAME", version, waitUntilTaskRef
)
```