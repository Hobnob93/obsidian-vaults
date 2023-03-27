#azure #az-204 

The goal of Azure Notification Hub is to send notifications to mobile apps in order to increase app engagement and usage.

You can use tags to filter which apps or users will receive notifications.
Those apps can be registered in Azure Notification Hub in 2 different ways:
1. **Installation Model**
	- App sends installation request to Notification Hub
	- It includes all information needed for the installation to be completed
	- This model is easier to set up and maintain
2. **Registration Model**
	- App sends registration request to Notification Hub
	- Request includes PNS handlers and tags
	- Hub responses with registration ID
	- Native or generic templates can be used in order to define the message