#azure #az-204 

A Function as a Service ([[Function As A Service (FaaS)|FaaS]]).
Allows devs to focus on writing code.
Not have top worry about maintaining underlying computing infrastructure.

A Function App defined underlying compute for a collection of functions.
A Function App defines hosting, runtime, and other global configs.
![[Azure Function Overview Diagram.png]]

Functions themselves represents code along with app runtime configuration.
A trigger is chosen event data causing trigger to execute.
- Can only have *one* trigger
Input bindings are one or more data sources passed to function when trigger occurs.
Output bindings are one or more data sinks/consumers that will receive output data from function on successful execution.