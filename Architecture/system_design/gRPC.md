# gRPC #
1. Topic: What is gRPC? When should we use it?
2. gRPC
	1. It is an open source RPC framework by Google
	2. What is an RPC?
		1. Local procedure call is a function call within a process
		2. RPC: Enables one machine to invoke code on another machine
			1. gRPC is a popular implementation of RPC
				1. Used to connect large number of microservices running within and across data centres
	3. Why is it so popular?
		1. Has thriving developer ecosystem
			1. gRPC Core (C, C++, Ruby, Node.js, Python, PHP, C#, Objective-C)
			2. gRPC Java (Java gRPC implementation. HTTP/2 based RPC)
				1. What is HTTP/2?
					1. It is the second version of HTTP protocol
					2. Advantages:
						1. Makes applications faster, simpler, more robust since it has improved on the drawbacks of HTTP version 1.1
					3. Goals:
						1. Enable request and response multiplexing
						2. Header compression
						3. Compatible with methods, status codes, URIs and header fields defined by HTTP/1.1 standard
						4. Optimized prioritization of requests
							1. Ensures loading for optimal user experience is as fast as possible
						5. Support for server-side push
						6. Server-side backwards compatibility
							1. Ensures that servers can serve clients supporting HTTP/1.1
						7. Transforming to a binary protocol from text-based HTTP/1.1
					4. Features
						1. **Binary:** Commands use 1s and 0s and not text
						2. **Multiplex:** Permits multiple requests and responses to be sent at the same time
						3. **Compression:** Compresses headers requested previously to make things more efficient
						4. **Stream prioritization:** Allows for exchange of successive streams at one time
						5. **Server push:** Server can send additional info needed for a request before it is requested
						6. **Increased security:** HTTP/2 is supported through encrypted connnections
			3. Makes it easy to develop production quality and type safe APIs that scale well
		2. It uses protobuf (data interchange format)
			1. It is a language agnostic and platform agnostic mechanism for encoding structured data
			2. It supports strongly typed schema definition
				1. Structure of data over the wire is defined in a `proto` file
				
						message Author {
							string name = 1;
							int32 id = 2;
						}

			3. Broad tooling support to turn schema defined in proto file into data access classes for all popular programming languages
			4. gRPC service is also defined in a proto file by specifying rpc methods, parameters and return types

					service Publisher {
						rpc SignBook (SignRequest) returns (SignReply) {}
					}

					message SignRequest {
						string name = 1;
					}

					message SignReply {
						string signature = 1;
					}

				1. Tooling is used to generate gRPC client and server code from the proto file
					1. Developers use the generated servers and clients to make rpc class
						1. Developers can independently choose the language for client and/or server depending on the use-case
		3. It is high performance out of the box
			1. Reasons?
				1. It is very efficient binary encoding format (much faster than json)
					1. Binary encoding - Protobuf
						1. type:
							1. 0b/string
							2. 0a/i64
							3. 0a/i64
						2. field tag
							1. 00 01
							2. 00 02
							3. 00 03
						3. length
							1. 00 08
						4. value
							1. k e y b o a r d
								1. 6B 65 79 62 6F 61 72 64