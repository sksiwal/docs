---
sidebar_position: 13
---

# Access Control Management - Applications

## Authorization Client Initialization

```python
from conductor.client.configuration.configuration import Configuration
from conductor.client.configuration.settings.authentication_settings import AuthenticationSettings
from conductor.client.orkes.orkes_authorization_client import OrkesAuthorizationClient

configuration = Configuration(
    server_api_url=SERVER_API_URL,
    debug=False,
    authentication_settings=AuthenticationSettings(key_id=KEY_ID, key_secret=KEY_SECRET)
)

authorization_client = OrkesAuthorizationClient(configuration)
```

## Application Management

### Creating an Application

```python
from conductor.client.http.models.create_or_update_application_request import CreateOrUpdateApplicationRequest
from conductor.client.http.models.conductor_application import ConductorApplication

request = CreateOrUpdateApplicationRequest("APPLICATION_NAME")
app = authorization_client.createApplication(request)
application_id = app.id
```

Creates an application and returns a ConductorApplication object.

### Retreive Application

To retreive/get an application:

```python
app = authorization_client.getApplication(application_id)
```

To retrieve a list of applications:

```python
apps = authorization_client.listApplications()
```

### Update Application

To update an application:

```python
request = CreateOrUpdateApplicationRequest("APPLICATION_NAME")
updated_app = authorization_client.updateApplication(request, application_id)
```

### Delete Application

To delete an application:

```python
authorization_client.deleteApplication(application_id)
```

### Add a Role for an Application User

To add a specified role (e.g., USER, ADMIN, METADATA_MANAGER) to an application user:

```python
authorization_client.addRoleToApplicationUser(application_id, "USER")
```

### Remove a Role assigned to an Application User

To add a specified role (e.g., USER, ADMIN, METADATA_MANAGER) to an application user:

```python
authorization_client.removeRoleFromApplicationUser(application_id, "USER")
```

## Tag Management

### Set Tags to an Application

To set tags to an application:

```python
from conductor.client.orkes.models.metadata_tag import MetadataTag

tags = [
    MetadataTag("auth_tag", "val"), MetadataTag("auth_tag_2", "val2")
]
authorization_client.getApplicationTags(tags, application_id)
```

### Retrieve Application Tags

To retreive tags associated with an application:

```python
tags = authorization_client.getApplicationTags(application_id)
```

### Delete Application Tags

To delete tags from an application:

```python
tags = [
    MetadataTag("auth_tag", "val"), MetadataTag("auth_tag_2", "val2")
]
authorization_client.deleteApplicationTags(tags, application_id)
```

## Access Key Management

### Generate Access Key

Generates an access key for the specified application and returns the access key details, including the secret.

```python
from conductor.client.orkes.models.created_access_key import CreatedAccessKey

created_access_key = authorization_client.createAccessKey(application_id)
```

### Retrieve Access Key

Retrieves all access keys for the specified application as a list:

```python
from conductor.client.orkes.models.access_key import AccessKey

access_keys = authorization_client.getAccessKeys(application_id)
```

### Enabling/Disabling Access Key

Toggles the status of an access key between ACTIVE and INACTIVE.

```python
 access_key = authorization_client.toggleAccessKeyStatus(application_id, created_access_key.id)
```

### Delete Access Key

Deletes the specified access key associated with the application.

```python
authorization_client.deleteAccessKey(application_id, created_access_key.id)
```