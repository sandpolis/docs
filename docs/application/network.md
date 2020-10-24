## Sandpolis Protocol
Sandpolis uses a custom binary protocol for all network communications that runs on TCP port **8768** by default. The Sandpolis protocol uses [protocol buffers](https://developers.google.com/protocol-buffers) extensively which allows it to be fast, flexible, and language independent.

Most communication happens over TCP connections among instances and the server, but Sandpolis can also coordinate direct TCP or UDP "sessions" between any two instances that need to transfer real-time data.

## Streams
Many Sandpolis operations require real-time data for a short-lived or long-lived session. This is accomplished with the concept of a stream.

All streams have a "source" and a "sink" and can exist between any two instances (a stream where the source and sink reside on the same instance is called a _local stream_). The source's purpose is to produce _stream events_ at whatever frequency is appropriate for the use-case and the sink's purpose is to consume those stream events.

### Multicasting
Stream sources can push events to more than one sink simultaneously. This is called stream multicasting and saves bandwidth when multiple users request the same resource at the same time.