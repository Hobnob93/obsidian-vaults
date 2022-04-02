#azure #az-204 

# Explore Azure Blob Storage Client Library
*Azure* .NET client libraries offer a convenient interface for making calls to *Azure Storage*.
It is recommended to use the latest version (12.x) for new applications.

Below are some of the classes in `Azure.Storage.Blobs` namespace and their purpose.
- `BlobClient`
	- Allows for manipulating blobs
- `BlobClientOptions`
	- Provides client config options for connecting to *Azure Blob Storage*
- `BlobContainerClient`
	- Allows you to manipulate containers and their blobs
- `BlobServiceClient`
	- Allows you to manipulate service resources and blob containers
	- Storage account provides top-level namespace for blob service
- `BlobUriBuilder`
	- Provides a convenient way to modify contents of URI instance to point to different *Azure* resources i.e. account, container, or blob