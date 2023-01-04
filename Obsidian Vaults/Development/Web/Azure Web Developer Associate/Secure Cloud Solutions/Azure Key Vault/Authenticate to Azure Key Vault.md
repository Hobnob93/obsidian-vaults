#azure #az-204 

## Overview
Authentication works in conjunction with [[About Azure Active Directory|Azure Active Directory]], which is responsible for authenticating identity of any given security principal.

For applications, there are ==two== ways to obtain a service principal:
- Enable system-assigned __managed identity__ for the application.
	- Azure internally manages the app's service principal
	- Automatically authenticates the app with other Azure services
	- Available for apps deployed to a variety of services
	- ==Recommended== by Azure
- Register the application with __Azure AD Tenant__
	- Use this when managed identity cannot be used
	- Registration creates a second app object that identifies the app across all tenants

## Authentication in Application Code
Key Vault SDK is using Azure Identity client library
- Allows seamless authentication to vaults across environments
- Uses the same code
- Table below provides information on client libraries

| .NET                    | Python                    | Java                         | JavaScript                    |
| ----------------------- | ------------------------- | ---------------------------- | ----------------------------- |
| [Azure Identity SDK .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/identity-readme) | [Azure Identity SDK Python](https://learn.microsoft.com/en-us/python/api/overview/azure/identity-readme) | [Azure Identity SDK Java](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)      | [Azure Identity SDK JavaScript](https://learn.microsoft.com/en-us/javascript/api/overview/azure/identity-readme) |

## Authentication with REST
Access tokens must be sent to the service using the HTTP Authorization header:
```http
PUT /keys/MYKEY?api-version=<api_version>  HTTP/1.1
Authorization: Bearer <access_token>
```

When access token not supplied, or token not accepted by service, an HTTP 401 will be returned to client and will include the `WWW-Authenticate` header. E.g.:
```http
401 Not Authorized
WWW-Authenticate: Bearer authorization="...", resource="..."
```
The parameters in the `WWW-Authenticate` header are:
- `authorization`
	- Address of OAuth2 authorisation service that may be used to obtain an access token for the request
- `resource`
	- Name of the resource to use the in the authorisation request