#azure #az-204 

The origin is what Azure Front Door will point at (serve up) to the end user.
Origin is the endpoint that points to your backend.
Must be assigned to an [[Front Door - Origin Group|origin group]].

Supported origins for Azure Front Door include:
- Azure Blob Storage
- Azure Storage (static website hosting)
- Cloud service
- App services
- Static Web App
- API Management (APIM)
- Application Gateway
- Public IP Address
- Azure Traffic Manager
- Azure Spring Cloud
- Azure Container Instances (ACI)
- Custom (provide a host name)

When you define an origin, you need to provide some properties, including:
- **Priority**
	- Determines who to send traffic to first
	- A number between 1-5
	- Lower number is higher priority
	- Multiple backends can have the same priority number
- **Weights**
	- Allow you to determine the split of traffic distribution between origins of the same priority
	- A number between 1-1000
	- Default value is 50
	- It's essentially the "chance" the origin will be chosen for a request