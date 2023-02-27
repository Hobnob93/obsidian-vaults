#azure #az-204 

Lets you avoid hardcoding access to other services.
Abstracts away boilerplate code keeping functions lean.

![[Azure Function Overview Diagram.png]]

**What is a Trigger?**
A trigger is a specific type of event which causes the function run.
A function *must* have *one* trigger.
Defines how a function is invoked.
Triggers have associated data often provided as payload to the function.

**What is a Binding?**
Define if your function is connected to another service.
Can be input or output.
Data from bindings is provided to the function as parameters.
They are optional, and there can be multiple input and/or output bindings.