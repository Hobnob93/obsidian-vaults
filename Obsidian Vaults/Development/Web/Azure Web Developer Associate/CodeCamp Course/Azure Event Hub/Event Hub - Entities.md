#azure #az-204 

#### Partition Count
Partitions are a data organisation mechanism.
They relate to the downstream parallelism required in consuming applications.
Number of partitions in an Event Hub directly relates to number of concurrent readers you expect to have.

#### Retention Period
The retention period for events.
Can set the period between 1 and 7 days.

#### Capture
Enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage, or Azure Data Lake Store account.
Has added flexibility of specifying a time or size interval.

Setting up Capture is fast.
No administrative costs to running it.
It scales automatically with Event Hubs throughput units.

Capture is the easiest way to load streaming data into Azure.
It enables you to focus on data processing rather than data capture.