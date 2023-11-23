---
sidebar_position: 5
---

# Monitoring Workflow Execution

## Get Workflow Details

Use the following SDK to get the workflow execution including the task details:

```python
workflow = workflow_client.getWorkflow(workflow_id, True)
```

If you opt out for task details, then use the following SDK to get the workflow execution excluding the task details:

```python
workflow = workflow_client.getWorkflow(workflow_id, False)
```

Use the following SDK to get the task logs, by providing the task_id:

```python
taskLogs = task_client.getTaskLogs("task_id")
```