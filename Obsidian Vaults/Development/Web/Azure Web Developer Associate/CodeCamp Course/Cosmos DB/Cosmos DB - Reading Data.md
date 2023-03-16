#azure #az-204 

There are two ways to read data from Cosmos DB:
1. Point Reads
	- A key/value lookup on a single *item ID* and partition key
2. Queries
	- Allows you to return multiple items

|                     | Point Reads | Queries                   |
| ------------------- | ----------- | ------------------------- |
| **Latency**         | ~10ms       | Varies                    |
| **RU Charges**      | 1 RU        | At least 2.3 RUs (varies) |
| **Items Returned**  | 1 item      | Unlimited                 |
| **Partition  Key?** | Required    | Recommended               |
