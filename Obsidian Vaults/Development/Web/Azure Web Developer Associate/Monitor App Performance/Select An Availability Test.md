#azure #az-204 

After deploying app or website, can set up recurring tests to monitor availability and responsiveness.
App Insights sends web requests to app at regular intervals from points around the world.
Can alert if app isn't responding or responds too slowly.

Can set up availability tests for any HTTP or HTTPS endpoint accessible from public internet.
Don't have to make changes to website you want to test.
Can also test availability of a REST API your service depends on.

Can create up to 100 availability tests per App Insights resource.
There are three types of availability tests:
- [URL ping test (class)](https://learn.microsoft.com/en-us/azure/azure-monitor/app/monitor-web-app-availability)
	- Create through portal
	- Validates whether endpoint is responding
	- Measure performance associated with response
	- Can set custom success criteria coupled with more advanced features
		- E.g. parsing requests and allowing for retries
- [Standard test (Preview)](https://learn.microsoft.com/en-us/azure/azure-monitor/app/availability-standard-tests)
	- Single request test is similar to URL ping test
	- Includes SSL certificate validity, proactive lifetime check, HTTP request verb, custom headers, and custom data associated with your HTTP request
- [Custom Track Availability test](https://learn.microsoft.com/en-us/azure/azure-monitor/app/availability-azure-functions)
	- If you decide to create a custom app to run availability tests
	- Can use `TrackAvailability()` method to send results to App Insights