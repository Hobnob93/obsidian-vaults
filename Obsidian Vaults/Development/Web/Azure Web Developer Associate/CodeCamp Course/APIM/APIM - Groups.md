#azure #az-204 

Groups are used to manage the visibility of products to developers.
A user can belong to more than one group.
There are 3 main groups:
- Administrators
- Developers
- Guests

#### Administrators
Manage APIM service instances.
Create the APIs, operations, and products consumed by developers.
Can create custom groups or use external groups in an associated AD tenant to give developers visibility and access to API products.

#### Developers
Authenticated developer portal users
Devs are granted access to portal and build apps that call the operations of an API.

#### Guests
Unauthenticated developer portal users.
May be prospective customers visiting the developer portal.
They can be granted certain read-only access, such as ability to view APIs but not call them.