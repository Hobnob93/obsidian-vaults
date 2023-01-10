#azure #az-204 

Azure Queue Storage is a service for storing large amounts of messages.
Access messages from anywhere via authenticated HTTP or HTTPS calls.
A message can be up to 64KB in size.
A queue may contain millions of messages, up to the capacity of the storage account.
Queues are commonly used to create a backlog of work to process asynchronously.

Queue service contains following components:
- __URL format__
	- Queues are addressable using URL format `https://<storage-account>.queue.core.windows.net/<queue>`
- __Storage Account__
	- All access is done through this
- __Queue__
	- Contains a set of messages
	- All messages must be in a queue
	- Queue name must be all lower case
- __Message__
	- Up to 64KB in any format
	- Maximum time to live can be any positive number
		- Or -1 indicating no expiry
		- Default is 7 days