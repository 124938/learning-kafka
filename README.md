## Overview

* Kafka is a distributed streaming platform, which has following capabilities:
  * **Publish & Subscribe** : It let's you publish and subscribe to streams of records/messages i.e. it allows to read and write stream of data like a messaging system.
  * **Process** : It let's you write scalable stream processing application that react to events in a real time.
  * **Store** : It let's you store streams of data safely in a distributed, replicated, fault-tolerant cluster.

* Kafka is generally used for two broad classes of applications:
  * Building real-time streaming data pipelines that reliably get data between systems or applications
  * Building real-time streaming applications that transform or react to the streams of data


## Architecture

### Few Important Concepts
* Kafka is run as a cluster on one or more servers.
* The Kafka cluster stores streams of records/messages in categories called topics.
* Each record consists of a key, a value and a timestamp.

### Core APIs
* **The Producer API** - It allows an application to publish a stream records to one of more Kafka topics.
* **The Consumer API** - It allows an application to subscribe to one or more topics and process the stream of records.
* **The Stream API** - It allows an application to act as a stream processor, consuming an input stream from one or more topics and producing an output stream to one of more topics, effectively transforming the input streams to output streams.
* **The Connector API** - It allows building and running reusable producers or consumers that connect Kafka topics to existing applications or data systems.

  ![Alt text](_images/_1_kafka_api.png?raw=true "Kafka API")

### Communication
* In Kafka the communication between client and kafka cluster is done with a simple, high-performance, language agnostic TCP protocol.
* Kafka client provides supports for many languages like java, c++, python, ruby, many more..


