#azure #az-204 

Both Azure Storage Queue and Azure Service Bus offer message queuing as a service.

#### [[CodeCamp - Azure Queue Storage|Azure Storage Queue]]
A simple message queuing service to store large numbers of messages.

Features:
- Can handle millions of messages
	- No guarantee of the order of the messages
- At-Least Once delivery
- 500 TB max queue size
- 64 KB message size (48 KB for Base64 encoding)
- Unlimited queues
- Unlimited concurrent clients
- Leased-based access mode
	- 30 seconds to 7 days
	- set for the entire queue

#### [[CodeCamp - Azure Service Bus|Azure Service Bus]]
Broader messaging service.
Supports queueing, pub/sub, and more advanced integration patterns.

Features:
- Offers first-in-first-out (FIFO)
	- Guarantees the order of messages being consumed
- Multiple delivery options:
	- At-Least Once delivery
	- At-Most Once delivery
- 1 GB to 80 GB max queue size
- 256 KB or 1 MB message size
- 10,000 max queues
- 5,000 concurrent clients
- Locked-based access mode
	- 60 seconds
	- can change settings per message
- Dead lettering supported
- Messaging group supported
- De-duping supported
- Purging queue supported
- Transactions supported