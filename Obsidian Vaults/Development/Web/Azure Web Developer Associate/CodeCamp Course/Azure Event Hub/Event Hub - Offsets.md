#azure #az-204 

An offset is the position of an event within a partition.
It enables consumers to specify a point in the event stream from which they want to begin reading events.

You can specify the offset as a timestamp or as an offset index value.
Consumers are responsible for storing their own offset values outside of the Event Hub service.
Within a partition, each event includes an offset.