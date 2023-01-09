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
	- 