#azure #az-204 #json

Allows you to pass variables to your ARM template.
Controlled via JSON properties:
- `type`
	- The expected data type of the input value
	- E.g. `string`, `securestring`, `int`, `bool`, `object`, `secureObject`, `array`
- `defaultValue`
	- If no value provided, it will be set to this value
- `allowedValues`
	- An array of allowed values
- `minValue`
	- The minimum possible value
- `maxValue`
	- The maximum possible value
- `minLength`
	- The minimum length of characters in an array
- `maxLength`
	- The maximum length of characters in an array
- `description`
	- Will be displayed in the Azure Portal

Below example names the storage resource based on the name provided as a parameter.
```json
{
	...
	"parameters": {
		"storageName": {
			"type": "string",
			"minLength": 5,
			"maxLength": 20
		}
	}
	...
	"resources": [
		{
			...
			"name": "[parameters('storageName')]"
			...
		}
	]
	...
}
```