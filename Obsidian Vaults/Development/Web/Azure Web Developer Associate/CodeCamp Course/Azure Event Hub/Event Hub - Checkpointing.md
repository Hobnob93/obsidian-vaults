#azure #az-204 

Checkpointing is a process by which readers mark or commit their position within a partition event sequence.
It is the responsibility of the consumer.
Occurs on a per-partition basis within a consumer group.

This means that for each consumer group, each partition reader must track its current position in the event stream.
It can then inform the service when it considers the data stream complete.