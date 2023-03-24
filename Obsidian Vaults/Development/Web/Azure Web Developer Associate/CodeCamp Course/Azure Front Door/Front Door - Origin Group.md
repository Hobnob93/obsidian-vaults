#azure #az-204 

Origin groups are a collection of origins.
Origins must belong to an origin group.
Azure Front Door Profiles have an origin by default when they are created.
- The default origin group will be called `default-origin-group`

Origin groups allow you to apply:
- Health probes
	- Check the health of your origins
	- See [[Front Door - Health Probes]]
- Load balancing settings
	- Ensure load balancing of the origins
	- See [[Front Door - Load Balancing Settings]]

In order for inbound traffic to reach an origin group, an endpoint needs to be associated via a route.
Can do this by clicking the button **Associate endpoint and route** within Azure Portal.