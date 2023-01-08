#azure #az-204 

## Overview
Azure Event Hubs enables you to automatically capture the streaming data.
Can be captured in Azure Blob storage or Azure Data lake Storage.
Added flexibility of specifying time or size interval.
Setting up Capture is fast
- No admin costs to run it
- Scales automatically
	- Throughput units in standard tier
	- Processing units in premium tier

![[Event Hubs Capture Diagram.png]]

Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.
Lets you build solutions that grow with your needs over time.

## How Event Hubs Capture Works
Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.
Key to scaling in Event Hubs is the partitioned consumer model.
Each partition is an independent segment of data and is consumed independently.
Over time, this data ages off.
- Based on configured retention period
As a result, a given hub never gets "too full".

Capture allows you to specify your own Azure Blob storage account and container (or Azure Data Lake Storage account).
Can be used to store the captured data.
These accounts can be in the same region or another region as the event hub.

Captured data is written in Apache Avro format: a compact, fast, binary format providing rich data structures with inline schema.
Format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.

## Capture Windowing
Event Hubs Capture allows you to set up a window to control capturing.
The window is a minimum size and time configuration with a "first wins policy".
- First trigger encountered causes a capture operation
Each partition captures independently and writes a completed block blob at the time of capture.
- Named for the time the capture interval was encountered

The storage naming convention is as follows:
```
{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}
```
Note the date values are padded with zeroes!

## Scaling To Throughput Units
Traffic is controlled by throughput units.
A single unit allows 1MB per second, or 1000 events per second of ingress and twice that of egress.
Standard Hubs can be configured with 1-20 throughput units, and more can be purchased with a quota support request.
Usage beyond your purchased throughput units is throttled.
Capture copies data directly from the internal Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.

Once configured, Capture runs automatically when you send your first event, and continues running.
Hubs writes empty files when there is no data, so downstream processing knows that the process is working.
This provides a predictable cadence and marker that can feed your batch processors.