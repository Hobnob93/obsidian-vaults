#azure #az-204 #json 

The *skeleton* is the general structure of an ARM template.
Defined via JSON, with the following properties:
- `$schema`
	- Describes properties available within a template
- `contentVersion`
	- Version of the template
	- Can provide any value for this property
- `apiProfile`
	- Use this to avoid having to specify API versions for each resource in the template
- `parameters`
	- Values you can pass along to your template
- `variables` ([[ARM Templates - Parameters|More Info]])
	- You transform parameters or resource properties using function expressions
- `functions` ([[ARM Templates - Functions|More Info]])
	- User-defined functions available within the template
- `resources` ([[ARM Templates - Resources|More Info]])
	- The Azure resources you'll want to deploy or update
- `outputs`
	- Values that are returned after the deployments

```json
{
	"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
	"contentVersion": "1.0.0",
	"apiProfile": "",
	"parameters": { },
	"variables": { },
	"functions": [ ],
	"resources": [ ],
	"outputs": { }
}
```