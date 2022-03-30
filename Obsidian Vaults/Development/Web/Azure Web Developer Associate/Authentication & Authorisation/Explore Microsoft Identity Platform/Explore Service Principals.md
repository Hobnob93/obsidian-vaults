#azure #azure-wda 

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
	- The local representation, or app instance, of a global application object 