#azure #az-204 

# Apply Best Practises to Microsoft Graph
## Authentication
App will need to acquire OAuth 2.0 access token.
Present this token to *MS Graph* in either of the following:
- HTTP *authorisation* request header, as a *Bearer* token if using [[Query Microsoft Graph Using REST|REST]]
- Graph client constructor, when using [[Query Microsoft Graph Using SDKs|client library]]

Use [[Explore Microsoft Authentication Library|MSAL]] to acquire access token.

## Consent & Authorisation
- **Use least privilege**
	- Only request permissions absolutely necessary
	- Only request perms when you need them
- **Use correct permission type based on scenarios**
	- If signed-in user present in app, use delegated permissions
	- Otherwise, use application permissions
- **Consider end user and admin experience**
	- Consider who will be consenting to your app
	- Ensure app requests permissions appropriately using [[Incremental & Dynamic User Consent|Incremental or Dynamic Consent]]
- **Consider multi-tenant applications**
	- Expect customers to have various app and consent controls in different states
	- Tenant admins can disable ability for end users to consent to apps
		- In this case, admin would need to consent on behalf of users
	- Tenant admins can set custom auth policies blocking users from reading other profiles
	- Or can limit self-service group creation to a limited set of users
		- In these cases, app should expect to handle 403 error responses on behalf of user

## Handle Responses Effectively
Apps should be prepared to handle different types of responses.
- **Pagination**
	- Results sometimes returned in multiple pages if there are a lot of results
	- App should always handle results as pages
- **Evolvable enumerations**
	- Adding members to existing enumerations can break apps already using these enums
	- Evolvable enums is mechanism *MS Graph* API uses to add new members to existing enumerations without causing a breaking change for apps.
	- By default, a `GET` operation only returns known members for properties of evolved enum types
	- App only needs to handle known members
	- Can opt-in to receive unknown members as well

## Storing Data Locally
App should make calls to *MS Graph* to retrieve data in real time as necessary.
Should only cache or store data if necessary for specific scenario.
Ensure scenario covered by privacy policy and terms of use.
App should implement proper retention and deletion policies.