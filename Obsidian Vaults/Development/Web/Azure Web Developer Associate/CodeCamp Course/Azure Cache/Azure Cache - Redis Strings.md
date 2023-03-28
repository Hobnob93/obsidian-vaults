#azure #az-204 

Redis strings are the most basic value.
They can have a max value of 512 MB.
Strings are binary-safe, so they contain data such as:
- JPEG image
- Serialised objects

Atomic counters can be applied to strings that represent a number:
- `INCR` - add 1
- `DECR` - subtract 1
- `INCBY` - change by a certain amount

Some other string commands:
- `GET` - Get a string by its key
- `SET` - Set a string for a key
- `APPEND` - Add additional text to end of a string
- `EXISTS` - Check if string exists for a given key

```c
redis:6379> GET nonexisting
(nil)
redis:6379> SET mykey "10"
OK
redis:6379> GET mykey
"10"
redis:6379> INCR mykey
(integer) 11
redis:6379> GET mykey
"11"
```