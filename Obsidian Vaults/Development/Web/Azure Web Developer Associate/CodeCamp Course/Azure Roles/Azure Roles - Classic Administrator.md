#azure #az-204 

Classic Administrators is the original role system.
You should use [[Azure Roles - Role-Based Access Control (RBAC)|RBAC]] instead whenever possible.

Classic Administrators have 3 types of roles:
1. **Account Administrator**
	- Billing owner of the subscription
	- Has no access to the Azure Portal
2. **Service Administrator**
	- Same access of a user assigned the "Owner" role at subscription scope
	- Full access to the Azure Portal
3. **Co-Administrator**
	- Same access of a user who is assigned the "Owner" role at the subscription scope