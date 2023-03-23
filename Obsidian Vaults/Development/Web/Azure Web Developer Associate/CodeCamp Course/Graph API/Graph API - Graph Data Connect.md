#azure #az-204 

Microsoft Graph Data Connect augments MS Graph's transactional model with an intelligent way to access rich data at scale.
Uses **Azure Data Factory** to copy MS 365 data to your application's storage at configurable intervals.

![[Graph API - Graph Data Connect Diagram.png]]

MS Graph Data Connect needs to be turned on.
Go to MS 365 Admin Centre under Settings -> Organisation Settings -> Services.
Once turned on, you can access MS 365 data in Azure Data Factory by adding it as a dataset and using it in a pipeline.