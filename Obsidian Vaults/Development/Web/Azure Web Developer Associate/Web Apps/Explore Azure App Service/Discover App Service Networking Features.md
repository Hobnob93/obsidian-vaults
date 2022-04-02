#azure #az-204

# Discover App Service Networking Features
By default, apps are accessible through internet and can only reach internet-hosted endpoints.
For some apps, you might want to control the inbound and outbound traffic.

Two main deployment types for *Azure App Service*:
* Multi-tenant public service hosts plans in `Free`, `Shared`, `Basic`, `Standard`, `Premium`, `PremiumV2`, and `PremiumV3` [[Examine Azure App Service Plans|App Service Plans]]
* Single-tenant App Service Environment (ASE) hosts `Isolated` plans directly in your virtual network

## Multi-tenant App Service Networking Features
*Azure App Service* is a distributed system.
Roles that handle incoming requests are called ==front ends==.
Roles that host customer workload are called ==workers==.
All roles in deployment exist in a multi-tenant network, and due to same scale unit containing multiple customers, you cannot connect these apps directly to your own network.

Instead of connecting the networks, you need features to handle aspects of app communication.
The features used for incoming requests can't be used for outgoing requests, and vice-versa. See table below for details.

| Inbound Features     | Outbound Features                 |
| -------------------- | --------------------------------- |
| App-assigned address | Hybrid Connections                |
| Access restrictions  | Gateway-required VNet Integration |
| Service endpoints    | VNet Integration                  |
| Private endpoints    |                                   |

There are a few exceptions to mixing and matching the features.
Below are examples of using *App Service* networking features to control inbound traffic.

| Inbound use case                                   | Feature              |
| -------------------------------------------------- | -------------------- |
| Support IP-based SSL                               | App-assigned address |
| Support unshared dedicated inbound address         | App-assigned address |
| Restrict access from set of well-defined addresses | Access Restrictions  |

## Default Networking Behaviour
*App Service* scale units support many customers on each deployment.
`Free` and `Shared` plans host customer workloads on multi-tenant workers.
`Basic` and higher plans host workloads dedicated to one service plan.
If you have a `Standard` plan, all apps in plan run on ==same== worker - if you scale out worker, all apps in plan will be replicated on a new worker for each instance in the service plan.

### Outbound Addresses
`Free`, `Shared`, `Basic`, `Standard`, and `Premium` plans all use the same ==VM type==.
`PremiumV2` uses a different VM type to those prior as well as `PremiumV3`.
Changing ==VM family== gives you a different set of ==outbound addresses== e.g. scaling from `Basic` to `PremiumV2` your outbound address changes.
In the ==older== scale units, changing the VM family also changed the inbound address.

Outbound addresses used by app for making outbound calls are listed in app properties.
Addresses are shared by all apps running on same worker VM family in *App Service* deployment.
Property `possibleOutboundAddresses` lists all outbound addresses app might use in a scale unit.

### Find Outbound IPs
Can be found in the properties of the app within *Azure Portal*.

These can also be found by running the following Cloud Shell command:
```shell
az webapp show --resource-group <group_name> --name <app_name> --query 
    outboundIpAddresses --output tsv
```

You can also find possible outbound IP addresses for app regardless of pricing tiers using this Cloud Shell command:
```shell
az webapp show --resource-group <group_name> --name <app_name> --query 
    possibleOutboundIpAddresses --output tsv
```