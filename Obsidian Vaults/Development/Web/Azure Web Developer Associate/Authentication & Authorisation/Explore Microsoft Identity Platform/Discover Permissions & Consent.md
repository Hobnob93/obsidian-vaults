#azure #azure-wda 

# Discover Permissions & Consent
Apps integrating with Microsoft identity platform use an authorisation model to control use/admin access to data.

Microsoft identity platform uses [OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols) authorisation protocol.
It is a method allowing a third-party app access to web-hosted resources on behalf of a user.
Any web-hosted resource integrating has a resource identifier; `application ID URI`.
The same is true for any third-party resources integrating with identity platform.

Some examples of Microsoft's web-hosted resources:
- Microsoft Graph [=>](https://graph.microsoft.com)
- Microsoft's 365 Mail API: [=>](https://outlook.office.com)
- Azure Key Vault [=>](https://vault.azure.net)

Resources can define a set of permissions used to divide functionality of resource into smaller chunks.
Resource functionality chunking allows third-party apps to request only permissions needed to perform their function.
Users and admins can know what data app can access.

In *OAuth 2.0*, permission sets are called ==scopes==.
They're often referred to as ==permissions==.
A permission is represented as a `string` value.
App requests permissions it needs by specifying the permission in `scope` query parameter.
Identity platform supports well-defined [OpenID Connect scopes](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#openid-connect-scopes).
Also supports resource-based permissions by appending permission value on resource's ID URI (e.g. `https://graph.microsoft.com/Calendars.Read`).

Some high-privilege permissions can only be granted through admin consent.
This can be done through the [administrator consent endpoint](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#admin-restricted-permissions).

## Permission Types
Microsoft identity platform supports two types of permissions:
- **Delegated permissions**
	- Used by apps with a signed-in user
	- Either user or admin consents to permissions the app requests
	- App is delegated with permission to act as a signed-in user when it makes calls to a target resource
- **Application permissions**
	- Used by apps that run without a signed-in user
	- Such as services
	- Only an admin can consent to app permissions

## Consent Types
Apps rely on consent in order to gain access to resources or APIs.
There are a number of consent kinds app may need to know about.
- [[Static User Content]]
- [[Incremental & Dynamic User Consent]]
- [[Admin Consent]]

## Requesting Individual User Consent
An app can request permissions it needs by using `scope` query parameter.
App can send a request like the following:
```http
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize
	?client_id=<id-guid>
	&response_type=code
	&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
	&response_mode=query
	&scope=
		https%3A%2F%2Fgraph.microsoft.com%2Fcalendars.read%20
		https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
	&state=12345
```

The `scope` parameter is a space-separated list of delegated permissions that app is requesting.
Each permission indicated by appending permission value to resource's identifier.

After user enters their credentials, identity platform checks for matching record of *user content*.
If user hasn't consented to any requested perms, and admin hasn't authorised, identity asks user to grant them.