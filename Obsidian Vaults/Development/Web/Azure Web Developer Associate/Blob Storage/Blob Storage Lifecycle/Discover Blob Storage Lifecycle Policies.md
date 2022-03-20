#azure #azure-wda #json 

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
