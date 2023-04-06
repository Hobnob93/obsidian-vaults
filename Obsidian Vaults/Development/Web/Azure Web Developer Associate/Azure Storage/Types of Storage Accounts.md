#azure #az-204 #topic #az-tiers 

# Types of Storage Accounts
*Azure Storage* offers two performance levels of storage accounts; `standard` and `premium`.
Each level supports different features and has its own pricing.
- `Standard`
	- General purpose v2 account
	- Recommended for most scenarios
- `Premium`
	- Offers higher performance
	- Uses solid-state drives
	- Can choose between three account types:
		- `Block blobs`
		- `Page blobs`
		- `File shares`

## Standard General Purpose v2
**Supported Storage Services**
	- Blob
	- Queue
	- Table Storage
	- Azure Files

**Usage**
	- Recommended for most scenarios

## Premium Block Blobs
**Supported Storage Services**
	- Blob

**Usage**
	- Premium account for block blobs and append blobs
	- Scenarios with high transaction rates
	- Scenarios using smaller objects
	- Scenarios requiring consistently low storage latency

## Premium page Blobs
**Supported Storage Services**
	- Page Blobs Only

## Premium File Shares
**Supported Storage Services**
	- Azure Files only