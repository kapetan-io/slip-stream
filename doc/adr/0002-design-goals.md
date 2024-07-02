# 4. design goals

Date: 2024-07-02

## Status

Accepted

## Context

Understanding the high level goals of the project is important information for contributors and users alike. This
allows us to focus on what is important and not get side tracked with implementing features which clash with the 
primary goals of the project.

## Decision

The primary goal of the project is to implement a highly efficient and simple to integrate with event streaming system.

### How we are different from kafka
[Kafka](https://www.confluent.io/what-is-apache-kafka/) is a high performance and high scale event streaming system
with many secondary products integrated to provide various processing capabilities. Their focus on performance and
scale has lead kafka to make several decisions which make using, integrating with and controlling costs difficult.

* Kafka has a custom wire protocol which is non-trivial for clients to implement.
* Kafka is tightly bound to its storage system, kafka does not scale client event consumption and production
  independent of the underlying storage.
* Kafka's design requires the producers and consumers to handle a large portion of the complexity. As a result
  it must rely heavily upon very complex clients to operate.
* Pushing complexity onto the clients means the kafka server can optimize read/write and replication of data
  but at the cost of lower interoperability.
* Because interoperating with Kafka is non-trivial, users must rely upon vendors for integration and features.
  Since implementing custom features on top of kafka can be a difficult task for developers -- believe me, 
  [we have tried](https://github.com/mailgun/kafka-pixy)

[Slip-Stream](https://slip-stream.net) is focused on simplicity and efficiency first. We are not focused on high
performance parity with kafka or any other streaming platform. Instead, we want to encourage customers who want to
embrace event driven architecture without needing to run expensive high performance clusters if such scale is not
needed. This does not mean, that slip-stream cannot scale, and is not performant, just that those are not primary
goals of the project. When deciding to do the efficient thing, or the fast thing we will always choose efficient.

* Well known wire protocol HTTP/Protobuf/JSON
* Separation of event consumer and producers from underlying storage. This allows storage to scale independently of
  the number of clients and the size and frequency of the data streamed.
* Complexity is handled by the server, with very simple client implementations. Allowing easy integration with
  slip-stream.
* Encourage a third-party developer ecosystem to develop around slip-stream to provide additional features that are
  out of scope for slip-stream.

## Consequences

By choosing to prioritize simplicity and efficiency over high performance and scalability, we can expect that kafka
will remain a top choice for very large enterprise companies with deep pockets. Slip-Stream's focus on simplicity and 
efficiency is designed to appeal to a different target market than Kafka, attracting users who are looking for a more
accessible, low cost, and easier-to-use event streaming system.

The use of well-known wire protocols such as HTTP, Protobuf, and JSON will make it easier for clients to integrate
with Slip-Stream, reducing the complexity, and dependence upon expensive vendor products.
