#azure #az-204 

## Overview
Azure Monitor collects, analyses, and acts on telemetry from cloud and on-premise environments.

The following diagram is a high level view of Azure Monitor
- Made up of data stores for metrics, logs, and changes
	- Fundamental types of data used by Azure Monitor
- Sources of monitoring data populate the data stores
- Functions that AM performs with collected data
![[Azure Monitor High Level Overview.png]]

## What Data Does Azure Monitor Collect?
Am collects a few different types of data:
- __Metrics__
	- Numerical values describing an aspect of a system at a point in time
	- Collected at regular intervals
	- Identified with a timestamp, name, value, and one or more labels
- __Logs__
	- Events that occurred within a system
	- Can contain different kinds of data
	- May be structured or free-form text
	- Has a timestamp
- __Distributed traces__
	- A series of related events
	- Follow a user request through a distributed system
- __Changes__
	- A series of events that occur in Azure apps and resources
	- Change Analysis tracks changes
	- Is a subscription-level observability tool
	- Built on power of Azure Resource Graph

## Insights & Curated Visualisations
Some Azure resource providers have a "curated visualisation" giving you a customised monitoring experience for a service or set of services.
Generally require minimal configuration.
Larger curated visualisations are known as *insights*, and are marked as such in documentation.
Some examples:
- __Application Insights__
	- Monitors availability, performance, and usage of web apps
	- Whether they hosted in cloud or on-premises
	- Leverages the powerful data analysis platform in AM
	- Provides deep insights into apps operations
	- Enables you to diagnose errors without waiting for a user to report them
- __Container Insights__
	- Monitors performance of container workloads
	- Containers deployed to Kubernetes clusters hosted on Azure Kubernetes Service (AKS)
	- Or hosted on [[Explore Azure Container Instances|Azure Container Instances]]
	- Gives you performance visibility
	- Collects metrics from controllers, nodes, and containers through the Metrics API
	- Container logs are also collected
- __VM Insights__
	- Monitors [[Explore Azure Virtual Machines|Azure Virtual Machines]] at scale
	- Analyses performance and health of Windows and Linux WMs
	- identifies different processes and interconnected dependencies on external processes