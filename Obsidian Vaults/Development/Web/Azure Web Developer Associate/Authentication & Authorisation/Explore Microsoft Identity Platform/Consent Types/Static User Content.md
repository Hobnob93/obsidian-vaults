#azure #azure-wda 

# Static User Content
You must specify all permissions in app's configuration in *Azure Portal*.
If user (or admin) has not granted consent for the app, identity platform will prompt user to provide consent at the time.
Enables admins to consent on behalf of all users in organisation.

Some possible problems for developers:
- App needs to request all perms it would ever need upon user's first sign-in
- Can lead to a list of permissions discouraging users from approving app's access
- App needs to know all resources it would ever access ahead of time
- Difficult to create apps that could access an arbitrary number of resources