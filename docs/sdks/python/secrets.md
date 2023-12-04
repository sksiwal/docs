---
sidebar_position: 12
---

# Storing Secrets

## Secret Client Initialization

```python
from conductor.client.configuration.configuration import Configuration
from conductor.client.configuration.settings.authentication_settings import AuthenticationSettings
from conductor.client.orkes.orkes_secret_client import OrkesSecretClient

configuration = Configuration(
    server_api_url=SERVER_API_URL,
    debug=False,
    authentication_settings=AuthenticationSettings(key_id=KEY_ID, key_secret=KEY_SECRET)
)

secret_client = OrkesSecretClient(configuration)
```

## Saving a Secret

To save a secret:

```python
secret_client.putSecret("SECRET_NAME", "SECRET_VALUE")
```

## Retreiving a Secret

To retrieve a specific secret value:

```python
value = secret_client.getSecret("SECRET_NAME")
```

## Listing Secret

To list all secret names:

```python
secret_names = secret_client.listAllSecretNames()
```

To list secret names that user can grant access to:

```python
secret_names = secret_client.listSecretsThatUserCanGrantAccessTo()
```

## Delete Secret

To delete a secret:

```python
secret_client.deleteSecret("SECRET_NAME")
```

## Adding Tags to Secrets

### Set Secret Tags

To set tags for a secret:

```python
from conductor.client.orkes.models.metadata_tag import MetadataTag

tags = [
    MetadataTag("sec_tag", "val"), MetadataTag("sec_tag_2", "val2")
]
secret_client.setSecretTags(tags, "SECRET_NAME")
```

### Retreiving Secret Tags

To retrieve tags associated with a secret:

```python
tags = secret_client.getSecretTags("SECRET_NAME")
```

### Deleting Secret Tags

To delete specific tags associated with a secret:

```python
tags = [
    MetadataTag("sec_tag", "val"), MetadataTag("sec_tag_2", "val2")
]
secret_client.deleteSecretTags(tags, "SECRET_NAME")
```