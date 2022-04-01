#azure #azure-wda 

# Choose When to Use Shared Access Signatures
Use SAS when you want secured access to resources in storage account to any client who does not otherwise have permissions to those resources.

Common scenario is a service where users read and write their own data to your storage account.
In scenario where storage account stores user data, there are two typical design patterns.

## Front End Proxy Service
Clients upload and download data via front-end proxy service.
This service performs authentication.
Has advantage of allowing validation of business rules.
Although, scaling for large amounts of data or high volume can be difficult and expensive.
![[Front End Proxy Service Diagram.png]]

## SAS Provider Service
A lightweight service authenticates client as needed and generates an SAS.
Once client app receives SAS, they can access storage resources directly with perms defined by SAS, and for duration allowed.
Mitigates need for routing all data through front end proxy service.
![[SAS Provider Service Diagram.png]]

## Conclusion
Many real-world services use hybrid of the two approaches.
Additionally, SAS is required to authorise access to source object in copy operation in certain scenarios:
- When blob copied to another blob residing in different storage account
- Copying a file to another file in a different storage account
- Copy a blob to file or vice versa, even if in same account