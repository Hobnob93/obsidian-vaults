#azure #azure-wda 

# Configure Path Mappings
Can use the ==Path Mappings== section to configure handler , virtual application, and directory mappings.
This page will different options depending on the ==OS Type==.

## Uncontainerised Windows Apps
You can customise the IIS handler mappings and virtual applications and directories.
==Handler Mappings== let you add custom script processors to handle requests for specific file extensions.
Select `New handler` to add a new handler as follows:
- `Extension`
	- The file extension you want to handle
- `Script processor`
	- Absolute path of the script processor
	- Requests to files that match the extensions will go via the processor
	- Use path `D:\home\site\wwwroot` to refer to app's root directory
- `Arguments`
	- Optional command-line arguments for the script processor

Each app has the **default root** mapped to `/`.
If your app is deployed to a different folder, or you have more than one application in a repo, you can edit or add virtual applications and directories.
Can specify each virtual directory with its corresponding physical path relative to `D:\home`.
To mark virtual directory as a web application, clear the `Directory` checkbox.

## Linux & Containerised Apps
Can add custom storage for a containerised app.
Containerised apps include all Linux apps as well as Windows and Linux custom containers.
Select `New Azure Storage Mount` to configure custom storage as per the following settings:
- `Name`: the display name
- `Configuration options`: Basic or Advanced
- `Storage accounts`: storage account with the container you want
- `Storage type`: [[Azure Blob Storage]] or [[Azure Files]] - Windows container apps only support *Azure Files*
- `Storage container`: for basic config; the container you want
- `Share name`: for advanced config; the file share name
- `Access key`: for advanced config; the access key
- `Mount path`: absolute path in your container to mount the custom storage