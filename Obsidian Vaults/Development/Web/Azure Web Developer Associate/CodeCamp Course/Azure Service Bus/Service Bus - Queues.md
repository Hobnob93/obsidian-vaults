#azure #az-204 

Queues are used to send and receive messages.
Messages are stored in queues until a receiving application is ready to accept and process them.

Messages in queues are ordered and timestamped on arrival.
Once accepted by the broker, the message is always held durably in triple-redundant storage spread across multiple availability zones if the namespace is zone-enabled.

Service bus never leaves messages in memory or volatile storage after they've been reported by the client as accepted.

Messages are delivered in pull mode, only delivering messages when requested.