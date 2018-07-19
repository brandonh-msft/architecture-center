# Serverless Workflow Orchestration
Implementing workflow orchestration in a serverless environment offers massive scaling and cost savings opportunities but is now without its own set of special considerations. These patterns are a few that work well in Azure.

## Context & Problem
Backend business processes often involve a multi-step "orchestration" of various sub-processes. As an example, a business may want to ingest many files, ensure they compose a proper batch, validate their structure and content, then pass them on to downstream systems.

In a traditional implementation, that ingestion and validation may take place wholly within a VM or a set of VMs. This presents us with the following considerations:
* How much idle time are you paying for?
* What is the cost to scale out/in to support varying degrees of load?
* How much could any one sub-process be potentially parallelized?

Each of these questions leads us toward considering Serverless as a way to implement a workflow. However Serverless has its own set of considerations:
* How much state does the workflow need?
    * Where should this be stored?
    * How should this be accessed?
    * What impact will it have on execution time?
* How can a request be traced through the various stateless steps of the system?
* What happens if something fails and we need to retry?

## Solution
< frame sample problem. We could use a real-world scenario like Coke's bottler-files ingestion or something made up >
### Azure Logic Apps
< implementation handling sample problem w/ Logic apps >

< Pros >

< Cons >
### Azure Functions + Messaging
< Link to docs comparing messaging offerings >

< implementation handling sample problem w/ Functions + Service Bus >

< Pros >

< Cons >
### Durable Functions
< implementation handling sample problem w/ Durable Functions >

< Pros >

< Cons >
## Related Guidance
< Other docs on messaging comparisons >

< Link to https://aka.ms/serverlessOrchestration? >