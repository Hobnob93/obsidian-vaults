#azure #azure-wda #authentication #authorization

# Explore Authentication & Authorization in App Service
*Azure App Service* provides built-in auth support.
Can sign in users and access data with minimal code support within apps.

## Why Use the Built-In Authentication?
Not *required* to use built-in auth features.
Many web frameworks come with security features already, and these can be used instead if preferred.
*App Service* auth features do provide more ==flexibility==.
You can also write your own auth ==utilities==.

It can save you time by providing out-of-the-box auth with identity providers, so focus can be on the rest of the application.

- Can integrate a variety of auth capabilities into app or API without implementing them yourself
- Built directly into the platform and doesn't require any particular language, SDK, security expertise, or even code in most cases
- Can integrate multiple ==login providers== such as *Azure AD*, *Facebook*, *Google*, or *Twitter*.

## Identity Providers
*App Services* uses ==federated== identity.
Third party providers manage user identities and auth flow for you.

The following providers are available by default:
| Provider                    | Sign in Endpoint          | How to Guide |
| --------------------------- | ------------------------- | ------------ |
| Microsoft Identity Platform | /.auth/login/aad          | [How-To](https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-aad)     |
| Facebook                    | /.auth/login/facebook     | [How-To](https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-facebook)     |
| Google                      | /.auth/login/google       | [How-To](https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-google)     |
| Twitter                     | /.auth/login/twitter      | [How-To](https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-twitter)     |
| Any OpenID Connect Provider | /.auth/login/[prov-name]  | [How-To](https://docs.microsoft.com/en-us/azure/app-service/configure-authentication-provider-openid-connect)     | 

## How It Works
Authentication and authorisation module runs in same sandbox as app.
When enabled, all incoming HTTP requests pass through it before being handled by application.

This module handles several things for the app:
- Authenticates users with specified provider
- Validates, stores, and refreshes tokens
- Manages authenticated session
- Injects identity information into request headers

Module runs separately from app and is configured to use app settings.
No SDK, specific language, or app changes needed.

## Authentication Flow
The flow is the same for all [[#Identity Providers|providers]], but differs on whether you want to sign in with provider's SDK.

- **Without Provider SDK**
	- App delegates federated sign-in to *App Service*
	- This is typically the case with browser apps, which can present the provider's login page to the user
	- Server manages the sign-in process
	- Called ==server-dedicated flow== or ==server flow==
- **With Provider SDK**
	- App signs in to provider manually and submits authentication token to *App Service* for validation
	- Typically the case with browser-less apps which cannot present a sign-in page to the user
	- App manages the sign-in process so is called ==client-directed flow== or ==client flow== 
	- Applies to *REST APIs*, *Azure Functions*, *JavaScript browser clients*, and *native mobile apps*

The steps of the authentication flow:
1. Sign User In
	- **w/o provider SDK:** Redirects client to `/.auth/login/<provider>`
	- **w/ provider SDK:** Client code signs user in directly using SDK and receives auth token
2. Post-authentication
	- **w/o provider SDK:** Provider redirects client to `/.auth/login/<provider>/callback`
	- **w/ provider SDK:** Client code posts token from provider to `/.auth/login/<provider>` for validation
3. Establish Authenticated Session
	- **w/o provider SDK:** App Service adds authentication cookie to response
	- **w/ provider SDK:** App Service returns its own authentication token to client code
4. Serve Authenticated Content
	- **w/o provider SDK:** Client includes auth cookie in subsequent requests (automatically handled by browser)
	- **w/ provider SDK:** Client code presents auth token `X-ZUMO-AUTH` header

*App Service* can automatically redirect all unauthenticated users to `/.auth/login/<provider>`.
Can present users with one or more `<provider>` links to sign in to app using a provider of their choosing.

## Authorisation Behaviour
Can configure *App Service* with a number of behaviours when incoming request not authenticated:
- **Allow unauthenticated requests**
	- Defers auth to application code
	- For authenticated requests, *App Service* passes auth info in the HTTP headers
	- Provides flexibility in handling anonymous requests
	- Lets you present multiple sign-in providers to users
- **Require Authentication**
	- Rejects any unauthenticated traffic
	- Rejection can be a redirect action to an [[#Identity Providers|identity provider]]
	- If anonymous request comes from a mobile app, returned response is `HTTP 401 Unauthorized`
	- Can configure to be `401` or `403 Forbidden` for all requests

## More Info
[[Azure User Authentication & Authorisation]]