#azure #az-204 #yaml

OpenAPI Specification (OAS) defines a standard, language-agnostic interface to RESTful APIs.
Allows both humans and computers to discover and understand capabilities of the service without access to source code, documentation, or network traffic inspection.

Swagger and OpenAPI used to eb the same thing, but as of OpenAPI v3, they are separate.
- OpenAPI: specification
- Swagger: tool for implementing the specification

Can be represented in either JSON or YAML.
```yml
paths:
	/users:
		post:
			summary: Adds a new user
			requestBody:
				content:
					application/json:
						schema: # Request body contents
							type: object
							properties:
								id:
									type: integer
								name:
									type: string
								example:
									id: 10
									name: Blarg Darg
			responses:
				'200':
					description: OK
```