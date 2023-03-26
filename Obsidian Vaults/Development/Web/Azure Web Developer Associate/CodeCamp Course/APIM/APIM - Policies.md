#azure #az-204 

API Management Policies allow you to change behaviour at multiple stages of an endpoint's request lifecycle.
You can update any part of the request and response messages, e.g. headers, body, URLs, etc.

There are 4 areas where policies can be applied:
1. **Inbound**
	- for incoming requests
2. Backend
	- before requests reach your backend
3. **Outbound**
	- before sending a response back to client
4. **Error**
	- when a request encounters an error

When an error occurs, no other policies are applied except the error policies.
If other policies were in effect prior to the error, they *will not* be removed.

Product-level policies apply to all API operations within a product.

![[APIM - Policies Diagram.png]]

Azure has a collection of policy groups which contain many policies you can apply:
- Access Restriction Policies
- Advanced Policies
- Authentication Policies
- Caching Policies
- Cross-Domain Policies
- Transformation Policies
- [[CodeCamp - Distributed Application Runtime|Dapr]] Integration Policies
- Validation Policies
- GraphQL Validation Policies