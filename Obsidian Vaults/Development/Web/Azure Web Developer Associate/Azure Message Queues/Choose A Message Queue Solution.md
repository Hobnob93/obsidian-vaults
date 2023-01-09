#azure #az-204 

## Overview
Storage queues and Service Bus queues have a slightly different feature set.
You can use either or both, depending on needs.

## Consider Using Service Bus Queues
Consider using Service Bus queues when:
- Solution needs to receive messages *without* having to poll the queue
	- Can use long-polling receive operation using supported TCP-based protocols
- Solution requires queue to provide guaranteed first-in-first-out (FIFO) delivery
- Solution needs automatic duplicate detection
- App to process messages as parallel long-running streams
	- Messages associated with stream using `session ID` property on message
	- Each node in consuming app competes for streams, as opposed to messages
	- When stream given to consuming node, it can examine state of app stream state using transactions
- Solution requires transactional behaviour and atomicity when sending/receiving multiple messages from a queue
- App handles messages that can exceed 64KB but likely won't approach the 256KB limit

## Consider Using Storage Queues
Consider using Storage queues when:
- App must store over 80GB of messages in a queue
- App wants to track progress for processing a message in the queue
	- Useful if worker processing a message crashes
	- Another worker can use that information to continue the processing
- Require server side logs of all transactions executed against the queue