#azure #azure-wda 

# Access Tiers for Block Blob Data
Different options for accessing block blob data based on usage patterns.
Each access tier optimised for particular pattern of data usage.
Selecting appropriate tier will ensure block blob data storage is as cost-effective as possible.

Available access tiers:
- `Hot`
	- Optimised for frequent access of objects
	- The most cost-effective option for data access
	- Storage costs are higher for this tier
	- New storage accounts use this tier by ==default==
- `Cool`
	- Optimised for large amounts of data
	- Data that is accessed infrequently and stored for at least 30 days
	- Storage is cost-effective
	- Accessing data may be more expensive than in the `hot` tier
- `Archive`
	- Available *only* for individual block blobs
	- Optimised for data that can tolerate several hours of retrieval latency
	- Data will remain in archive for at least 180 days
	- Most cost-effective option for storing data
	- Accessing data is more expensive than data in `hot` or `cool` tiers

You are able to switch between these tiers at any time.