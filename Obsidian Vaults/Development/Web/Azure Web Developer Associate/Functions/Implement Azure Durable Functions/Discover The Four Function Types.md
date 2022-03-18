#azure #azure-wda 

# Discover The Four Function Types
Currently, the types are:
- [[#Orchestrator Functions]]
- [[#Activity Functions]]
- [[#Entity Functions]]
- [[#Client Functions]]

## Orchestrator Functions
Describe how, and the order in which, actions are executed.
Orchestration described via code using [[Explore Durable Functions App Patterns#Application Patterns|Application Patterns]].
An orchestration can have many types of actions, including; activity functions, polling, HTTP, and timers.
They can interact with [[#Entity Functions]].

There are strict requirements on how to write the code.
Code must be deterministic.
Failing to follow determinism requirements can cause functions to fail to ruin correctly.

## Activity Functions
The basic unity of work in a durable function orchestration.
Each task to complete a scenario (such as processing an order) would be a separate activity function.
They may be executed serially, in parallel, or a combination thereof.

Not restricted to the type of work you can do in them.
Frequently used to make network calls or run CPU intensive operations.
Can return data back to the orchestrator function.

An ==activity trigger== defines an activity function.
.NET functions receive a `DurableActivityContext` as a parameter.
Can bind trigger to any other JSON-serialisable object to pass inputs to the function.
In JavaScript you can access input via the `<activity-trigger-binding-name>` property on the `context.bindings` object.

Can only have a single value passed to them.
To pass multiple, you'll need to use `tuples`, `arrays`, or other complex types.

## Entity Functions
Define operations for reading and updating small pieces of state.
Might be referred to as ==durable entities==.
They have a special trigger type; `entity trigger`.
Can be invoked from client functions or from orchestrator functions.
They do not have specific code constraints.
They manage state explicitly rather than implicitly, representing state via control flow.

Additional notes:
- Entities accessed via unique identifier
	- `Entity ID`
	- A pair of strings uniquely identifying an entity instance
- Operations on entities require their `entity ID` and the `operation name`
	- Op name is a string specifying operation to perform

## Client Functions
[[#Orchestrator Functions|Orchestrator]] and [[#Entity Functions|Entity]] functions are triggered by their bindings.
Both these triggers work by reacting to messages enqueued in a ==task hub==.
These messages are delivered by using an ==orchestrator client binding==, or ==entity client binding==, from within a ==client function==.
Any non-orchestrator function can be a client function.
What makes a function a "client function" is the use of *durable client output binding*.

Orchestrator and Entity functions cannot be triggered directly using buttons in *Azure Portal*.
Must instead run a client function that starts one of them as part of its implementation.
A `manual trigger` function is recommended, especially when testing.