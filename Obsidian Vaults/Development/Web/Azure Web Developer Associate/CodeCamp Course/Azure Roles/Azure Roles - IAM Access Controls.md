#azure #az-204 

**Identity Access Management (IAM)** allows you to create and assign roles to users.

##### Azure Roles (RBAC)
Roles restrict access to resource actions (a.k.a. operations).
There are two types of roles:
- **Built in role**
	- Managed Microsoft roles are read-only pre-created roles for you to use
		- Owner
		- Contributor
		- Reader
		- AcrDelete
		- AcrImageSigner
		- AcrPush
- **Custom role**
	- A role created by you with your own custom logic

##### Role Assignment
This is when you apply a role to a:
- service principle
- user
- group of users

##### Deny Assignments
Block users from performing specific actions.
Overrides role assignments that may grant them access otherwise.
Only way to deny assignments is through **Azure Blueprints**.