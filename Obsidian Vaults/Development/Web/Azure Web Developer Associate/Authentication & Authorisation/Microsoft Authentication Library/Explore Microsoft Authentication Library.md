#azure #azure-wda

# Explore Microsoft Authentication Library
The *Microsoft Authentication Library* (MSAL) is used to provide secure access to *Microsoft Graph*, other MS APIs, third-party web APIs, or your own web API.
*MSAL* supports many app architectures and platforms.
*MSAL* gives you many ways to get tokens, with consistent API for number of platforms.

Using *MSAL* provides the following benefits:
- No need to directly use OAuth libraries
- No need to code against protocol in app
- Acquires tokens on behalf of an app
- Maintains token cache and refreshes tokens when they are close to expiring
- Don't need to handle token expiration
- Helps specify which audience you want your app to sign in
- Helps set up your app from config files
- Helps troubleshoot app by exposing actionable exceptions, logging, and telemetry

## Application Types & Scenarios
| Library              | Supported platforms & frameworks                      |
| -------------------- | ----------------------------------------------------- |
| MSAL for Android     | Android                                               |
| MSAL Angular         | SPAs with Angular and Angular.js                      |
| MSAL for iOS & MacOS | iOS & macOS                                           |
| MSAL Go (preview)    | Windows, macOS, Linux                                 |
| MSAL Java            | Windows, macOS, Linux                                 |
| MSAL.js              | JavaScript/TypeScript frameworks i.e. Vue.js          |
| MSAL.NET             | .NET Framework, .NET Core, Xamarin, UWP               |
| MSAL Node            | Web with Express, desktop with Electron, console apps |
| MSAL Python          | Windows, macOS, Linux                                 |
| MSAL React           | SPAs with React and React-based libraries (Next.js)   | 

## Authentication Flows
Authentication flows provided by *MSAL*.
These flows can be used in variety of different app scenarios.

| Flow               | Description                                               |
| ------------------ | --------------------------------------------------------- |
| Authorization Code | Apps securely obtain tokens in name of user               |
| Client credentials | Service apps run without user interaction                 |
| On-behalf-of       | App calls service/web API, which calls MS Graph           |
| Implicit           | Used in browser-based apps                                |
| Device code        | Enables sign-in to device through another device          |
| Integrated Windows | Windows silently acquires access token when domain joined |
| Interactive        | Mobile & desktop apps call MS Graph in name of user       |
| Username/Password  | App signs in as user by using their credentials           | 

## Public Client & Confidential Client Applications
Security tokens can be obtained by multiple types of applications.
These apps tend to be separated into following categories, each used with different libraries and objects:
- **Public client applications**
	- Apps run on devices, desktop computers, or in a web browser
	- Not trusted to safely keep app secrets
	- They only access web APIs on behalf of user
	- Public clients can't hold config-time secrets, so they don't have client secrets
- **Confidential client applications**
	- Apps run on servers
	- They're considered difficult to access
	- They are capable of keeping an application secret
	- Can hold config-time secrets
	- Each instance of client has a distinct configuration