#azure #az-204 

## Overview
Azure Event Grid allows level of access to be controlled.
Allows different users to do various management operations such as list event subscriptions, create new ones, and generate keys.
Azure role-based access control (Azure RBAC) is used.

## Built-In Roles
EG provides the following built-in roles:
- __Event Grid Subscription Reader__
	- Read event subscriptions
- __Event Grid Subscription Contributor__
	- Manage event subscription operations
- __Event Grid Contributor__
	- Create and manage EG resources
- __Event Grid Data Sender__
	- Send events to Event Grid topics

Subscription roles are important when implementing event domains because they give users the permissions they need to subscribe to topics in your event domain.

## Permissions For Event Subscriptions
For event handlers that aren't a Webhook, you need write access to that resource.
This permissions check prevents unauthorised users from sending events to your resource.

You must have `Microsoft.EventGrid/EventSubscriptions/Write` permission on resource that is the event source.
This is because you're writing a new subscription at the scope of the resource.
Required resource differs based on whether you're subscribing to a system topic or a custom topic.
- System Topics
	- Need permissions to write a new event subscription at scope of resource publishing event
	- Format of the resource is `/subscriptions/{sub-id}/resourceGroups/{rg-name}/providers/{resource-prov}/{resource-type}/{resource-name}`
- Custom topics
	- Need permissions to write a new event subscription at scope of event grid topic
	- Format of the resource is `/subscriptions/{sub-id}/resourceGroups/{rg-name}/providers/Microsoft.EventGrid/topics/{topic-name}`