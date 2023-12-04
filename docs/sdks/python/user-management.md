---
sidebar_position: 14
---

# User Management

## Create/Update User

Creates a new user or updates an existing user.

```python
from conductor.client.http.models.upsert_user_request import UpsertUserRequest
from conductor.client.http.models.conductor_user import ConductorUser

user_id = 'test.user@company.com'
user_name = "Test User"
roles = ["USER"]
req = UpsertUserRequest(user_name, roles)
user = authorization_client.upsertUser(req, user_id)
```

## Retreive User

Fetches details of a specific user based on their user ID.

```python
user = authorization_client.getUser(user_id)
```

## List All Users

Retrieves a list of all users available in the system.

```python
users = authorization_client.listUsers()
```

## Delete User

Removes a specific user from the system based on their user ID.

```python
authorization_client.deleteUser(user_id)
```