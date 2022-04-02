#azure #az-204 

# Discover Microsoft Graph
A gateway to data and intelligence in *Microsoft 365*.
Provides a unified programmability model to access tremendous amount of data.
![[MS 356 Platform Diagram.png]]

Three main components facilitate the access and flow of data:
- **MS Graph API**
	- A single endpoint; `https://graph.microsoft.com`
	- Can use REST APIs or SDKs to access endpoint
	- Manages device identity, access, compliance, security, and protect orgs from data leakages or loss
- **MS Graph Connectors**
	- Work in incoming direction
	- Delivering data external to MS Cloud into MS Graph services and apps
	- Enhances MS 365 experiences such as MS Search
	- Exist for commonly used data sources such as *Box*, *Google Drive*, *Jira*, and *Salesforce*
- **MS Graph Data Connect**
	- Provides set of tools to streamline secure and scalable delivery of MS Graph data to *Azure* data stores
	- Cached data serves as data sources for *Azure* dev tools