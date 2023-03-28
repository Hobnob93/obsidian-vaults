#azure #az-204 

[[CodeCamp - Azure Event Grid|Event Grid]], [[CodeCamp - Azure Event Hub|Event Hub]], and [[CodeCamp - Azure Service Bus|Service Bus]] all are event driven services for app integration.
They all use an event bus as means to work with event data.

#### Azure Event Grid
- Serverless Event Bus
	- Azure service-to-service communication
- Dynamically scalable
- Low cost
- At least once delivery of events

#### Azure Event Hubs
- Streaming data
- Low latency
- Can receive and process millions of events per second
- At least once delivery of an event

#### Azure Service Bus
- Queue or pub/sub for web apps
- Reliable asynchronous message delivery that requires polling
- Advanced messaging features:
	- FIFO
	- batching
	- sessions
	- transactions
	- dead-lettering
	- temporal control
	- routing and filtering
	- duplicate detection
- At least once delivery of a message
- Optional ordered delivery of messages