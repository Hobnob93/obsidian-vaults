#azure #az-204 

Specifies what a container should do when their process has completed.
Azure Container Instances has 3 restart-policy options:
- **Always** (default)
	- Containers are always restarted
	- Suited for long running tasks i.e. web servers
- **Never**
	- Containers run once only
	- Suited for one-off tasks i.e. a background job
- **On Failure**
	- Containers that encounter an error