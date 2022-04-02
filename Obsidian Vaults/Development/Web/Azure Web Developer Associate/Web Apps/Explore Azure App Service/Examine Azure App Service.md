#azure #az-204 #ci #deployment

# Examine Azure App Service
## Built-in Auto Scale Support
Has the ability to scale ==up/down== or ==in/out== automatically.
- Scale up/down refers to scaling the **resources**
	- Cores available
	- RAM available
- Scaling in/out refers to number of machine instances running the app

## Continuous Integration and Deployment Support
*Azure Portal* provides ==CI== and ==deployment== with DevOps, GitHub, BitBucket, FTP, or a local Git repo on development machine.
Connect these sources to *App Services*  and it'll auto-sync code and future changes to web app.

## Deployment Slots
Can add deployment slots to web app using *Azure Portal* or cmd tools.
E.g. can create a staging slot where code is pushed to for testing - once happy, can swap staging slot and production slot to release the app's new version.

[[Explore Azure App Service Deployment Slots]]

## App Service on Linux
*App Service* can host apps natively on Linux for supported application stacks.
Can also run custom Linux containers (*Web App for Containers*) - see [[Infrastructure as a Service Solutions]].
It supports a number of language-specific built-in images, including ==Node.js==, ==Java==, ==PHP==, ==Python==, ==.NET Core==, and ==Ruby==.
Can deploy with a ==custom container== if runtime requires language not supported.

Supported languages are updated on regular basis.
A Cloud Shell command for retrieving current Linux web app runtimes:
```shell
az webapp list-runtimes --linux
```

## Linux Limitations
There are a few notable limitations when running on Linux:
	- Not supported on the ==shared pricing tier==
	- Can't mix Windows and Linux apps in same [[Examine Azure App Service Plans|App Service plan]]
	- Historically, couldn't mix Windows and Linux apps in same ==resource group==, however this changed for resource groups created after ==Jan 21, 2021==
	- *Azure Portal* only shows features working for Linux; these are activated as they become functional