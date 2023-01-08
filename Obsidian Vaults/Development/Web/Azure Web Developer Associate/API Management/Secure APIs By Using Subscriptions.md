#azure #az-204 #cli 

## Overview
It's easy and common to secure access to APIs by using subscription keys.
Devs who need to consume APIs must include a valid key in HTTP requests when making calls.
Otherwise, calls are rejected by API Management gateway.

A subscription is required to get a subscription key for accessing APIs.
A subscription is a named container for a pair of subscription keys.
API publishers can create subscriptions directly for API consumers.

## Subscriptions and Keys
A subscription key is a unique auto-generated key.
Key is directly related to a subscription, which can be scoped to different areas.
Subscriptions give you granular control over permissions and policies.

The ==three== main subscription scopes are:
1. All APIs
	- Applies to every API accessible from the gateway
2. Single API
	- Applies to a single imported API and all its endpoints
3. Product
	- A collection of one or more APIs that you configure in API Management
	- Can assign APIs to more than one product
	- Products can have different access rules, usage quotas, and terms of use

Can regenerate subscription keys at any time, such as if you suspect a key has been shared with unauthorised users.

Every subscription has two keys; a primary and secondary.
Makes it easier when you do need to regenerate a key as you can avoid downtime by just using the secondary key in your apps.
![[Primary & Secondary Subscription Keys.png]]

For products where subscriptions are enabled, clients must supply a key when making calls to any API in that product.
Devs can obtain a key by submitting a subscription request.
If you approve the request, you must send them the subscription key securely.
This step is a core part of the API Management workflow.

## Call An API With The Subscription Key
Apps must pass a valid key in all HTTP requests when calling the API endpoints protected by a subscription.
Keys can be passed in the request header or as a query string parameter.
The default header name is `Ocp-Apim-Subscription-Key`.
The default query string is `subscription-key`.

To test API calls, you can use the developer portal, or CLI tools.
Below is an example of a GET request using developer portal.
![[Testing API Request In Developer Portal.png]]

How to pass a key in request header:
```shell
curl --header "Ocp-Apim-Subscription-Key: <key>" https://<apim gateway>.azure-api.net/api/path
```

How to pass a key in query parameter:
```shell
curl https://<apim gateway>.azure-api.net/api/path?subscription-key=key
```

If you do not pass a key when it is needed, you will get a `401 Access Denied` error from API gateway.