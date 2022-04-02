#azure #az-204

# Explore Durable Orchestrations
Use an [[Discover The Four Function Types#Orchestrator Functions|Orchestrator Function]] to orchestrate execution of other *durable functions* within an app.
They have the following characteristics:
- Define function workflows using procedural code
- No declarative schemas or designers are needed
- Can call other durable functions synchronously and asynchronously
- Output from called functions can be saved to local variables
- They are durable and reliable
- Progress is automatically ==checkpointed== when functions `await` or `yield`
- Local state never lost when process recycles or VM reboots
- They can be long-running
- Total lifespan of an ==orchestration instance== is indefinite

## Orchestration Identity
Each orchestration *instance* has an `instance ID`.
By default, this is generated from a GUID.
Can be a user-generated `string` value.
Each ID **must** be unique within a [[Explore Task Hubs|task hub]].

The `instance ID` is required for most instance management operations.
Also important for diagnostics, such as in *Application Insights* for troubleshooting analytics purposes.
Recommended to save generated IDs to an external location, such as database or app logs.

## Reliability
They maintain execution state by using ==event sourcing design pattern==.
Instead of storing current state of orchestration, *Durable Task Framework* uses an append-only store to record series of actions the function orchestration takes.

Behind the scenes, `await` or `yield` in an orchestrator function yields control of orchestrator thread back to *Durable Task Framework* dispatcher.
Dispatcher commits any new actions that orchestrator scheduled, such as calling one more child functions.
Transparent commit action appends to ==execution history== of orchestration instance.
History is stored in a storage table.
Commit action adds messages to a queue to schedule the actual work.
Orchestrator at this point can be unloaded from memory.

When orchestration given more work to do, it wakes up and re-executes the entire function from start to rebuild local state.
If a call to a function, or does any other async work, *Durable Task Framework* consults execution history of current orchestration.
If it finds activity already executed and yielded a result, it replays the function's result and orchestrator continues.
Replay continues until code is finished or until it has scheduled new async work.

## Features & Patterns
There are a number of features and patterns of orchestrator functions.

- `Sub-orchestrations`
	- Orchestrator functions can call activity functions as well as other orchestrator functions
	- Example 1: can build a larger orchestration out of a library of orchestration functions
	- Example 2: run multiple instances of orchestration in parallel
- `Durable timers`
	- Orchestrations can reschedule timers to implement delays
	- Can use them to set up timeout handling on async actions
	- In C#, use durable timers instead of `Thread.Sleep` and `Task.Delay`
	- In JavaScript, use durable timers instead of `setTimeout()` and `setInterval()`
- `External events`
	- Can wait for external events to update an orchestration instance
	- Often useful for handling human interaction or other external callbacks
- `Error handling`
	- Can use error-handling features of the programming language
	- Existing patterns like `try-catch` are supported
- `Critical sections`
	- Instances are single-threaded, so not necessary to worry about race conditions **within** an orchestration
	- Race conditions possible when interacting with external systems
	- Can use a `LockAsync` method to define ==critical sections==
- `Calling HTTP endpoints`
	- Orchestrations aren't permitted to do I/O
	- Typical workaround is to wrap any code that needs I/O in activity function
	- When interacting with external systems, activity functions used to make HTTP calls and return result to orchestration
- `Passing multiple parameters`
	- Can only pass one param at a time to an activity function
	- Use an array or `ValueTuple` if you want to pass multiple params