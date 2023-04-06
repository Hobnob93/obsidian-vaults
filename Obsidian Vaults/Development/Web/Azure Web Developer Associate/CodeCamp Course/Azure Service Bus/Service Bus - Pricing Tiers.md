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
| Topics                 |      | Yes      | Yes     |
| Transactions           |      | Yes      | Yes     |
| Deduplication          |      | Yes      | Yes     |
| Sessions               |      | Yes      | Yes     |
| Forward To / Send Via  |      | Yes      | Yes     |
| Message Size           | 256 KB | 256 KB   | 1 MB    |
| Resource isolation     |      |        | Yes     |
| Geo-disaster recovery  |      |        | Yes     |
| Java Messaging Service |      |        | Yes     |
| AZ Support             |      |        | Yes     | 
