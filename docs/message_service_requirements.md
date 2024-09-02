# **CDEvents Message Service Requirements**

## **1\. Introduction**

The purpose of this document is to outline the requirements for implementing a CDEvents message service for all open-source projects. This service will be based on CDEvents and **WILL** run in an environment that will utilize the CDEvents message service. The message service **WILL** utilize any supported protocols of CloudEvents and will incorporate security measures to prevent attacks.

This document covers the requirements for developing, and deploying a CDEvents message service. It includes functional and non-functional requirements, security measures, and constraints of the overall environment.

## **2\. Overall Description**

### **2.1 Product Perspective**

The CDEvents message service is an integral component of the CI/CD pipeline for open-source projects. It will facilitate event-driven communication across different stages of the development lifecycle, ensuring seamless integration and automation.

### **2.2 Product Functions**

The service will support publishing and subscribing to CDEvents based on CloudEvents specifications. It will handle event routing to appropriate services and optionally persist events for auditing and replay purposes.

### **2.3 User Characteristics**

The primary users of the CDEvents message service are developers, DevOps engineers, and security teams. Developers require easy integration with CI/CD pipelines, while DevOps engineers need reliable and secure operation within the infrastructure. Security teams demand robust measures to prevent unauthorized access and attacks.

### **2.4 Constraints**

The service must run within an  infrastructure and adhere to CloudEvents specifications. Security measures must be in place to prevent attacks.

### **2.5 Assumptions and Dependencies**

This document assumes that any system involved with utilizing the messaging service **MAY** support CDEvents which means that any protocol that is used by CDEvents **MUST** be supported by the messaging service.

## **3\. Specific Requirements**

### **3.1 Functional Requirements**

The system **SHALL** support publishing and subscribing to CDEvents. It **SHALL** route events to appropriate subscribers and **COULD** provide mechanisms for storing events for auditing purposes. CDEvents SDK will be available for integration with CI/CD pipelines. Additionally, events COULD be persisted in native JSON format to a document or graph database for visualization and reporting.

### **3.2 Non-Functional Requirements**

The system must ensure high availability and resilience. It should be scalable to handle varying loads and provide low latency in event processing. The system should also be maintainable and easy to upgrade.

### **3.3 Security Requirements**

The system could use whitelisted trusted sources that publish and subscribe. Also, Personal access tokens could be used for authentication. Rate limiting will be implemented to prevent denial of service attacks. Data will be available to the public based on whitelisting and/or access tokens.

### **3.4 System Requirements**

The system shall run on an infrastructure that supports Cloud Events. It should support various messaging tools, such as CNCF NATS, KNative, RabbitMQ and Kafka, but it is not restricted to these.

### **3.5 Interface Requirements**

Integration with logging and monitoring tools will be supported to provide web-based dashboard for monitoring and management. Optional integration with a document or graph database for persisting events would provide playback and auditing of the events.

## **4\. Use Cases**

### **4.1 Use Case Diagrams**

\[Include use case diagrams illustrating the interactions between actors and the system.\]

### **4.2 Detailed Use Cases**

#### **Use Case 1: Publishing an Event**

**Actors**: CI/CD Pipeline
**Preconditions**: The system is operational and the CI/CD pipeline is configured.
**Postconditions**: The event is published and subscribers get notification of the event.
**Main Flow**: The CI/CD pipeline generates an event, which is sent to the message service. The service validates and optionally stores the event, then routes it to subscribers.

#### **Use Case 2: Subscribing to Events**

**Actors**: Developer, Application
**Preconditions**: The system is operational and the subscription is configured.
**Postconditions**: The subscriber receives the event.
**Main Flow**: The subscriber registers with the message service, which acknowledges the subscription. When an event occurs, it is sent to the subscriber.

#### **Use Case 3: Persisting an Event**

**Actors**: Message Service
**Preconditions**: The system is operational and the optional database is configured.
**Postconditions**: The event is persisted in the database.
**Main Flow**: An event is generated, validated by the message service, and sent to the database, where it is stored.

## **5\. Tool Comparison: CNCF NATS, KNative, Kafka, and RabbitMQ**

To meet the requirements outlined in this document, we consider CNCF NATS, KNative, Kafka and RabbitMQ as potential tools for the CDEvents message service. Below, we evaluate each tool in terms of its pros and cons:

### **CNCF NATS**

**Pros:**

* **Simplicity and Performance**: NATS is lightweight and offers high performance, with low latency and high throughput.
* **Scalability**: NATS can scale horizontally and handle large numbers of connections and messages.
* **Ease of Deployment**: It integrates well with Kubernetes, making it easy to deploy and manage within a Kubernetes cluster.

**Cons:**

* **Limited Features**: Compared to Kafka, NATS has fewer features and may not support complex use cases out of the box.
* **Persistence**: NATS is primarily designed for ephemeral messaging and may require additional tools for persistent storage of messages.

### **KNative**

**Pros:**

* **Kubernetes Native**: KNative is designed to work seamlessly with Kubernetes, providing a serverless framework that simplifies the deployment and scaling of applications.
* **Event-Driven Architecture**: KNative Eventing is built to handle CloudEvents and integrates well with various event sources and sinks.

**Cons:**

* **Complexity**: KNative can be complex to set up and manage, particularly for users unfamiliar with Kubernetes and serverless concepts.
* **Performance Overhead**: The serverless model introduces some performance overhead compared to traditional messaging systems like NATS and Kafka.

### **Kafka**

**Pros:**

* **Feature-Rich**: Kafka offers robust features for streaming, storage, and processing of large volumes of data.
* **Durability and Reliability**: Kafka is designed for high durability and fault tolerance, ensuring message persistence and reliability.
* **Ecosystem**: Kafka has a rich ecosystem of tools and integrations, making it suitable for complex event-driven architectures.

**Cons:**

* **Resource Intensive**: Kafka requires significant resources for deployment and management, which can be a drawback for smaller projects.
* **Operational Complexity**: Managing a Kafka cluster can be complex and requires expertise in distributed systems.

### **RabbitMQ**

* **Pros:**
  * Flexibility: RabbitMQ supports multiple messaging protocols (AMQP, MQTT, STOMP) and is highly configurable to fit various use cases.
  * Reliability: RabbitMQ provides robust messaging features, including message acknowledgment, retries, and persistence.
  * Ease of Use: RabbitMQ has a relatively easy learning curve and offers extensive documentation and community support.
* **Cons:**
  * Performance: RabbitMQ may not scale as efficiently as Kafka for very high throughput scenarios.
  * Overhead: RabbitMQ’s feature set can introduce overhead in terms of resource usage and complexity for simple messaging needs.
