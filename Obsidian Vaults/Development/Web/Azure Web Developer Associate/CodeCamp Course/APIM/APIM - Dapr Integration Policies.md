#azure #az-204 #xml 

#### Send Request to a Service
Uses [[CodeCamp - Distributed Application Runtime|Dapr]] runtime to locate and reliably communicate with a Dapr microservice.

#### Send Message to Pub/Sub Topic
uses Dapr runtime to publish a message to a Publish/Subscribe topic.

#### Trigger Output Binding
Uses Dapr runtime to invoke an external system via output binding.
```xml
<invoke-dapr-binding name="bind-name" operation="op-name" ignore-error="false"
					 response-variable-name="rep-var-name" timeout="<seconds>"
					 template="Liquid" content-type="application/json">
	<metadata>
		<item key="item-name">
			<!-- item-value -->
		</item>
	</metadata>
	<data>
		<!-- message content -->
	</data>
</invoke-dapr-binding>
```