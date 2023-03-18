#azure #az-204 

In some cases you'll need to set up your own domain controller(s).
When doing a *lift-and-shift* from *on-premise* to *Microsoft Azure* and migrating Active Directory, Azure AD does **not** support some domain services.

Azure Active Directory Domain Services (AD DS) provides managed domain services such as:
- Domain joins
- Group policies
- Lightweight directory access protocol (LDAP)
- Kerberos / NTLM authentication

You can use these domain services without the need to deploy, manage or patch domain controllers in the cloud.