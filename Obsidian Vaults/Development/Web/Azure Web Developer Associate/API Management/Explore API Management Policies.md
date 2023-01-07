#azure #az-204 #xml 

## Overview
Policies are a powerful capability.
Allows publisher to change behaviour of the API through config.
Policies are a collection of statements executed sequentially on request or response of an API.

Policies are applied inside the gateway.
Gateway receives all requests and usually forwards them unaltered to the underlying API.
However, a policy can apply changes to inbound requests and outbound responses.
Policy expressions can be used as attribute values or text values in any of the API Management policies, unless a policy specifies otherwise.

## Understanding Policy Configuration
Policy definition is a simple XML document describing sequence of inbound and outbound statements.
XML can be edited directly in the definition window.

Configuration is divided into `inbound`, `backend`, `outbound`, and `on-error`.
The series of statements is executed in order for a request and a response.
```xml
<policies>
	<inbound>
		<!-- statements applied to request -->
	</inbound>
	<backend>
		<!-- statements applied before request is forwarded to backend -->
	</backend>
	<outbound>
		<!-- statements applied to the response -->
	</outbound>
	<on-error>
		<!-- statements applied if there is an error condition -->
	</on-error>
</policies>
```

If there is an error in the process, any remaining steps in the given section are skipped.
Execution then jumps to `on-error`.
Placing statements in `on-error`, you can review the error by using `context.LastError` property; inspect and customise the error response using `set-body`; and configure what happens if an error occurs.

## Apply Policies Specified At Different Scopes
If you have a policy at the global level and a policy configured for an API, then whenever that particular API is used, both policies will be applied.
API Management allows for deterministic ordering of combined policy statements via the base element.

In this example, `cross-domain` would execute before any higher policies, which in turn is before the `find-and-replace` policy.
```xml
<policies>
	<inbound>
		<cross-domain />
		<base />
		<find-and-replace from="xyz" to="abc" />
	</inbound>
</policies>
```

## Filter Response Content
Policy defined in example below demonstrates how to filter data elements from response payload based on product associated with the request.

Snippet assumes that response content is formatted as JSON and contains root-level properties named "minutely", "hourly", "daily", "flags".
```xml
<policies>
	<inbound>
		<base />
	</inbound>
	<backend>
		<base />
	</backend>
	<outbound>
		<base />
		<choose>
			<when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">
				<set-body>
					@{
						var response = context.Response.Body.As<JObject>();
						var keys = new[] 
							{ "minutely", "hourtly", "daily", "flags" };
						
						foreach (var key in keys)
							response.Property(key).Remove();
					
						return response.ToString();
					}
				</set-body>
			</when>
		</choose>
	</outbound>
	<on-error>
		<base />
	</on-error>
</policies>
```