#azure #az-204 

## Overview
Application Insights is an extension of [[Explore Azure Monitor|Azure Monitor]].
It provides Application Performance Monitoring (APM) features.

## Application Insights Features
Features include, but are not limited to:
- __Live Metrics__
	- Observe activity from deployed app in real time with no effect on host env
- __Availability__
	- Probe app external endpoint(s) to test overall availability and responsiveness over time
- __GitHub or Azure DevOps integration__
	- Create GitHub or Azure DevOps work items in context of Application Insights data
- __Usage__
	- Reveals which features are popular
	- How users interact and use your apps
- __Smart Detection__
	- Automatic failure and anomaly detection through proactive telemetry analysis
- __Application Map__
	- A high level top-down view of app architecture
	- At-a-glance visual references to component health and responsiveness
- __Distributed Tracing__
	- Search and visualise end to end flow of a given execution or transaction
## What Application Insights Monitors
Application Insights collects metrics and app telemetry data.
The describe app activities and health, as was as trace logging data.
- __Request rates, response times, and failure rates__
	- Find which pages are popular, and at what times of day
	- Find where your users are
	- See response times and failure rates and if they correlate with number of requests
- __Dependency rates, response times, and failure rates__
	- Find whether external services are slowing your app down
- __Exceptions__
	- Analyse aggregated statistics
	- Pick specific instances and drill into stack trace and related requests
	- Both server and browser exceptions are reported
- __Page views and load performance__
	- Reported by users' browsers
- __AJAX calls__
	- From web pages
	- rates, response times, and failure rates
- __User and session counts__
- __Performance counters__
	- From Windows or Linux server machines
	- CPU, memory, and network usage
- __Host diagnostics__
	- From Docker or Azure
- __Diagnostic trace logs__
	- From your app
	- Can correlate trace events with requests
- __Custom events and metrics__
	- You write yourself in client or server code
	- Track business events such as items sold or games won

## Getting Started With Application Insights
App Insights is one of many services hosted within Microsoft Azure.
Telemetry is sent there for analysis and presentation.
Free to sign up.
Can choose the basic plan for no charge until application has grown to have substantial usage.

Several ways to get started monitoring and analysing app performance:
- __At run time__
	- Instrument your web app on the server
	- Ideal for apps already deployed
	- Avoids any update to the code
- __At development time__
	- Add App Insights to your code
	- Allows you to customise telemetry collection and send more telemetry
- __Instrument your web pages__
	- For page view, AJAX, and other client-side telemetry
- __Analyse mobile app usage__
	- Integrate with Visual Studio App Centre
- __Availability tests__
	- Ping your website regularly from Azure servers