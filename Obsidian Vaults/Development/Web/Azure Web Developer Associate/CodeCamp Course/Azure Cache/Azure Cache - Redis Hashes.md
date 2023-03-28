#azure #az-204 

Redis hashes represent a mapping between string fields and string values to represent an object.
It is quite similar to JSON in functionality.

Common commands for hashes:
- `HGET` - get the value of a hash field
- `HDEL` - delete one or more hash fields
- `HMSET` - set multiple has fields to multiple values
- `HMGET` - get multiple hash fields from multiple values
- `HVALS` - get all the values
- `HKEY` - get all the fields in a hash

```c
redis:6379> HMSET myhash field1 "Hello" field2 "World"
OK
redis:6379> HGET myhash field1
"Hello"
redis:6379> HGET myhash field2
"World"
```