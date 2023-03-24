#azure #az-204 

Azure Front Door rules engine allows you to customise how HTTP requests get handled at the edge and provides a more controlled behaviour to your web application.

![[Front Door - Rules Engine.png]]

There are many things that can be customised within rules.
Conditions:
- Device type
- HTTP version
- Request cookies
- Post args
- Query string
- Remote address
- Request body
- Request file name
- Request file extension
- Request header
- Request method
- Request path
- Request protocol
- Request URL

Operators:
- Equal /not
- Contains /not
- Less than /equal to /not
- Greater than /equal to /not
- Begins/ends with /not
- RegEx /not

Action:
- Cache expiration
- Cache behaviour
	- bypass, override, set if missing
- Cache key query string
	- include, cache every unique URL, exclude, ignore query string
- Modify request header / modify response header
	- append, overwrite, delete
- URL redirect
	- type: Found (302), Moved (301), Temporary redirect (307), Permanent redirect (308)
	- protocol: match request, HTTP, HTTPS
- URL rewrite
	- source pattern
	- destination
- Origin group override