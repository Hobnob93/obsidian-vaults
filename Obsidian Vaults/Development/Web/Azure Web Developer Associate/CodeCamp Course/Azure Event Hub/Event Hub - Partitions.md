#azure #az-204 

Event Hub organises sequences of events sent to an Event Hub into one or more partitions.
As newer events arrive, they're added to the end of this sequence.

Partitions hold the following data about the event:
- Body
- User-defined property bag describing the event
- Metadata, such as its offset position in the partition
- Number in the stream sequence
- Service-side timestamp at which it was accepted

Partitioning allows for multiple parallel logs to be used for the same Event Hub and therefore multiplying the available raw IO throughput capacity.

You can use a partition key to map incoming event data into specific partitions for the purpose of data organisation.
Partition key is a sender-supplied value passed into an Event Hub.