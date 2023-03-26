#azure #az-204 #xml 

#### Check HTTP Header
Enforces existence and/or value of an HTTP header

#### Limit Call Rate
Prevents API usage spikes by limiting call rate.
On a per-subscription basis.
On a per-key basis.

#### Restrict Caller IPs
Filters (allow/disallow) calls from specific IP addresses and/or address ranges.
```xml
<ip-filter action="allow">
	<address>13.66.201.169</address>
	<address-range from="13.66.140.128" to="13.66.140.143" />
</ip-filter>
```

#### Set Usage Quota
Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota.
On a per-subscription basis.
On a per-key basis.

#### Validate JWT
Enforces existences of a valid JWT.
Extracted from specified HTTP header.
Or extracted from specified query string parameter.
```xml
<validate-jwt header-name="Authorization" require-scheme="Bearer">
	<issuer-signing-keys>
		<key>{{jwt-signing-key}}</key>
	</issuer-signing-keys>
	<audiences>
		<audience>@(context.Request.OriginalUrl.Host)</audience>
	</audiences>
	<issuers>
		<issuer>https://contoso.com</issuer>
	</issuers>
</validate-jwt>
```

#### Validate Client Certificate
Enforces a certificate presented by client to an APIM instance matches specified validation rules and claims.

#### Control Flow
Conditionally applies policy statements based on the evaluation of boolean expressions.

#### Forward Request
Forwards the request to the backend service.

#### Limit Concurrency
Prevents enclosed policies from executing by more than the specified number of requests at a time.
```xml
<limit-concurrency key="@((string)context.Variables['connectionId'])"
				   max-count="3">
	<forward-request timeout="120" />
</limit-concurrency>
```

#### Log to Event Hub
Sends messages in specified format to a message target defined by a Logger entity.
Messages sent to [[CodeCamp - Azure Event Hub|Event Hub]].

#### Emit Metrics
Sends custom metrics to [[CodeCamp - Application Insights|Application Insights]] at execution.

#### Mock Response
Aborts pipeline execution and returns a mocked response directly to the caller.
```xml
<mock-response status-code="200" content-type="application/json" />
```

#### Retry
Retries execution of enclosed policy statements.
Retries until condition is met.
Execution will repeat at specified intervals.
Will only retry up to a specified retry count.

#### Return Response
Aborts pipeline execution and returns specified response directly to the caller.