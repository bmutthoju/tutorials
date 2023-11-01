## What is `Collection.singletonList` ##
In Java, `Collection.singletonList` is a utility method provided by the `java.util.Collections` class. It is used to create an immutable (read-only) singleton list containing a single element.

Here's how `Collection.singletonList` works:

		List<T> list = Collections.singletonList(element);

The method takes an element of type `T` as an argument and returns a `List<T>` containing only that element. The returned list is of fixed size and cannot be modified. Any attempt to add, remove, or modify elements in the list will result in an `UnsupportedOperationException`.

The purpose of `Collection.singletonList` is to provide a convenient way to create a singleton list when you need a list with only one element. It is useful in cases where you want to pass a single element to a method or when you need to create a temporary list for a specific operation.

Here's an example usage of `Collection.singletonList`:

		import java.util.Collections;
		import java.util.List;

		public class Main {
			public static void main(String[] args) {
				String element = "Hello";
				List<String> singletonList = Collections.singletonList(element);
				System.out.println(singletonList);  // Output: [Hello]

				// Attempting to modify the list will result in an exception
				singletonList.add("World");  // Throws UnsupportedOperationException
			}
		}

In the example, `Collections.singletonList(element)` creates a singleton list containing the element "Hello". The list is printed, showing `[Hello]`. However, when attempting to add another element to the list, it throws an `UnsupportedOperationException` because the list is immutable.

## How does `Flux<T>` work internally? ##
`Flux<T>` is a class from Project Reactor, which is a reactive programming library for building asynchronous and non-blocking applications in Java. It provides a programming model based on the Reactive Streams specification.

Internally, `Flux<T>` represents a stream of zero or more elements of type `T`. It follows the Publisher-Subscriber pattern defined by the Reactive Streams specification. The key concepts and mechanisms involved in the internal workings of `Flux<T>` are as follows:

1. Publisher: A `Flux<T>` instance acts as a Publisher, responsible for emitting elements to its Subscribers. It implements the `org.reactivestreams.Publisher` interface, which defines the `subscribe` method.
2. Subscriber: A Subscriber subscribes to a `Flux<T>` to receive elements emitted by the Publisher. It implements the `org.reactivestreams.Subscriber` interface, which defines methods such as `onSubscribe`, `onNext`, `onError`, and `onComplete`.
3. Subscription: When a Subscriber subscribes to a `Flux<T>`, it receives a `Subscription` object via the `onSubscribe` method. The `Subscription` represents the connection between the Subscriber and the Publisher. It allows the Subscriber to request elements and cancel the subscription when it's no longer interested in receiving elements.
4. Backpressure: `Flux<T>` supports backpressure, which is a flow control mechanism that allows Subscribers to signal how many elements they are ready to consume. The Publisher respects the requested demand and emits elements accordingly.
5. Operators: `Flux<T>` provides various operator methods that allow transforming, filtering, combining, or manipulating the stream of elements. These operators create new `Flux` instances based on the original `Flux` and the applied transformation.
6. Lazy Evaluation: `Flux<T>` operates lazily, meaning that elements are not produced until a Subscriber subscribes to it. The elements are generated or fetched on-demand as requested by Subscribers.
7. Asynchronous and Non-blocking: `Flux<T>` is designed for asynchronous and non-blocking processing. It **leverages features such as event loops, thread pools, and backpressure to efficiently handle large streams of data without blocking threads**.

By combining these mechanisms, `Flux<T>` allows for efficient and reactive processing of data streams. It enables developers to build asynchronous, non-blocking, and reactive applications by composing and transforming streams of elements using operators and subscribing to them with reactive Subscribers.