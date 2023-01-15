#azure #az-204 

## Overview
App Insights is enabled through either Auto-instrumentation (agent) or by adding App Insights SDK to app code.

## Auto-Instrumentation
Preferred instrumentation method.
Requires no developer investment.
Eliminates future overhead when SDK needs updating.
Only way to instrument an app when you don't have access to source code.

Simply enable, and sometimes configure, the agent to collect telemetry automatically.

## Enabling Via Application Insights SDKs
Only need to install App Insights SDK in following circumstances:
- Require custom events and metrics
- Require control over flow of telemetry
- Auto-instrumentation isn't available (due to language or platform limitations)

Install a small instrumentation package in app.
Can instrument app itself and/or any background components, or JavaScript within web pages.
App and/or components don't have to be hosted in Azure.
Instrumentation monitors app and directs telemetry data to an App Insights resource by using a unique token.

Any technology can be tracked manually with a call to `TrackDependency` on the `TelemetryClient`.

## Enable Via OpenCensus
App Insights supports distributed tracing through OpenCensus.
An open source, vendor-agnostic, single distribution of libraries to provide metrics collection and distributed tracing for services.
Enables open source community to use distributed tracing with popular technologies like Redis, Memcached, or MongoDB.