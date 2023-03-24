#azure #az-204 

Azure Front Door is a modern application delivery network platform.
It provides:
- Traffic management
- [[Front Door - Traffic Acceleration|Traffic acceleration]]
- Global Load Balancing
- A Content Distribution Network (CDN)

Some features of Azure Front Door:
- **Caching**
	- like CDNs with rules and expiring policies
- **Resiliency**
	- by distributing incoming traffic across multiple regions
- **Cookie-based session affinity**
	- for stateful apps when traffic needs to be redirected to the same backend
- **Health probe**
	- to determine healthiest and closest backend to the client request
- **Web Application Firewall (WAF)**
	- protecting your backends from malicious attacks and vulnerabilities
- **URL redirect**
	- redirects traffic based on:
		- Protocol (HTTP or HTTPS)
		- Host name
		- Path
		- Query String
- **URL rewrite**
	- rewrite incoming requests to a different backend request with a powerful rewrite engine

An Azure Front Door is made up of frontends/domains.
These are connected to backend pools where connections are filtered by routing rules.