#azure #az-204 #xml 

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

#### Send Request
Can send "one way" request to the specified URL without waiting for a response.
Can send normal request to specified URL and waits for a response.

#### Set HTTP Proxy
Allows you to route forwarded requests via an HTTP proxy.

#### Set Variable
Persist a value in a named context variable for later access.
```xml
<set-variable name="IsMobile" 
			  value="@(context.Request.Headers.GetValueOrDefault
				  ('User-Agent','').Contains('iPad') ||
			  context.Request.Headers.GetValueOrDefault
				  ('User-Agent','').Contains('iPhone'))" />
```

#### Wait
Waits for enclosed send request, [[APIM - Caching Policies#Get Value from Cache|get value from cache]], or control flow policies to complete before proceeding.

#### Set Request Method
Allows you to change the HTTP method for a request.

#### Set Status Code
Changes the HTTP status code to the specified value.

#### Trace
Adds custom traces into the API Inspector output, Application Insights telemetries, and Resource Logs.