#azure #az-204 

A dead letter queue is a service implementation to store messages that fail to deliver.
Common reasons messages fail to deliver:
- Message sent to queue that does not exist
- Queue length limit exceeded
- Message length limit exceeded
- Message rejected by another queue exchange
- Message reaches threshold read counter number, as it is not consumed
	- Sometimes called "back out queue"
- Message expires due to TTL
- Message not processed successfully

A dead letter queue could be used for:
- Monitoring failed attempts
- Requeuing failed attempts
- Trigger a follow up action