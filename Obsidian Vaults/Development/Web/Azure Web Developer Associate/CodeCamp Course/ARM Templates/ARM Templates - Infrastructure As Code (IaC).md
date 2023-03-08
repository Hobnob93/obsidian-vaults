#azure #az-204 

You write a script that will setup cloud services for you.

**IaC** is the process of managing and provisioning computer data centres (e.g. Azure) through machine-readable definition files (e.g. JSON) rather than physical hardware configuration, or interactive config tools.

IaCs can either be:
- **Declarative**
	- You define exactly what you want, and you get exactly that
- **Imperative**
	- You define what you generally want, and the service fills in the blanks

**ARM Templates** are JSON files that define Azure resources you want to provision, and Azure services you want to configure.

With ARM Templates you can:
- Set requirements *declaratively*
- Set up, tear down, or share entire architectures in minutes
- Reduce configuration mistakes
- Establish an architectural baseline for compliance
- Break up architecture in multiple files and reuse them (modular)
- Add PowerShell and Bash scripts to your templates (extensible)
- Use ARM Template Tool Kit (ARM-TTK) for **testing**
- Preview changes before you create infrastructure via template
- Deploy your template only if it passes **built-in validation**
- Keep track of changes to architecture deployments over time
- Apply Azure policies to ensure you remain compliant
- Use Microsoft Blueprints (establishes relationship between resource and the template)
- Use CI/CD integration
- Export current state of a resource group and its resources
- Use authoring tools, such as VS Code which has advanced features for authoring ARM templates

Use ARM Templates/IaC whenever you can, and avoid using the console unless you're testing things.