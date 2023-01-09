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