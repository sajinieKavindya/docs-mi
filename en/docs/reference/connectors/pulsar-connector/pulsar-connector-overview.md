# Apache Pulsar Connector Overview

# Apache Pulsar Connector Overview

[Apache Pulsar](https://pulsar.apache.org/docs/) is a distributed, cloud-native messaging and streaming platform that supports both publish-subscribe and message queueing models. In Pulsar, **producers** send messages to **topics**, which can be consumed by one or more consumers.

The Apache Pulsar connector focuses on **publishing messages** to Pulsar topics. It enables RESTful communication with the Pulsar broker, allowing external systems to **send messages over HTTP/HTTPS** without needing native Pulsar client integrations.

## Features

- **Topic-Based Architecture**  
  Messages are published to specified Pulsar topics, including partitioned topics for scalability.

- **Secure Communication**  
  Supports **TLS encryption** to ensure data confidentiality and integrity during transmission.

- **Authentication**  
  Supports **JWT-based authentication** to restrict access to authorized clients only.

This setup is ideal for scenarios where services need to push data into Apache Pulsar securely and efficiently via simple HTTP/HTTPS calls.

Go to the <a target="_blank" href="https://store.wso2.com/connector/esb-connector-kafka">WSO2 Connector Store</a> to download the Apache Pulsar connector.

<img src="{{base_path}}/assets/img/integrate/connectors/pulsar/Apache-Pulsar-Connector-02.png" title="Apache Pulsar Connector Store" width="200" alt="Apache Pulsar Connector Store"/>

## Compatibility

| Connector Version | Supported Product Versions |
|-------------------|----------------------------|
| 1.0.0             | MI 4.4.0                   |

## Apache Pulsar Connector documentation

The Apache Pulsar connector allows you to access the Apache Pulsar Producer API from the integration sequence and acts as a message producer that facilitates message publishing. The Apache Pulsar connector sends messages to the Apache Pulsar brokers.

Follow the topics given below to get started with the Apache Pulsar connector.