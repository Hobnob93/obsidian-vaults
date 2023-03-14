#azure #az-204 #cli 

Allow you to pass configuration details to your containers.
They can be set via the *Azure Portal*, CLI, or PowerShell.
It's essentially a collection of key-value pairs.

**Secure Environment Variables**
By default, environment variables are stored in plain text.
If you have sensitive data and you need to secure it (such as a secret or key), you can use the `--secure-environment-variables` flag.
```shell
az container create \
	--resource-group aci-resource-group \
	--name aci-demo-secure \
	--image exampro/rails:backend \
	--ip-address Public \
	--location eastus \
	--secure-environment-variables \
	STRIPE_SECRET_KEY=$STRIPE_SECRET_KEY
```