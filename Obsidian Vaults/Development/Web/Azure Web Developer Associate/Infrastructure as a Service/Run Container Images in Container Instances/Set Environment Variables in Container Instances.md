#azure #az-204#shell #json 

# Set Environment Variables in Container Instances
Setting environment variables in container allows for dynamic configuration of app or script the container runs.
To pass secrets, *ACI* supports secure values for both Windows and Linux containers.
An example of passing variables to the container:
```shell
az container create --resource-group <resource-group> --name <container-name>
	--image <container-image> --restart-policy <policy>
	--environment-variables 'NumWords'='5' 'MinLength'='8'
```

## Secure Values
Intended to hold sensitive information, suck as keys or passwords.
Using secure values for environment variables is safer and more flexible than including in container image.

They aren't visible in container properties.
Can only be accessed from within the container.
When viewed in *Azure Portal* or *Azure CLI*, only variable's name is shown, and not value itself.

Set a secure environment variable by specifying `secureValue` property instead of regular `value` for variable's property.
This is done when defining the image file.