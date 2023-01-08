#azure #az-204 #json 

## Overview
When creating an event subscription, you have three filtering options:
1. Event types
2. Subject begins or ends with
3. Advanced fields and operators

## Event Type Filtering
By default, all event types for event source are sent to endpoint.
Can decide to send only certain event types to your endpoint by filtering.
E.g. can get notified of updates but, not deletions, of resources.
- Filter by the `Microsoft.Resources.ResourceWriteSuccess` event type.
Provide an array with event types, or specify `All`.

The JSON syntax for filtering by event type is:
```json
"filter": {
	"includeEventTypes": [
		"Microsoft.Resources.ResourceWriteFailure",
		"Microsoft.Resources.ResourceWriteSuccess"
	]
}
```

## Subject Filtering
For simple filtering, you can specify a starting or ending value for the subject.
E.g. can specify subject ends with `.txt`.
Or you can filter by `/blobServices/default/containers/testcontainer` to get all events for that container but not other containers.

The JSON syntax for filtering by subject is:
```json
"filter": {
	"subjectBeginsWith": "/blobServices/default/containers/{container}/log",
	"subjectEndsWith": ".jpg"
}
```

## Advanced Filtering
Filter by values in the data fields.
Specify comparison operator.
In advanced filtering, you specify the:
- operator type
	- type of comparison
- key
	- field in event data you're using for filtering
- value or values
	- value or values to compare

The JSON syntax for using advanced filters:
```json
"filter": {
	"advancedFilters": [
		{
			"operatorType": "NumberGreaterThanOrEquals",
			"key": "Data.Key1",
			"value": 5
		},
		{
			"operatorType": "StrigContainers",
			"key": "Subject",
			"values": [ "container1", "container2" ]
		}
	]
}
```