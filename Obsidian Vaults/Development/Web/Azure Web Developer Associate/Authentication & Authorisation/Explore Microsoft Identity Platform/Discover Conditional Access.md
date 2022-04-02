#azure #az-204 

# Discover Conditional Access
Feature of *AAD* offering several ways to secure app and protect a service.
Enables develops and enterprise customers to protect services in a multitude of ways, including:
- Multifactor authentication
- Allowing only Intune devices to access specific services
- Restricting user locations and IP ranges

## How Does Conditional Access Impact an App?
It does not change app's behaviour, or require changes from dev, *in most cases*.
In cases where app indirectly or silently requests a token for a service does an app require dev changes.
This is to handle Conditional Access challenges.
It may be as simple as performing an interactive sign-in request.

The following scenarios require handling of Conditional Access challenges:
- Apps performing on-behalf-of flow
- Apps accessing multiple services/resources
- Single-page apps using MSAL.js
- Web apps calling a resource

Policies can be applied to app and the web API it accesses.
Depending on scenario, an enterprise customer can apply and remove Conditional Access policies at any time.
For app to continue functioning when new policy applied, implement challenge handling.

## Conditional Access Examples
A few scenarios using Conditional Access to do multifactor auth that gives some insight into the difference.

1. You're building single-tenant iOS app and apply Conditional Access policy. App signs in user and doesn't request access to API. When user signs in, policy is automatically invoked and user needs to perform multifactor authentication.
2. You're building native app using middle-tier service to access downstream API. An enterprise customer at company using app applies a policy to downstream API. When end user signs in, native app requests access to middle-tier and sends token. Middle-tier performs on-behalf-of flow to request access to downstream API. A claims "challenge" is presented in middle-tier, which sends challenge back to native app - which needs to comply with Conditional Access policy.