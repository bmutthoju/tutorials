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

#### Using the API ####
#### Synchronous vs. asynchronous ####
### RPC life cycle ###
#### Unary RPC ####
#### Server streaming RPC ####
#### Client streaming RPC ####
#### Bidirectional streaming RPC ####
#### Deadlines/Timeouts ####
#### RPC termination ####
#### Cancelling an RPC ####
#### Metadata ####
#### Channels ####