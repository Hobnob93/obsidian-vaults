#azure #az-204 

## Overview
The queues, topics, subscriptions, and rules/actions form the core of the messaging capabilities.

## Queues
Queues offer first-in-first-out (FIFO) message delivery to one or more competing consumers.
Receivers typically receive and process messages in order they were added to the queue.
Only one message consumer receives and processes each message.
Messages are stored durably in the queue so producers (senders) and consumers (receivers) don't have to process messages concurrently.

Another benefit is _load-levelling_.
Enables producers/consumers to send/receive messages at different rates.
In apps, system load varies over time, however, processing time for a unit of work is typically constant.
Intermediating producers/consumers with a queue means consuming app only has to handle average load instead of peak load.

Using queues provides loose coupling between components.
Producers/consumers not aware of each other, a consumer can be upgraded without affecting the producer.

Can create queues using portal, PowerShell, CLI, or Resource Manager templates.
Send/receive messages using clients written in C#, Java, Python, and JavaScript.

## Receive and Delete Mode
One of the two receive modes.
Service Bus receives request from consumer & marks message as consumed and returns it to consumer application.
This is the simplest model.
Works best for scenarios in which app can tolerate not processing a message if failure occurs.

## Peek Lock Mode
The other of the two receive modes.
Receive operation becomes two-staged to support apps that cannot tolerate missing messages.
1. Finds next message to be consumed and _locks_ it to prevent other consumers receiving it, then returns message to consumer
2. After app finishes processing, it requests Service Bus to complete second stage of receive process. Only then is it marked as consumed.

If app is unable to process message from some reason, an _abandon message_ request can be sent.
Service Bus will _unlock_ the message to make it receivable again, either by the same consumer or another one.
There's a _timeout_ associated with the lock.
If app fails to process message before lock expires, Service Bus unlocks it to make it available as before.

## Topics & Subscriptions
A queue allows processing of a message by a single consumer.
In contrast to queues; topics and subscriptions provide a one-to-many relationship in a publish and subscribe pattern.
Useful for scaling to large numbers of recipients.
Each published message is made available to each subscriber registered with the topic.
Publisher sends a message to a topic, and one or more subscribers receive a copy of the message.
This will depend on filter rules set on the subscriptions.

Publishers send messages to a topic the same way as they do to a queue.
However, consumers don't receive messages directly from the topic.
Consumers receive messages from subscriptions of the topic.
A topic subscription resembles a virtual queue which receives copies of topic messages.
Consumers receive messages from a subscription the same way as they do a queue.

Creating a topic is similar to creating a queue.
Can create topics and subscriptions using the portal, PowerShell, CLI. or Resource Manager templates.
Send messages to a topic and receive messages from subscriptions using clients written in C#, Java, Python, and JavaScript.

## Rules & Actions
Messages that have specific characteristics must be processed a different way.
To enable this, you can configure subscriptions to find messages that have desired properties, and then perform modifications to those properties.
Although Service Bus subscriptions see all messages sent to a topic, you can only copy a subset of those messages to the virtual subscription queue.
This filtering is done using subscription filters.
Such modifications are called _filter actions_.
When subscription created, you can supply a filter expression that operates on the properties of a message.
Properties can be system properties (such as `label`), and/or custom properties (like `StoreName`).
The SQL filter expression is optional.
Without a SQL filter expression, any filter action defined on a subscription will be done on all messages for that subscription.