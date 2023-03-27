#azure #az-204 

When an app wants to receive a notification, it contacts the PNS for the target platform it's running on and requests a unique and temporary push handle.
The handle type depends on the system (e.g. WNS uses URIs, while APNS uses tokens).

The client app stores this handle in the app backend or provider.

The app backend contacts the PNS using the handle to target a specific client app to send a push notification.

The notification is sent to the device specified by the handle by the PNS.