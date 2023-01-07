#azure #az-204 

## Overview
A solution may contain several front- and back-end services.
How does a client know which endpoints to call?
What happens when new services are introduced, or existing ones refactored?
How do services handle SSL termination, authentication, and other concerns?
An __API Gateway__ helps to address these things.

## What Is An API Gateway?
![[API Gateway Diagram.png]]

An API Gateway sits between clients and services.
Acts as a reverse proxy, routing requests from clients to services.
May perform authentication, SSL termination, and rate limiting.

## Problems With Exposing Services to Clients
If you don't deploy a gateway, clients must send requests directly to front-end services.
There are some potential problems with exposing services:
- Can result in complex client code
	- Client must track multiple endpoints, and handle failures resiliently
- Creates coupling between client and backend
	- Client needs to know how individual services are decomposed
	- Harder to maintain client
	- Harder to refactor services
- A single operation might require calls to multiple services
	- Can result  in multiple network round trips between client and server, adding latency
- Each public-facing service must handle concerns such as authentication, SSL, and rate limiting
- Services must expose a client-friendly protocol such as HTTP or WebSocket
	- Limits choice of communication protocols
- Services with public endpoints are a potential attack surface, and must be hardened

## How A Gateway Helps
Gateway helps address the problems by decoupling clients from services.
Gateways can perform a number of different functions.
Functions can be grouped into the following design patterns:
- __Gateway routing__
	- Use gateway as a reverse proxy to route requests to one or more backend services
	- This uses layer 7 routing
	- Provides a single endpoint for clients
	- Helps decouple clients from services
- __Gateway aggregation__
	- Aggregate multiple individual requests into a single request
	- Applies when a single operation requires calls to multiple backend services
	- Client only sends the one request to the gateway
	- Gateway dispatches requests to various backend services
	- Results are aggregated and sends them back to the client
	- Helps reduce chattiness between client and backend
- __Gateway Offloading__
	- Offload functionality from individual services to the gateway
	- Can be useful to consolidate functions into one place, rather than making every service responsible for implementing them

## Gateway Functionality
Here are some examples of functionality that can be added to a gateway:
- SSL termination
- Authentication
- IP allow/block list
- Client rate limiting (throttling)
- Logging and monitoring
- Response caching
- GZIP compression
- Servicing static content
