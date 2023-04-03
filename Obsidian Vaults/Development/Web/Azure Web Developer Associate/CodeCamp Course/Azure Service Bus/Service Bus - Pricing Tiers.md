#azure #az-204 #az-tiers 

Azure Service Bus has 3 different pricing tiers:
- Basic
	- ~$0.05 per 1M operations per month
- Standard
	- ~$10 per 12.5M operations per month
- Premium
	- ~$668 per MU per month

|                        | Basic  | Standard | Premium |
| ---------------------- | ------ | -------- | ------- |
| Queues                 | Yes    | Yes      | Yes     |
| Scheduled Messages     | Yes    | Yes      | Yes     |
| Topics                 | No     | Yes      | Yes     |
| Transactions           | No     | Yes      | Yes     |
| Deduplication          | No     | Yes      | Yes     |
| Sessions               | No     | Yes      | Yes     |
| Forward To / Send Via  | No     | Yes      | Yes     |
| Message Size           | 256 KB | 256 KB   | 1 MB    |
| Resource isolation     | No     | No       | Yes     |
| Geo-disaster recovery  | No     | No       | Yes     |
| Java Messaging Service | No     | No       | Yes     |
| AZ Support             | No     | No       | Yes     | 
