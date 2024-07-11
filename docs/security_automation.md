# Use Case: Enhance Security Posture through Automation

Software development requires an ever-growing set of security practices to be implemented in order to produce software that can be trusted. Generating Software Bill of Materials (SBOMs), running vulnerability scans, static analysis, signing artifacts and more.

Implementing all these in existing CI/CD pipelines introduces churn and extra cognitive load on DevOps engineers, which maintain the pipeline definitions and need to familiarize themselves with all this new technologies.

It's not only about triggering extra CI jobs: this new checks and practices in turn produce extra data which needs to be stored, evaluated and understood. 

CDEvents allow implementing this new security practices as a result of events in existing CI/CD pipelines. This way the implementation of security practices does not impact the original pipelines and can be performed by individuals that are familiar with the security requirements and technologies.
Storing the events from the existing CI/CD pipelines along with those from the security tools in and *evidence store* allows for auditing of CI/CD processes and obtaining lineage information about artifacts produced in the software factory.

## State of the Art

Vendors like GitHub provide integrated tools, like "Dependabot" and "CodeQL" which can be used to add some of the required security features with minimal configuration. Such tools are tightly integrated with GitHub's own CI/CD system and are not easily ported to other CI/CD systems.

## Requirements

* Minimal or no change to existing CI/CD systems and pipelines
* Security checks and tools can be triggered in response to **policies** applied to a **collection** of events
* Execution of security tools can be audited

## Architecture

1. Existing CI/CD pipelines produce events about their lifecycle and artifacts being built. All the events are sent to the message bus. A few options are available:
    * The CI/CD tool natively supports CDEvents
    * A plugin is available for the tool that produces CDEvents
    * The CI/CD tool can produce events or trigger webhooks. They can be converted to CDEvents via an adapter
    * The CI/CD tool can be observed in some way by an external watcher which can produce CDEvents

2. An event ingestor process subscribes to the message bus, consumes events and stores them in an event database.
3. A query API allows high-performance access to previous events stored in the event database.
4. A policy engine subscribes to specific events. It evaluates policies that apply to the specific events and previous events (accessible via the query API) and triggers the execution of security tools and pipelines in response.

5. Security engineers may define policies in the policy engine to add new security tooling, without touching the original pipelines. 
6. Security engineers and DevOps engineers may observe the execution or regular and security pipelines through a consolidated dashboard. 
7. Security engineers may audit all events associated with specific software artifacts.

![](./security_automation.drawio.svg)

## Personas

### Open Source Projects

### In-House Development