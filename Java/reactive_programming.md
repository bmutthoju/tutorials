# Reactive Programming in Java #
## Course Introduction (Reactive Programming with Java - Full Course ##
1. Agenda:
	1. The "default" blocking programming model and its limitations.
	2. Understanding Reactive programming
	3. Build scalable reactive code using Project Reactor
		1. Similar project: RxJava
	4. Learn operators and transform reactive streams
	5. Learn patterns, common best practices and pitfalls with reactive programming
	6. Reactive programming + Spring Boot application development architecture
2. Prerequisites:
	1. Some Java knowledge including Collections and streams basics.
	2. A computer with Java 11+ installed (Java 17+ preferred)
	3. A Java IDE like IntelliJ IDEA (Free version should do)

## What is Reactive Programming (Reactive Programming with Java - Full Course ##
1. Definition: Reactive programming is a declarative programming paradigm concerned with data streams and the propagation of change. With this paradigm, it's possible to express static (e.g., arrays) or dynamic (e.g., event emitters) data streams with ease, and also communicate that an inferred dependency within the associated execution model exists, which facilitates the automatic propagation of the changed data flow.
	1. Declarative: This is what I want to happen and it happens in the background
	2. Data streams: stream of elements
		1. Reactive programming works with the stream
2. Reactive is not Async
	1. Async: Things are not happening one after another
	2. Reactive: can be synchronous
		1. Non Reactive programming can be asynchronous
3. Use cases:
	1. User events:
		1. When user clicks a button
			1. We wire with a callback
				1. Reacting to a button click
	2. When I/O response happens
		1. When file is read, execute a function
4. React to something
5. Why do we care?
	1. Server side web development:
		1. Request comes in (only reactive part)
		2. We do processing
			1. Call API, microservice, ...
		3. We return response
			1. The steps happen in sequence and are synchronous
		4. A case for reactive programming

## Why Do Reactive Programming ##
1. Modern application development:
	1. We deal with high data scale (10 years back not so much data)
	2. We have high usage scale
		1. We have to scale availability as well
			1. If we have high usage scale, every inefficiency is multiplied with scales
	3. We worry about costs now especially cloud based costs
		1. We immediately see the impact of badly written code in terms of cloud costs
2. How do you scale up?
	1. Vertical scaling:
		1. Increasing the power of the computers (RAM, CPU, ...)
			1. Problem: After certain point, we cannot scale
	2. Horizontal scaling:
		1. Add more servers
3. Before we scale, we need to optimize:
	1. What's the problem here?
		1. Calling two services in sequence
			1. Blocking
				1. After we issue the first call, we need to wait for it to return
				2. Second service call waits unnecessarily for the first service to return
					1. **unnecessarily sequential**
			2. Cost: Performance (to the user)
				1. Response is slower than it is supposed to be
		2. Web application:
			1. Server: When a web-server gets a request, it spins up a new thread
				1. The longer it takes to respond, there is more likely that there are more threads
					1. At some point in time, capacity limit might get reached.
						1. Problem: **Idling threads**
							1. Cost: **Wasted hardware** (forces us to scale horizontally or vertically)

## Async in Server Side Apps ##
1. Spoilt backend developers!
	1. We assume we are handling a single request
	2. Multiple simultaneous users abstracted out
		1. We can do this because we write stateless code mostly (unless we are hitting the database)
	3. Delays abstracted out
	4. We pay with sequential blocking operations
	5. We pay with idling threads
2. But wait!
	1. There are concurrency APIs
		1. Examples: `Future` and `CompletableFuture`
		
				CompletableFuture userAsync = CompletableFuture.supplyAsync(() -> userService.getUser(userId));
				
			1. Since Java 8
				1. Implements `Future` and goes beyond it!
			2. Works with `CompletionStage` to coordinate async operations
	2. Using CompletableFuture:
		1. Call userService
		2. Call userProfileService in parallel
		3. When both return, merge the data structures
		4. Return merged object
	3. Code:
	
			CompletableFuture<User> userAsync = CompletableFuture.supplyAsync(() -> userService.getUser(userId));
			CompletableFuture<User> userPreferencesAsync = CompletableFuture.supplyAsync(() -> userPreferenceService.getPreferences(...));
			CompletableFuture bothFutures = CompletableFuture.allOf(userAsync, userPreferencesAsync);
			bothFutures.join();
			
		1. Both calls in parallel:
			1. `join()` is still blocking
				1. Code needs to wait until it constructs the object `User`
				2. If the two calls are long running, the parent thread is blocked
		2. Code looks ugly
		3. Too much for the dev to do
		4. Error handling is messy
		5. It's still sync after all
	4. Solution: New paradigm and framework needs to support it

## A New Paradigm ##
1. We must not be compelled to wait inside the method
2. Reactive programming:
	1. Example:
	
			@GetMapping("/users/{userId}")
			public Mono<User> getUserDetails(@PathVariable String userId) {
				return userService.getUser(userId)
					.zipWith(userPreferencesService.getPreferences(userId))
					.map(tuple -> {
						User user = tuple.getT1();
						user.setUserPreferences(tuple.getT2());
						return user;
					});
			}
			
		1. What's different
			1. Much simpler than the manual concurrent way (objectively)
				1. Once familiar
			2. Few reusable flexible functions
			3. Combine and reuse in powerful ways
				1. It makes it easy to use knowledge again and again (not much is required to learn)
3. Ractive programming:
	1. Declarative code to build asynchronous processing pipelines
	2. Different way of thinking about flow
	3. Different way of thinking about data
	4. Integrated with Java! `Flow` Interface
		1. Java doesn't have implementation
			1. Libraries will give the implementation
			2. No one uses it directly
	5. Learning curve:
		1. May not be worth it for small projects
			1. Because of effort required to get it to work
		2. Use it when application scales (wait until the tipping point)
	6. Familiar yet different
		1. It looks similar to collection streams

## A Java Streams Detour ##
1. Loops:
	1. Java streams - alternative
		1. Represents a sequence of data
		2. Focus on computations
			1. More about how to process
		3. vs collections which focus on storage
		4. Iternal iteration
	2. Example:
	
			List<Integer> numbers = Arrays.asList(1, 2, 3, ..., 10);
			
			for (int i = 0; i < numbers.length; i++) {
				System.out.println(numbers.get(i));
			}
			
			/* Using streams */
			numbers.stream().forEach(number -> System.out.println(number));
			
2. Stream operators:
	1. map
	2. filter
	3. flatMap - take another stream and flat map it
	4. findFirst - matches a predicate
	5. ...
3. Exercises:

		numbers.stream().forEach(System.out::println);
		
		numbers.stream().filter(number -> number < 5).forEach(System.out::println);
		
		numbers.stream()
			.filter(number -> number > 5)
			.skip(1)
			.limit(2)
			.forEach(System.out::println);
			
		Integer value = numbers.stream()
			.findFirst(number -> number > 5)
			.orElse(-1);
		System.out.println(value);
		
		users.stream()
			.map(user -> user.getFirstName())
			.forEach(System.out::println);
			
		StreamSources.intNumbersStream()
			.flatMap(id -> StreamSources.userStream().filter(user -> user.getId() == id))
			.map(user -> user.getFirstName())
			.forEach(userName -> System.out.println(userName));
			
		// flatMap: returns result of stream
		
		StreamSources.intNumbersStream()
			.filter(u -> StreamSources.intNumbersStream().anyMatch(i -> i == u.getId()))
			.forEach(System.out::println);
			
4. `flatMap`
	1. Helps when we map to a stream
		1. Example: `.map(id -> StreamSources.userStream().filter(...))`
			1. Returns stream
				1. We want flattened value of stream, however

## Collection Stream Exercises ##
## Audience Q & A ##
1. Parallel streams:
	1. Allows us to use multiple threads in the case when we have multiple cores on the machine

## The Story of Two Design Patterns ##
1. Object Oriented Design patterns:
	1. Iterator pattern
		1. The iterator pattern is a design pattern in which an iterator is used to traverse a container and access the container's elements.
		2. The iterator pattern decouples algorithms from containers
		3. It gives a consistent experience no matter how the collection fetches data
			1. Container returns an iterator implementation
			2. Consumer talks to the iterator
		4. Consumer asks for the next item and iterator returns the next item or says sorry
	2. Observer pattern
		1. The observer pattern is a design pattern where the subject maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.
			1. We want to observe for an event and then react to it
		2. Source - aware when something changes
			1. It tells the observer when something happens and gives the data
		3. Pub-Sub?
			1. A little more long running comparitively
		4. Behaviour is handed over to the source which sends data when an event occurs

## Iterator and Observer Patterns ##
1. The two patterns are closely linked
2. Two patterns:
	1. What is common between the two?
		1. The behaviour is inverted between the two
			1. Iterator pattern: consumer asks for the next item and iterator gives the item
			2. Observer pattern: Source sends the data when it get it to the Observer
		2. Difference?
			1. Who controls when the data is sent
				1. Iterator: Pull vs Observer: Push
3. Iterator pattern:
	1. Print every element in the List
	
			myList.forEach(element -> System.out.println(element)); // forEach is fetching element by element
			
4. Observer pattern:
	1. clicksChannel.addObserver(event -> System.out.println(event));
	
5. The above are the same
	1. Irrespective of who is pushing or pulling the data, the programming model is the same
		1. **Irrespective of whether we pull the data or push the data, the programming model is the same**
6. Chain operations:

		myList
			.filter(element -> element != null)
			.forEach(element -> System.out.println(element));
			
		clicksChannel
			.filter(event -> event != null)
			.addObserver(event -> System.out.println(event));
			
	1. Only control has shifted to the source but programming model is the same
	2. Reactive programming syntax:
	
			clicksChannel
				.filter(event -> event != null)
				.subscribe(event -> System.out.println(event));

## The Better Assembly Line Analogy ##
1. Assembly line analogy:
	1. True assembly line. Items come over time
		1. This is an analogy of reactive programming
			1. Some external event puts items on conveyer belt

## Calling Subscribe on Reactive Sources ##
1. Print off numbers in the ReactiveSources.intNumbersFlux stream

		ReactiveSources.intNumbersFlux().subscribe(e -> System.out.println(e)); // forEach alternative
		
	1. Whenever a number is emitted, run the method in the subscribe
2. Another with users:

		ReactiveSources.userFlux().subscribe(user -> System.out.println(user));

## Audience Q & A on Reactive Sources ##
1. The programming paradigm is agnostic of single thread or multi-threaded execution.
2. Order of subscription does not decide the ordering of processing events.
3. Publisher & Subscriber:
	1. Flux - publisher
	2. Lambda - Subscriber
4. But I want a List
	1. What if you want to get a list of items?

## Blocking to Get a List ##
1. Converting async model to everything in memory using stream

		List<Integer> numbers = ReactiveSources.intNumbersFlux().toStream().toList();
		
	1. Takes total amount of time it needs to get all the items (blocks until all elements are obtained)

## Key Interfaces and Types ##
1. Reactive Streams:
	1. Introduced in Java 9
		1. `Flow` API
			1. `Publisher` interface
			2. `Subscriber` interface
			3. `Subscription` interface
	2. They are interfaces only (standardization)
		1. You don't use any of them directly
2. What you will use:
	1. `Flux`
	2. `Mono`
3. `Flux`:
	1. Needs dependeny: `io.projectreactor:reactor-core`
		1. We are using implementations of this in code
	2. **It represents an asynchronous sequence of items**
		1. It could be synchronous (it can be considered as an instance of asynchronous if delay is 0)
	3. 0/n items
	4. **It has back-pressure**
		1. So that subscriber can keep up with publisher
4. `Mono`:
	1. **It represents an asynchronous item that may or may not come in the future**
		1. 0/1 item

## Working with Mono and Audience Q & A ##
1. Print the value from intNumberMono when it emits

		ReactiveSources.inteNumberMono().subscribe(number -> System.out.println);
		
	1. Only one value is processed at most
2. We can block one Mono:

		Integer number = ReactiveSources.intNumberMono().block(); // it could be null
		
		Optional<Integer> number = ReactiveSources.intNumberMono().blockOptional(); // this causes losing the benefits of reactive programming
		
	1. Mono gives only one value so we can block
3. If we return a Mono to MVC framework. We are telling the framework to take the value when it is available
	1. Blocking is pushed to the framework (we are not blocking our threads)
		1. Framework has optimizations to remove its waiting threads (ideally only one place should be blocking)

## Event Types and Terminal Events ##
1. What's coming?
	1. When it runs out of data, Mono and Flux have completion event
		1. Could be immediately after last event or waits for certain time and then sends done
	2. A complete event
	3. A failure event
		1. An error occurred
2. For Mono, a complete is sent after one item
3. For Flux, a complete event is sent anytime or not at all (infinite stream)
4. Complete event & failure event are terminal events
	1. Failures - terminal event (nothing is accepted after that)

## The Subscribe Method ##
1. Subscribe method:

		`subscribe();` - no lambda to execute (no one will listen to an emitted event)
		`subscribe(Consumer<? super T> consumer);` - consumer - functional interface
			1. takes an element and processes it (when there is an item)
		`subscribe(Consumer<? super T> consumer, Consumer<? super Throwable> errorConsumer);`
		`subscribe(Consumer<? super T> consumer, Consumer<? super Throwable> errorConsumer, Runnable completeConsumer);`
		`subscribe(Consumer<? super T> consumer, Consumer<? super Throwable> errorConsumer, Runnable completeConsumer, Consumer<? super Subscription> subscriptionConsumer);`
		
			ReactiveSources.intNumberMono().subscribe(
				number -> System.out.println(number),
				err -> System.out.println(err.getMessage()),
				() -> System.out.println("Complete")
			);

## Controlling Backpressure with Subscription Classes ##
1. Disposable

		Disposable subscribe = ReactiveSources
								.intNumbersFlux()
								.subscribe(number -> System.out.println(number);
								);
								
	1. Another way to subscribe:
		1. Using an implementation of `BaseSubscriber` Interface
			1. Pass that to `subscribe`
			
					
					class MySubscriber<T> extends BaseSubscriber<T> {
						public void hookOnSubscribe(Subscription subscription) {
							System.out.println("Subscribe happenede");
							request(1); // send 2 items whenever they are ready (backpressure)
						}
						
						public void hookOnNext(T value) {
							System.out.println(value.toString() + " received");
							request(1); // send 1 whenever it is ready
						}
					}
					
					...
					
					ReactiveSources.intNumbersFlux().subscribe(new MySubscriber<>());
					
			2. We need to describe backpressure
				1. We can have a queue and if it getting full, we can request fewer items.
					1. We can scale
					2. Performance might be impacted
						1. We might run out of memory
						2. We might run out of cpu

## Audience Q & A on Backpressure ##
1. We can set up breakpoints inside methods.
2. Blocking:
	1. It may not return a value.

## Handling Unresponsive Monos with Timeout ##
1. How do we handle errors?
	1. Unresponsive Flux or Mono
		1. Wait for certain time and give up
		
				String foo = ReactiveSources.unresponsiveMono().block(Duration.ofSeconds(5)); // wait for 5 seconds, then exit

## Reactive All the Way! ##
1. What's the point?
	1. There has to be a block somewhere.
		1. We want to go reactive all the way and push the blocking until only the caller is the one who is blocking.
			1. Example: Restaurant - everyone hands over to the next person and is not blocked. Finally only the one who has given the order is blocked.
				1. ideally he is the one who is waiting (if he is reactive, then he will be doing something else)
2. Web Apps:
	1. HTTP request comes in and the one who sent the request waits
		1. However, reactive web-servers exist
			1. Example: Netty
				1. **Netty doesn't spawn a new thread and wait for the response to come**
					1. **It keeps the request in a data-structure and doesn't hold the thread**
						1. We only return **Mono** or **Flux** to Netty
							1. Upto 100k simultaneous requests on decent cloud environment.
	2. Example:
	
			@GetMapping("/users/{userId}")
			public Mono<User> getUserDetails(@PathVariable String userId) {
				return userService.fetchUserMono(userId);
			}
			
		1. The number of threads not blocked and waiting is significantly pushed to a higher value (for the same hardware assuming tasks are I/O intensive)

## Operators Why They are Needed ##
1. What if you need to process?

		@GetMappnig("/users/{userId}")
		public Mono<User> getUserDetails(@PathVariable String userId) {
			userService.fetchUserMono(userId);
			// Check if User object has an active flag
			// Fetch User details from database
			// Populate user object and return
		}
		
	1. Handled using operators:
		1. Example of Collection stream:
		
				arrayList.stream()
					.filter(element -> element != null)
					.forEach(element -> System.out.println(element));
					
		2. Flux and Mono operators:
		
				flux
					.filter(element -> element != null) // return another Flux
					.subscribe(element -> System.out.println(element)); // subscribed to second Flux
					
				mono
					.filter(user -> user.isActive())
					.subscribe(user -> System.out.println(user));
					
			1. The operations are performed when the event is fired

## The Log Operator ##
1. Log:
	1. Logs the elements in a stream
		1. [https://projectreactor.io/docs/core/release/api/reactor/core/publisher/Flux.html#log](https://projectreactor.io/docs/core/release/api/reactor/core/publisher/Flux.html#log)
			1. `public final Flux<T> log()`
				1. Observes all Reactive Streams signals and traces them using `Logger` support. Default will use `level.INFO` and `java.util.logging`. If SLF4J is available, it will be used instead.
					1. Doesn't modify anything
	2. Example:
	
			List<Integer> numbers = ReactiveSources
										.intNumbersFlux()
										.log() // logs the element and returns the Flux
										.toStream()
										.toList();
										
		1. Good for debugging.
	3. Exercise:
	
			// Print off values from intNumbersFlux that's greater than 5
			ReactiveSources.intNumbersFlux()
				.log()
				.filter(e -> e > 5)
				.subscribe(System.out::println);

## Exercise Using Operators ##
1. Print 10 multiplied by  each value from intNumberFlux that's greater than 5

		ReactiveSources.intNumbersFlux()
			.filter(e -> e > 5)
			.map(e -> e * 10)
			.subscribe(System.out::println);
			
2. Print 10 multiplied by each value from intNumberFlux for the first 3 numbers emitted that's greater than 5

		ReactiveSources.intNumbersFlux()
			.filter(e -> e > 5)
			.take(3)
			.map(e -> e * 10)
			.subscribe(System.out::println);
			
	1. the operators might be implemented in a different thread each
3. Way to handle empty flux:

		ReactiveSources.intNumbersFlux()
			.filter(e -> e > 20)
			.defaultIfEmpty(-1)
			.subscribe(System.out::println);

## Exercise Using flatMap and Distinct Operators ##
1. Switch ints from intNumbersFlux to the right user from userFlux

		ReactiveSources.intNumberFlux()
			.flatMap(id -> ReactiveSources.userFlux().filter(user -> user.getId() == id))
			.take(1)
			.subscribe(System.out::println);
			
2. Print only distinct numbers from intNumbersFluxWithRepeat

		ReactiveSources.intNumberFluxWithRepeat()
			.distinct()
			.log()
			.subscribe(); // this is a must to trigger the process (turns on the switch)
			
3. Print from intNumbersFluxWithRepeat excluding immediately respeating numbers

		ReactiveSources.intNumberFluxWithRepeat()
			.distinctUntilChanged()
			.log()
			.subscribe();
			
4. Learn from Javadocs.
5. Read the documentation of the project Reactor
	1. Operators and their uses

## Avoid These Issues with Reactive Programming ##
1. What's wrong with this code?

		Flux<Integer> flux = getFlux();
		flux.map(value -> getNewValue(value));
		flux.subscribe(next -> System.out.println("Received: " + next)); // doesn't take the new Flux but uses the first Flux
2. `subscribe` method doesn't return a Flux
	1. It returns a `Disposable` - we can stop the conveyer belt
3. Error handling:
	1. A usecase for timeout:
		1. Fallback if something is taking too much time
			1. Example: Webclient (Reactive model)
				1. Fallback if there is timeout (do an alternative thing if the request times out)

## Error Handling in Reactive Programming ##
1. Error handling:
	1. Terminal event
		1. A Flux or Mono can emit an Error and it is done
	2. Original sequence does not continue
	3. Calls the `onError` method of the `Subscriber`
2. Exercise:
	1. Print values from intNumbersFluxWithException and print a message when error happens
	
			ReactiveSources.intNumbersFluxWithException()
				.subscribe(
					num -> System.out.println(num),
					err -> System.out.println(err)
				); // like a catch
				
			// alternative
			ReactiveSources.intNumbersFluxWithException()
				.doOnError(
					e -> System.out.println("Error!!! " + e.getMessage()) // has only side effect but doesn't handle the error
				)
				.subscribe(
					num -> System.out.println(num),
					err -> System.out.println(err) // swallows the error
				);
				
	2. Print values from intNumberOfFluxWithException and continue on errors
	
			ReactiveSources.intNumbersFluxWithException()
				.onErrorContinue(
					(e, item) -> System.out.println("Error!!! " + e.getMessage()) // has only side effect but doesn't handle the error
				)
				.subscribe(
					num -> System.out.println(num),
					err -> System.out.println(err) // swallows the error
				);
				
		1. If consumer wants to continue (instead of terminating)
			1. Changes the default behavior
	3. Print values from intNumbersFluxWithException and when errors happen, replace with a fallaback sequence of -1 and -2
	
			ReactiveSources.intNumbersFluxWithException()
				.onErrorResume(err -> Flux.just(-1, -2))
				.subscribe(num -> System.out.println(num));
				
3. `doFinally` - analogous to try/catch/finally, terminal clause

		flux.doFinally(signalType -> {
			if (signalType == SignalType.ON_COMPLETE) { // Type provided by project Reactor
				System.out.println("Done!");
			} else if (signalType == SignalType.ON_ERROR) {
				System.out.println("Error!");
			}
		});

## Flux to Mono ##
1. Print size of intNumbersFlux after the last item returns:
	
		ReactiveSources.intNumbersFlux()
			.count() // returns a Mono - returns value on terminal event (completion or error)
			.subscribe(System.out::println);
			
2. Collection all items of intNumbersFlux into a single list and print it
	1. Return a Mono of a List
	
			ReactiveSources.intNumbersFlux()
				.collectList() // returns Mono of java.util.List<T>
				.subscribe(System.out::println);
				
3. Transform a sequence of sums of adjecant two numbers

		ReactiveSources.intNumbersFlux()
			.buffer(2) // every 2 events get converted to a single event, returns a Flux<List>
			.map(list -> list.get(0) + list.get(1))
			.subscribe(System.out::println);

## Constructing a Reactive Spring Boot App ##
1. Spring Boot Webflux project:
	1. https://start.spring.io
		1. Dependencies:
			1. Spring Reactive Web
				1. Webflux
				2. Netty
	2. Open the project:
	
			@RestController
			public class MyController {
				@GetMapping("/demo")
				public String greetingMessage() {
					return "HelloWorld"; // blocking if we are calling a service
				}
			}
			
			// alternative
			
			@RestController
			public class MyController {
				@GetMapping("/demo")
				public Mono<String> greetingMessage() {
					return computeMessage()
							.zipWith(getNameFromDB())
							.map((t1, t2) -> {
								rseturn t1.getT1() + t2.getT2()
							}); // returns in around 5 seconds
				}
			}
			
			private Mono<String> computeMessage() {
				returns Mono.just("Hello").delayElement(Duration.ofSeconds(5));
			}
			
			private Mono<String> getNameFromDB() {
				return Mono.just("Kaushik").delayElement(Duration.ofSeconds(5));
			}
			
		1. Our code is non-blocking; however, framework handles the blocking part

## Wrap Up ##
1. Recap