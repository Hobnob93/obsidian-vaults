#azure #az-204 

Azure Event Grid is made up of quite a few parts:
- **Domain**
	- Used to group Event Grid topics that are related to the same application for easier management
- **Topics**
	- The endpoint where events are sent
	- System Topics are built-in provided by Azure Services
	- Custom Topics are apps and third-party topics
- **Events**
	- The event that occurred in the service
	- Partner Events provide a way for third-party SaaS to publish events
- **Publishers**
	- The service that published the event
- **Event Sources**
	- Where the event took place
- **Event Subscriptions**
	- The mechanism that routes the events
	- You can set an expiration for event subscriptions
- **Event Handlers**
	- The app(s) or service(s) that receives the event
- **Event Delivery**
	- The delivery of events in batches or as single events
- **Batching**
	- Sending a group of events in a single request

![[Event Grid - Concepts Diagram.png]]