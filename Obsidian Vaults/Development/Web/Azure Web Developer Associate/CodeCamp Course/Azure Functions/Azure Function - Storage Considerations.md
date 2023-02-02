#azure #az-204 

Every function app **requires a storage account to operate**.
If that account is deleted, your functions won't work.

Azure Functions uses the following storage types in the Storage Account:
- Blob Storage
	- Maintain bindings state and function keys
- Azure Files
	- File share used to store and run function app code in a Consumption Plan and Premium Plan
	- Set up by default, but you can create an app without Azure Files under certain conditions
- Queue Storage
	- Used by task hubs in Durable Functions
- Table Storage
	- Used by task hubs in Durable Functions