#azure #az-204 #xml 

#### Validate Content
Validates the size or JSON schema of a request or response body against the API schema.

#### Validate Parameters
Validates request header, query, or path parameters against API schema.

#### Validate Headers
Validates the response headers against the API schema.

#### Validate Status Code
Validates HTTP status codes in responses against the API schema.
```xml
<validate-status-code unspecified-status-code-action="prevent"
					  errors-variable-name="resposneStatusCodeValidation" />
```

#### Validate GraphQL Request
Validates and authorises a request to a GraphQL API.