# gRPC #
## What is gRPC? ##
gRPC is a high-performance, open-source, remote procedure call (RPC) framework developed by Google. It enables client and server applications to communicate with each other across different programming languages and platforms, using a protocol buffer serialization format. gRPC is designed to be fast, efficient, and scalable, making it ideal for building distributed systems and microservices.

gRPC uses a client-server model, where the client sends a request to the server and waits for a response. The server processes the request and returns a response to the client. This communication is done using the HTTP/2 protocol, which supports bi-directional streaming, flow control, and multiplexing. This means that multiple requests and responses can be sent over a single connection, improving performance and reducing latency.

One of the key benefits of gRPC is its support for code generation. With gRPC, developers can define a service and its methods using a protocol buffer definition file, and then generate client and server code in various programming languages, including C++, Java, Python, and Go. This makes it easy to build distributed systems that are language-agnostic and interoperable.

## What are the features of gRPC? ##
gRPC offers a number of features that make it a powerful and efficient communication protocol for building distributed systems and microservices. Some of the key features of gRPC are:

1. High performance: gRPC uses the HTTP/2 protocol to enable efficient communication between client and server. It uses binary serialization and compression to reduce the size of data being transmitted, and supports multiplexing, flow control, and bi-directional streaming to improve performance.
2. Language agnostic: gRPC uses protocol buffers as the default data format for exchanging messages between client and server, which means it is not tied to any specific programming language. Developers can use the gRPC code generator to generate client and server code in a number of different languages, including C++, Java, Python, and Go.
3. Cross-platform support: gRPC supports communication between clients and servers running on different platforms, including Linux, Windows, macOS, iOS, and Android. This means developers can build distributed systems that work seamlessly across different environments.
4. Bi-directional streaming: gRPC supports bi-directional streaming, which allows both the client and server to send and receive data simultaneously. This is particularly useful for applications that require real-time communication or that need to process large amounts of data.
5. Authentication and encryption: gRPC supports Transport Layer Security (TLS) encryption and authentication, which ensures that communication between client and server is secure and private.
6. Interoperability with other systems: gRPC supports interoperability with other systems, including REST APIs. Developers can use the gRPC gateway to expose gRPC services as REST APIs, or to call REST APIs from gRPC clients.

Overall, gRPC offers a range of powerful features that make it an ideal choice for building distributed systems and microservices.

## What are the differences between gRPC and REST API? ##
gRPC and REST API are two popular ways of building communication protocols for distributed systems and microservices. While both are used to enable communication between client and server applications, there are some key differences between gRPC and REST API:

1. **Data Format**: gRPC **uses Protocol Buffers, which is a binary serialization format that is smaller, faster, and more efficient than JSON used by REST API**. REST API uses JSON or XML as its data format.
2. **API Style**: gRPC **uses an RPC (Remote Procedure Call) style, where the client sends a request and waits for a response, similar to a function call**. **REST API uses a Resource-based style, where the client requests a specific resource or endpoint, and the server returns the data related to that resource**.
3. **Performance**: **gRPC is generally faster and more efficient than REST API, thanks to its binary serialization format, use of HTTP/2, and support for bi-directional streaming**. **REST API may be slower due to its use of text-based data formats like JSON or XML, and lack of built-in support for streaming**.
4. **Language Support**: **gRPC supports a wide range of programming languages, including C++, Java, Python, and Go, among others**. **REST API is also language-agnostic, but requires developers to implement their own serialization and deserialization logic for different programming languages**.
5. **Tooling**: **gRPC comes with its own code generation tool that generates client and server stubs in different programming languages, making it easier to build and maintain distributed systems** **REST API does not have such tooling, and developers need to use third-party libraries or write their own code to handle serialization, deserialization, and other functionality**.

Overall, gRPC and REST API are both powerful communication protocols with their own strengths and weaknesses. **gRPC is well-suited for building high-performance, low-latency systems that require streaming and bi-directional communication, while REST API is a more flexible and familiar choice for building web APIs that work over HTTP/1.1**.

## How to learn gRPC? ##
There are several resources available to learn gRPC:

1. **Official Documentation**: The official gRPC documentation is a great place to start learning about the framework. It provides a comprehensive guide to building gRPC applications, with examples and tutorials in several programming languages.
2. **Online Courses**: There are several online courses available that teach gRPC, including those on platforms like Udemy, Coursera, and Pluralsight. These courses offer step-by-step guidance and practical exercises to help you learn gRPC.
3. **Books**: There are several books available that cover gRPC in detail, including "gRPC: Up and Running" by Kasun Indrasiri and Danesh Kuruppu, and "Hands-On gRPC" by Tarun Pabbi. These books provide a thorough introduction to gRPC and its features, as well as practical examples and best practices.
4. **Code Examples**: There are many code examples and sample applications available on GitHub and other code-sharing platforms. These examples can be a great resource for learning how to use gRPC, as they provide real-world use cases and practical guidance.
5. **Community Support**: The gRPC community is active and helpful, with forums, mailing lists, and Slack channels available for support and collaboration. Joining the community can help you learn from other users' experiences and get answers to your questions.

Overall, the best way to learn gRPC is to start with the official documentation and then explore other resources based on your learning style and preferences. Practice building small applications and experimenting with different gRPC features to gain hands-on experience with the framework.

# Documentation Notes #
## Introduction to gRPC ##
1. Topics:
	1. gRPC
	2. Protocol buffers
2. gRPC can use protocol buffers as both **IDL** and also as a **message interchange format** (?)

### Overview ###
1. **A client application can directly call a method on a server application on a different machine as if it were a local object**
	1. Makes it easier to construct distributed applications and services
2. gRPC is based on the idea of:
	1. Defining a service
	2. Specifying the methods that can be called remotely with their parameters and return types
	3. Server side:
		1. Server implements the interface and runs a gRPC server to handle client calls
	4. Client side:
		1. Client has stub (referred to as client in some languages)
			1. It provids the same methods as the server
	5. Communication:
	
			+-------------+                       +---------------+
			| |gRPC Stub| |--- Proto Request ---> | |gRPC Server| |
			| Ruby Client |<-- Proto Response --- |  C++ Service  |
			+-------------+                       +---------------+
			
3. gRPC clients and servers can run and talk to each other **in a variety of environments**
	1. From **servers inside Google to your own desktop**
	2. Can be **written in any of gRPC's supported languages**
	3. Example: **gRPC server can be constructed in Java with clients in Go, Python, or Ruby**
	4. Latest Google APIs will have gRPC versions of their interfaces
		1. Helps us **build Google functionality into our application** (?)

### Working with Protocol Buffers ###
1. gRPC uses [Protocol Buffers](https://protobuf.dev/overview)
	1. Google's mature open-source mechanism for serializing structured data (can also be used with other data formats such as JSON)
2. Steps:
	1. First define the structure of the data we want to serialize in a proto file
		1. proto file: An ordinary text file with a `.proto` extension.
		2. Protocol buffer data is structured as messages
			1. Message: A small logical record of information containing a series of name-value paris called `fields`
		3. Example:
		
				message Person {
					string name = 1;
					int32 id = 2;
					bool has_ponycopter = 3;
				}
				
	2. Use protocol buffer compiler `protoc` to generate data access classes in preferred langauge(s) from the proto definitions
		1. They provide simple accessors to fields
			1. `name()`
			2. `set_name()`
		2. They provide methods to serialize/parse the whole structure to/from raw bytes
			1. Example: C++
				1. Class name: `Person`
					1. Use the class to populate, serialize, and retrieve `Person` protocol buffer messages
		3. Define gRPC services in ordinary proto files with RPC method parameters and return types specified as protocol buffer messages
		
				// The greeter service definition.
				service Greeter {
					// Sends a greeting
					rpc SayHello (HelloRequest) returns (HelloReply) {}
				}
				
				// The request message containing the user's name
				message HelloRequest {
					string name = 1;
				}
				
				// The response message containing the greetings
				message HelloReply {
					string message = 1;
				}
				
			1. gRPC uses `protoc` with a special gRPC plugin to generate code from proto file
				1. Code:
					1. gRPC client
					2. gRPC server
					3. protocol buffer code for populating, serializing, and retrieving message types
				2. [Protocol buffers documentation](https://protobuf.dev/overview)
					1. How to install `protoc` with gRPC plugin in chosen langauge

### Protocol Buffer Versions ###
1. proto3 is used (slightly simplified syntax, useful new features, more languages supported)
2. [proto3 language guide](https://protobuf.dev/programming-guides/proto3)
3. [Reference documentation](https://protobuf.dev/reference)
	1. [formal specification](https://protobuf.dev/reference/protobuf/proto3-spec): for `.proto` file format
4. **Use proto3 with gRPC**:
	1. lets us use full range of gRPC supported languages
	2. Avoid compatibility issues with proto2 clients talking to proto3 servers and vice versa

## Core concepts, architecture and lifecycle ##
### Overview ###
#### Service definition ####
1. gRPC defines a service
	1. It species methods that can be called remotely with their parameters & return types
	2. Uses Protocol Buffers by default as the IDL
		1. For describing service interface
		2. For describing structure of payload messages
	3. **Other alternatives can be used as well**
2. Example:

		service HelloService {
			rpc SayHello (HelloRequest) returns (HelloResponse);
		}
		
		message HelloRequest {
			string greeting = 1;
		}
		
		message HelloResponse {
			string reply = 1;
		}
		
3. gRPC lets us define four kinds of service methods:
	1. **Unary RPCs**:
		1. Client sends a single request to server and gets a single response back (like normal function call)
		
				rpc SayHello (HelloRequest) returns (HelloResponse);
				
	2. **Server streaming RPCs**:
		1. Client sends a request to the server and gets a stream ot read a sequence of messages back
			1. Client reads from a returned stream until there are no more messages
		2. gRPC guarantees message ordering within an individual RPC call.
		
				rpc LotsOfReplies (HelloRequest) returns (stream HelloResponse);
				
	3. **Client streaming RPCs**:
		1. Client writes a sequence of messages and sends them to server (using provided stream)
		2. Once client has finished writing messages, it waits for server to read them and return its response
		3. gRPC guarantees message ordering within an individual RPC call
		
				rpc LotsOfGreetings(stream HelloRequest) returns (HelloResponse);
				
	4. **Bidirectional streaming RPCs**:
		1. Both sides send a sequence of messages using read-write stream
			1. Two streams operate independently
				1. Clients and servers can read and write in whatever order they like
				2. Example: Server could wait to receive all client messages before writing its response or could read a message then write a message, or any other combination of reads and writes
		2. The order of messages in each stream is preserved.
		
				rpc BidiHello(stream HelloRequest) returns (stream HelloResponse);

#### Using the API ####
1. gRPC provides protocol buffer compiler plugins that generate client-side and server-side code
	1. We can call APIs on client side & implement the corresponding APIs on server side
2. On the server side:
	1. Server implements methods declared by service
	2. Server runs a gRPC server to handle client calls
	3. gRPC infra decodes incoming requests, executes service methods, and encodes service responses
3. On the client side:
	1. Client has local object called stub (client in some languages)
	2. It implements the same methods as the service
	3. Client can just call the methods on the local object
		1. Methods wrap parameters for the call in appropriate protocol buffer message type, send the requests to server, return server's protocol buffer responses

#### Synchronous vs. asynchronous ####
1. Synchronous RPC calls block until a response arrives from the server
	1. Closest approximation to abstraction of a procedure call that RPC aspires to (?)
		1. However, networks are inherently asynchronous (latency can vary widely, can error out at times)
			1. Solution: **Start RPC without blocking the current thread**
2. gRPC programming API in many languages comes in both **synchronous** and **asynchronous** flavors
	1. Refer to the **reference documentation of the languages**

### RPC life cycle ###
1. What happens when a gRPC client calls a gRPC server method

#### Unary RPC ####
1. Consider the case where client sends a single request and gets back a single response
	1. Client calls a stub method.
	2. Server is notified that RPC is invoked with client's [metadata](https://grpc.io/docs/what-is-grpc/core-concepts/#metadata), method name & [deadline](https://grpc.io/docs/what-is-grpc/core-concepts/#deadlines) if applicable
		1. **Metadata**: It is info about a particular RPC call (say [authentication details](https://grpc.io/docs/guides/auth/)) as a list of key-value pairs
			1. Values: 
				1. Strings or binary data
			2. Keys: 
				1. Strings
				2. Case insensitive
				3. Consist of ASCII letters, digits, and special characters `-`, `_`, `.`
				4. Must not start with `grpc-` (reserved for gRPC)
				5. Binary valued keys end in `-bin`
				6. ASCII-valued keys do not end in `-bin`
			3. User-defined metadata is not used by gRPC
				1. Allows user to provide info associated with the call to the server and vice-versa
			4. Access to the metadata is language dependent
		2. **Deadlines/ Timeouts**:
			1. gRPC gives the client the option to specify how long they are willing to wait for an RPC to complete before the RPC is termintated with a `DEADLINE_EXCEEDED` error
			2. On server-side, server can query to see
				1. If a particular RPC has timed out
				2. How much time is left to complete the RPC
			3. Specifying deadline/timeout is language specific
				1. Some language APIs work in terms of timeouts (durations of time)
				2. Some language APIs work in terms of a deadline (a fixed point in time)
					1. They may or may not have a default deadline
	3. Server can send back its own initial metadata (which need to be sent before any response) right away, or wait for client's actual request message.
		1. Which happens first, is application-specific
	4. Once server has client's request messages, it does whatever work is necessary to construct and populate a response.
	5. Response is returned to the client (if successful) together with status details (status details: status code, optional status message) and optional trailing metadata
	6. If response status is okay, client gets the response, which completes the call on client's side

#### Server streaming RPC ####
1. It is similar to a unary RPC
	1. But server returns a stream of messages in response to client's request
2. After sending all messages, server's status details (status details: status code, optional status message) and optional trailing metadata are sent to client
	1. This completes processing on the server side
3. Client completes once it has all the server's messages

#### Client streaming RPC ####
1. It is similar to a unary RPC
	1. But client sends a stream of messages to server instead of a single message
2. Server responds with a single message (along with status details and optional metadata)
	1. Typically (but not necessarily) it has received all the client's messages

#### Bidirectional streaming RPC ####
1. The call is initiated by the client invoking the method and server receiving the client metadata, method name, and deadline.
2. Server can either send back its initial metadata or wait until client starts streaming messages
3. Stream processing on both client-side and server-side are application specific
	1. Client & server can read and write messages in any order
		1. Examples:
			1. Server can wait until it has received all of the messages from client OR
			2. Server & client can play "ping-pong"
				1. Client sends a request
				2. Server gets the request
				3. Server sends a response
				4. Client sends another request based on the previous response(s)

#### RPC termination ####
1. In gRPC, client & server make independent and local determinations of success of a call
	1. Conclusions may not match
		1. Example: An RPC might finish successfully on server-side ("I have sent all my responses") but fails on the client side ("The responses arrived after by deadline!")
	2. Server might decide to complete before a client sends all its requests

#### Cancelling an RPC ####
1. Client or server can cancel an RPC at any time
	1. Cancellation termintates RPC immediately
		1. No further work is done
		2. Changes made before cancellation are not rolled back
		
#### Channels ####
1. gRPC channel:
	1. It provides a connection to a gRPC server on a specified host and port
	2. It is used during the creation of a client stub
		1. Clients specify channel arguments to modify gRPC's default behavior
			1. Example: Switching message compression on or off
	3. A channel has state
		1. `connected`
		2. `idle`
	4. How gRPC deals with closing a channel is langauge dependent
	5. Some languages permit querying channel state
	
## FAQ ##
### What is gRPC? ###
1. It is a modern, open-source remote procedure call (RPC) framework
2. It can run anywhere
3. It allows client & server applications to communicate transparently
4. It makes it easier to build connected systems
5. [Motivation & Design Principles](https://grpc.io/blog/principles/) - background on why gRPC was created

### What does gRPC stand for? ###
1. gRPC Remote Procedure Calls

### Why should I want to use gRPC? ###
1. Usage scenarios:
	1. Low latency, highly scalable, distributed systems
	2. Developing mobile clients which are communicating to a cloud server
	3. Designing a new protocol that needs to be:
		1. Accurate
		2. Efficient
		3. Language independent
	4. Layered design to enable extension
		1. Authentication
		2. Load balancing
		3. Logging
		4. Monitoring
		5. ...

### Who's using this and why? ###
1. gRPC is [Cloud Native Computing Foundation (CNCF)](https://cncf.io/)
2. Google has been using underlying technologies and concepts
	1. Cloud products
	2. Externally facing APIs
3. Other companies:
	1. Square
	2. Netflix
	3. CoreOS
	4. Docker
	5. CockroachDB
	6. Cisco
	7. Juniper Networks
	8. ...

### Which programming languages are supported? ###
1. [Officient support](https://grpc.io/docs/#official-support)
	1. C/C++
		1. GCC
		2. Clang
		3. Visual Studio
	2. C#
		1. .Net Core
		2. Mono
	3. Dart
	4. Go
	5. Java
	6. Kotlin
	7. Node.js
	8. Objective-C
	9. PHP
	10. Python
	11. Ruby

### How do I get started using gRPC? ###
1. [Installation](https://grpc.io/docs/quickstart/)
2. [gRPC GitHub org page](https://github.com/grpc)
	1. Pick the runtime or language
	2. Follow README instructions

### Which license is gRPC under? ###
1. Apache 2.0

### How can I contribute? ###
1. [Contributors](https://grpc.io/community/#contribute)
	1. Community feedback
	2. Additions
	3. Bugs
2. [Submit ideas for projects around gRPC](https://github.com/grpc/grpc-contrib/blob/master/CONTRIBUTING.md)
3. [List of projects](https://github.com/grpc-ecosystem)

### Where is the documentation? ###
1. [https://grpc.io/docs/](https://grpc.io/docs/)

### What is the road map? ###
1. New features are designed and approved for implementation through an RFC process
	1. Tracked in the following [repository](https://github.com/grpc/proposal)

### How long are gRPC releases supported for? ###
1. No LTS releases
	1. Current release
	2. Latest release
	3. Prior release
2. Support: Bug fixes, security fixes

### What is the gRPC versioning policy? ###
1. [See here](https://github.com/grpc/grpc/blob/master/doc/versioning.md)

### What is the latest gRPC version? ###
1. Latest release tag: v1.58.0

### When do gRPC releases happen? ###
1. Tip of the master branch is stable all the times
	1. Project, across various runtimes, targets to ship checkpoint releases every 6 weeks on a best effort basis
		1. [Release schedule](https://github.com/grpc/grpc/blob/master/doc/grpc_release_schedule.md)

### How can I report a security vulnerability in gRPC? ###
1. [Process](https://github.com/grpc/proposal/blob/master/P4-grpc-cve-process.md)

### Can I use it in the browser? ###
1. [gRPC-Web](https://github.com/grpc/grpc-web) - Generally available

### Can I use gRPC with my favorite data format (JSON, Protobuf, Thrift, XML)? ###
1. Yes
	1. gRPC is extensible to support multiple content types
	2. Other content types: FlatBuffers, Thrift

### Can I use gRPC in a service mesh? ###
1. Yes
	1. gRPC applications can be deployed in a service mesh like any other application
	2. gRPC also supports [xDS APIs](https://www.envoyproxy.io/docs/envoy/latest/api-docs/xds_protocol)
		1. Enables deploying gRPC applications in a service mesh without sidecar proxies
	3. [Proxyless service mesh features supported in gRPC](https://github.com/grpc/grpc/blob/master/doc/grpc_xds_features.md)

### How does gRPC help in mobile application development? ###
1. gRPC and Protobuf provide an easy way to define a service & auto-generate reliable client libraries for iOS, Android & servers (back-end)
	1. Clients can take advantage of **advanced streaming and connection features**
		1. Helps **save bandwidth**
		2. Do more over **fewer TCP connections**
		3. **Save CPU usage & battery life**

### Why is gRPC better than any binary blob over HTTP/2? ###
1. gRPC is a **set of libraries that provides higher-level features consistently across platforms that common HTTP libraries typically do not provide**
	1. Examples:
		1. Interaction with **flow-control at the application layer**
		2. **Cascading call-cancellation**
		3. **Load balancing** & **failover**

### Why is gRPC better/worse than REST? ###
1. gRPC follows HTTP semantics over HTTP/2 but full-duplex streaming is allowed
	1. Divergence from REST conventions:
		1. Use of static paths for performance reasons during call dispatch
			1. Call parameter, query parameters, payload body parsing adds latency and complexity
		2. Formalization of errors that are applicable directly to API use cases as compared to HTTP status codes

### How do you pronounce gRPC? ###
1. jee-arr-pee-see

## Languages ##
### Suported Languages ###
1. Pages:
	1. Quick start
	2. Tutorials
	3. API reference
2. Languages:
	1. C++: [https://grpc.io/docs/languages/cpp/](https://grpc.io/docs/languages/cpp/)
	2. Go: [https://grpc.io/docs/languages/go/](https://grpc.io/docs/languages/go/)
	3. Java: [https://grpc.io/docs/languages/java/](https://grpc.io/docs/languages/java/)
	4. Node: [https://grpc.io/docs/languages/node/](https://grpc.io/docs/languages/node/)
	5. Python: [https://grpc.io/docs/languages/python/](https://grpc.io/docs/languages/python/)
	
# Java #
## Quick Start ##
### Prerequisites ###
1. JDK 7 or higher

### Get the Example Code ###
1. [Download the repo as a zip file](https://github.com/grpc/grpc-java/archive/v1.58.0.zip)
2. Clone repo:

		git clone -b v1.58.0 --depth 1 https://github.com/grpc/grpc-java
		
3. Change to examples directory:

		cd grpc-java/examples

### Run the Example ###
1. Compile the client and server:

		./gradlew installDist
		
2. Run the server:

		./build/install/examples/bin/hello-world-server
		
3. Run the client from another terminal

		./build/install/examples/bin/hello-world-client

### Update the gRPC Service ###
1. Adding another server method
	1. Service is defined using protocol buffers:
		1. [protocol buffers](https://developers.google.com/protocol-buffers)
	2. How to define a service in `.proto` file:
		1. [Basic tutorial](https://grpc.io/docs/languages/java/basics/)
2. Both client and server have `SayHello()` RPC method
	1. It takes `HelloRequest` parameter from client
	2. It returns `HelloReply` from server
3. Definition:

		// The greeting service definition.
		service Greeter {
			// Sends a greeting
			rpc SayHello (HelloRequest) returns (HelloReply) {}
		}
		
		// The request message containing the user's name
		message HelloReques {
			string name = 1;
		}
		
		// The response message containing the greetings
		message HelloReply {
			string message = 1;
		}
		
4. Open `src/main/proto/helloworld.proto` and add a new `SayHelloAgain()` method with same request and response types as `SayHello()`:

		// The greeting service definition
		service Greeter {
			// Sends a greeting
			rpc SayHello (HelloRequest) returns (HelloReply) {}
			// Sends another greeting
			rpc SayHelloAgain (HelloRequest) returns (HelloReply) {}
		}
		
		// ...

### Update the App ###
1. The build process regenerates `GreeterGrpc.java` file which contains gRPC client and server classes

### Update the Server ###
### Update the Client ###
### Run the Updated App ###
### What's Next ###
