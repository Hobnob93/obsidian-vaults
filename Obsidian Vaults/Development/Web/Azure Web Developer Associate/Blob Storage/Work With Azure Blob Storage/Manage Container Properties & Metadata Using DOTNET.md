#azure #azure-wda #csharp 

# Manage Container Properties & Metadata Using .NET
Blob containers support system properties and user-defined metadata
- **System Properties**
	- Exist on each blob storage resource
	- Some can be read or set
	- Others are read-only
	- Some correspond to certain standard HTTP headers
	- The [[Explore Azure Blob Storage Client Library|Client Library]] maintains these properties for you
- **User-Defined Metadata**
	- Consists of one or more name-value pairs
	- Can specify for each blob resource
	- Used to store additional data with each resource
	- They are for custom purposes only
	- Does *not* affect resource behaviour
	- They are valid HTTP headers to should adhere to all restrictions given this

## Retrieve Container Properties
To do this you can call one of the following methods of the `BlobContainerClient` class:
- `GetProperties`
- `GetPropertiesAsync`

Following code example fetches container's system properties and writes them to a console window:
```cs
private static async Task ReadContainerPropertiesAsync(
	BlobContainerClient container)
{
	try
	{
		var properties = await container.GetPropertiesAsync();
		Console.WriteLine($"Properties for container {container.Uri}");
		Console.WriteLine($"Public access level: {properties.Value.PublicAccess}");
		Console.WriteLine($"Last modified time in UTC " +
			"{properties.Value.LastModified}");
	}
	catch (RequestFailedException ex)
	{
		Console.WriteLine($"HTTP error code {ex.Status}: {ex.ErrorCode}");
		Console.WriteLine(ex.Message);
		Console.ReadLine();
	}
}
```

## Set Metadata
To set metadata, add name-value pairs to an `IDictionary` object.
Then call one of the following methods on `BlobContainerClient` to write the values:
- `SetMetadata`
- `SetMetadataAsync`

Name of metadata must conform to naming conventions of C# identifiers.
Preserves the case in which they are created but are ==case-insensitive== when set or read.
If same name used twice, the values become comma-separated and concatenated.

The following example sets metadata on a container.
```cs
public static async Task AddContainerMetadataAsync(
	BlobContainerClient container)
{
	try
	{
		var metadata = new Dictionary<string, string>();

		metadata.Add("docType", "textDocument");
		metadata.Add("category", "guidance");

		await container.SetMetadataAsync(metadata);
	}
	catch (RequestFailedException ex)
	{
		Console.WriteLine($"HTTP error code {ex.Status}: {ex.ErrorCode}");
		Console.WriteLine(ex.Message);
		Console.ReadLine();
	}
}
```

## Retrieve Metadata
The `GetProperties` and `GetPropertiesAsync` methods are used to retrieve metadata in addition to system properties.
```cs
public static async Task ReadContainerMetadataAsync(
	BlobContainerClient container)
{
	try
	{
		var properties = await container.GetPropertiesAsync();
		
		// Enumerate the container's metadata.
		Console.WriteLine("Container metadata:");
		foreach (var metadataItem in properties.Value.Metadata)
		{
			Console.WriteLine($"\tKey: {metadataItem.Key}");
			Console.WriteLine($"\tValue: {metadataItem.Value}");
		}
	}
	catch (RequestFailedException ex)
	{
		Console.WriteLine($"HTTP error code {ex.Status}: {ex.ErrorCode}");
		Console.WriteLine(ex.Message);
		Console.ReadLine();
	}
}
```