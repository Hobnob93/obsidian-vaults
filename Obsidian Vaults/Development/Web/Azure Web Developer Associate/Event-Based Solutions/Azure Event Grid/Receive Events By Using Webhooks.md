#azure #az-204 

## Overview
Webhooks one of many ways to receive events from Azure Event Grid.
EG POSTs an HTTP request to configured endpoint with event in request body.

EG requires you to prove ownership of webhook.
Requirement prevents malicious user from flooding endpoint with events.

When any of these Azure services is used, Azure automatically handles this validation:
- Azure Logic Apps with Event Grid Connector
- Azure Automation via webhook
- Azure Functions with Event Grid Trigger

## Endpoint Validation With Event Grid Events
If another type of endpoint is used, such as HTTP trigger based Azure function, your endpoint code needs to participate in a validation handshake with EG.

EG supports two ways of validating the subscription:
- __Synchronous Handshake__
	- At time of event creation, EG sends a subscription validation event to endpoint
	- Schema of event is similar to any other EG event
	- Data portion of event includes a `validationCode` property
	- Your app verifies validation request is for an expected event subscription & return resulting validation code in the response synchronously
	- This handshake mechanism is supported in all EG versions
- __Asynchronous Handshake__
	- Sometimes validation code can't be returned synchronously
	- Such as if you use a third party service like Zapier or IFTTT
	- You can't programmatically respond with a validation code

Starting with version 2018-05-01-preview, EG supports manual validation handshake.
If creating event subscription with SDK or tool using this API version or later, EG sends a `validationUrl` property in data portion of subscription validation event.
To complete handshake, do a `GET` request to that URL; can either use a REST client or a web browser.

This validation URL is valid for 5 minutes.
During this time, the provisioning state of the event subscription is `AwaitingManualAction`.
If you fail to complete within 5 minutes, state changes to `Failed`.
You'll have to create the event subscription again before starting manual validation.

This mechanism also requires webhook endpoint to return an HTTP status code of 200 so it knows the POST for validation event was accepted before it can be put into manual mode.
if the endpoint returns 200 but doesn't return a validation response synchronously, mode is transitioned to manual validation.