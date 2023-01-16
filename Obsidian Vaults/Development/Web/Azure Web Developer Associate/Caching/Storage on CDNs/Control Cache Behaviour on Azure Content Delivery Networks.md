#azure #az-204 #cli 

## Overview
As cached resources can potentially be out of date or stale, it is important for caching to control when content is refreshed.
To save timer and bandwidth, a cached resource is not compared to version on origin server every time it is accessed.
Instead, cached resource is assumed to be fresh, and cached version is always sent to client.
A cached resource is considered fresh when its age is then age or period defined by a cache setting.

## Controlling Caching Behaviour
Azure CDNs provide two mechanisms for caching files.
These config settings depend on the tier you've selected.
Caching rules in Azure CDN Standard for Microsoft are set at endpoint level and provide three options.
Other tiers provide additional config options, including:
- __Caching rules__
	- Can be global (apply to all content from endpoint) or custom
	- Custom rules apply to specific paths and file extensions
- __Query string caching__
	- Enables you to configure how CDN responds to a query string
	- Has no effect on files that can't be cached

With Azure CDN Standard for Microsoft, caching rules are as simple as the three options:
- __Ignore query strings__
	- This option is default
	- CDN POP simply passes request and any query strings directly to origin server on first request and caches the asset
	- New requests for same asset will ignore any query strings until TTL expires
- __Bypass caching for query strings__
	- Each query request from client is passed directly to origin server with no caching
- __Cache every unique URL__
	- Every time a requesting client generates a unique URL, that URL is passed back to origin server
	- Response cached with own TTL
	- Inefficient where each request is a unique UYL, as cache-hit ratio becomes low

To change these settings, in the Endpoint pane, select `Caching rules` then select the caching option you want to apply.

## Caching And Time To Live
Files on site are cached until their TTL expires.
Cache-Control header contained in HTTP response from origin server determines TTL duration.
If you don't set a TTL for a file, default is used.
Default may be overridden if you have set up caching rules.
Default TTL values are as follows:
- Generalised web delivery optimisations: 7 days
- Large file optimisations: 1 day
- Media streaming optimisations: 1 year

## Content Updating
An Azure CDN edge node will server an asset until its TTL expires.
Edge node reconnects to origin server when TTL expires and client makes request to the same asset.
Node will fetch another copy of asset, refreshing the TTL.

To ensure users always receive latest version of an asset, consider including version string in asset URL.
This approach causes CDN to retrieve new asset immediately.

Alternatively, you can purge cached content from edge nodes, which refreshes content on next client request.
You might purge cached content when publishing new version of a web app or to replace any out of date assets.

Can purge content in several ways:
- On an endpoint basis
- All endpoints simultaneously
- Specify a file, by using an asset path or all assets on selected endpoint
- Based on wildcards or using the root

Azure CLI provides a special purge verb that will unpublish cached assets from an endpoint.
Useful if you have an app scenario where a large amount of data is invalidated and should be updated in the cache.
To unpublish, you must specify a file path, a wildcard directory, or both.
```shell
az cdn endpoint purge --content-paths '/css/*' '/js/app.js' \
	--name ConstosoEndpoint --profile-name DemoProfile \
	--resource-group example-rg
```

Can also preload assets into an endpoint.
Useful for scenarios where app creates a large number of assets, and may want to improve user experience by prepopulating cache before any actual requests occur.
```shell
az cdn endpoint load --content-paths '/img/*' '/js/module.js' \
	--name ContosoEndpoint --profile-name DemoProfile \
	--resource-group example-rg
```

## Geo-Filtering
Enables you to allow or block content in specific countries/regions, based on country/region code.
With Azure CDN Standard for Microsoft, you can only allow or block the entire site.
With the Verizon and Akamai tiers, you can also set up restrictions on directory paths.