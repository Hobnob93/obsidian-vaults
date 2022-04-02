#azure #az-204

# Query Microsoft Graph Using REST
*MS Graph* is a RESTful API enabling access to *MS Cloud* resources.
Can make requests with an auth token combined with a registered app.

API defines most of its resources, methods, and enumerations in the *OData* namespace, `microsoft.graph`, in the [metadata](https://docs.microsoft.com/en-us/graph/traverse-the-graph).
Small number of API sets defined in sub-namespaces, such as [call records API](https://docs.microsoft.com/en-us/graph/api/resources/callrecords-api-overview) defining resources like [callRecord](https://docs.microsoft.com/en-us/graph/api/resources/callrecords-callrecord) in `microsoft.graph.callRecords`.

Assume types, methods, and enumerations part of `microsoft.graph` namespace, unless specified otherwise.

## Call a REST API Method
To read/write from/to a resource such as email message, you construct a request such as the following:
```http
{HTTP Method} https://graph.microsoft.com/{version}/{resource}/?{query-params}
```

Components of a request include:
- `HTTP Method`: method used on request to *MS Graph*
- `version`: version of *MS Graph* API app is using
- `resource`: resource in *MS Graph* you're referencing
- `query-params`: optional *OData* or REST method params customising response

A response returned includes:
- **Status code**: HTTP status code indicating success or failure
- **Response message**: data requested or result of operation
	- response message can be empty for some operations
- **`nextLink`**: if request returns lots of data, it might be paginated
	- next page can be received by following this link

## HTTP Methods
[[HTTP Methods]]

- For CRUD methods `GET` and `DELETE`, no request body returned.
- `POST`, `PATCH`, and `PUT` methods require request body, usually in JSON format, containing additional info, such as values for properties of resource.

## Version
*MS Graph* currently supports two versions:
- `v1.0`
	- includes generally available APIs
	- use for all production apps
- `beta`
	- includes APIs currently in preview
	- may contain breaking changes
	- recommended to only use to test apps in development

## Resource
Can be an entity or complex type.
Commonly defined with properties.
Entities different from complex types by always including an `id` property.

URL will include resource interacting with, such as:
- **me**
- **user**
- **group**
- **drive**
- **site**

Top-level resources may include *relationships* to access additional resources, such as `me/messages` or `me/drive`.
Can also interact using *methods*, such as `me/sendMail` to send an email.

## Query Parameters
Can be *OData* system query options.
Can be strings a method accepts to customise response.

Can use *OData* query options to include fewer properties than default response, filter response items based on a query, or provide additional parameters for a method.

E.g. the following filter restricts messages returned:
```http
GET https://graph.microsoft.com/v1.0/me/messages?filter=emailAddress eq 'jon@contoso.com'
```

## Additional Resources
[Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)
[Postman](https://www.getpostman.com/)