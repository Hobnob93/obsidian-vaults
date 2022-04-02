#azure #az-204 

# Configure General Settings
In the ==General Settings== section you can configure common app settings.
Some settings require higher [[Examine Azure App Service Plans#Pricing Tiers|pricing tiers]].
Currently available settings:
- `Stack settings`
	- Software stack to run the app
	- Includes language and SDK versions
	- For Linux apps or custom containers, can set optional start-up command or file
- `Platform settings`
	- Lets you configure hosting platform settings
		- `Bitness`: 32-bit or 64-bit
		- `WebSocket protocol`: e.g. ASP.NET SignalR or socket.io
		- `Always On`: keep app loaded even when no traffic, which is disabled by default - app is unloaded after 20 minutes of inactivity
			- Required enabled for ==continuous WebJobs== or ==CRON WebJobs==
		- `Managed pipeline version`: IIS pipeline mode - set to `Classic` if you have legacy app requiring older version of IIS
		- `HTTP version`: set to 2.0 to enable support for ==HTTPS/2 protocol==
		- `ARR affinity`: ensure client is routed to same instance for whole session when multiple instances are used - set to `Off` for ==stateless applications==
- `Debugging`
	- Enable remote debugging
	- Used with ==ASP.NET==, ==ASP.NET Core==, or ==Node.js== apps
	- Turns off automatically after 48 hours
- `Incoming client certificates`
	- Require client certificates in mutual authentication
	- ==TLS mutual auth== is used to restrict access to app by enabling different types of auth for it