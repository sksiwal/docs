---
sidebar_position: 1
---

# Installation & Setup

The Orkes Conductor Python SDK is available on GitHub at https://github.com/conductor-sdk/conductor-python. 

## Installation

You can install it using pip:

```shell
python3 -m pip install conductor-python
```

## Initialization

All server-related configurations are managed through the *Configuration* class during the initialization of an object. Use the following template:

```python
configuration = Configuration(
    server_api_url='https://play.orkes.io/api',
    debug=True
)
```

### Configuration Parameters:

* **server_api_url**: The Conductor server address. For a local server on port 8080, use http://localhost:8080/api.
* **debug**: Set to True for verbose logging, or False to display only errors.

### Authentication Settings (Optional)

To enable secure access, you may configure authentication settings using an access key and secret. Obtain these credentials through the [Security via Applications](/content/access-control-and-security/applications#generating-access-keys) process or refer to the [video guide](/content/how-to-videos/access-key-and-secret) on Getting Access Key and Secret for detailed instructions.

#### Example Authentication Configuration:

Once we have a key and secret, we can configure the app from properties or environment variables, as shown in this example:

```python
configuration = Configuration(
    authentication_settings=AuthenticationSettings(
        key_id='key',
        key_secret='secret'
    )
)
```

Remember to treat your application secrets with the same level of security as passwords.

## Related Topics

- Video Guide on [Getting Access Key and Secret](/content/how-to-videos/access-key-and-secret)
- [Access Control & Security](/content/category/access-control-and-security)

