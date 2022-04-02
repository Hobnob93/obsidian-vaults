#azure #az-204

# Explore Service Principals
App must be registered with *Azure Active Directory* (AAD) in order to delegate Identity and Access Management functions to *Azure Active Directory*.
When registering apps with *AAD*, you're creating an identity configuration for your app.
This allows it to integrate with *AAD*.

When you register an app in *Azure Portal*, you choose whether it is:
- **Single tenant**: only accessible in your tenant
- **Multi-tenant**: accessible in other tenants

If you register app in portal, an app object, as well as a service principal object, are automatically created in home tenant.
App also has a globally unique ID.
In portal, you can then add secrets or certificates and scopes to make app work.
Can customise sign-in dialog, too.

## Application Object
*AAD* is defined by one and only one app object.
This resides in *AAD* tenant where the app was registered (known as ==home tenant==).
An app object is used as a template or blueprint to create one or more service principal objects.
Service principals are created in every tenant where app is used.
Application has some static properties that are applied to all created service principals (or app instances).

Application object describes three aspects of an application:
- how service can issue tokens for application access
- resources app might need to access
- the actions the application can take

## Service Principal Object
Entity requiring access must be represented by a security principal in order for it to access resources secured by *AAD* tenant.
This is true for both users (principal) and applications (service principal).

Security principal defines the access policy and permissions for the user/app in the *AAD* tenant.
This enables core features, such as auth of user/app during sign-in, and authorisation during resource access.

There are three types of service principal:
- **Application**
	- The local representation, or app instance, of a global application object in a single tenant or directory
	- Created in each tenant where app is used and references globally unique app or object
	- Service principal object defines what app can actually do in specific tenant; who can access the app; what resources app can use
- **[Managed identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)**
	- Provide identity for apps to use when connecting to resources supporting *AAD* authentication
	- When enabled, a service principal representing managed identity is created in your tenant
	- Service principals representing managed identities can be granted access and permissions
	- They cannot be updated or modified directly
- **Legacy**
	- Service principal representing a legacy app created before app registrations were introduced
	- Or for an app created through legacy experiences
	- Can have credentials, service principal names, reply URLs, and other properties an authorised user can edit
	- Does not have associated app registration
	- Can only be used in tenant where it was created

## Relationship Between App Objects & Service Principals
App object is *global* representation of app across all tenants.
Service principal is *local* representation for use in specific tenant.
App object serves as template from which common and default properties are *derived* for use in creating corresponding service principal objects.

An application has:
- A 1:1 relationship with software app
- A 1:many relationship with corresponding service principal object(s)

Service principal must be created in each tenant where app is used.
Enables it to establish identity for sign-in and/or access to resources being secured by tenant.
Single-tenant app has only one service principal (in home tenant).
Created and consented for use during app registration.
Multi-tenant app also has a service principal created in each tenant where user from that tenant has consented to its use.