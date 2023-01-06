#azure #az-204 

## Keys
Serve as the name of the key-value pair.
Used to store and retrieve a corresponding value.
Common practise to organise keys into hierarchical namespace by using a character delimiter, such as `/` or `:`.
App Config treats keys as a whole.
- It doesn't parse to work out structure or enforce any rule on them
Keys stored are ==case sensitive== and need to be ==unicode-based==.

Can use any unicode character, except for `*` `,` `\` as they are reserved.
If you need these characters, you need to escape it using `\`.
A combined size limit of 10,000 characters on a key-value pair (includes *both* key *and* value, as well as any associated optional attributes).

## Design Key Namespaces
Two general approaches for naming keys in config; __flat__ or __hierarchical__.
From an app standpoint, it makes little difference, but hierarchical has human benefits such as being able to read and finding a setting for a specific app more easily.

Some examples:
```
AppName:Service1:ApiEndpoint
AppName:Service2:ApiEndpoint

AppName:Region1:DbEndpoint
AppName:Region2:DbEndpoint
```

## Label Keys
Keys can optionally have a label attribute.
Used to differentiate key values with the same key.
By default, a label is empty or `null`.

Labels create a convenient way to create variants of a key:
```
Key = AppName:DbEndpoint & Label = Test
Key = AppName:DbEndpoint & Label = Staging
Key = AppName:DbEndpoint & Label = Production
```

## Version Key Values
App Config doesn't version key values automatically as they are modified.
Use labels as a way to create multiple versions of a key value.
Example; you can use git commit IDs as the label to identify key values associated with a particular software build.

## Query Key Values
Each key value is identified by its key plus label.
Query an App Config store for key values by specifying a pattern.
App Config store returns all key values that match the pattern, along with their values and attributes.

## Values
Values assigned to keys are also unicode strings.
Can use all unicode characters for values.
Optionally, there is user-defined content type associated with each value.
- Can be used to store information, such as encoding scheme, or any other info that helps the app process it properly

All values are encrypted at rest as well as in transit.
It isn't a replacement for Azure Key Vault, so ==do not store secrets in it==.