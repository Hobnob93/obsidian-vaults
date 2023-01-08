#azure #az-204 #cli 

## Overview
Event Grid provides durable delivery.
Each event is tried at least once to be delivered to each matching subscription.
If a subscriber's endpoint doesn't acknowledge receipt, or if there is a failure, Event Grid retries delivery based on a fixed retry schedule and retry policy.
By default, one event at a time is delivered to a subscriber, and payload is an array with a single event.

## Retry Schedule
When an error is received for a delivery attempt, Eg decides whether it should retry the delivery; dead-letter the event; or drop the event based on the type of error.

If error returned by subscriber is configuration-related, that can't be fixed with retries.
EG will either perform dead-lettering on the event or drop it if dead-letter isn't configured.

Types of endpoints and error codes where retry doesn't happen:
- __Azure Resources__
	- 400 Bad Request
	- 413 Request Entity Too Large
	- 403 Forbidden
- __Webhook__
	- 400 Bad Request
	- 413 Request Entity Too Large
	- 403 Forbidden
	- 404 Not Found
	- 401 Unauthorized

If error returned isn't one of the above, 30 seconds is waited for a response.
If endpoint hasn't responded, message is queued for retry.
EG uses an exponential backoff retry policy for event delivery.

If endpoint responds within 3 minutes, the requeued event will attempt to be removed.
However, duplicates may still be received.
A small randomisation to all retry steps is added, and so may opportunistically skip certain retries if an endpoint is consistently unhealthy, down for a long period, or appears to be overwhelmed.

## Retry Policy
Can customise the retry policy when creating an event subscription by using the following two configurations.
An event will be dropped if either limit is reached.
- __Maximum number of attempts__
	- Integer between 1 and 30
	- Default is 30
- __Event time-to-live__ (TTL)
	- Integer between 1 and 1440 minutes
	- Default is 1440 minutes

An example setting max number of attempts to 18:
```shell
az eventgrid event-subscription create -g gridResourceGroup \
	--topic-name <topic-name> --name <event-subscription-name> \
	--endpoint <endpoint-url> --max-delivery-attempts 18
```

## Output Batching
Can configure batching of events to improve HTTP performance in high-throughput scenarios.
Batching is disabled by default.
Can be enabled per-subscription via the portal, CLI, PowerShell, or SDKs.

Batch delivery has two settings:
- __Max events per batch__
	- Will never be exceeded, but may be less if no other events at time of publish
	- No delay implemented to create a batch if fewer events are available
	- Must be between 1 and 5,000
- __Preferred batch size in kilobytes__
	- Target ceiling of batch size in KB
	- Batch may be smaller
	- Possible to be larger *if* a single event is larger than preferred size

## Delayed Delivery
As an endpoint experiences delivery failures, a delay will begin when retrying.
New deliveries to the same endpoint will also be impacted by a delay.
In some cases, delays can be several hours.

Purpose is to protect unhealthy endpoints and the Event Grid system.
Without back-off delay, retry policies and volume capabilities can overwhelm a system.

## Dead Letter Events
If an event can't be delivered in a certain time period, or after retrying a number of times, the event can be sent to a storage account.
Process is known as dead-lettering.

By default, dead lettering is disabled, so events reaching these thresholds will be dropped instead.
Must specify a storage account to hold undelivered events when creating the event subscription in order to enable.
Pull events from the storage account to resolve deliveries.

There is a 5 minute delay between last delivery attempt and dead-lettering.
Intended to reduce number of Blob storage operations.
if dead-letter location is unavailable for 4 hours, then the event is dropped.

## Custom Delivery Properties
Event subscriptions allow you to set up HTTP headers included in delivery events.
Allows you to set custom headers required by a destination.
Can set up to 10 headers when creating an event subscription.
Each header value shouldn't be greater than 4,096 bytes.
Custom headers on events delivered to following destinations:
- Webhooks
- Azure Service Bus topics and queues
- Azure Event Hubs
- Relay Hybrid Connections

Before setting dead-lettering location, you must have a storage account with a container.
You provide the endpoint for this container when creating the event subscription.