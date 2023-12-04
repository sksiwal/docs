---
sidebar_position: 15
---

# Group Management

## Create/Update Group

Creates an user group or update an existing user group:

```python
from conductor.client.http.models.upsert_group_request import UpsertGroupRequest
from conductor.client.http.models.group import Group

group_id = 'test_group'
group_name = "Test Group"
group_user_roles = ["USER"]
req = UpsertGroupRequest("Integration Test Group", group_user_roles)
group = authorization_client.upsertGroup(req, group_id)
```

## Retreive Group

Fetches details of a specific group based on its ID.

```python
group = authorization_client.getGroup(group_id)
```

Retrieves the list of all groups available in the system as a list.

```python
users = authorization_client.listGroups()
```

## Delete Group

Removes a specific group from the system based on its ID.

```python
authorization_client.deleteGroup(group_id)
```

## Add Users to Group

Adds users to a specified group.


```python
authorization_client.addUserToGroup(group_id, user_id)
```

## Retreive All Users in a Group

Retrieves all users in a specific group.

```python
users = self.authorization_client.getUsersInGroup(group_id)
```

## Remove Users from a Group

Removes users from a specific group.

```python
authorization_client.removeUserFromGroup(group_id, user_id)
```

## Permission Management

### Grant Permissions

Grants a set of accesses to the specified Subject for a given Target.

```python
from conductor.client.http.models.target_ref import TargetRef, TargetType
from conductor.client.http.models.subject_ref import SubjectRef, SubjectType
from conductor.client.orkes.models.access_type import AccessType

target = TargetRef(TargetType.WORKFLOW_DEF, "TEST_WORKFLOW")
subject_group = SubjectRef(SubjectType.GROUP, group_id)
access_group = [AccessType.EXECUTE]

subject_user = SubjectRef(SubjectType.USER, user_id)
access_user = [AccessType.EXECUTE, AccessType.READ]

authorization_client.grantPermissions(subject_group, target, access_group)
authorization_client.grantPermissions(subject_user, target, access_user)
```

### Get Permissions for a Target

Returns all permissions associated with a specific target.

```python
from conductor.client.http.models.target_ref import TargetRef, TargetType

target = TargetRef(TargetType.WORKFLOW_DEF, WORKFLOW_NAME)
target_permissions = authorization_client.getPermissions(target)
```

### Get Permissions granted to a Group

Returns all permissions granted to a specific group.

```python
from conductor.client.orkes.models.granted_permission import GrantedPermission

group_permissions = authorization_client.getGrantedPermissionsForGroup(group_id)
```

### Get Permissions granted to a User

Returns all permissions granted to a specific user.

```python
from conductor.client.orkes.models.granted_permission import GrantedPermission

user_permissions = authorization_client.getGrantedPermissionsForUser(user_id)
```

### Remove Permissions

Removes a set of accesses from a specified Subject for a given Target.

```python
from conductor.client.http.models.target_ref import TargetRef, TargetType
from conductor.client.http.models.subject_ref import SubjectRef, SubjectType
from conductor.client.orkes.models.access_type import AccessType

target = TargetRef(TargetType.WORKFLOW_DEF, "TEST_WORKFLOW")
subject_group = SubjectRef(SubjectType.GROUP, group_id)
access_group = [AccessType.EXECUTE]

subject_user = SubjectRef(SubjectType.USER, user_id)
access_user = [AccessType.EXECUTE, AccessType.READ]

authorization_client.removePermissions(subject_group, target, access_group)
authorization_client.removePermissions(subject_user, target, access_user)
```