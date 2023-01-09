#azure #az-204 

## Overview
Azure Service Bus is a fully managed enterprise integration message broker.
It can decouple applications and services.
Data transferred between apps and services using *messages*.
A message is a container with metadata and actual data.
The data can be any information, including structured data in formats like JSON, XML, Apache Avro, Plain Text, etc.

Common messaging scenarios:
- Messaging
	- Transfer business data, such as sales or purchase orders, journals, or inventory movements
- Decouple applications
	- Improve reliability and scalability of apps and services
	- Client and service don't have to be online at the same time
- Topics and subscriptions
	- Enable 1:*n* relationships between publishers and subscribers
- Message sessions
	- Implement workflows that require message ordering or message deferral

## Service Bus Tiers
Service Bus offers a standard and premium tier.
Feature sets are nearly identical, but designed to service different use cases.
Premium recommended for production scenarios.
- Addresses requests for scale, performance, and availability for critical apps

Some high-level differences:
| Premium                    | Standard                 |
| -------------------------- | ------------------------ |
| High throughput            | Variable throughput      |
| Predictable performance    | Variable latency         |
| Fixed pricing              | Pay as you go            |
| Scale workload up and down | N/A                      |
| Message size up to 100MB   | Message size up to 256KB |

## Advanced Features
Service Bus has advanced features enabling solutions to more complex problems.
- __Message sessions__
	- Guarantees a first-in-first-out (FIFO) queue
	- Enables exclusive ordered handling of unbound sequences of related messages
- __Auto-forwarding__
	- Chains a queue or subscription to another queue or topic in the same namespace
- __Dead-letter queue__
	- Supports a DLQ
	- Holds messages that can't be delivered to any receiver
	- Lets you remove messages from DLQ and inspect them
- __Scheduled delivery__
	- Can submit messages to queue or topic for delayed processing
	- Can schedule a job to become available for processing at a certain time
- __Message deferral__
	- A queue or subscription client can defer retrieval of message until later time
	- Message remains in queue or subscription, but set aside
- __Batching__
	- Client-side batching enables queue or topic client to delay sending a message for a period of time
- __Transactions__
	- Groups two or more operations together in an _executing scope_
	- Supports grouping operations against single messaging entity within scope of a single transaction
	- Message entity can be a queue, topic, or subscription
- __Filtering and actions__
	- Subscribers can define which messages they want to receive from a topic
	- Messages are specified in form of one or more named subscription rules
- __Auto-delete on idle__
	- Enables specifying an idle interval after which a queue is automatically deleted
	- Minimum duration is 5 minutes
- __Duplicate detection__
	- Error could cause client to have a doubt about outcome of a send operation
	- Duplicate detection enables sender to resend the same message
	- Or for queue or topic to discard any duplicate copies
- __Security protocols__
	- Supports security protocols such as [[Shared Access Signatures]] (SAS), Role-based Access Control (RBAC), and [[Managed Identities]] for Azure resources
- __Geo-disaster recover__
	- When regions or data centres experience downtime, disaster recovery enables data processing to continue operating on a different region or data centre
- __Security__
	- Supports standard AMQP 1.0 and HTTP/REST protocols

## Compliance With Standards & Protocols
Primary wire protocol for Service Bus is [Advanced Messaging Queueing Protocol](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-amqp-overview) (AMQP) 1.0; an open ISO/IEC standard.
Allows customers to write apps that work against Service Bus and on-premises brokers such as ActiveMQ or RabbitMQ.

Service Bus Premium is fully compliant with Java/Jakarta EE [Java Message Service](https://learn.microsoft.com/en-us/azure/service-bus-messaging/how-to-use-java-message-service-20) (JMS) 2.0 API.