#azure #az-204 #json 

Allows you to apply transformations to your ARM variables
- Template Functions (built-in)
- User-Defined Functions

Functions are called using parentheses:
```json
{
	"condition": "[equals(parameters('newOrExisting'), 'new')]"
}
```

There are a whole host of functions available:
- **Array**
	- `array`, `concat`, `contains`, `createArray`, `empty`, `first`, `intersection`, `last`, `length`, `min`, `max`, `range`, `skip`, `take`, `union`
- **Comparison**
	- `coalesce`, `equals`, `less`, `lessOrEquals`, `greater`, `greaterOrEquals`
- **Date**
	- `dateTimeAdd`, `utcNow`
- **Deployment**
	- `deployment`, `environment`, `parameters`, `variables`
- **Logical**
	- `and`, `or`, `if`, `not`
- **Numeric**
	- `add`, `copyIndex`, `div`, `float`, `int`, `min`, `max`, `mod`, `mul`, `sub`
- **Object**
	- `contains`, `empty`, `intersection`, `json`, `length`, `union`
- **Resource**
	- `extensionResourceId`, `ListAccountSas`, `listKeys`, `listSecrets`, `list*`, `picZones`, `providers`, `reference`, `resourceGroup`, `resourceID`, `subscription`, `subscriptionResourceId`, `tenantResourceId`
- **String**
	- `base64`, `base64ToJson`, `base64ToString`, `concat`, `contains`, `dataUri`, `DataUriToString`, `empty`, `endsWith`, `first`, `format`, `guid`, `indexOf`, `last`, `lastIndexOf`, `length`, `newGuid`, `padLeft`, `replace`, `skip`, `split`, `startsWith`, `string`, `substring`, `take`, `toLower`, `toUpper`, `trim`, `uniqueString`, `uri`, `uriComponent`, `uriComponentToString`