#azure #az-204 

Azure Queue Storage is a simple message broker enabling cloud message exchange between apps and services.
It uses authenticated HTTP/S protocols.
Supports messages up to size 64 KB.

Queue Storage is within an Azure Storage Account.
Can access with same access keys and connection strings as the rest of the account's resources.

Azure Queue Storage offers 3 ways of handling messages on the queue:
1. **Peek**
	- look at a message without removing or locking it
2. **Delete**
	- removes message after it has been processed
3. **Receive**
	- takes the message at the front of queue for processing
	- locks the message temporarily

You can use the Portal to send a message to the queue.
Allows you to test the queue or receivers.

Most interactions with the queue will actually come from services, usually programmatically via the SDK, or through CLI operations.