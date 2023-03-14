#azure #az-204 

App Service Environment (ASE) is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running apps at high scale.

This allows you to host:
- Windows web apps
- Linux web apps
- Docker containers
- Mobile apps
- Functions

ASEs are appropriate for application workloads that require:
- Very high scale
- Isolation and secure network access
- High memory utilisation

Customers can create multiple ASEs within a single Azure region, or across multiple Azure regions.
This makes ASEs ideal for horizontally scaling stateless application tiers in support of high requests per second (RPS) workloads.

ASE comes with its own pricing tier (Isolated Tier).
Can be used to configure security architecture.
Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).
ASEs can be deployed into Availability Zones (AZ) using zone pinning.

There are 2 deployment types for an ASE:
- **External ASE**
	- Exposes the ASE-hosted app on an internet-accessible IP address
	- If VNet is connected to your on-premises network, apps in your ASE have access to resource there without additional config
	-  It can also access resources within the VNetwithout any additional config
- **ILB ASE**
	- Essentially the same an as External ASE
	- Only difference is it contains an Internal Load Balancer (ILB)
	- It exposes the ASE-hosted apps on an IP address inside your VNet
	- The internal endpoint is an ILB

