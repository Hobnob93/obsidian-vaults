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
	- 