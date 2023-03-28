#azure #az-204 

Sets are like lists, but each string stored within is unique.
There are two types of sets;
- Unordered
- Sorted/Ordered

#### Unordered Sets
Redis Sets are an unordered collection of strings.
As they are unordered, items exist in the order they are added.

Common commands:
- `SADD` - add one or more members to a set
- `SMEMBERS` - get all members in a set
- `SMOVE` - move a member from one set to another
- `SPOP` - remove and return one or multiple random members from a set

```c
redis:6379> SADD myset "Hello"
(integer) 1
redis:6379> SADD myset "World"
(integer) 2
redis:6379> SADD myset "World"
(integer) 0
redis:6379> SMEMBERS myset
1) "Hello"
2) "World"
```

#### Ordered Sets
Sorted sets are a collection of strings that are sorted based on an associated score.
Sorted sets are great for leader boards, as an example.

Common sorted set commands:
- `ZADD` - adds an element to the set with an associated score
- `ZREM` - removes an element from the set
- `ZRANGE` - returns specified range of elements in the sorted set
- `ZRANK` - returns the rank of a member in the sorted set
- `ZSCORE` - returns the score of member in the sorted set

```c
redis:6379> ZADD myzset 1 "one"
(integer) 1
redis:6379> ZADD myzset 1 "uno"
(integer) 1
redis:6379> ZADD myzset 2 "two" 3 "three"
(integer) 2
redis:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "one"
2) "1"
3) "uno"
4) "1"
5) "two"
6) "2"
7) "three"
8) "3"
```