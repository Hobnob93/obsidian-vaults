#azure #az-204 #xml 

## Control Flow
The `choose` policy applies enclosed statements based on outcome of valuation of boolean expressions.
Similar to an if-then-else or switch construct in a programming language.
```xml
<choose>
	<when condition="Expression | Constant">
		<!-- statements to be applied if expression met -->
	</when>
	<when condition="Expression | Constant">
		<!-- statements to be applied if expression met -->
	</when>
	<otherwise>
		<!-- statements to be applied if NO expression met -->
	</otherwise>
</choose>
```

Control flow policy must contain at least one `when` element.
The `otherwise` element is optional, and only applies if all other `when` elements evaluate to false.
Conditions are evaluated in the order that they appear.

## Forward Request
The `forward-request` policy forwards incoming request to backend service specified in request context.
The backend service URL is specified in the API settings and can be changed using the set backend service policy.

```xml
<forward-request timeout="time in seconds" follow-redirects="true | false" />
```

Removing this policy results in request not being forwarded to the backend service, and policies in outbound section are evaluated immediately upon successful completion of policies in inbound section.

## Limit Concurrency
The `limit-concurrency` policy prevents enclosed policies from executing more than specified number of requests at any time.
Upon exceeding that number, new requests will fail immediately with a `429 Too Mnay Requests` status code.
```xml
<limit-concurrency key="expression" max-count="number">
	<!-- statements to be limited -->
</limit-concurrency>
```

## Log To Event Hub
The `log-to-eventhub` policy sends messages in specified format to Event Hub defined by Logger entity.
Policy is used for saving selected request or response context information for online or offline analysis.
```xml
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">
	Expression returning a string to be logged
</log-to-eventhub>
```

## Mock Response
`The mock-response` policy is used to mock APIs and operations.
It aborts normal pipeline execution and returns a mocked response to the caller.
Policy always tries to return responses of highest fidelity.
It prefers response content examples, whenever available.
It generates sample responses from schemas, when provided and examples are not.
If neither examples or schemas are found, responses with no content are returned.
```xml
<mock-response status-code="code" content-type="media type" />
```

## Retry
The `retry` policy executes its child policies once and then retries their execution until retry `condition` becomes false, or retry `count` is reached.
```xml
<retry condition="expression | constant" count="number" interval="in seconds" max-interval="in seconds" delta="retry interval in delta seconds" first-fast-retry="bool expression | constant">
	<!-- statements to be retried -->
</retry>
```

## Return Response
The `return-response` policy aborts pipeline execution and returns either default or custom response to the caller.
Default response is `200 OK` with no body. 
Custom response can be specified via context variable or policy statements.
When both are provided, response contained with context variable is modified by policy statements before being returned to caller.
```xml
<return-response response-variable-name="existing context variable">
	<set-header />
	<set-body />
	<set-status />
</return-response>
```