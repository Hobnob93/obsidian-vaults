#azure #az-204 #xml 

#### Convert JSON to/from XML
Converts request or response body from/to JSON to/from XML.
```xml
<outbound>
	<xml-to-json kind="direct" apply="always" consider-accept-header="false" />
</outbound>
```

#### Find & Replace String in Body
Finds a request or response substring and replaces it with a different substring.

#### Mask URLs in Content
Rewrites links in the response body so they point to the equivalent link via the gateway.

#### Set Backend Service
Changes the backend service for an incoming request.

#### Set Body
Sets message body for incoming and outgoing requests.

#### Set HTTP Header
Assigns a value to an existing response or request header.
Or adds a new response or request header.
```xml
<set-header name="<header-name>" exists-action="override">
	<value>20</value>
</set-header>
```

#### Set Query String Parameter
Adds, replaces value of, or deletes request string parameter.

#### Rewrite URL
Converts a request URL from its public form to the form expected by the web service.

#### Transform XML using an XSLT
Applies an XSL transformation to XML in the request or response body.