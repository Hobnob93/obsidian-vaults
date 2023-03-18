#azure #az-204 

Groups lets the resource owner (or Azure AD directory owner) assign a set of access permissions to all members of a group.
This is instead of having to apply the same rights one-by-one.
Groups contain:
- **Owners**
	- Permissions to add and remove members
- **Members**
	- Permissions to do various things within AD

**Assignment**
Can assign roles directly to a group.
Can assign applications directly to a group.

**Request to Join Groups**
Group owner can let users find their groups so they can request to join.
Removes need for group owner to find and add them one-by-one.
Group can be set to automatically accept users that try to join, or can set it so all new requests require approval.