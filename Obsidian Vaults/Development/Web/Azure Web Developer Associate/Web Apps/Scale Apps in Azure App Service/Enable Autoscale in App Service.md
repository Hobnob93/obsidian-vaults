#azure #az-204 

# Enable Autoscale in App Service
## Enable Autoscaling
Done through *App Service plan* in *Azure Portal* - just select `Scale out (App Service plan)` in the ==Settings== group.
Not all [[Examine Azure App Service Plans#Pricing Tiers|pricing tiers]] support autoscaling.

By default, an *App Service Plan* only implements manual scaling.
Select `Custom autoscale` to manage condition groups for autoscale settings.

## Add Scale Conditions
Once enabled, you can edit the default scale condition.
You can also add your own scale conditions.
The default condition is executed when none of the other scale conditions are active.

A metric-based scale condition can specific min or max number of instances to create.
The maximum cannot exceed that of the max as part of the pricing tier.
All conditions (except default) may include a schedule with which to scale.

## Create Scale Rules
A metric-scale condition contains one or more scale rules.
Click `Add a rule`  to create custom rules.
Define criteria indicating when a rule should trigger an autoscale action.

## Monitor Autoscaling Activity
Autoscaling can be tracked through *Azure Portal* .
There is a ==Run History== chart detailing number of instances over time, and which conditions caused each change.
Can use the chart in conjunction with ==Overview== page to correlate events with resource utilisation.