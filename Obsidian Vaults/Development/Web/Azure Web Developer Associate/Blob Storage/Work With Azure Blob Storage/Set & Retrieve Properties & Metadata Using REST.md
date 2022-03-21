#azure #azure-wda #shell 

# Set & Retrieve Properties & Metadata Using REST
## Metadata Header Format
The format for the header is:
`x-ms-meta-<name>:<string-value>`

## Operations on Metadata
Metadata on a blob or container resource can be set or retrieved directly.
This can be done without returning or altering the content of the resource.

Metadata values can only be read or written in *full*; partial updates are *not* supported.
Setting metadata on resource overwrites any existing metadata values for that resource.

All operations start with the `base-address`:
`https://myaccount.blob.core.windows.net`

## Retrieving Properties & Metadata
The `GET` and `HEAD` operations both retrieve metadata headers for specified container or blob.
These operations return headers *only*.

URI syntax for retrieving metadata on a container is:
`GET/HEAD <base-address>/myContainer?restype=container`
The URI syntax for retrieving metadata headers on a blob is:
`GET/HEAD <base-address>/myContainer/myBlob?comp=metadata`

## Setting Metadata Headers
The `PUT` operation sets metadata headers on specified container or blob.
This will overwrite *any* existing metadata on the resource.
Calling this operation *without* any headers erases all existing metadata on the resource.

The URI syntax for setting metadata headers on container:
`PUT <base-address>/myContainer?comp=metadata&restype=container`
The URI syntax for setting metadata headers for a blob:
`PUT <base-address>/myContainer/myBlob?comp=metadata`

## Standard HTTP Properties for Containers & Blobs
Containers and blobs support certain standard HTTP properties.
Properties and metadata both represented as standard HTTP headers.
Difference between them is the naming of the headers.
Metadata has prefix `x-ms-meta-`.
Property headers use standard HTTP header names, as defined in the HTTP protocol spec.

Standard headers supported on containers:
- `ETag`
- `Last-Modified`

Standard headers supported on blobs:
- `ETag`
- `Last-Modified`
- `Content-Length`
- `Content-Type`
- `Content-MD5`
- `Content-Encoding`
- `Content-Language`
- `Cache-Control`
- `Origin`
- `Range`