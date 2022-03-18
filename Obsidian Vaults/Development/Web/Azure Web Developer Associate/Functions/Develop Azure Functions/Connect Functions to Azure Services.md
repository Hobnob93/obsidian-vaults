#azure #azure-wda 

# Connect Functions to Azure Services
Reference connection info by name from its config provider.
It does not directly accept connection details.
Allows them to be changed across environments.
You cannot set the connection string directly in `function.json`, instead you set it to the name of an `environment variable` containing the connection string.

The default config provider uses environment variables.
They can be set by [[Configure Application Settings]] when running in *Azure Functions* service.
Can also be set by local settings file when developing locally.

## Connection Values
When connection name resolves, runtime identifies the value as a `connection string`, which typically includes a ==secret==.
Details of connection string defined by service to which you want to connect.

A connection name can also refer to multiple configuration items.
Environment variables can be treated as a collection by using a shared prefix ending in double underscores (`__`).
This group can be referenced by setting connection name to prefix.

## Configure An Identity-Based Connection
Some connections in *Azure Functions* are configured to use identity instead of a secret.
Support depends on extension using the connection.
Sometimes a connection string may still be required, even if the service supports identity-based connections.

When hosted in *Azure Functions* service, identity-based connections use a `managed identity`.
System-assigned identity used by default.
User-assigned identity can be specified with `creditional` and `clientID` properties.
When running locally, your developer identity is used, although this can be customised.

*NOT* supported with [[Implement Azure Durable Functions|Durable Functions]].

## Grant Permission to the Identity
Identity *must* have permissions to perform intended actions.
Typically done by assigning role in *Azure RBAC* or specifying identity in an access policy.
Which you use depends on service you are trying to connect to.