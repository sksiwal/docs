---
sidebar_position: 4
---

# Trigger a workflow

This SDK documentation provides guidance on triggering workflows using both synchronous and asynchronous approaches.

## Triggering a Workflow Asynchronously

To initiate a workflow asynchronously, follow these steps using the ***StartWorkflowRequest***:

1. Create a ConductorWorkflow instance.
2. Define input parameters.
3. Add tasks to the workflow.
4. Obtain the workflow definition.
5. Create a StartWorkflowRequest.
6. Start the workflow and retrieve the workflow ID.

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

To trigger a workflow using its name, use the following approach:

```python
wfInput = { "a" : 5, "b": "+", "c" : [7, 8] }
workflow_id = workflow_client.startWorkflowByName("WORKFLOW_NAME", wfInput)
```

## Triggering a Workflow Synchronously

Initiate a workflow synchronously using the ***executeWorkflow*** method:

```python
wfInput = { "a" : 5, "b": "+", "c" : [7, 8] }
requestId = "request_id"
version = 1
waitUntilTaskRef = "task_ref_name" # Optional
workflow_id = workflow_client.executeWorkflow(
    startWorkflowRequest, requestId, "WORKFLOW_NAME", version, waitUntilTaskRef
)
```

This command starts a workflow and waits until the workflow completes or the specified task *waitUntilTask* completes.