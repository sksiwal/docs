---
sidebar_position: 9 
---

# Schedule a Workflow

This section provides guidance on scheduling workflows to run periodically using the Scheduler Client SDK. Learn how to initialize the scheduler, save schedules, retrieve schedule information, delete schedules, pause and resume schedules, and manage scheduler tags.

## Scheduler Client Initialization

Initialize the Scheduler Client by configuring the server API URL, authentication settings, and other necessary parameters.

```python
from conductor.client.configuration.configuration import Configuration
from conductor.client.configuration.settings.authentication_settings import AuthenticationSettings
from conductor.client.orkes.scheduler_client import SchedulerClient

configuration = Configuration(
    server_api_url=SERVER_API_URL,
    debug=False,
    authentication_settings=AuthenticationSettings(
        key_id=KEY_ID,
        key_secret=KEY_SECRET
    ),
)

scheduler_client = SchedulerClient(configuration)
```

### Saving Schedule

Save a schedule to run a workflow periodically using a cron expression.

```python
from conductor.client.http.models.save_schedule_request import SaveScheduleRequest
from conductor.client.http.models.start_workflow_request import StartWorkflowRequest

startWorkflowRequest = StartWorkflowRequest(
    name="WORKFLOW_NAME", workflow_def=workflowDef
)
saveScheduleRequest = SaveScheduleRequest(
    name="SCHEDULE_NAME",
    start_workflow_request=startWorkflowRequest,
    cron_expression= "0 */5 * ? * *"
)

scheduler_client.saveSchedule(saveScheduleRequest)
```

### Get Schedule

Retrieve information about a specific schedule or all schedules for a workflow.

#### Get a specific schedule
```python
scheduler_client.getSchedule("SCHEDULE_NAME")
```

#### Get all schedules
```python
scheduler_client.getAllSchedules()
```

#### Get all schedules for a workflow
```python
scheduler_client.getAllSchedules("WORKFLOW_NAME")
```

### Delete Schedule
Delete a specific schedule based on its name.

```python
scheduler_client.deleteSchedule("SCHEDULE_NAME")
```

### Pause and Resume Schedule

Pause or resume a specific schedule or all schedules.

#### Pause a schedule
```python
scheduler_client.pauseSchedule("SCHEDULE_NAME")
```

#### Pause all schedules
```python
scheduler_client.pauseAllSchedules()
```

#### Resume a scheduler
```python
scheduler_client.resumeSchedule("SCHEDULE_NAME")
```

#### Resume all schedules
```python
scheduler_client.resumeAllSchedules()
```
### Set, Get, and Delete Scheduler Tags

Manage metadata tags associated with schedules.

#### Set scheduler tags
```python
from conductor.client.orkes.models.metadata_tag import MetadataTag

tags = [
    MetadataTag("sch_tag", "val"), MetadataTag("sch_tag_2", "val2")
]
scheduler_client.setSchedulerTags(tags, "SCHEDULE_NAME")
```

#### Get scheduler tags
```python
tags = scheduler_client.getSchedulerTags("SCHEDULE_NAME")
```

#### Delete scheduler tags
```python
tags = [
    MetadataTag("sch_tag", "val"), MetadataTag("sch_tag_2", "val2")
]
scheduler_client.deleteSchedulerTags(tags, "SCHEDULE_NAME")
```