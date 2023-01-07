#azure #az-204 

## Overview
Provides core functionality to ensure a successful API program though developer engagement, business insights, analytics, security, and protection.
Each API consists of one or more operations.
Each API can be added to one or more products.
To use an API, developers subscribe to a product that contains that API, then they can call API's operations, subject to usage policies.

## Components
The system is made up of the following components:
- The __API Gateway__ is the endpoint that:
	- Accepts API calls and routes them to backend(s)
	- Verifies API keys, JWT tokens, certificates, and other credentials
	- Enforces usage quotas and rate limits
	- Transforms API on the fly without code modifications
	- Caches backend responses where set up
	- Logs all metadata for analytics purposes
- The __Azure Portal__ is the administrative interface where you set up the API program:
	- Define or import API schema
	- Package APIs into products
	- Set up policies like quotas or transformations on the APIs
	- Get insights from analytics
	- Manage users
- The __Developer Portal__ serves as main web presence for developers:
	- Read API documentation
	- Try out API via interactive console
	- Create account and subscribe to get API keys
	- Access analytics on their own usage

## Products
How APIs are surfaced to developers.
Products have one or more APIs.
They are configured with:
- Title
- Description
- Terms of use
Products can be __Open__ or __Protected__.
Open products don't need to be subscribed to to use.
Protected products must be subscribed to before they can be used.
Subscription approval is configured at product level and can either require admin approval, or be auto-approved.

## Groups
Used to manage visibility of products to developers.
API management has the following immutable system groups:
- __Administrators__
	- Azure subscription admins are members of this group
	- Manage API service instances
	- Creating the APIs, operations, and products used by developers
- __Developers__
	- Authenticated developer portal users fall into this group
	- They are the customers that build applications using your APIs
	- Developers are granted access to developer portal and build applications that call the operations of an API
- __Guests__
	- Unauthenticated developer portal users,
	- Prospective customers visiting the portal
	- Can be granted certain read-only access, such as ability to view APIs but not call them

Administrators can create custom groups or leverage external groups in associated Azure Active Directory tenants.

## Developers
Represent the user accounts in an API Management service instance.
Can be created or invited to join by admins.
They can also sign up via the Developer Portal.
Each developer is a member of one or more groups.
They can subscribe to products that grant visibility to those groups.

## Policies
A powerful capability of API Management that allow Azure Portal to change behaviour of the API through configuration.
A collection of statements executed sequentially on the request or response of an API.
Popular statements include:
- Conversion from XML to JSON
- Call rate limiting
- Many others

## Developer Portal
Developers can:
- Learn about your APIs
- View and call operations
- Subscribe to products
Prospective customers can:
- Visit the portal
- View APIs and operations
- Sign up

The URL for your developer portal is located on the dashboard in Azure Portal for your API Management service instance.