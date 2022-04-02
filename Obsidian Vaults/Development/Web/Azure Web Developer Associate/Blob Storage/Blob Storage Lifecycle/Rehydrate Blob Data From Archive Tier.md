#azure #az-204

# Rehydrate Blob Data From Archive Tier
While blob is in `archive` tier, it is considered ==offline== and *cannot* be read or modified.
In order to do this, you must first ==rehydrate== to either `hot` or `cool` [[Access Tiers for Block Blob Data|tier]].
There are two options for rehydrating:
- **Copy archived blob to online tier**
	- Copies it to a new blob in destination tier
	- There is a [Copy blob](https://docs.microsoft.com/en-us/rest/api/storageservices/copy-blob) or [Copy blob from URL](https://docs.microsoft.com/en-us/rest/api/storageservices/copy-blob-from-url) operation
	- This is recommended for most scenarios
- **Change blob's tier to online tier**
	- Change a blob's tier using the [Set Blob Tier](https://docs.microsoft.com/en-us/rest/api/storageservices/set-blob-tier) operation

Rehydrating can take several hours to complete.
Rehydrate larger blobs for optimal performance, as rehydrating several smaller blobs may require additional time.

## Rehydration Priority
Can set priority for rehydration via optional `x-ms-rehydrate-priority` header on a "Set Blob Tier" or "Copy From URL" operation.
Priority options include:
- **Standard priority**
	- Request will process in order it was received
	- May take up to 15 hours
- **High priority**
	- Prioritised over standard priority
	- May complete in under an hour for objects under 10GB in size

You can call [Get Blob Properties](https://docs.microsoft.com/en-us/rest/api/storageservices/get-blob-properties) to find rehydration priority in `x-ms-rehydrate-priority` header.
It will return either `Standard` or `High`.

## Copy Archived Blob to Online Tier
When copying, source blob remains unmodified in the archive tier.
Must copy archived blob to a new blob with different name or to a different container.
You *cannot* overwrite source blob by copying to same blob.

Can only copy within the same storage account.
Cannot copy archived blob to a destination blob that is also in the archive tier.

Table below shows behaviour of copying a blob based on the tier of the source and destination.

|                     | Hot Source | Cool Source | Archive Source            |
| ------------------- | ---------- | ----------- | ------------------------- |
| Hot Destination     | Supported  | Supported   | Supported in same account |
| Cool Destination    | Supported  | Supported   | Supported in same account |
| Archive Destination | Supported  | Supported   | Not Supported             |

## Change Blob's Tier to Online Tier
With this operation, can change tier of archived blob to either hot or cool.

Once request initiated it *cannot* be cancelled.
Will continue to show as archived until process is completed.