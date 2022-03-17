#azure #azure-wda 

# Explore Azure Functions Development
A function contains two pieces:
1. Code - which can be written in a variety of languages
2. Config - the `function.json` file

Config file is generated automatically from annotations within the code.
For scripting languages, you must provide the config yourself.

The `function.json` file defines:
- Trigger
- Bindings
- Other config settings

Every function has a config file.
Every function has exactly *one* trigger.
The runtime uses the config to determine the events to monitor, as well as how to pass data into the function, and how to return it from the function.
Below is an example config file.

```json

```