#azure #az-204 

To use Application Insights you need to instrument your application.
To instrument, you need to either:
- install the instrument package (SDK)
- enable Application Insights using the agents when supported

Apps can be instrumented from anywhere.
When you set up Application Insights monitoring for the app, you create an App Insights resource in Azure.
You open this resource in the portal in order to see and analyse telemetry collected.
The resource is identified by an instrumentation key (`ikey`).

![[Application Insights - Overview Diagram.png]]

There are many ways to view your telemetry data:
- Smart detection and manual [[Azure Monitor - Azure Alerts|alerts]]
- Application map
- Profiler
- Usage Analysis
- Diagnostic search for instance data
- [[Azure Monitor - Metrics Explorer|Metrics Explorer]] for aggregated data
- Dashboards
- Live Metrics Stream
- Analytics
- Power BI
- Snapshot Debugger
- Visual Studio
- REST API
- Continuous Export