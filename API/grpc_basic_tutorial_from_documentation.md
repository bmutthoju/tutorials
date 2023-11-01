## Basics Tutorial ##
1. Tutorial: Basic Java programmer's introduction to working with gRPC
2. Learnings:
	1. Define a service in `.proto` file
	2. Generate server and client code using protocol buffer compiler
	3. Use Java gRPC API to write a simple client and server for our service
3. Pre-requisites:
	1. [Introduction to gRPC](https://grpc.io/docs/what-is-grpc/introduction/)
	2. [Protocol Buffers](https://protobuf.dev/overview)

### Why Use gRPC? ###
1. Example: Consider a simple route mapping application
	1. Clients can get info about:
		1. Features on their route
		2. Prepare summary of their route
		3. Exchange route info such as traffic updates with server and clients
2. Wite gRPC, we can define service once in `.proto` file and generate clients and servers in any gRPC supported langauges
	1. The generated code can be run in many environments:
		1. servers in large data centers
		2. tablet
		3. ...
3. The complexity of communication between different languages and environments is handled for us by gRPC
4. We can also work with protocol buffers
	1. Supports:
		1. Efficient serialization
		2. Simple IDL
		3. Easy interface updating

### Example Code and Setup ###
1. [https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/routeguide](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/routeguide)
2. Clone the latest release in `grpc-java` repo by running:

		git clone -b v1.58.0 --depth 1 https://github.com/grpc/grpc-java
		
3. Go to `grpc-java/examples`

		cd grpc-java/examples

### Defining the Service ###
1. Step 1: Define gRPC service and the method *request* and *response* types using protocol buffers
	1. Example: [grpc-java/examples/src/main/proto/route_guide.proto](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/routeguide)
2. `java_package` file option in our `.proto` file:

		option java_package = "io.grpc.examples.routeguide";
		
	1. Specifies the package that we want to use for our generated Java classes
		1. If no explicit `java_package` option is given in `.proto` file, by default the proto package (specified using the "package" keyword) will be used.
			1. Proto packages do not make good Java packages since proto packages are not expected to start with reverse domain names
		2. If we generate code in another language from the `.proto` file, `java_package` option has no effect
3. Steps:
	1. Specify named `service` in `.proto` file to define a service:

		service RouteGuide {
			...
		}
		
	2. Define `rpc` methods inside the service definition with their request and response types
		1. Four kinds of service methods can be defined
			1. Simple RPC:
				1. Client sends a request to the server using the stub and waits for a response to come back (like a normal function call)
				
						// Obtains the feature at a given position.
						rpc GetFeature(Point) returns (Feature) {}
						
			2. Server-side Streaming RPC:
				1. Client sends a request to the server and gets a stream to read a sequence of messages back
				2. Client reads from returned stream until there are no more messages
				3. Place a `stream` keyword before response type:
				
						// Obtains the Features available within the given Rectangle. Results are
						// streamed rather than returned at once (e.g. in a response message with a
						// repeated field), as the rectangle may cover a large area and contain a
						// hug number of features.
						rpc ListFeatures(Rectangle) returns (stream Feature) {}
						
			3. Client-side streaming RPC:
				1. Client writes a sequence of messages and sends them to the server using the provided stream
				2. Once client has finished writing the messages, it waits for the server to read them all and return its response
				3. We specify client-side streaming method by placing `stream` keyword before the request type.
				
						// Accepts a stream of Points on a route being traversed, returning a
						// RouteSummary when traversal is completed.
						rpc RecordRoute(stream Point) returns (RouteSummary) {}  
						
			4. Bidirectional streaming RPC:
				1. Both sides send a sequence of messages using a read-write stream
				2. Two streams operate independently
					1. Clients and servers can read and write in whatever order they like
						1. Example: server could wait to receive all the clietn messages before writing its responses
							1. Server could alternatively read a message then write a message
							2. Server could use any other combination of reads and writes
					2. **Order of messages in each stream is preserved**
				3. Defined by placing `stream` keyword before both the request and the response
				
						// Accepts a stream of RouteNotes sent while a route is being traversed,
						// while receiving other RouteNotes (e.g. from other users).
						rpc RouteChat(stream RouteNote) returns (stream RouteNote) {}
						
	3. Define protocol buffer message type definitions for all the request and response types used in the service methods - example, `Point` message type:
	
			// Points are represented as lattitude-longitude pairs in the E7 representation
			// (degrees multiplied by 10**7 and rounded to the nearest integer).
			// Latitudes should be in the range +/- 90 degrees and longitude should be in
			// the range +/- 180 degrees (inclusive).
			message Point {
				int32 latitude = 1;
				int32 longitude = 2;
			}

### Generating Client and Server Code ###
1. We need to generate gRPC client and server interfaces from the `.proto` service definition.
	1. This can be done using the protocol buffer compiler `protoc` with a special gRPC Java plugin.
		1. Use the [proto3 compiler](https://github.com/google/protobuf/releases) to generate gRPC services
			1. Supports proto2 and proto3 syntax
2. When using Gradle or Maven, `protoc` build plugin can generate necessary code as part of build
	1. Refer to [grpc-java README](https://github.com/grpc/grpc-java/blob/master/README.md)
3. The following classes are generated from service definition:
	1. `Feature.java`, `Point.java`, `Rectangle.java`, ... which contain all the protocol buffer code to populate, serialize, and retrieve our request and response message types
	2. `RouteGuideGrpc.java` which contains (along with some other useful code):
		1. Base class for `RouteGuide` servers to implement `RouteGuideGrpc.RouteGuideImplBase` with all the methods defined in the `RouteGuide` service
		2. *Stub* classes that clients can use to talk to a `RouteGuide` server

### Constructing the Server ###
1. Creation of `RouteGuide` server
	1. Two parts to making our `RouteGuide` service:
		1. Overriding service base class generated from our service definition:
			1. Doing the actual "work" of our service
		2. Running a gRPC server to listen for requests from cients and return the service responses
2. Example `RouteGuide` server: [https://github.com/grpc/grpc-java/blob/master/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideServer.java](https://github.com/grpc/grpc-java/blob/master/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideServer.java)

### Implementing RouteGuide ###
1. The `RouteGuideService` class extends `RouteGuideGrpc.RouteGuideImplBase` abstract class:

		private static class RouteGuideService extends RouteGuideGrpc.RouteGuideImplBase {
			...
		}

#### Simple RPC ####
1. `RouteGuideService` implements all service methods
2. `GetFeature()` - gets a `Point` from the client and returns the corresponding feature information from its database in a `Feature`
	
		@Override
		public void getFeature(Point request, StreamObserver<Feature> responseObserver) {
			responseObserver.onNext(checkFeature(request));
			responseObserver.onCompleted();
		}
		
		...
		
		private Feature checkFeature(Point location) {
			for (Feature feature : features) {
				if (feature.getLocation().getLatitude() == location.getLatitude() && feature.getLocation().getLongitude() == location.getLongitude()) {
					return feature;
				}
			}
		}
		
		// No feature was found, return an unnamed feature.
		return Feature.newBuilder().setName("").setLocation(location).build();
		
	1. `getFeature()` takes two parameters:
		1. `Point`: the request
		2. `StreamObserver<Feature>`: a response observer
			1. A special interface for the server to call with its response
	2. To return a response to client and complete the call:
		1. Construct and populate a `Feature` response object to return to the client (as specified in service definition).
			1. Example: Do it in `checkFeature()` method
		2. Use response observer's `onNext()` method to return the `Feature`
		3. Use response observer's `onCompleted()` method to specify that we've finished dealing with the RPC

#### Server-Side Streaming RPC ####
1. `ListFeatures` is server-side streaming RPC
	1. Used to send multiple `Feature`s to client
2. Code example:

		private final Collection<Feature> features;
		
		...
		
		@Override
		public void listFeatures(Rectangle request, StreamObserver<Feature> responseObserver) {
			int left = min(request.getLo().getLongitude(), request.getHi().getLongitude());
			int right = max(request.getLo().getLongitude(), request.getHi().getLongitude());
			int top = max(request.getLo().getLatitude(), request.getHi().getLatitude());
			int bottom = min(request.getLo().getLatitude(), request.getHi().getLatitude());
			
			for (Feature feature : features) {
				if (!RouteGuideUtil.exists(feature)) {
					continue;
				}
				
				int lat = feature.getLocation().getLatitude();
				int lon = feature.getLocation().getLongitude();
				if (lon >= left && lon <= right && lat >= bottom && lat <= top) {
					responseObserver.onNext(feature);
				}
			}
			responseObserver.onCompleted();
		}
		
	1. The method gets a request object (`Rectangle` in which client wants to find `Feature`s) and a `StreamObserver` response observer
	2. We get as many `Feature` objects as we need to return to the client (based on whether they are inside the request `Rectangle`)
		1. We write them in turn to the response observer using `onNext()` method
	3. We use `onCompleted()` method to tell gRPC that we've finished writing responses

#### Client-Side Streaming RPC ####
1. More complicated code.
2. Client-side streaming method `RecordRoute()`
	1. Client sends a stream of `Point`s
	2. We need to return a single `RouteSummary` with information about their trip
3. Code:

		@Override
		public StreamObserver<Point> recordRoute(final StreamObserver<RouteSummary> responseObserver) {
			return new StreamObserver<Point> () {
				int pointCount;
				int featureCount;
				int distance;
				Point previous;
				long startTime = System.nanoTime();
				
				@Override
				public void onNext(Point point) {
					pointCount++;
					if (RouteGuideUtil.exists(checkFeature(point))) {
						featureCount++;
					}
					
					// For each point after the first, add the incremental distance from the previous point
					// to the total distance value.
					if (previous != null) {
						distance += calcDistance(previous, point);
					}
					previouis = point;
				}
				
				@Override
				public void onError(Throwable t) {
					logger.log(Level.WARNING, "Encountered error in recordRoute", t);
				}
				
				@Override
				public void onCompleted() {
					long seconds = NANOSECONDS.toSeconds(System.nanoTime() - startTime);
					responseObserver.onNext(RouteSummary.newBuilder()
						.setPointCount(pointCount)
						.setFeatureCount(featureCount)
						.setDistance(distance)
						.setElapsedTime((int) seconds)
						.build()
					);
					responseObserver.onCompleted();
				}
			};
		}
		
	1. Method gets a `StreamObserver` response observer parameter
	2. It returns a `StreamObserver` for the client to write its `Point`s
	3. Method body instantiates an anonymous `StreamObserver` to return. In which we:
		1. Override the `onNext()` method to get features and other information each time the client writes a `Point` to the message stream.
		2. Override the `onCompleted()` method (called when client has finished writing messages) to populate and build `RouteSummary`
			1. We then call method's own response observer's `onNext()` with `RouteSummary`
			2. We then call its `onCompleted()` method to finish the call from server side

#### Bidirectional Streaming RPC ####
1. Bidirectional streaming RPC `RouteChat()`

		@Override
		public StreamObserver<RouteNote> routeChat(final StreamObserver<RouteNote> responseObserver) {
			return new StreamObserver<RouteNote>() {
				@Override
				public void onNext(RouteNote note) {
					List<RouteNote> notes = getOrConstructNotes(note.getLocation());
					
					// Respond with all previous notes at this location.
					for (RouteNote prevNote : notes.toArray(new RouteNote[0])) {
						responseObserver.onNext(prevNote);
					}
					
					// Now add the new note to the list
					notes.add(note);
				}
				
				@Override
				public void onError(Throwable t) {
					logger.log(Level.WARNING, "Encountered error in routeChat", t);
				}
				
				@Override
				public void onCompleted() {
					responseObserver.onCompleted();
				}
			}
		}
		
	1. We get and return a `StreamObserver` response observer
		1. We return values via method's response observer while the client is still writing messages to their message stream
		2. Syntax is same as client-streaming and server-streaming methods
		3. Each side will always get the other's messages in the order they were written.
			1. But the client and server can read and write in any order
				1. Why? Streams operate completely independently

#### Starting the Server ####
1. After implementing our methods, we need to start up a gRPC server so that clients can actually use our service
	1. The following code shows how we do it for `RouteGuide` service:
	
			public RouteGuideServer(int port, URL featureFile) throws IOException {
				this(ServerBuilder.forPort(port), port, RouteGuideUtil.parseFeatures(featureFile));
			}
			
			/** Construct a RouteGuide server using serverBuilder as a base and features as data. */
			public RouteGuideServer(ServerBuilder<?> serverBuilder, int port, Collection<Feature> features) {
				this.port = port;
				server = serverBuilder.addService(new RouteGuideService(features))
					.build();
			}
			...
			public void start() throws IOException {
				server.start();
				logger.info("Server started, listening on " + port);
			}
			
		1. We build and start server using `ServerBuilder`:
			1. How to do this?
				1. Specify address and port we want to use to listen for client requests using builder's `forPort()` method.
				2. Construct an instance of our service implementation class `RouteGuideService` and pass it to the builder's `addService()` method.
				3. Call `build()` and `start()` on builder to construct and start an RPC server for our service.

### Constructing the Client ###
1. Constructing a client for `RouteGuide` service
	1. Complete example: [https://github.com/grpc/grpc-java/blob/master/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideClient.java](https://github.com/grpc/grpc-java/blob/master/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideClient.java)

#### Instantiating a Stub ####
1. To call service method, we need to construct a stub:
	1. a blocking/synchronous stub: RPC call waits for the server to respond
		1. It will either send response or raise exception
	2. a non-blocking/asynchronous stub: Makes non-blocking calls to server, where response is returned asynchronously.
		1. We can make certain types of streaming call only using asynchronous stub
2. Step 1: Construct a gRPC channel for the stub
	1. Specify server address and port we want to connect to:
	
			public RouteGuideClient(String host, int port) {
				this(ManagedChannelBuilder.forAddress(host, port).usePlainText());
			}
			
			/** Construct client for accessing RouteGuide server using the existing channel..*/
			public RouteGuideClient(ManagedChanneBuilder<?> channelBuilder) {
				channel = channelBuilder.build();
				blockingStub = RouteGuideGrpc.newBlockingStub(channel);
				asyncStub = RouteGuideGrpc.newStub(channel);
			}
			
	2. We can use `ManagedChannelBuilder` to construct a channel
	3. The channel can be used to construct stubs using `newStub` and `newBlockingStub` methods provided in `RouteGuideGrpc` class we generated from `.proto`
	
			blockingStub = RouteGuideGrpc.newBlockingStub(channel);
			asyncStub = RouteGuideGrpc.newStub(channel);

#### Calling Service Methods ####
1. How to call service methods?

##### Simple RPC #####
1. Calling simple RPC `GetFeature` on blocking stub is straightforward as calling a local method:

		Point request = Point.newBuilder().setLatitude(lat).setLongitude(lon).build();
		try {
			feature = blockingStub.getFeature(request);
		} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return;
		}
	
	1. We construct and populate a request protocol buffer object (in our case `Point`)
	2. We pass it to `getFeature()` method on blocking stub & get back `Feature`
	3. If an error occurs, it is encoded as a `Status` which can be obtained from `StatusRuntimeException`

##### Server-Side Streaming RPC #####
1. Server-side streaming call to `ListFeatures`
2. It returns a stream of geographical `Feature`s

		Rectangle request = Rectangle.newBuilder()
			.setLo(
				Point.newBuilder()
					.setLatitude(lowLat)
					.setLongitude(lowLon)
					.build()
			)
			.setHi(
				Point.newBuilder()
				.setLatitude(hiLat)
				.setLongitude(hiLon)
				.build()
			)
			.build();
			
		Iterator<Feature> feature;
		try {
			features = blockingStub.listFeatures(request);
		} catch (StatusRuntimeException e) {
			logger.log(Level.WARNING, "RPC failed: {0}", e.getStatus());
			return;
		}
		
	1. It returns an instead of returning a single `Feature`
		1. Client can use the `Iterator` to read all the returned `Feature`s

##### Client-Side Streaming RPC #####
1. The client-side streaming method `RecordRoute` where we send a stream of `Point`s to the server and get back a single `RouteSummary`
2. **We need to use the asynchronous stub**
3. Implementation:

		public void recordRoute(List<Feature> features, int numPoints) throws InterruptedException {
			info("*** RecordRoute");
			final CountDownLatch finishLatch = new CountDownLatch(1);
			StreamObserver<RouteSummary> responseObserver = new StreamObserver<RouteSummary>() {
				@Override
				public void onNext(RouteSummary summary) {
					info("Finished trip with {0} points. Passed {1} features. " + "Travelled {2} meters. It tool {3} seconds.", summary.getPointCount(),
					summary.getFeatureCount(),
					summary.getDistance(),
					summary.getElapsedTime());
				}
				
				@Override
				public void onError(Throwable t) {
					Status status = Status.fromThrowable(t);
					logger.log(Level.WARNING, "RecordRoute Failed: {0}", status);
					finishLatch.countDown();
				}
				
				@Override
				public void onCompleted() {
					info("Finished RecordRoute");
					finishLatch.countDown();
				}
			};
			
			StreamObserver<Point> requestObserver = asyncStub.recordRoute(resonseObserver);
			
			try {
				// Send numPoints points randomly selected from the features list.
				Random rand = new Random();
				for (int i = 0; i < numPoints; i++) {
					int index = rand.nextInt(features.size());
					Point point = features.get(index).getLocation();
					info("Visiting point {0}, {1}", RouteGuideUtil.getLatitude(point), RouteGuideUtil.getLongitude(point));
					requestObserver.onNext(point);
					// Sleep for a bit before sending the next one.
					Thread.sleep(rand.nextInt(1000) + 500);
					if (finishLatch.getCount() == 0) {
						// RPC completed or errored before we finished sending.
						// Sending further requests won't error, but they will just be thrown away.
						return;
					}
				}
			} catch (RuntimeException e) {
				// Cancel RPC
				requestObserver.onError(e);
				throw e;
			}
			// Mark the end of requests
			requestObserver.onCompleted();
			
			// Receiving happens asynchronously
			finishLatch.await(1, TimeUnit.MINUTES);
		}
		
	1. `StreamObserver` needed to be created to call the method
		1. It implements a special interface for the server to call with its `RouteSummary` response
		2. We:
			1. Override `onNext()` method to print out returned info when the server writes a `RouteSummary` to the message stream.
			2. Override `onCompleted()` method (called when the server has completed the call on its side) to reduce a `CountDownLatch` that we can check to see if server has finished writing.
	2. We then pass `StreamObserver` to asynchronous stub's `recordRoute()` method and get back our own `StreamObserver` request observer to write our `Point`s to send to server
	3. Once we finished writing points, we use request observer's `onCompleted()` method to tell gRPC that we've finished writing on client side

##### Bidirectional Stream RPC #####
1. Bidirectional streaming RPC `RouteChat()`
2. Implementation:

		public void routeChat() throws Exception {
			info("*** RouteChat");
			final CountDownLatch finishLatch = new CountDownLatch(1);
			StreamObserver<RouteNote> requestObserver = asyncStub.routeChat(new StreamObserver<RouteNote>() {
				@Override
				public void onNext(RouteNote note) {
					info("Got message \"{0}\" at {1}, {2}",
					note.getMessage(),
					note.getLocation().getLatitude(),
					note.getLocation().getLongitude());
				}
				
				@Override
				public void onError(Throwable t) {
					Status status = Status.fromThrowable(t);
					logger.log(Level.WARNING, "RouteChat Failed: {0}", status);
					finishLatch.countDown();
				}
				
				@Override
				public void onCompleted() {
					info("Finished RouteChat");
					finishLatch.countDown();
				}
			});
			
			try {
				RouteNote[] requests = {
					newNote("First message", 0, 0),
					newNote("Second message", 0, 1),
					newNote("Third message", 1, 0),
					newNote("Fourth message", 1, 1)
				};
				
				for (RouteNote request : requests) {
					info("Sending message \"{0}\" at {1}, {2}",
					request.getMessage(),
					request.getLocation().getLatitude(),
					request.getLocation().getLongitude());
					requestObserver.onNext(request);
				}
			} catch (RuntimeException e) {
				// Cancel RPC
				requestObserver.onError(e);
				throw e;
			}
			// Mark the end of requests
			requestObserver.onCompleted();
			
			// Receiving happens asynchronously
			finishLatch.await(1, TimeUnit.MINUTES);
		}
		
	1. We get and return a `StreamObserver` response observer
		1. Except, this time we send values via our method's response observer while server is still writing messages to their message stream
	2. Each side will always get the other's messages in the order they were written
	3. Both client and server can read and write in any order
		1. The streams operate completely independently

### Try it Out ###
1. [https://github.com/grpc/grpc-java/blob/master/examples/README.md](https://github.com/grpc/grpc-java/blob/master/examples/README.md)