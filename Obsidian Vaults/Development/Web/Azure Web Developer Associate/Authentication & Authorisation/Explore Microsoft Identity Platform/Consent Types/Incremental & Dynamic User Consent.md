#azure #azure-wda 

# Incremental & Dynamic User Consent
Using identity platform endpoint, you can ignore static permissions defined in app registration.
Can request permissions incrementally instead.
Can ask for a minimum set of permissions upfront, and request more as the customer uses additional app features.

Can specify scopes app needs at any time by including new scopes in `scope` parameter when requesting access token.
No need to pre-define them in app registration information.
If user hasn't consented to a new scope yet, they'll be prompted to do so.
Only applies to delegate permissions and not to application permissions.