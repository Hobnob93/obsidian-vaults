#azure #az-204 

Unique keys provide developers with the ability to add a layer of **data integrity** to their database.
You can create a unique key policy when creating a container.
Ensures uniqueness of one or more values per partition key.

A unique key is scoped to a logical partition.
- If you partition the container based on the ZIP code, you end up with duplicated items in each logical partition

You can't update an existing container to use a different unique key.

A unique key policy can have a maximum of 16 path values.
Each unique key policy can have a maximum of 10 unique key constraints or combination.
When a container has a unique key policy, Request Unit (RU) charges to create, update, and delete an item are slightly higher,
Unique key names are case-sensitive.