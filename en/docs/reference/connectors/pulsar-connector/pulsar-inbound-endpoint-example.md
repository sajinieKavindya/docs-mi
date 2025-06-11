# Apache Pulsar Inbound Endpoint Example

The Apache Pulsar Inbound Endpoint allows you to connect to Apache Pulsar server and consume messages form topics. The messages are then injected into the mediation engine for further processing and mediation.

## What you’ll build

By following this tutorial, you will gain hands-on experience in:

- Configuring the Apache Pulsar Inbound Endpoint in WSO2 Micro Integrator using the Visual Studio Code extension.
- Consuming and processing messages from a Pulsar topic.
- Run and test the integration to receive real-time notifications.

The inbound endpoint acts as a message receiver and injects those messages into an integration sequence. In this section, we will demonstrate how to configure the inbound endpoint to establish a secure connection with the Apache Pulsar server using **TLS encryption** and **JWT-based authentication**. In this example, we will simply log the message, but you can extend this to perform any complex mediation logic using [WSO2 Micro Integrator mediators]({{base_path}}/reference/mediators/about-mediators/).

## Prerequisites 

### Setup Apache Pulsar

To connect with Apache Pulsar using the WSO2 Micro Integrator Apache Pulsar Connector, you need to first set up a running Pulsar instance locally or on a server. In this example, we will use an Apache Pulsar standalone server. Set up Apache Pulsar by following the instructions in [Set up Apache Pulsar]({{base_path}}/reference/connectors/pulsar-connector/pulsar-connector-setup/).

### Setup Environment for Apache Pulsar Connector

To configure the Apache Pulsar connector with Apache Pulsar version 4.0.4, copy the following client libraries to the `<MI_HOME>/lib` directory.

* [pulsar-client-4.0.4.wso2v1.jar](https://mvnrepository.com/artifact/org.apache.kafka/kafka_2.12/2.8.2)
* [pulsar-client-original-4.0.4.jar](https://repo1.maven.org/maven2/org/apache/pulsar/pulsar-client-original/4.0.4/pulsar-client-original-4.0.4.jar)
* [pulsar-common-4.0.4.jar](https://repo1.maven.org/maven2/org/apache/pulsar/pulsar-common/4.0.4/pulsar-common-4.0.4.jar)
* [bookkeeper-common-allocator-4.16.6.jar](https://repo1.maven.org/maven2/org/apache/bookkeeper/bookkeeper-common-allocator/4.16.6/bookkeeper-common-allocator-4.16.6.jar)
* [netty-codec-dns-4.1.119.Final.jar](https://repo1.maven.org/maven2/io/netty/netty-codec-dns/4.1.119.Final/netty-codec-dns-4.1.119.Final.jar)
* [netty-resolver-dns-4.1.119.Final.jar](https://repo1.maven.org/maven2/io/netty/netty-resolver-dns/4.1.119.Final/netty-resolver-dns-4.1.119.Final.jar)
* [netty-transport-classes-epoll-4.1.119.Final.jar](https://repo1.maven.org/maven2/io/netty/netty-transport-classes-epoll/4.1.119.Final/netty-transport-classes-epoll-4.1.119.Final.jar)
* [netty-incubator-transport-classes-io_uring-0.0.26.Final.jar](https://repo1.maven.org/maven2/io/netty/incubator/netty-incubator-transport-classes-io_uring/0.0.26.Final/netty-incubator-transport-classes-io_uring-0.0.26.Final.jar)

## Configure Inbound Endpoint using WSO2 Micro Integrator VS Code Extension

1. Follow [Create Integration Project]({{base_path}}/develop/create-integration-project/) steps to set up your project.

2. Go to the **Add Artifact** section and select **Event Integration**.

    <img src="{{base_path}}/assets/img/integrate/connectors/pulsar-inbound/AddEventIntegration.png" title="Add an Event Integration" width="800" alt="Add an Event Integration"/>

3. Create a **Apache Pulsar Inbound Endpoint**.

    <img src="{{base_path}}/assets/img/integrate/connectors/salesforce-inbound/AddPulsarInboundEndpoint.png" title="Create Pulsar Inbound Endpoint" width="800" alt="Create Pulsar Inbound Endpoint"/>

4. Fill in the form with the following values:

   * **Name**: ApachePulsarInboundEP
   * **Injecting Sequence Name**: test
