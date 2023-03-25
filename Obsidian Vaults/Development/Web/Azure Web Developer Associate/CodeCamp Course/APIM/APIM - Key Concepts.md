#azure #az-204 

API represents a set of operations.
- API operation connects an API endpoint to its backend

A single API or group of APIs make up a product.
- How your APIs are presented to developers
- Can be either public or private

Group, used to manage the visibility of products to developers:
- Administrators have full access to the API Management
- Developers are users with access to developer portal with permissions to build applications
- Guests are users without access tot he developer's portal but have read permissions in some services

Developer
- Belongs to one or more product groups
- Each has a primary and secondary key to call a product's API

Policies
- Configurations and validations
- Applied to incoming requests and outgoing responses

Named Values
- Key-value pairs used within policies
- Values can be a result of an expression

Gateway
- Where your API calls are received
- Policies are applied to incoming requests

Developer Portal
- Where developers can access all APIs and products listed by your APIM
- Can see API's operations and documentation
- Devs can request access to your APIs from the developer portal