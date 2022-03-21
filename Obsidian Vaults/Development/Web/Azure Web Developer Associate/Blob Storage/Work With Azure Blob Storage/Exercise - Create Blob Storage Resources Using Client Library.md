#azure #azure-wda #exercise #shell #csharp 

# Exercise - Create Blob Storage Resources Using Client Library
## Prerequisites
- An *Azure*  account with active subscription
- An IDE
- Azure CLI
- .NET Core 3.1 or 5.0

## Setting Up
Perform the following actions to prepare *Azure* and local environment:
1. Open VS Code and its ==Terminal== window
2. Log in to *Azure*
```shell
az login
```
3. Create a resource group
```shell
az group create --location <my-loc> --name <resource-group>
```
4. Create storage account
```shell
az storage account create --resource-group <resource-group> --name 
	<storage-acct-name> --location <my-loc> --sku Standard_LRS
```
5. Get credentials for the storage account
	1. Navigate to *Azure Portal*
	2. Locate storage account created
	3. Select `Access keys` in ==Security + networking==
	4. Find ==Connection string== value under `key1` and copy the string - keep it safe as will need it later

## Prepare .NET Project
Here we will create the project and install the *Azure Blob Storage* client library.
1. Using the terminal in VS Code in directory you want to create the project, create a new project and build it
```shell
dotnet new console -n <project-name>
cd <project-name>
dotnet build
```
2. Create another folder called *data* - this is where blob data files will be created and stored
```shell
mkdir data
```
3. While in app directory, install client library
```shell
dotnet add package Azure.Storage.Blobs
```
4. Add the following code to `Program.cs`
```cs
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;
using System;
using System.IO;
using System.Threading.Tasks;

namespace project_name;

class Program
{
	public static void Main()
	{
		Console.WriteLine("Azure Blob Storage exercise\n");

		// Run the examples asynchronously, wait for results before proceeding
		PrcoessAsync().GetAwaiter().GetResult();

		Console.WriteLine("Press enter to exit the same app");
		Console.ReadLine();
	}

	private static async Task ProcessAsync()
	{
		// Copy connection string from portal in variable below
		var storageConnString = "CONN_STRING";

		// Create a client that can auth with a conn string
		var blobServiceClient = new BlobServiceClient(storageConnString);

		// Example code would start below here
	}
}
```
5. Set the `storageConnString` to variable copied from Portal earlier

## Build The Full App
For each example below, **append** the snippet to the previous snippet under "Example code".

### Create A Container
Use the instance of `BlobServiceClient` to create a blob container in the storage account.
GUID value appended to ensure name is unique as the create method will fail if the container already exists.
```cs
// Create a unique name for container
var containerName = "wtBlob" + Guid.NewGuid().ToString();

// Create container and return client object
var containerClient = await
	blobServiceClient.CreateBlobContainerAsync(containerName);
	
Console.WriteLine("A container named '" + containerName + "' has been created. " +
				  "\nTake a minute and verify in the portal." + 
				  "\nNext a file will be created and uploaded to the container."); Console.WriteLine("Press 'Enter' to continue.");
Console.ReadLine();
```

### Upload Blobs to a Container
Get a reference to `BlobClient` from the previously created container.
It will then asynchronously upload the blob, creating it if it doesn't exist or overwriting it if it does.
```cs
// Create a local file in data directory for uploading and downloading
var localPath = "./data/";
var fileName = "wtfile" + Guid.NewGuid().ToString() + ".txt";
var localFilePath = Path.Combine(localPath, fileName);

// Write text to the file
await File.WriteAllTextAsync(localFilePath, "Hello, World!");

// Get reference to the blob
var blobClient = containerClient.GetBlobClient(fileName);

Console.WriteLine("Uploading to Blob storage as blob:\n\t {0}\n", blobClient.Uri);

// Open file and upload its data
using FileStream uploadFileStream = File.OpenRead(localFilePath);
await blobClient.UploadAsync(uploadFileStream, true);
uploadFileStream.Close();

Console.WriteLine("\nThe file was uploaded. We'll verify by listing" + 
				  " the blobs next.");
Console.WriteLine("Press 'Enter' to continue.");
Console.ReadLine();
```

### List Blobs in a Container
In this case, just the one blob uploaded so only that one will be returned.
```cs
// List blobs in container
Console.WriteLine("Listing blobs...");
await foreach (BlobItem blobItem in containerClient.GetBlobsAsync())
{
	Console.WriteLine("\t" + blobItem);
}

Console.WriteLine("\nYou can also verify by looking inside the " + 
				  "container in the portal." + 
				  "\nNext the blob will be downloaded with an altered file name.");
Console.WriteLine("Press 'Enter' to continue.");
Console.ReadLine();
```

### Download Blobs
In the sample code, we'll add the "DOWNLOADED" suffix to the blob name so it can be identified.
```cs
var downloadFilePath = localFilePath.Replace(".txt", "DOWNLOADED.txt");

Console.WriteLine("\nDownloading blob to\n\t{0}\n", downloadFilePath);

// Download blob's contents and save it to file
BlobDownloadInfo download = await blobClient.DownloadAsync();

using (FileStream downloadFileStream = File.OpenWrite(downloadFilePath))
{
	await download.Content.CopyToAsync(downloadFileStream);
	downloadFileStream.Close();
}

Console.WriteLine("\nLocate the local file to verify it was downloaded."); Console.WriteLine("The next step is to delete the container and local files."); Console.WriteLine("Press 'Enter' to continue.");
Console.ReadLine();
```

### Delete A Container
Cleans up resources app ahs created by deleting entire container.
It also deletes local files created by the app.
```cs
// Delete the container and clean up local files created
Console.WriteLine("\n\nDeleting blob container...");
await containerClient.DeleteAsync();

Console.WriteLine("Deleting the local source and downloaded files...");
File.Delete(localFilePath);
File.Delete(downloadFilePath);

Console.WriteLine("Finished cleaning up.");
```

## Clean Up Other Resources
App deleted resources created.
Can delete everything from this exerciseusing the command below:
```shell
az group delete --name <resource-group> --no-wait
```