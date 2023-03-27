#azure #az-204 

You can set scaling to be done automatically using **auto-inflate**.
This is not available in the *Basic* tier.
In the *Premium* tier it is enabled by default.
In other tiers, you check a checkbox for "Enable Auto-Inflate" when selecting your pricing tier and throughput units.

Scaling will scale up to the maximum TUs based on the traffic demand.
You can set the upper limit of TUs that it's allowed to scale to.