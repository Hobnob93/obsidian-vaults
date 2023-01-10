#azure #az-204 

## Overview
Messages carry payload and metadata.
Metadata is a key-value pair of properties describing the payload, and gives handling instructions to Service Bus and apps.
Sometimes metadata alone is sufficient and the payload remains empty.

The object model of the official Service Bus client for .NET and Java reflect the abstract Service Bus message structure, which is mapped to and from the wire protocols Service Bus supports.

A Service Bus consists of a binary payload section (which Service Bus never handles server-side), and two sets of properties.
The *broker properties* are predefined by the system.
- Either control message-level functionality inside the broker, or maps to common and standardised metadata items
The *user properties* are key-value pairs defined and set by the application.

## Message Routing & Correlation
A subset of the broker properties are used to help apps route messages to particular destinations.
- Specifically `To`, `ReplyTo`, `ReplyToSessionId`, `MessageId`, `CorrelationId`, and `SessionId`

Consider a few patterns:
- __Simple request/reply__
	- Publisher sends message to queue & expects reply from message consumer
	- Publisher owns a queue into which it expects replies
	- Address of that queue is expressed in the `ReplyTo` property of the outbound message
	- On response, consumer copies `MessageId` of message into the `CorrelationId` property of the reply
	- Reply message is then delivered to the publisher's queue
	- One message can yield multiple replies
- __Multicast request/reply__
	- Publisher sends message to topic
	- Multiple subscribers eligible to consume message
	- Each sub might respond in the simple way
	- Pattern is used in discovery or roll-call scenarios and respondent typically identifies itself with a user property or inside the payload
	- If `ReplyTo` is a topic, such a set of discovery responses can be distributed to an audience
- __Multiplexing__
	- Session feature
	- Enables multiplexing of streams of related messages through single queue or subscription
	- Related messages is identified by matching `SessionId` values
	- Each session (or group) is routed to a specific receiver
	- Receiver holds the session under lock
- __Multiplexed request/reply__
	- Session feature
	- Enables multiplexed replies
	- Allows several publishers to share a reply queue
	- Set `ReplyToSessionId` to instruct consumer(s) to copy that value to `SessionId` property of reply message
	- Publishing queue or topic does not need to be session-aware
	- As message is sent, publisher can specifically wait for a session with given `SessionId` to materialise on the queue by conditionally accepting a session receiver

Routing inside of a Service Bus namespace done using auto-forward chaining and topic subscription rules.
Routing across namespaces can be done using Azure Logic Apps.
The `To` property is reserved for future use and may be interpreted by broker with a specially enabled feature.
Apps wishing to implement routing should based on user properties and not use the `To` property.
- However, doing so will not cause compatibility issues

## Payload Serialisation
When in transit, or stored in Service Bus, payload is always an opaque, binary block.
The `ContentType` property enables apps to describe the payload.
Suggested format being MIME content-type description according to IETF RFC2045 e.g. `application/json;charset=utf-8`.

.NET Framework version of Service Bus API supports creating `BrokeredMessage` instances by passing .NET objects into constructor.

When using legacy SBMP protocol, objects are serialised with default binary serialiser, or with one that is externally supplied.
When using AMQP protocol, object is serialised into an AMQP object.
Receiver can retrieve objects with `GetBody<T>()` method, supplying expected type.
With AMQP, objects are serialised into an AMQP graph of `ArrayList` and `IDictionary<string,object>` objects.
Any AMQP client can decode them.