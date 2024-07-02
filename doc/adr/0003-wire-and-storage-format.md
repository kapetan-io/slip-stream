# 3. wire and storage format

Date: 2024-07-02

## Status

Accepted

## Context

We need a wire, memory and storage format which is simple and performant. Although Slip Stream is focused on 
efficiency and simplicity, we should attempt to implement high performance patterns such as zero copy and data
batching. In order the meet this pattern, we need a portable data format which can remain the same as we move large
batches of events from wire, memory and storage. Although a wire format API is not in scope for the first version of
slip-stream, the storage format decision will heavily affect how that future API is implemented. As such we should be 
very thoughtful of how we design the storage format used in V1.

## Decision

Our storage format will be implemented using `protobuf`

* Simple Implementation: Protobuf has a simple and well-defined syntax, making it easy to implement a high-performance 
  custom parser if needed.
* Well-Known Format: Protobuf is a widely used and well-known format in the industry, ensuring that there are many
  resources available for implementation and troubleshooting.
* Maximum Size Compatibility: The maximum Protobuf size is well above our target page size of 4-8k, ensuring that it
  can handle our data requirements efficiently.
* Key/Value Storage System Fit: Protobuf fits seamlessly into a simple key/value storage system, making it an ideal
  choice for our event streaming service which will store batches of events into a sequential key/value storage 
  system.

## Consequences

The Google implementation of `protobuf` employs mutexes and thus heap only structs. This is suboptimal for a high
speed streaming platform. However, future work could include writing our own `protobuf` parser specific for our
particular structs (not a general use parser). 

Protobuf isn't the fastest serialization format, but it is the most widely supported. This is important for future
client implementations who wish to implement the future wire format API slip-stream might eventually provide.

NOTE: Implementation details of the storage system is beyond the scope of this document.
