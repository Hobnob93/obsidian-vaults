#azure #az-204 #cli

You can interact with the queue via the Azure CLI command: `az storage message <action>`.
There are a few actions available:
- `clear`
	- deletes all messages from specified queue
- `delete`
	- deletes the specified message
- `get`
	- retrieves one or more messages from the front of the queue
- `peek`
	- retrieves one or more messages from the front of the queue
	- does not alter their visibility
- `put`
	- adds a new message to the back of the message queue
- `update`
	- updates visibility timeout of a message