#azure #az-204 

## Overview
Azure Content Delivery Network (CDN) offers devs global solution for delivering high-bandwidth content by caching content at strategically placed physical nodes across the world.
CDN can accelerate dynamic content, which cannot be cached, by7 leveraging network optimisations using _CDN POPs_ (Point of Presence).
E.g. route optimisation to bypass Border Gateway Protocol (BGP).

Benefits of using Azure CDN to deliver web site assets include:
- Better performance and improved user experience
	- Especially when multiple round trips required to load content
- Large scaling to better handle instantaneous high loads, such as at the start of a product launch
- Distribution of user requests and serving of content delivery from edge servers so that less traffic is sent to the origin server

## How Azure Content Delivery Networks Works
![[How Azure CDN Works.png]]
1. A user (Alice) requests a file by using a URL with a special domain name
	- E.g. `<endpoint>.azureedge.net`
	- Can be an endpoint hostname or a custom domain
	- DNS routes request to best performing POP location, usually the one geographically closest to the user
2. If no edge servers in POP have the file in cache, POP requests file from origin server
	- Origin server can be an Azure Web App, Azure Cloud Service, Azure Storage account, or any publicly accessible web server
3. Origin server returns file to an edge server in the POP
4. Edge server in POP caches file and returns file to original requestor (Alice)
	- File remains cached on edge server in the POP until time-to-live (TTL) expires
	- TTL specified by HTTP headers
	- If origin server didn't specify a TTL, default is 7 days
5. Additional users can request same file by using the same URL, and can also be directed to the same POP
6. If the TTL for file hasn't expired, POP edge server returns file directly from the cache
	- Process results in a faster, more responsive user experience

## Requirements
Need to create at least one CDN profile, which is a collection of CDN endpoints.
Every CDN endpoint represents a specific config of content deliver behaviour and access.
Organise endpoints by internet domain, web app, or some other criteria, by using multiple profiles.
Pricing is applied at CDN profile level, so you must create multiple CSN profiles if you want to use a mix of pricing tiers.

## Limitations
Each Azure subscription has default limits for the follow resources:
- Number of CDN profiles that can be created
- Number of endpoints within a profile
- Number of custom domains that can be mapped to an endpoint

## Azure Content Delivery Network Products
Azure CDN includes four products:
- Azure CDN Standard from Microsoft
- Azure CDN Standard from Akamai
- Azure CDN Standard from Verizon
- Azure CDN Premium from Verizon