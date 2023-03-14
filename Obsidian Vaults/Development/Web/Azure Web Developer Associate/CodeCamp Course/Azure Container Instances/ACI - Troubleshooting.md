#azure #az-204 #cli 

You have a few options for troubleshooting container issues.

Can pull the logs with `az container logs`:
```shell
az container logs \
	--resource-group exampro \
	--name prod-web-app
```

Can get diagnostic information during container startup with `az container attach`:
```shell
az container attach \
	--resource-group exampro \
	--name prod-web-app
```

Can have an interactive container with a terminal, which is very useful, using `az container exec`:
```shell
az container exec \
	--resource-group exampro \
	--name my-web-app \
	--exec-command /bin/sh
```

Can get metrics such as CPU usage with `az monitor metrics list`:
```shell
az monitor metrics list \
	--resouce $CONTAINER_ID \
	--metric CPUUsage \
	--output table
```