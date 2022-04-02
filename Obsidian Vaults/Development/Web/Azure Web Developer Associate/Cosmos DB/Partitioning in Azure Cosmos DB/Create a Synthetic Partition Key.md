#azure #az-204 

# Create A Synthetic Partition Key
Best practise to have a key with many distinct values.
Goal is to distribute data and workload evenly across items associated with partition key values.
If such a property doesn't exist in your data, can construct a ==synthetic partition key==.

## Concatenate Multiple Properties of an Item
Can form a key by concatenating multiple properties.
Creates an artificial `partitionKey` property.
Consider the following document:
```json
{
	"deviceId": "abc-123",
	"date": 2018
}
```
Could use either of those properties as key, OR concatenate to create a synthetic `partitionKey`:
```json
{
	"deviceId": "abc-123",
	"date": 2018,
	"partitionKey": "abc-123-2018"
}
```
Can define ==client-side logic== to add synthetic key into items in containers.

## Use a Partition Key With Random Suffix
Another possible strategy is to append a random number at start of partition key value.
Allows for parallel write operations across partitions.

An example is if a date is used as a partition key.
Might choose a number between 1 and 400 and concatenate as suffix to the date.
This might create a key such as `2018-08-09.1`.
Due to randomised partition key, write operations on container on each day are spread evenly across multiple partitions.
Results in better parallelism and overall higher throughput

## Use a Partition Key with Pre-Calculated Suffixes
Random suffix makes it hard to read an item.
You also don't know the suffix value used when you wrote the item.
Can use pre-calculated suffixes instead; usually based on something you want to query.

An example would be calculating a hash on something like a `vehicle-identification-number`, and appending that to the partition key, such as the date mentioned previously.
This might generate a number between 1 and 400 as before, but it can be determined.
The determinism allows you to workout the full partition key or a particular item.