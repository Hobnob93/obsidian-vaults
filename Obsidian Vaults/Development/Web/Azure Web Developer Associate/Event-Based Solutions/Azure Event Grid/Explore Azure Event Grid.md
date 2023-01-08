#azure #az-204 

## Overview
Azure Event Grid allows for event-driven, reactive programming.
Uses the publish-subscribe model.
Publishers emit events, but have no expectations about how an event is handled.
Subscribers decide what events they want to listen for.

Easily build applications with event-based architecture.
Event Grid has built-in support for events from Azure services, like storage blobs and resource groups.
Has support for your own events using custom topics.

Can use filters to route specific events to different endpoints.
Multicast to multiple endpoints.
Filters can make sure your own events are reliably delivered.

Image below shows how Event Grid connects sources and handlers (not a comprehensive list of supported integrations).
![[Event Grid Sources & Handlers.png]]

## Concepts in Azure Event Grid
- Events
- Event sources
- Topics
- Event subscriptions
- Event handlers

## Events
The smallest amount of information that describes something happened.
Event event has common information:
- Source
- Unique Identifier
Every event also has specific information relevant to the specific type of event e.g.:
- Azure Storage has file details, such as `lastTimeModified`
- Event Hubs has the URL of the Capture file

An event of size up to 64KB is covered by __General Availability__ (GA) __Service Level Agreements__ (SLA).
Support for an event of up to 1MB is currently in preview.
Events over 64KB are charged in 64KB increments.

## Event Sources
Where the event happened.
Each source related to one or more event types.
E.g. Azure Storage is the event source for blob created events.
IoT Hub is event source for device created events.
Your application is the source for custom events that you define.
Event sources are responsible for sending events to Event Grid.

## Topics
Event grid topic provides an endpoint where source sends events.
Publisher creates the topic, and decides whether an event source needs one or more topics.
A topic is used for a collection or related events.
To respond to certain types of events, subscribers decide which topics to subscribe to.

__System Topics__ are built-in topics provided by Azure services.
You don't see these in your subscription because the publisher owns the topics, but you can subscribe to them.
To subscribe, provide information about the resource you want to receive events from.
As long as you have resource access, you can subscribe.

__Custom Topics__ are app and third party topics.
You can see custom topics in your subscription when you create or are assigned access.

## Event Subscriptions
A subscription tells Event Grid which events on a topic you're listening to.
When creating subscription, provide endpoint for handling the event.
Can filter events that are sent to the endpoint by subject or subject pattern.
Set an expiration for event subscriptions that are only needed for a limited time.

## Event Handlers
The place where the event is sent.
Handler takes from further action to process the event.
Event Grid supports several handler types.
Can sue supported Azure service or your own webhook as the handler.
Event Grid follows different mechanisms to guarantee the delivery of the event, depending on type of handler.
For HTTP webhook handlers, events are retried until handler returns a status code of `200 OK`.
For Azure Storage Queue, events are retried until the Queue service successfully processes the message push into the queue.