#azure #az-204 

### Azure Policies
They are used to ensure compliance of a resource.
Evaluates state by examining properties on resources represented in Resource Manager, and properties of some Resource Provider.

Doesn't restrict actions (also called operations).
Ensures that resource state is compliant to your business rules without concern for who made the change or who has permission to make a change.

If the result is a non-compliant resource, even if an individual has access to perform an action, Azure Policy still blocks the create or update.

### Azure Roles
They are used to control access to *just* Azure resources (so not AD).
Focuses managing user actions at different scopes.
Does restrict on Azure resources.

Resources include:
- Virtual Machines
- Databases
- Cloud storage
- Cloud networking

### Azure AD Roles
They are used to control access to *AD* resources.
Resources include:
- Users
- Groups
- Billing
- Licensing
- Application registration
