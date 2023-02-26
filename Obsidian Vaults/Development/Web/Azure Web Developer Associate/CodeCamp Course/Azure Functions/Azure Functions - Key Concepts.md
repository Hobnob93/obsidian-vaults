#azure #az-204 

Azure Functions are *lightweight* and *can be* serverless.
Azure Functions are easier to write and deploy, but may need more work when it comes to integrating with other apps.
Azure Functions are *fast* as there is no large application, start-up time, initialisation, or other events to fire before code execution.
- However, there are still *cold starts* where a function hasn't been used in a while
- Methods to keep the function "warm" but then technically not taking advantage of serverless as not scaling to zero!

Azure Functions are executed when a trigger event is fired.
- This makes them *event-driven*
- They can also emit event data
With Azure Functions, *you* don't need to worry about infrastructure.
- Maintenance comes from Azure changing versions and deprecating/changing features

Azure Functions can be built, tested, and deployed in Azure portal using a browser.
- There are some limitations to this
- Most alleviated if you develop using Windows

Azure Functions are *generally* easy to upgrade and doesn't affect other parts of the website.
- This is code dependent, and may not always be the case

Azure Functions use industry standard protocols to communicate with other APIs, databases, and libraries.
You only pay while functions are *running* - if you're using the serverless model!
- They have Scale-to-Zero cost depending on hosting
Azure Functions automatically scale to meet demand of traffic.
- Azure will provision more serverless containers

Azure Functions has built in monitoring via Azure Monitor.
Has built in Azure CI/CD via Azure DevOps.