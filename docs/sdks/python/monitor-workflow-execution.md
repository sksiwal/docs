---
sidebar_position: 5
---

# Monitoring Workflow Execution

This section outlines the SDK methods to retrieve details about workflow execution and task information.

## Get Workflow Details

To obtain comprehensive information about a workflow execution, including task details, use the following SDK:

```python
workflow = workflow_client.getWorkflow(workflow_id, True)
```

If you choose to exclude task details and retrieve only high-level workflow information, use the following SDK:

```python
workflow = workflow_client.getWorkflow(workflow_id, False)
```
## Get Task Logs

To retrieve task logs for a specific task, provide the **task_id** using the following SDK:

```python
taskLogs = task_client.getTaskLogs("task_id")
```

These methods enable you to monitor and analyze workflow executions and task-specific details, giving you valuable insights into the workflow's progress and performance.