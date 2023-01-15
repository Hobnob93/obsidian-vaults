#azure #az-204 

## Overview
Lets you analyse health of monitored apps.
Create powerful dashboards.
Configure alerts.

There are two kinds of metrics:
- __Log based metrics__
	- Translated into Kusto queries behind the scenes from stored events
- __Standard metrics__
	- Stored as pre-aggregated time series

Standard metrics have better performance at query time as pre-aggregate during collection.
Makes them a better choice for dashboarding and in real-time alerting.
Log-Based metrics have more dimensions, so a superior option for data analysis and ad-hoc diagnostics.

## Log-Based Metrics
Developers can use the SDK to either emit events manually, or can rely on automatic collection of events from auto-instrumentation.
App Insights backend stores all collected events as logs.
App Insights blades in portal act as an analytical and diagnostic tool for visualising event-based data from logs.

Using logs to retain complete set of events has analytical and diagnostic value.
Can get an exact count of requests to a particular URL, with number of distinct users who made the calls.
Can get detailed diagnostic traces, including exceptions and dependency calls for a user session.
Can improve visibility into app health and usage.
Can cut down time necessary to diagnose issues with an app.

Collecting a complete set of events may be impractical (or impossible) for apps that generate large volume of telemetry.
Apps Insights implements telemetry volume reduction techniques, such as sampling and filtering.
Unfortunately, lowering number of stored events affects accuracy of metrics.

## Pre-Aggregated Metrics
Not stored as individual events with properties.
Instead, stored as pre-aggregated time series, with only key dimensions.
Makes new metrics superior at query time.
- Retrieving data happens much faster with less compute power
Enables new scenarios such as near real-time alerting on dimensions of metrics, more responsive dashboard, etc.

Newer SDKs (post-App Insights 2.7) pre-aggregate metrics during collection.
Applies to standard metrics by default, so accuracy not affected by sampling or filtering.
Applies to custom metrics using GetMetric resulting in less data ingestion and lower cost.

For SDKs older than 2.7, App Insights backend still populates new metrics by aggregating events received by App Insights event collection endpoint.
You don't benefit from reduced volume, but can still use pre-aggregated metrics.