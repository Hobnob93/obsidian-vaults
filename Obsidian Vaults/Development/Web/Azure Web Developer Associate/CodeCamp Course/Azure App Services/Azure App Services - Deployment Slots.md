#azure #az-204 

Deployment Slots allow you to create different environments of your web application associated to a different hostname.
This is useful when you need a staging, UAT, beta, environment.
Think of it as a way to quickly clone your production environment for other uses.

You can also *Swap* environments.
This could be how you perform a blue/green deploy.
You can promote your staging to production by swapping.
If something goes wrong you can just swap back!