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
