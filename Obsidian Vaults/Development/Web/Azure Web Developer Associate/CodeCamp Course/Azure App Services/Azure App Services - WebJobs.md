#azure #az-204 

WebJobs is a feature of Azure App Service that enables you to run a program or script in the same instance as a web app, API, or mobile app.
There is no additional cost to use WebJobs.
- It is *not* supported for App Service on Linux.

The following file types are supported:
- `.cmd`, `.bat`, `.exe` (using Windows CMD)
- `.ps1` (using PowerShell)
- `.sh` (using Bash)
- `.php` (using PHP)
- `.py` (using Python)
- `.js` (using Node.js)
- `.jar` (using Java)

WebJobs Types
- Continuous
	- Run continually until stopped
		- Support debugging
- Triggered
	- Run only when triggered
	- Such as a schedule
	- Expose a webhook that can be called to enable scenarios like scheduling
	- Doesn't support debugging

WebJobs Scale (Only for Continuous)
- Multi Instance
	- Will scale your WebJob across all instances of your App Service plan
- Single Instance
	- Will only keep a single copy of your WebJob running regardless of App Service plan instance count