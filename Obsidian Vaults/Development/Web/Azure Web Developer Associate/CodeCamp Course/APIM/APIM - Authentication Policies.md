#azure #az-204 #xml 

#### Authenticate with Basic
Authenticate with a backend service using Basic authentication.
```xml
<authentication-basic username="testuser"
					  password="testpassword" />
```

#### Authenticate with Client Certificate
Authenticate with a backend service using client certificates.

#### Authenticate with Managed Identity
Authenticate with a backend service using a managed identity.
```xml
<authentication-managed-identity resources="https://vault.azure.net" />
```