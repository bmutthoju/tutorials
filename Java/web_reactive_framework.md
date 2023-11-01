# Web Reactive Framework #
1. Basic info on Spring Web Reactive support in Spring Framework 5

## Introduction ##
### Reactive Programming ###
1. Reactive programming:
	1. It is about **non-blocking applications** that are **asynchronous** and **event-driven** and **require a small number of threads to scale**
	2. Backpressure: mechanism to ensure producers do not overwhelm consumers
		1. Example: Consider a pipeline of reactive components that extend from database to HTTP socket
			1. When HTTP client is slow, data repository slows down or stops until capacity is freed up
2. Programming model used:
	1. A major shift from imperative style logic to a declarative composition of async logic
		1. Comparable to using `CompletableFuture` in Java 8 and composing follow up actions using lambda expressions
3. Extended intro on reactive programming:
	1. [Notes on Reactive Programming](https://spring.io/blog/2016/06/07/notes-on-reactive-programming-part-i-the-reactive-landscape)

### Spring Web Reactive Types ###
1. [Reactive Streams](https://github.com/reactive-streams/reactive-streams-jvm#reactive-streams) are used by Spring Framework 5 as contract for communicating backpressure across async components and libraries
	1. It is a specification created through industry collaboration adoped in Java 9 as `java.util.concurrent.Flow`
2. Spring Framework uses [Reactor](https://projectreactor.io/) internally for its own reactive support
	1. Reactor: It is a Reactive Streams implementation that further extends the basic Reactive Streams `Publisher` contract with `Flux` and `Mono` composable API types to provide declarative operations on data sequences of `0..N` and `0..1`
		1. Spring Framework exposes `Flux` and `Mono` in its own reactive APIs
	2. At application level, Spring provides choice and fully supports the use of `RxJava`
		1. ["Understanding Reactive Types"](https://spring.io/blog/2016/04/19/understanding-reactive-types)

## Spring Web Reactive Overview ##
### Spring Web Reactive Module ###
1. `spring-web-reactive` module
	1. Supports same `@Controller` programming model as Spring MVC
	2. Executed on **reactive, non-blocking engine**
2. Comparison:
	1. Common features:
		1. `@Controller`
		2. `@RequestMapping`
	2. Spring MVC vs Spring Web Reactive
		1. Spring MVC vs Spring Web Reactive
		2. Servlet API vs Reactive HTTP
		3. Servlet Container vs Servlet 3.1, Netty, Undertow
3. Spring Web Reactive:
	1. Makes use of **Servlet 3.1**
		1. **Servlet 3.1**: **Non-blocking I/O and runs on Servlet 3.1 containers**
	2. The runtime is adapted to a set of shared, reactive `ServerHttpRequest` and `ServerHttpResponse` abstractions
		1. That expose request and response body as `Flux<DataBuffer>`
		2. Has full backpressure support on read and write side
	3. `spring-core` modules provides reactive `Encoder` and `Decoder` contracts that enable serialization of a `Flux` of bytes to and from typed objects
		1. `spring-web` adds JSON (Jackson) and XML (JAXB) implementations for use in web applications and others **for SSE streaming** and **zero-copy file transfer**

### Reactive Web Client ###
## Getting Started ##
### Spring Boot Starter ###
### Manual Bootstrapping ###
### Extent of Support in 5.0 M1 ###

# Q & A #
## What is `Flux<DataBuffer>` in Spring Web Reactive? ##
In Spring Web Reactive, `Flux<DataBuffer>` **represents a stream of data buffers**.

Spring Web Reactive is a module in the Spring Framework that **provides support for building reactive web applications**. It **allows you to handle HTTP requests and responses in a non-blocking manner using reactive programming concepts**.

A `Flux<DataBuffer>` is a **reactive type that emits a sequence of** `DataBuffer` **objects**. `DataBuffer` **represents a chunk of data**, typically used for reading or writing data in a non-blocking manner. It is **often used for handling large data streams, such as file uploads or downloads**.

With `Flux<DataBuffer>`, you **can read or write data in a streaming fashion**. For example, **when handling an HTTP request, you can use** `Flux<DataBuffer>` **to read the request body as a stream of data buffers**. Similarly, **when sending a response, you can write the response body as a stream of data buffers using** `Flux<DataBuffer>`.

Here's a simple example of using `Flux<DataBuffer>` to read and write data:

		@RequestMapping(value = "/upload", method = RequestMethod.POST)
		public Mono<Void> upload(@RequestBody Flux<DataBuffer> body) {
			// Process the uploaded data buffers
			return body.doOnNext(dataBuffer -> {
				// Process each data buffer
				// ...
			}).then();
		}

		@RequestMapping(value = "/download", method = RequestMethod.GET)
		public Flux<DataBuffer> download() {
			// Create a Flux of DataBuffers to represent the response body
			Flux<DataBuffer> responseBody = Flux.just(createDataBuffer("Hello"), createDataBuffer("World"));

			return responseBody;
		}

In the above example, the **upload method receives a** `Flux<DataBuffer>` as the request body, **allowing you to process the uploaded data buffers as they arrive**. The **download method returns a** `Flux<DataBuffer>` **representing the response body, which will be streamed back to the client**.

Note that `DataBuffer` is **an abstraction and can be implemented by different classes depending on the underlying technology or libraries you use**. For example, **in Spring WebFlux, the default implementation is** `DefaultDataBuffer`, **which is backed by** a `ByteBuffer`. Other implementations may exist for different scenarios or libraries.

## What is `ByteBuffer`? ##
`ByteBuffer` is a class in Java's `java.nio` package that provides a way to store and manipulate binary data in memory. It is a **fundamental part of the NIO (New I/O) framework introduced in Java 1.4**, which provides **an alternative to the traditional I/O operations based on streams**.

A `ByteBuffer` is a **container for a fixed-size sequence of bytes**. It **represents a resizable, mutable buffer that can be used for reading from or writing to, allowing efficient manipulation of binary data**.

Here are some key features and functionalities provided by `ByteBuffer`:

1. **Capacity and Position**: A `ByteBuffer` **has a fixed capacity defined at its creation, which represents the maximum number of bytes it can hold**. It also **maintains a position, which is the index of the next byte to be read or written**. The **position can be updated as bytes are read or written**.
2. **Read and Write Operations**: `ByteBuffer` **provides various methods for reading and writing data**, such as `get()`, `put()`, `getInt()`, `putInt()`, etc. These **methods allow you to read or write data of different types** (e.g., bytes, integers, characters) **from or to the buffer at the current position**.
3. **Flipping and Rewinding**: `ByteBuffer` provides methods like `flip()` and `rewind()` **to control the position and limit of the buffer**. The `flip()` method **sets the position to zero and the limit to the current position, making the buffer ready for reading after writing**. The `rewind()` method **resets the position to zero**, **allowing you to re-read the buffer from the beginning**.
4. **Direct and Indirect Buffers**: `ByteBuffer` can be **either direct or indirect**. **Direct buffers are allocated outside the Java heap and provide a more efficient way to work with native I/O operations**. **Indirect buffers are allocated within the Java heap and are suitable for most general-purpose use cases**.
5. **Ordering** `ByteBuffer` provides **methods to handle byte order**, such as `order()`, `putChar()`, `getShort()`, etc. You can **specify the byte order as either big-endian or little-endian when reading or writing multibyte data**.

`ByteBuffer` is widely **used in various Java APIs and libraries for efficient handling of binary data**. In the context of Spring Web Reactive, as mentioned earlier, `DefaultDataBuffer` (used in `Flux<DataBuffer>`) is often backed by a `ByteBuffer` to provide a **low-level representation of data buffers in a non-blocking, reactive manner**.

## What is `DefaultDataBuffer`? ##
`DefaultDataBuffer` is a class in Spring Framework's `org.springframework.core.io.buffer` package that represents a default implementation of the `DataBuffer` interface. It is part of the Spring Web Reactive module and is **used for handling data buffers in a non-blocking, reactive manner**.

The `DataBuffer` interface provides an abstraction for working with binary data buffers, **allowing efficient manipulation and streaming of data**. It is **often used in scenarios where large amounts of data need to be processed or transferred, such as network communication or file handling**.

`DefaultDataBuffer` implements the `DataBuffer` interface and provides the following functionalities:

1. **Storage of Binary Data**: `DefaultDataBuffer` **stores binary data in memory**. It typically uses a `ByteBuffer` **as the underlying storage mechanism for efficient manipulation of the data**.
2. **Non-blocking and Reactive**: `DefaultDataBuffer` is **designed to be used in reactive programming models, such as Spring WebFlux**. It **allows non-blocking I/O operations by providing reactive APIs like** `Flux<DataBuffer>` and `Mono<DataBuffer>`, which **can be processed asynchronously in a streaming fashion**.
3. **Flexibility**: `DefaultDataBuffer` **provides methods for reading and writing data, as well as manipulating the buffer position and limit**. It **supports different modes of accessing data, such as getting or putting individual bytes, accessing ranges of bytes, or converting data to/from other types**.
4. **Memory Management**: `DefaultDataBuffer` **manages memory allocation and deallocation for the stored data**. It **leverages efficient memory management techniques to minimize memory footprint and optimize performance**.

`DefaultDataBuffer` is a **commonly used implementation in Spring Web Reactive applications when working with data buffers**. It **provides a convenient and efficient way to handle binary data in a non-blocking, reactive manner**.

## How is the `ByteBuffer` efficient? ##
`ByteBuffer` provides several features and design choices that contribute to its efficiency:

1. **Direct Memory Allocation**: `ByteBuffer` allows for **direct memory allocation outside of the Java heap**, **known as direct buffers**. This **allows ByteBuffer to leverage operating system and hardware optimizations for I/O operations**. **Direct buffers are particularly useful when working with native I/O operations, as they can be directly passed to operating system calls without requiring data copying**.
2. **Native I/O Operations**: `ByteBuffer` is designed to work efficiently with native I/O operations. It can be used with classes in the `java.nio.channels` package, such as `FileChannel` or `SocketChannel`, **to perform I/O operations directly on the buffer without intermediate copies**. This **reduces the overhead of data transfer and improves performance**.
3. **Resizable Capacity**: `ByteBuffer` can have a resizable capacity, allowing it to grow or shrink as needed. This flexibility enables efficient memory utilization, as the buffer can be expanded when more space is required and contracted when less space is needed. Resizable capacity is particularly beneficial when dealing with dynamic or unpredictable data sizes.
4. **Position and Limit Management**: `ByteBuffer` maintains the current position and limit, which allows for efficient sequential data processing. The **position represents the index of the next byte to be read or written, while the limit sets a boundary on the accessible portion of the buffer**. This **design enables efficient sequential reading or writing of data without the need for additional bookkeeping**.
5. **Direct Data Access**: ByteBuffer provides direct access to the underlying byte array or memory region through its array() or address() methods. This allows for efficient bulk operations or direct manipulation of the data without the need for individual byte-level operations.
6. **Byte Order Support**: ByteBuffer includes methods for handling byte order, such as order(), putChar(), getShort(), etc. Byte order manipulation is important when working with multibyte data, such as integers or floating-point numbers, and ByteBuffer provides efficient mechanisms for handling different byte orders.

By incorporating these efficiency-focused design choices, ByteBuffer provides a high-performance mechanism for working with binary data in Java. It allows for efficient I/O operations, reduces memory overhead, and enables streamlined data processing.