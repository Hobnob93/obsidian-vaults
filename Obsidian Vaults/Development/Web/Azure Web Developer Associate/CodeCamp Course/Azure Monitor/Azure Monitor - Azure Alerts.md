#azure #az-204 

Alerts notify you when issues are found with your infrastructure or application.
They allow you to identify and address issues before the users of your system notice them.
When an alert is triggered, you can be notified and have it take action.

Azure has 3 kinds of alerts:
1. Metric Alerts
2. Log Alerts
3. Activity Log Alerts

The anatomy of an alert:
- **Alert Rule**
	- Defines who should be monitored
	- When you should react
- **Target Resource**
	- A resource such as Azure VM
	- Designated as the target resource
	- It omits a signal
- **Signal**
	- A data payload emitted from the resource
	- It could be the following:
		- Metric
		- Log
		- Activity Log
		- Application Insights
- **Criteria/Logic**
	- Signal is evaluated against this
	- Determines if alert has been triggered
	- You might trigger an alert if CPU > 70% as an example
- **Action Group**
	- Contains actions to be performed when alert triggered
- **Action**
	- This could be an Automation Runbook, Azure Function, ITSM, Logic App, Webhook, or Secure Webhook
- **Alert State**
	- Monitor Condition
		- Set by the system
	- Alert State
		- Set by the user
		- Might want to have a history or resolved/closed issues

![[Azure Monitor - Anatomy of an Alert Diagram.png]]