#azure #az-204 

#### Frontends
Frontends define the route/endpoint.
They have the documentation and configuration around that endpoint.

APIM does *not* host APIs, it creates a façade for your APIs.

You may have the frontend `POST /resource` which has the valid responses of `200 OK`.
Then within the documentation and configuration for this frontend you can set:
- Display name e.g. `Create resource`
- Name e.g. `create-resource`
- URL e.g. `POST /resource`
- Description
- Tags

#### Backends
For backends you can set the following:
- **Custom URL**
	- point to a server where your service is running
- **Azure Resource**
	- integrate directly to an Azure resource
		- [[CodeCamp - Azure Functions|Azure Functions]]
		- [[CodeCamp - Azure App Services|App Services]]
		- Container App
		- Logic App
- **Azure Service Fabric**

**Authorisation credentials** present authorise request credentials to the backend service.
- **Headers**
	- you can fetch from named values
- **Query**
	- you can fetched from named values
- **Client certificates**
	- you can use [[CodeCamp - X.509 Certificates|X.509 certificates]]
	- certificates stored in [[CodeCamp - Azure Key Vault|Key Vault]]