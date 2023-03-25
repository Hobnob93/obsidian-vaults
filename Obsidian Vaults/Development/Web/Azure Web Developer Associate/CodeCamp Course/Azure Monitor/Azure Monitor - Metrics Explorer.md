#azure #az-204 

Metrics Explorer is a sub-service of Azure Monitor.
It allows you to:
- plot charts
- visualise correlating trends
- investigate spikes and dips

To visualise a metric you need to define:
- Scope
	- The resource e.g. VM, Storage Account
- Namespace
	- A specific group of metric data within a resource
- Metric
	- The actual value you are interested in visualising
- Aggregation
	- How you want to group the values into the final result e.g. min, average, max