# CDEvents Implementation

The implementation of CDEvents is use case driven. We focus on a few use cases that demonstrate the business value of interoperability in the CI/CD space and for each of them we identify a target architecture, its logical building blocks and a set of software components that can be used to implement it.

Some of the software required is part of the CDEvents project and other is external. All proposed implementation focus exclusively on open source software components. Commercial software that implements standard protocols like CDEvents can be slotted in to replace or complement the open source software adopted by the CDEvents Implementation WG.

## Use Cases

CDEvents use cases may apply to two personas: open source project communities and organizations doing in-house software development.
The requirements and design of the implementation vary based on the persona and are documented in the use-case specific document.

- [Enhance Security Posture through Automation](./security_automation.md)
- Improve Developer Experience through Consistency and Visibility (TBD)
- Drive Efficiency through DevOps Metrics (TBD)

## Common Components

### Messaging Platform

TBD - Link to component requirements and design

### Event Producers

TBD - Describe various type of event producers: tools native, via tool plugin, via external adapter, via external watcher

#### Webhook Adapter

TBD - Adapter and plugins

### CDEvents SDKs

CDEvents provides SDKs for various programming languages.
The Implementation WG focusses on providing consistency across the various SDKs to simplify adoption.

* [Golang SDK][sdk-go]
* [Java SDK][sdk-java]
* [Rust SDK][sdk-rust]
* [Python SDK][sdk-python]
* [.NET SDK][sdk-dotnet]


<!-- External Links -->

[sdk-go]: https://github.com/cdevents/sdk-go
[sdk-java]: https://github.com/cdevents/sdk-java
[sdk-rust]: https://github.com/cdevents/sdk-rust
[sdk-python]: https://github.com/cdevents/sdk-python
[sdk-dotnet]: https://github.com/cdevents/sdk-dotnet