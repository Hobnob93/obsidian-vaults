#azure #az-204 

Not specific to Azure, but good to know in the context of DevOps.

Observability is the ability to measure and understand how internal systems work in order to answer questions regarding performance, tolerance, security and faults with a system or application.

To obtain observability you have to use metrics, logs, and traces.
These *have* to be used together; using them in isolation does not grant you observability.
In more detail:
- **Metrics**
	- A number that is measured over a period of time
	- Example; if we measured CPU usage and aggregate it over a period we would have the average CPU metric
- **Logs**
	- A text file where each line contains event data about what happened at a certain time
- **Traces**
	- A history of requests that travel through multiple apps/services so we can pinpoint performance or failure