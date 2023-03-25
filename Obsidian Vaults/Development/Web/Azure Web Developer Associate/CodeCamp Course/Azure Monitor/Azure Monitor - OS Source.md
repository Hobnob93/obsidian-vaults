#azure #az-204 

This is for the *guest* operating system **not** the host operating system!
With virtualisation, the VM has its own OS - but the actual underlying hardware has its own OS which is the *host*. This does *not* cover that as the cloud provider/Azure will do that itself.
The guest OS is the OS in which we can actually control.

Log Analytics Agent is installed for comprehensive monitoring.
Dependency Agent collects discovered data about processes running on VM and external process dependencies.
Agents can be installed on OS for VMs running in Azure, on-premise, or other cloud provider.

Diagnostics Extension collects performance counters and stores them in metrics.
Application Insights collects logs and performance counters from the compute resource supporting your app to be analysed with other app data.
Diagnostics Extension can stream data to other locations using [[CodeCamp - Azure Event Hub|Azure Event Hub]].
Diagnostic Extension always writes to an Azure Storage Account.
Azure Monitor for VMs uses the Log Analytics agent to store health state information in a custom location.

![[Azure Monitor - OS Source Diagram.png]]