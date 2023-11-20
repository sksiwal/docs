---
sidebar_position: 4
---

# Trigger a workflow

## Trigger asynchronously

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