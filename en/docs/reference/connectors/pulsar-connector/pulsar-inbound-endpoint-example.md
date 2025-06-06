# Apache Pulsar Inbound Endpoint Example

The Apache Pulsar Inbound Endpoint allows you to connect to Apache Pulsar server and consume messages form topics. The messages are then injected into the mediation engine for further processing and mediation.

## What you’ll build

By following this tutorial, you will gain hands-on experience in:

- Configuring the Apache Pulsar Inbound Endpoint in WSO2 Micro Integrator using the Visual Studio Code extension.
- Consuming and processing messages from a Pulsar topic.
- Run and test the integration to receive real-time notifications.

The inbound endpoint acts as a message receiver and injects those messages into an integration sequence. In this section, we will demonstrate how to configure the inbound endpoint to establish a secure connection with the Apache Pulsar server using **TLS encryption** and **JWT-based authentication**. In this example, we will simply log the message, but you can extend this to perform any complex mediation logic using [WSO2 Micro Integrator mediators]({{base_path}}/reference/mediators/about-mediators/).

## Prerequisites 

To proceed with this scenario, you need to first set up a running Pulsar instance locally or on a server. In this example, we will use an Apache Pulsar standalone server.

1. Refer to the [Setting up the Apache Pulsar Environment]({{base_path}}/reference/connectors/pulsar-connector/set-up-amazonlambda/) to:

    1. Download Apache Pulsar standalone server.
    2. Obtain TLS certificates required for TLS encryption.
    3. Obtain the **JWT Token** required for JWT-based authentication.
    4. Configure the Pulsar server to enable TLS encryption and JWT authentication.
    5. Start the Pulsar Standalone Server.
    6. Setup WSO2 Micro Integrator to use the Pulsar Inbound Endpoint.

## Configure Inbound Endpoint using WSO2 Micro Integrator VS Code Extension

1. Follow [Create Integration Project]({{base_path}}/develop/create-integration-project/) steps to set up your project.

2. Go to the **Add Artifact** section and select **Event Integration**.

    <img src="{{base_path}}/assets/img/integrate/connectors/pulsar-inbound/AddEventIntegration.png" title="Add an Event Integration" width="800" alt="Add an Event Integration"/>

3. Create a **Apache Pulsar Inbound Endpoint**.

    <img src="{{base_path}}/assets/img/integrate/connectors/salesforce-inbound/AddPulsarInboundEndpoint.png" title="Create Pulsar Inbound Endpoint" width="800" alt="Create Pulsar Inbound Endpoint"/>

4. Fill in the form with the following values:
