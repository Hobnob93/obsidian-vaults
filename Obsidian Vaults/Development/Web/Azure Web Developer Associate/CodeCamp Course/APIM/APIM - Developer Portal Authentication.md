#azure #az-204 

You can configure many different types of authentications within APIM:
- Azure Active Directory
- Azure AD B2C
- Identity Providers (IdPs): Google, Microsoft, Facebook, etc.
- Basic authentication (default)

Basic Authentication (Basic Auth) is a built-in auth method for APIM.
It requires developer to register with email and password in order to obtain an API key.
API key is used in requests to authenticate the requests.

Delegated authentication allows you to use your own web app sign-in, sign-up, and product subscription instead of the built-in developer portal functionality.

You can add this if you go into the "Identities" blade within APIM and then click "Add".