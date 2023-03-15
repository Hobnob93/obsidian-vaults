#azure #az-204 

A partition key has two components; a *partition key path* and the associated *partition key value*.
Consider the following object:
```json
{ 
	"userId": "Andrew",
	"worksFor": "Microsoft"
}
```
If you choose `userId` as the partition key, the following are the two partition key components:
1. **Partition key path**: `/userId`
	- Always begins with a slash when being defined
	- Accepts alphanumeric and underscore characters
	- Can also use nested objects/properties by using the standard path notation (/)
2. **Partition key value**: `Andrew`
	- The value must be either a string or numeric type

Your partition key for all containers should be:
- A property that has a value which does **not** change
	- You can't change the value if it's your partition key
- A property that *should* have a wide range of possible values
- Spread **request unit (RU)** consumption and data storage evenly across all logical partitions
	- Ensures even RU consumption and storage distribution across your physical partitions