#azure #az-204

# Explore Partitioning
Items in container are divided into distinct subsets.
Subsets are called ==logical partitions==.
They are formed based on the value of a `partition key`, associated with each container.
All items in a logical partition have the same partition key value.

As an example; if a container contains 1,000 items with unique `UserID` values, and `UserID` servers as the partition key, then there will be 1,000 logical partitions in the container.

In addition to `partition key`, each item in a container has an `ItemID` which is unique within a logical partition.
Combining `partition key` and `ItemID` forms item's index, uniquely identifying the item.
Choosing a partition key is important as it will affect app's performance.

## Logical Partitions
Consists of a set of items containing the same partition key value.
Another example would be to use `FoodGroup` as a partition key; then food items that share the same group (such as `Beef`, `Poultry`, or `Fish`) will be within the same logical partition.

Partition defines the scope of database transactions.
Can update items within logical partition using ==transaction== with ==snapshot isolation==.
When new items added, new logic al partitions transparently created by system.
Partition deleted when all underlying data is deleted.

## Physical Partitions
Container is scaled by distributing data and throughput across physical partitions.
Internally, one or more logical partitions are mapped to a single physical partition.
Smaller containers tend to have many logical partitions, but only require a single physical partition.
Physical partitions are an internal implementation of system and entirely managed by *Azure Cosmos DB*.

 Number of physical partitions in container depends on following:
 - Number of throughput provisioned
	 - Each physical partition can provide throughput of 10,000 request units per second
	 - This implies logical partitions also have a throughput limit of 10,000 request units per second
 - Total data storage
	 - Each physical partition can store up to 50GB of data

Throughput provisioned for container divided evenly among physical partitions.
A partition key that doesn't distribute requests evenly might result in too many requests directed to a small subset of partitions.
These subsets can become "hot", leading to inefficient use of provisioned throughput.
This might result in rate-limiting and higher costs.