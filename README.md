# Slip Stream
[Slip-Stream](https://slip-stream.net) is focused on simplicity and efficiency first. We are not focused on high
performance parity with kafka or any other streaming platform. Instead, we want to encourage customers who want to
embrace event driven architecture without needing to run expensive high performance clusters. This does not mean, 
that slip-stream cannot scale, and is not fast, just that those are not primary goals of the project. When deciding
to do the efficient thing, or the fast thing we will always choose efficient.

#### Features
* Well known wire protocol HTTP/Protobuf/JSON
* Separation of event consumer and producers from underlying storage. This allows storage to scale independently of
  the number of clients and the size and frequency of the data streamed.
* Complexity is handled by the service, with very simple client implementations. Allowing easy integration with
  slip-stream.

### Design
See our [Architecture Decision Docs](doc/adr) for details on our current implementation design.

#### TODO
* [ ] Everything