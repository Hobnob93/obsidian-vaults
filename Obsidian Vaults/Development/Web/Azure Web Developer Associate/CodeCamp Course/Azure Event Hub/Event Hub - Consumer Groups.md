#azure #az-204 

A consumer group is a view (state, position, or offset) of an entire Event Hub.
They enable multiple consuming apps to each have their own view of the event stream.
Each app can read the stream independently and at their own pace.

In stream processing architecture, each downstream app equates to a consumer group.

There's always a default consumer group in an Event Hub.
You can create up to the maximum groups for the corresponding pricing tier.

There can be at most 5 concurrent readers on a partition per consumer group.
It's recommended there's only one **active receiver** on a partition per consumer group.

Some clients offered by Azure SDKs are intelligent consumer agents which automatically manage the details of ensuring each partition has a single reader.
They also ensure all partitions from an Event Hub are being read from.
This allows your code to focus on the processing of events, so it can ignore the details of the partitions.