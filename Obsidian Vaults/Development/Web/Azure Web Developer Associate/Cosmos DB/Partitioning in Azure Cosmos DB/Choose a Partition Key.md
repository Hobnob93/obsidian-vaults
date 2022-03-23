#azure #azure-wda 

# Choose A Partition Key
A partition key has two components; `partition key path` and `partition key value`.
Consider the following item:
```json
{
	"userId": "Andrew",
	"worksFor": "Microsoft"
}
```
If choosing `userId` as partition key, the following are the two partition key components:
- `partition key path`: "/userId" - accepts alphanumeric and underscore characters, as well as supporting path (/) notation should you want a nested object value
- `partition key value`: "Andrew" - can be string or numeric types

Once selected partition key, it is not possible to change ==in-place==.
Need to move data to a new container in order to change the key.

For *all* containers, partition key *should*:
- Be a property whose value will not change
- Have a high cardinality; wide range of possible values
- Spread data consumption and storage across logical partitions

## Partition Keys for Read-Heavy Containers
Might consider using a partition key that is frequently used as a filter for queries.
This will efficiently route the queries, as partition key used in query predicate.

If container is small, probably not enough physical partitions to worry about performance impact of cross-partition queries.
If container could grow to more than a few physical partitions, pick a key that minimises cross-partition queries.

## Using Item ID as Partition Key
Property with wide range of possible values likely a great partition key choice.
One example is the `ItemID`; suitable for small read-heavy containers or write-heavy containers of any size.

System property `ItemID` exists in every item in container.
Properties representing your own logical unique identifier can also be a great choice.
Item IDs make a great key because:
- Wide range of possible values
- Can uniquely identify an item; evenly balances RU consumption and data storage
- Efficient point reads

Things to consider when using `ItemID` as key:
- It will become unique identifier throughout entire container
	- Won't be able to have items with duplicate IDs
- A read-heavy container with a lot of [[Explore Partitions#Physical Partitions|physical partitions]] will be more efficient if an equality filter is used as a key instead
- Can't run stored procedures or triggers across multiple logical partitions