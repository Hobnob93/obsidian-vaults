#azure #az-204 

There are three plans from which to choose.

**Consumption Plan (Serverless)**
- Will have *cold-starts*
- Only pay for time the code or app is running
- Billing based on number of executions, duration of each execution, and amount of memory used
- Pay while functions running and they scale-out automatically, even through long loading times

**Premium Plan (Functions Premium)**
- Will be *pre-warmed*
- User has designated a set of pre-warmed cases
- Azure provides any additional computing services required when function is running
- Pay for constantly pre-warmed instances including any additional instances needed to scale the app in/out
- Azure Functions host instances added and removed based on number of incoming events.

**Dedicated Plan (App service plan)**
- Uses VM sharing
- When you use App Service for other apps, your functions will run on the same plan (VMs) at no extra cost
- May scale out manually by adding more VM instances for an App Service plan
- May also have autoscale enabled
- Optimal when you have existing underutilised VMs, which also operate other instances of the App Service