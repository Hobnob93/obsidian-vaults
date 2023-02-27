#azure #az-204 #json

Every function contains a function config file called `function.json`.
It defines function's trigger, bindings, and other config settings.
```json
{
	"disabled": false,
	"bindings": [
		{
			"type": "bindingType",
			"direction": "in",
			"name": "myBindingName"
		}
	]
}
```

Each function also has a file called `hosts.json`.
It contains global configs - *a lot* of them!
```json
{
	"extensions": {
		"http": {
			"routePrefix": "api",
			"maxOutstandingRequests": 200,
			"maxConcurrentRequests": 100,
			"dynamicThrottlesEnabled": true,
			"hsts": {
				"isEnabled": true,
				"maxAge": "10"
			},
			"customHeaders": {
				"X-Content-Type-Options": "nosniff"
			}
		}
	}
}
```