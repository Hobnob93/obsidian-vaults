#azure #az-204 #json 

Event Hubs Schema Registry provides a centralised repository for schemas.
It provides flexibility for producer and consumer apps to exchange data without having to manage and share the schema between them.
It also allows them to evolve at different rates.

Schema Groups are under your namespace and can be accessed by all topics/Event Hubs under that namespace.
You can set compatibility to:
- Forward
- None
- Backward

Example schema:
```json
{
	"namespace": "com.azure.schemaregistry.samples",
	"type": "record",
	"name": "Order",
	"fields": [
		{
			"name": "id",
			"type": "string"
		},
		{
			"name": "amount",
			"type": "double"
		}
	]
}
```