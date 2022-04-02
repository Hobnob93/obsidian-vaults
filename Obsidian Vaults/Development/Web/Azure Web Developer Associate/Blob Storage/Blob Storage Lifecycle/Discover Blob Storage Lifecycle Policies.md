#azure #az-204 #json 

# Discover Blob Storage Lifecycle Policies
A lifecycle management policy is a ==collection of rules==.
Each rule includes a ==filter== and an ==action== set.
Filter limits rule actions to certain set of objects within a container or object names.
Action applies the tier or delete actions to the filtered set of objects.
```json
{
	"rules": [
		{
			"name": "rule1",
			"enabled": true,
			"type": "Lifecycle",
			"definition": {...}
		},
		{
			"name": "rule2",
			"type": "Lifecycle",
			"definition": {...}
		}
	]
}
```

A policy is a collection of `rules`:
- At least one rule is required in a policy
- Can define up to 100 rules in a policy

Each rule has several parameters:
- `name`
	- Up to 256 characters
	- It is case-sensitive
	- Unique within a policy
- `enabled`
	- Optional boolean to control if rule applies
	- Default is `true` if not set
- `type`
	- An enum value
	- Current valid type is `Lifecycle`
- `definition`
	- An object defining the lifecycle rule
	- Made up a filter and an action

## Rules
Each rule definition includes a filter and an action set.

The JSON below runs actions on objects that exist inside `container1` and start with `foo`
```json
{
	"rules": [
		{
			"name": "ruleFoo",
			"enabled": true,
			"type": "Lifecycle",
			"definition": {
				"filters": {
					"blobTypes": [ "blockBlob" ],
					"prefixMatch": [ "container1/foo" ]
				},
				"actions": {
					"baseBlob": {
						"tierToCool": { 
							"daysAfterModificationGreaterThan": 30
						},
						"tierToArchive": {
							"daysAfterModificationGreaterThan": 90
						},
						"delete": {
							"daysAfterModificationGreaterThan": 2555
						}
					},
					"snapshot": {
						"delete": {
							"daysAfterCreationGreaterThan": 90
						}
					}
				}
			}
		}
	]
}
```

## Rule Filters
Filters limit rule actions to a subset of blobs within the storage account.
A logical `AND` runes if there are multiple filters applied.
- `blobTypes`
	- An array of predefined enum values
- `prefixMatch`
	- Array of string prefixes to be matched
	- Each rule can define up to 10 prefixes
	- Prefix string *must* start with a container name
- `blobIndexMatch`
	- Array of dictionary values consisting of blob index tag key and value conditions to be matched
	- Each rule can define up to 10 blob index tag conditions

## Rule Actions
Actions applied to filtered blobs when condition is met.

Lifecycle management supports tiering and deletion of blobs as well as snapshots.
Define *at least* one action for each rule.
- `tierToCool`
	- Supported for blockBlob
	- Supported for snapshot
- `enableAutoTierToHotFromCool`
	- Supported for blockBlob
	- Not supported for snapshot
- `tierToArchive`
	- Supported for blockBlob
	- Supported for snapshot
- `delete`
	- Supported for blockBlob
	- Supported for appendBlob
	- Supported for snapshot

Run conditions are based on age.
base blobs use the latest modified time to track age.
Blob snapshots use the creation time to track age.
- `daysAfterModificationGreaterThan`
	- Integer value indicating age in days
- `daysAfterCreationGreaterThan`
	- Integer value indicating age in days