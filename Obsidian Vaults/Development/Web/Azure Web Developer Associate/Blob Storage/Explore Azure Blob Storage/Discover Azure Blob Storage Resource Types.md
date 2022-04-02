#azure #az-204 

# Discover Azure Blob Storage Resource Types
Blob storage offers three types of resources:
1. The [[#Storage Accounts|storage account]]
2. A [[#Containers|container]] in the storage account
3. A [[#Blobs|blob]] in the container

## Storage Accounts
Provides a unique namespace in *Azure* for your data.
Every object stored has an address that includes unique account name.
Combination of account name and blob endpoint forms base address for objects.

For example, the default endpoint for blob storage is:
```
http://mystorageaccount.blob.core.windows.net
```

## Containers
Organises a set of blobs, similar to a directory in a file system.
A storage account can have unlimited number of containers.
Container can store an unlimited number of blobs.
Container name *must* be lowercase.

## Blobs
*Azure Storage* supports three types of blobs:
1. `Block blobs`
	- Store text and binary data
	- Up to 4.7TB
	- Made up of blocks of data that can be managed individually
2. `Append blobs`
	- Made up of blocks
	- Optimised for append operations
	- Ideal for scenarios such as logging data from virtual machines
3. `Page blobs`
	- Random access files
	- Up to 8TB
	- Store Virtual Hard Drive (VHD) files
	- Serve as disks for *Azure* VMs