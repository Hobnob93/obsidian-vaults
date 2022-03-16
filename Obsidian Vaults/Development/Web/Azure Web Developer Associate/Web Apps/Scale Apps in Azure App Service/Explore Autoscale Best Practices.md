#azure #azure-wda 

# Explore Autoscale Best Practices
Not following good practices can lead to **undesirable results**.

## Autoscale Concepts
Autoscaling scales ==horizontally==; it scales *out* and back *in* again.
There is a maximum, minimum, and default for instance count.
Autoscale jobs always checks if metrics are crossing any defined thresholds.
All thresholds calculated at an instance-level.
All success and failures of autoscaling are logged to *Activity Log*.
	- Can configure an activity log alert for notifications through email, SMS, or webhooks.

## Autoscale Best Practices
- **Ensure max and min values are different with adequate margin between**
	- If max and min are same value, no scaling can occur
	- Keep an adequate margin between the values (which are both inclusive) as autoscale can only scale between these limits
- **Diagnostic metric statistic should be appropriate**
	- You can choose any of `Average`, `Minimum`, `Maximum`, and `Total` as a metric to scale by
	- Most common is going to be `Average`
- **Choose thresholds carefully for all metric types**
	- Carefully choose different thresholds for in/out scaling based on practical situations
	- *Not recommended* to do something like the following:
		- `Thread Count` >= 600; increase instance count by 1
		- `Thread Count` <= 600; decrease instance count by 1
	- This can cause what is known as "==flapping==" - where instances are always going up and down due to the threshold being so close for both
	- Choose an adequate margin between in/out scales to avoid ==flapping==.
	- *Autoscaling* tries to avoid flapping, and may not autoscale as a result.
- **Considerations for scaling when multiple rules are configured**
	- Scaling *out* runs if **any** scale out rules are met
	- Scaling *in* runs if *all* scale in rules are met
- **A safe default instance count**
	- Ensure it is safe for expected idle workloads
	- Ensure it is cost effective
- **Configure autoscale notifications**
	- *Autoscale* will post to *Activity Log* if any of the following occurs:
		- A scale operation issued
		- Scale action completes successfully
		- Scale action fails
		- Metrics not available for autoscale service to make a decision
		- Metrics have been recovered again to make decisions
- Can use *Activity Log* to monitor health of autoscale engine
- Can configure email or webhook notifications