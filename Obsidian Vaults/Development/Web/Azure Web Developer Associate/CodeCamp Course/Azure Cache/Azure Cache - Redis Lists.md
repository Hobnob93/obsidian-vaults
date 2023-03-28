#azure #az-204 

Redis lists are an ordered collection of strings.
Lists do not ensure unique strings, so they can have duplicates.
Lists are referred to by a key.

Common commands for lists:
- `LPOP` - Removes and returns first element in a list
- `RPOP` - Removes and returns last element in a list
- `LPUSH` - Adds a string to the end of a list
- `LPOS` - Returns the index of the provided string
- `LRANGE` - Display list values within the range
	- value of `0 -1` returns all in the list

```c
redis:6379> LPUSH mylist "world"
(integer) 1
redis:6379> LPUSH mylist "hello"
(integer) 2
redis:6379> LRANGE mylist 0 -1
1) "hello"
2) "world"
```