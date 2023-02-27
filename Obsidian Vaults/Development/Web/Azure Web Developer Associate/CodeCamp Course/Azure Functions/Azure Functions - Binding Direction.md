#azure #az-204 #json

All triggers and bindings have a direction property in the `function.json` file:
- Triggers are always *in*
- Input and output bindings can be *in* and/or *out*
- Some bindings support a special *inout* direction

The trigger is defined alongside the Input and Output bindings,
- Trigger will have the same name as a normal binding type, but with `Trigger` appended
- See below json for an example
```json
{
	"scriptFile": "__init__.py",
	"disabled": false,
	"bindings": [
		{
			"authLevel": "function",
			"type": "httpTrigger",
			"direction": "in",
			"name": "req"
		},
		{
			"type": "http",
			"direction": "out",
			"name": "$return"
		}
	]
}
```