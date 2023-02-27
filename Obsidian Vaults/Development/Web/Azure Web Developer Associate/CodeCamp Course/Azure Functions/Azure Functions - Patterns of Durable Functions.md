#azure #az-204 

**Function Chaining**
- Executing a sequence of functions in a specific order
- Often the output of one function needs to be applied to the input of another function
- Durable Functions allow us to implement this pattern concisely

**Fan-out/fan-in**
- Executing multiple functions in parallel then waiting for them all to finish

**Fanning out**
- Can be completed with normal functions
- Have one function send multiple messages to a queue

**Fanning in**
- More difficult as we have to track when queue-triggered functions end and store function outputs
- Durable Functions extension handles this pattern with relatively simple implementation

**Async HTTP API**
- Addresses the problem of coordinating state of long-running operations with external clients
- Have an HTTP call trigger the long-running action, then redirect client to a status endpoint that they can poll to learn when the operation is complete
- Durable Functions provide built-in APIs that simplify code we write for interacting with long-running function executions

**Monitor**
- Refers to flexible recurring process in a workflow, such as polling until a certain condition is met
- Generally addressed with a regular timer trigger with a fixed interval, making managing instance lifetimes difficult
- Durable Functions enables flexible recurrence intervals, task lifetime management, and ability to create multiple monitor processes from a single orchestration

**Human Interaction**
- Many automated processes involve some form of human interaction
- Humans are not always available and as responsive as cloud services, so including humans can be tricky
- Automated processes must allow for this, and they often do this with timeouts and compensation logic

**Aggregator (stateful entities)**
 - Aggregating event data over a period of time into a single, addressable entity
 - Data being aggregated may come from multiple sources, be delivered in batches, or may be scattered over long periods of time
 - Aggregator may need to act on event data as it arrives as external clients may need to query the aggregated data