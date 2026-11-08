# Event-Driven Architecture - The Complete Guide #
## Section 1: Welcome ##
### Course Introduction ###
1. Why learn event-driven architecture?
	1. Evolution of microservices architecture
		1. microservices - most popular
	2. Becomes super popular
		1. More systems are built in this style
	3. Platform agnostic
		1. Java
		2. .NET
		3. Node.js
		4. PNP
		5. ...
	4. Extremely scalable
		1. We can add more components without modifying the core components of the system
			1. For unpredictable load
2. But it is not a silver bullet
	1. Must be handled carefully and needs a lot of thought
3. Know
	1. If it is good
	2. How to do it?
4. Dangers of badly designed EDA
	1. Slow
	2. Unmaintainable
	3. Frustrating
	4. Costly
5. By the end of this course:
	1. Will know what event-driven architecture is
	2. Will know what problems it solves
	3. Will know how to design a robust, scalable, easy to maintain event-driven architecture
	4. Will know when NOT to use event-driven architecture
	5. Will become a much better software architect
6. And
	1. Course is extremely practical
	2. Going to design and build a real-world event-driven system
		1. Using RabbitMQ, SignalR, etc.
7. NOP System
8. We can use the system as a template for our own systems

### Join the Software Archicts Community ###
1. Software architecture community: [Software Architecture Discussion](https://www.facebook.com/groups/127639125043271/)
	1. Ask questions
	2. Bring up dilemmas
	3. Post interesting links
	4. Announce relevant events
2. [Newsletter](https://memilavi.com/newsletters)

### Get the Course Slides ###
1. Attached to every last lecture.

### Who is This Course For ###
1. Developers
	1. Preferably back-end developers, but not mandatory
2. Architects
3. Anyone who is interested in software architecture

### Agenda ###
1. Welcome
2. Introduction to events
3. Event-driven architecture
4. Event sourcing and CQRS
5. When to use event-driven architecture
6. Stateless and stateful EDA
	1. Need to choose
7. Streaming and EDA
8. Logging and monitoring
	1. Challenges
9. Implementing EDA
	1. Tools and engines
10. Case study
11. Conclusion

## Section 2: Events ##
### Introduction ###
1. Events
	1. The cornerstone of event driven architecture
	2. Require a well-defined definition
	3. Evolved from other architectures

### Microservices Architecture ###
1. Event-driven architecture is based on microservices architecture
2. microservices architecture
	1. Based on loosely-coupled services
	2. Each service in its own process
	3. Lightweight communication protocols (services used them)
		1. No CORBA or JMS
	4. Polyglot
		1. No platform dependency between services
			1. Java
			2. Python
			3. ...
	5. Replaces two legacy architectures
		1. Monolith
			1. All components reside in same process
				1. Difficult to scale
				2. Platform limitations
		2. SOA (Service Oriented Architecture)
			1. Applications are separate services (they expose API)
				1. Difference?
					1. An application itself has separate services
					2. SOA considers each application as a service with its own API
	6. Typical microservices system
		1. services communicate among each with
			1. Using network
		2. Each service has its own database
	7. Communication:
		1. Perhaps the most important part in microservices architecture
		2. Dictates performance, scalability, implementation and more
		3. Event-driven architecture handles the communication part
			1. We are not dealing with the services themselves
				1. We only deal with how services talk to each other

### Command and Query ###
1. Command and Query
	1. The classic communication between services
		1. Services either
			1. Send command
			2. Query for data
2. Command
	1. Service asks another service to do something
		1. Orders services asks the Payment service to process payment
			1. There might be a response to the command, usually a success or failure indicator
				1. Payment service might return a response saying the payment processing completed successfully
3. Query
	1. Service asks another service for data
		1. Cuseromers service asks Orders service: How many orders were made by customer X?
	2. THere's always a response to the query, containing the data
4. Main characteristics of command and query
	1. Command
		1. Do something
		2. Usually synchronous
			1. Waits for command to complete
		3. Sometimes returns a response
		4. **Calling service needs to know who handles the command**
	2. Query
		1. Retrieve data
		2. Almost always synchronous
		3. Always returns a response
		4. **Calling service needs to know who handles the query**

### Problems with Command and Query ###
1. Problems with command and query
	1. Three major problems
		1. Performance
		2. Coupling
		3. Scalability
2. Performance
	1. Synchronous = the calling service waits for the command / query to complete
		1. We have a potential for performance hit
			1. Causes trouble if a system is under heavy load (?)
3. Coupling
	1. A calling service calls a specific service
		1. If the called service changes, the calling service has to change too (API)
			1. More maintenance
4. Scalability
	1. The calling service calls a single instance of a service
		1. If the instance is busy - there's a performance hit
			1. Solution:
				1. Load balancer
				2. Probing - for availability
				3. Service registry
				4. ...

### Event ###
1. Event:
	1. Indicates that something happened in the system
		1. We just notify that something happened
	2. Example:
		1. Customers service - new customer was added
	3. THere's never a response to the event
	4. Main characteristics
		1. Event
			1. Something happened
			2. Asynchronous
				1. Doesn't exect a response
			3. Never returns a response
			4. Calling service has no idea who handles the event

### Contents of Event ###
1. Data in an event
	1. Two types of event data:
		1. Complete
			1. Contains all the relevant data
			2. Usually entity data
				1. Changed
				2. Added
				3. Deleted
				4. ...
			3. No additional data is required for the event processing
				1. Example:
				
				```
				event_type: CustomerCreated
				customer_id: 17
				first_name: David
				last_name: Jones
				join_date: 2022-03-15
				```
				
		2. Pointer
			1. Contains pointer to the complete data of the entity
			2. Complete data usually stored in a database
			3. Event handler needs to access the database to retrieve complete data
			4. Example:
			
			```
			event_type: CustomerCreated
			customer_id: 17
			```
			
				1. It is a pointer
2. Flow of complete event handling
	1. Customers service - New customer was added -> Event handler (1. Recieves event data, 2. Processes the event)
3. Flow of pointer event handler

```
Customer service - New customer was added -> Event handler (receives event data, retrieves complete data from database, processed the event)
```

4. Complete vs Pointer
	1. Complete
		1. The better approach
		2. Makes the event completely autonomous
		3. Can get out of the system boundaries
			1. Can be sent to external systems that may not have access to the database
	2. Pointer
		1. Use when:
			1. Data is large 
				1. Cannot be transfered as n event
			2. Need to ensure data is up-to-date
				1. Assuming database is a single-source-of-truth

## Section 3: Event-Driven Architecture ##
### Introduction ###
1. Event-Driven Architecture
	1. A software architecture paradigm that uses events as the mean of communication between services
	2. Often called EDA
	3. Has three main components
		1. Producer
		2. Channel
		3. Consumer
2. Producer
	1. The component/service sending the event
	2. Often called publisher
	3. Usually sends event reporting something the component has done
	4. Example:
		1. Custoemr service -> New customer added event
		2. Inventory service -> Item sold out event
	5. The producer sends the event to the channel

### Producer ###
1. Exact method of calling the channel depends on the channel
	1. Usually using a dedicated SDK developed by the channel vendor
2. Utilizes some kind of network call, usually with specialized ports and proprietary protocol
	1. Example: RabbitMQ listens on port 5672 and uses the AMQP protocol
3. Producer can be developed using any development language (that can use the channel's SDK)

### Channel ###
1. The most important component in the Event-Driven architecture
2. Responsible for distributing the events to the relevant parties
3. The channel places the event in a specialized queue, often called Topic or Fanout
4. Consumers listen to the queue and grab the event
5. Note:
	1. Implementation details vary wildly between channels
		1. RabbitMQ works differently than Kafka that works differently than WebHooks, etc.
6. Always deep-dive into the docs of the channel you're using
7. We'll use RabbitMQ and SingalR in the implementation section
8. Channel distributes events to the consumers

```
channel -> Consumer
        -> Consumer
		...
```

9. The channel's method of distribution varies between channels
	1. Can be
		1. Queue
		2. REST API call (consumer exposes)
		3. Proprietary listener

### Consumer ###
1. The component that receives the event sent by the Producer and distributed by the Channel
2. Can be developed in any development language compatible with the Channel's libraries (if any)
	1. Some of them will do with REST API
3. Processes the event
4. Sometimes - reports back when processing is complete (ACK)
5. The consumer receives and processes the event
6. Consumer gets the event using either:
	1. Push
		1. Channel pushes the event to the consumers
	2. Pull
		1. Consumers poll the channel for new events

### Advantages of Event-Driven Architecture ###
1. Advantages of EDA
	1. Event-Driven Architecture has a lot of advantages over other architecture paradigms
		1. As a quick refresher
			1. Problems with Command and Query
				1. Three problems
					1. Performance
						1. Event-driven architecture
							1. It is asynchronous architecture
								1. Channel does not wait for response from consumer (no waiting at all)
									1. No performance bottlenecks
					2. Coupling
						1. Event-driven architecture
							1. The producer sends events to the channel
							2. The channel distributes events to the topics / queues
								1. No direct call to the consumer
							3. Both have no idea who's listening to the event (except in WebHooks - some kind of coupling) (not coupled to a consumer)
					3. Scalability
						1. Event-driven architecture
							1. Many consumers can listen to events from channel
							2. More can be added as needed
							3. Channel doesn't care, producer doesn't know
							4. Fully scalable
								1. We can add as many consumers as we want

### EDA vs Pub/Sub ###
1. Event-Driven Architecture is often mentioned with Pub/Sub
2. Pub/Sub = Publish and Subscribe
	1. A messageing pattern used by Event-Driven architecture
		1. Publisher
		2. Broker
		3. Subscriber
3. Differences?
	1. EDA
		1. It describes the **whole architecture of the system**
	2. Pub/Sub
		1. It is a **messaging pattern used by the system**
			1. Not exclusively
				1. It implements the event-driven aspects of the architecture
					1. Example:
						1. My event-driven architecture uses mainly Pub/Sub for inter-service communication, but I do have some REST APIs for synchronous queries

### Ordering in EDA ###
1. Messaging engines often guarantee the order of the messages
	1. The order in which we send messages is the same order in which the other end receives the messages
		1. Popular in traditional queues
		
		```
		Service A - 3, 2, 1 -> Service B
		```
		
			1. With Event-Driven Architecture (especially with Pub/Sub) ordering is not always guaranteed
			2. Ordering might be affected by consumer latency, code performance and more
			
			```
			Service A - Pub/Sub -> Service B (3, 1, 2) (no ordering)
			```
			
				1. Solution: If ordering is important, make sure to select a channel that supports this capability
					1. RabbitMQ supports ordering
					2. SignalR does not support ordering

### Orchestration and Choreography ###
1. Event-Driven architecture usually employs one of two architectural styles
	1. Orchestration
		1. Flow of events in the system is determined by a central orchestrator
		2. Orchestrator recieves output from components and calls the next component in the flow
			1. State-machine
		3. The next component sends the output back to the orchestrator
		
		```
		Order service <- New order recieved - Orchestrator
		Order service - Order complete -> Orchestrator
		Inventory service <- Items ordered - Orchestrator
		Inventory service - Inventory updated -> Orchestrator
		```
		
			1. Orchestrator acts as a state-machine
			2. All events go through the orchestrator
				1. The services have no idea about the flow of the system
				2. The services have no idea what other services exist in the system
					1. Autonomous
						1. They perform only their designated tasks
		
	2. Choreography
		1. No central "knowing all" component
		2. Each component notifies about the status of events
		3. Other components listen to the events and act accordingly
		
		```
		Orders service
		|
		| New order recieved
		|
		v
		Customer service
		|
		| Order Complete
		|
		v
		Inventory service
		```
		
			1. All services listen to all events and decide which events to handle
2. Comparison
	1. Orchestration
		1. Logic is defined in a single place - easier to maintain
			1. If we need to change the logic (flow), we can update it in a single place
		2. Central traffic gateway
			1. Easier monitoring and logging (traffic)
	2. Choreography
		1. Performance - no middleman
			1. No need to go through an orchestrator to communicate with another service
		2. Reliability - if one component fails, the rest still work
			1. If an orchestrator fails, the whose system goes down
3. Orchestration vs Choreography decision
	1. Not constrained to EDA only
	2. Can be used with other types of communication
	3. Became popular with EDA

## Section 4: Event Sourcing and CQRS ##
### Introduction ###
1. Event Sources and CQRS
	1. Event-Driven Architecture is mainly about services
	2. Events can be used as the basic building blocks of data too (?)
	3. Event-sourcing and CQRS offer a pattern to store data as events
		1. Sometimes the best pattern to use for data

### Problems with Traditional DBs ###
1. Traditional databases hold data about current state of entity
	1. This is true for SQL and NoSQL databases
2. Example:
	1. Employees table
		1. Problems
			1. What was John's previous role?
			2. When did Sarah move to NYC?
			3. Did any of the employees change his/her name?
		2. There is no way to see historical data of entities
		3. Data is a "snapshot" of a point in time
			1. Problems in some cases:
				1. Bank-account statement
					1. List of transactions
						1. Previous actions are important
							1. We want to know how reached the bottomline
3. Event-Sourcing and CQRS try to solve the problem

### Event Sourcing ###
1. What is it?
	1. A data store pattern in which every change in the data is captured and saved
	2. Database stores list of changes for the entity, not the entity itself
		1. Example: When a property was changed, but when and what changed
	3. No updates or deletes, just inserts
		1. Every row documents a change in a property/properties of the entity
	4. In this pattern, the database is called Event Store
		1. Example:
		
		```
		event_id | timestamp  | event
		1        | 2009-04-23 | Employee John Smith joined
		2        | 2009-04-23 | Address of John Smith updated to Hott Street, Clinton
		3        | 2009-04-23 | Role of John Smith updated to Junior Developer
		4        | 2013-04-22 | Address of John Smith updated to Beverly Hills 90210
		...
		```
		
			1. Specific columns are up to you, depends on the system requirements
			2. There's lot more information than in the regular table
				1. We can do a lot more analysis on the data
2. How can we view the current state of an entity?
	1. By replaying the events related to it, from the first event
3. Pros and Cons
	1. Pros
		1. Extremely easy to view historical data
		2. Simple database structure
			1. Only 3 columns in most cases
		3. Simple database operations (no updates, no concurrency)
			1. Only inserts
				1. Very fast
					1. Why?
						1. Simple DB structure
							1. No indexes
							2. No keys
							3. No complex operations (joins etc.)
	2. Cons:
		1. Viewing current entity state is cumbersome and slow
			1. We need to replay all the events to the entity to get a view of the current state
				1. Problem if we are dealing with a lot of entities.
		2. Large database capacity (many records per entity)
			1. The size increases with the number of changes.
4. Solution:
	1. CQRS

### CQRS ###
1. Stands for:
	1. Command and Query Responsibility Segregation
		1. Means:
			1. Separating the command (updates/inserts/deletes) from the queries
			2. Each one of them in a separate database
			3. Commands database is implemented as Event Store to improe performance and simplicity
			4. Queries database stores entities
			5. Databases are synced using a **central synchronization mechanism**
	2. Structure:
	
	```
	Commands DB (Event Store)
	|
	| Sync - Replay events and constructs entity
	|
	v
	Queries DB
	```
	
		1. To query, we make requests to the Queries DB
2. Pros:
	1. Combines Event Sourcing pros with traditional entity query
	2. No performance hit when querying entities
3. Cons:
	1. Entity data is not updated in real-time
		1. It might take time to sync
	2. Difficult to set-up and maintain
		1. Two database
		2. Synchronization mechanism
			1. Development and maintenance

### When to use Event Sourcing and CQRS ###
1. When access to historical data is extremely important
	1. Regulation, finance, healthcare, etc.
2. When data is large and replaying events is not feasible
	1. Not just event-store
3. When performance is critical (inserts or queries)

## Section 5: When to use Event-Driven Archicture ##
### Introduction ###
1. When to use EDA
	1. Event-Driven architecture is not easy to implement
	2. Requires setting up and configuring channels
	3. Not trivial to log and monitor
	4. Be sure to use it when needed

### Scalability ###
1. Scalability is a non-issue in EDA
2. New consumers can be added as needed with no changes to the architecture
3. Great for fluctuating load
	1. If the system is constantly in need of scalability, EDA can be considered
		1. Just add more consumers without changing anything else

### Asynchronous ###
1. If inter-service communication can be asynchronous, consider EDA
	1. Cannot call from channel to consumer synchronously
		1. There are some channels who can do that - exception
	2. Remember: EDA is async by nature
	3. Example:
		1. Send instructions to perform payment and doesn't wait for response
		2. Writing to log
2. Check how many synchronous interactions there are
3. Usually mainly queries
	1. Queries - synchronous by nature
		1. The more synchronous calls - the less EDA is relevant

### Reliable Network ###
1. EDA utilizes a lot of traffic
	1. Hence the network has to be reliable
		1. Otherwise, performance will be slow

### When not to use EDA ###
1. EDA is not suitable for:
	1. Small systems with a few services
		1. Overhead in maintaining EDA components 
			1. Channels, say
	2. Synchronous-oriented systems
		1. Eg: Information system serving mainly queries from end users
		2. Rule of thumb: The more the system interacts with the end-user, the less EDA must be used.

## Section 6: Stateless and Stateful EDA ##
### Introduction ###
1. Stateless vs Stateless EDA
	1. There are two main patterns in implementing EDA 
		1. Stateless and Stateful
	2. Related to the consumers behavior
	3. Both are legitimate, but make sure to select the right one for your scenario
2. In software architecture there's also the stateless vs stateful debate
	1. While the concepts are similar, the reasoning is different
	2. With software architecture it's often said that:
		1. Stateful is bad
			1. This is not necessarily the case with EDA
				1. Sometimes, stateful can make the EDA as useful as possible 

### Stateless EDA ###
1. If each event handled by a consumer is completely autonomous and is not related to past / future events
	1. Should be used when the event is an independent unit with its own outcomes
2. Example:

```
Channel - New order submitted -> Payment processor (processes payment) (n)
```

	1. It doesn't matter which consumer is handling the event
	2. The outcome is always the same
	3. Should be used when each event is autonomous
		1. Example: Each order is independent, say
	4. Note: Statelessless has nothing to do with the question of what data is contained in the event and whether a call to a DB is required (could be a pointer)

### Stateful EDA ###
1. Events might be related to past / future events
2. SHould be used for aggregators and time-related events
	1. Examples: 
		1. Send an email if more than 5 failure events were received in a single minute
			1. We need to know the past events in a given minute
				1. Each event is related to previous events
		2. Calculate the amount of orders submitted in an hour
			1. Need to know how many events were submitted in the hour
3. Example:

```
Channel - Order submit failed -> Monitoring consumer - aggregates failed orders (other consumers cannot aggregate)
```

	1. All events must be routed to a single consumer - the consumer is stateful (it keeps the data of previous events)
4. It's extremely important which consumer handles the event
	1. Current state is stored in specific consumer(s)
6. Should be used when events are part of a chain of events

### Problems with Stateful EDA ###
1. Stateful EDA presents some problems that should be taken care of
	1. Load balancing
	2. Scalability
2. Load balancing
	1. Since the state is stored in a specific consumer, subsequent events must be routed to the same consumer
		1. Hence, no load balancing is possible
			1. Example: Order submit failed - must be routed to the same consumer which aggreates failed orders
3. Scalability
	1. Since the state is stored in a specific consumer, additional consumers cannot be added to handle the events
		1. If another consumer is added, it will still not process because the load goes to the same consumer
4. Stateless vs Stateful
	1. Rule of thumb:
		1. Use stateless EDA unless the business requirements force you to use stateful

## Section 7: Event Streaming ##
### Introduction ###
1. Event Streaming:
	1. So far we talked about Event Driven Architecture
		1. Something happened
		2. An event was created
		3. Someone listened to the event and handled it
			1. Consumer
2. Event streaming is another event-oriented pattern
	1. These are not the same as EDA, but share similar characteristics

### What is Event Streaming ###
1. What is it?
	1. Event streaming engines publish stream of events
		1. E.g. telemetry from sensors, system logs etc.
		2. The events are published to a "stream"
		3. Consumers subscribe to specific stream
		4. Events are retained in a stream for a specified amount of time
			1. Unline in EDA where the events are removed after they are processed
2. Example:

```
Producer - Streams -> Consumers 
```
	1. Streams
		1. Queues - they hold the events
		2. The consumers listen to the queues and pull the events when needed
3. Consumers can retrieve events that were sent in the past (usually up to a few days)
	1. Configurable
4. Streaming engine can be used as a central database
	1. A single source of truth
		1. Streaming engines can hold data of the past - the data is accessable to the consumer on demand
5. Not all events are necessarily handled using event-streaming
	1. Some might not be relevant

### Differences between Streaming and EDA ###
1. Event streaming
	1. Usually used for events generated outside of the system
		1. Log records
		2. Telemetry from sensors
		3. ...
	2. Events are retained
		1. As long as the retention period has not expired (configurable)
	3. Not all events are handled
	4. High load
		1. It must handle this load
2. EDA
	1. Usually used for events happening inside the system
		1. New order generated
		2. New employee added
	2. Events are not retained
	3. All events are handled
		1. System generates events that are of interest to the consumers
	4. No high load

### When to use Event Streaming and How ###
1. Scenarios
	1. When the system needs to handle stream of events from the outside
		1. Example: Sensor data, logs, etc.
	2. When events should be retained for future use
		1. Classic EDA doesn't retain events
	3. When high load is expected
2. Implementing Event Streaming
	1. Use specialized streaming tools
		1. Never develop one
	2. The most notable one:
		1. Apache Kafka
			1. Free to use

## Section 8: Logging and Monitoring ##
### Introduction ###
1. Logging and Monitoring
	1. Crucial for getting wholistic view of what's going on in the system
	2. Extremely important in every distributed system
		1. EDA is not a regular distributed system
	3. Especially challenging in EDA
		1. Implementing it is not simple

### Challenges of Logging in EDA ###
1. In EDA, there are distributed, non-coupled components
2. Getting unified, chronolically ordered log is difficult
	1. Each component writes log to different destination
	2. Log formats are different
	3. Timestamps are not synchronized
3. Example:

```
Producer - 11.28 Msg 14 was sent -> channel
Producer - 11.30 Msg 15 was sent -> channel

	1. 11.26 Receiving msg 14 ... - channel's clock is not synchronized
	2. 11.26 Handling msg 14 ...
	3. 11.30 Sending msg 14
	4. 11.29 Reciving msg 15 ...
	
Consumer - 11.33 Msg: 14, Status: received
```

	1. They use different formats for the log
	2. The timestamps are not synced
	3. Different destinations
		1. They write to their own files
	4. Many records, hard to trace
4. Solution:
	1. Using correlation id

### Correlation Id ###
1. Handles the following problems
	1. Timestamps not synced
	2. Different destinations
	3. Many records, hard to trace
2. Correlation id:
	1. At the beginning of each transaction, a unique identifier is attached to the message
	2. The identifier is logged as part of the log record
	3. ALlows tracing across components
3. Example:

```
Producer: 11.28 CID 8, Msg 14 was sent
Producer: 11.30 CID 9, Msg 15 was sent

Channel: 11.26 CID 8, Receiving msg 14 ...
Channel: 11.26 CID 8, Handling msg 14 ...
Channel: 11.28 CID 8, Sending msg 14
Channel: 11.26 CID 9, Receiving msg 15 ...

Consumer 1: 11.33 CID 8, Msg: 14, Status: received
Consumer 2: 11.34 CID 9, Msg: 15, Status: received
```

### Central Logging Engine ###
1. Handles the following problems:
	1. Different formats
	2. Different destinations
2. What is central engine?
	1. Central engine used for aggregating all the log records
		1. In a central data store
	2. Central engine has converters that convert between log formats (to unify all log records)
	3. Great analytics and visualization capabilities
	4. Can utilize the existing channel for log transport
3. Example:

```
Business consumer 
 |
 | logging event
 |
 v
Channel
 |
 | logging event
 |
 v
Logging consumer
```

4. How to implement central logging engine
	1. Do not develop one
	2. There are a lot of great logging engines
	3. Most are free
	4. The most popular
		1. Elastic stack (ELK)

### What Should be Logged ###
1. There is no standard
2. Rules:
	1. Logs should reflect the behavior of the system
	2. Not just errors!
	3. Should be able to replay a transaction using logs
		1. To analyze the behavior
		2. To find out performance
		3. ...
3. What should be logged?
	1. Event trigger
		1. Function call
		2. File upload
		3. Timer (trigger every 30 seconds)
		4. ...
	2. Event contents (incl correlation id)
	3. Event receive
		1. When consumer receives an event, log it
	4. Event handling complete
		1. When consumer handles an event
	5. Any errors

## Section 9: Advanced Topics ##
### Introduction ###
1. There are a lot of nuances with EDA
2. We talked about the mainstream implementations
	1. Covers ~ 80% of the cases
4. There are advanced topics you should be aware of
	1. Perhaps will be never used but it's good to be aware of
5. Advanced Topics
	1. Mixing EDA with Request/response
	2. Synchronous EDA
	3. Events as source of truth
	4. Saga pattern
	5. EDA on the front-end

### Mixing EDA with Request/Response ###
1. Most EDA systems are not pure EDA
	1. We usually use some other forms
		1. Reaons? End-users using UI
			1. UI clients need responsiveness and use WEB API to call the backend
				1. REST
				2. gRPC
				3. GraphQL
				4. ...
			2. User waits for response
	2. If client only asks for data, EDA will probably won't work
		1. EDA is not designed for it
			1. EDA doesn't support response
2. Example:

```
Laptop
|							^
| REST request 				|
| with command 				| Command
| (add to shopping cart)	| receives
|							| HTTP status 201
v							|
[REST API]
Producer
|
| Item added to cart
|
v
Consumer
```

### Synchronous EDA ###
1. EDA is asynchronous by nature
	1. Normally the producer does not wait for a response to the event
		1. Sometimes it does, as a separate event
			1. Quite difficult to implement
2. Mechanism:

```
Producer - New order placed -------------> Channel
         <- Ordered placed successfully -  Channel
```

	1. Send the event
	2. Wait for the response event...
	3. Wait some more...
	4. Handle the return event in a separate code segment
3. Solution:
	1. To make the process easier you can construct a wrapper around the producer
	2. The wrapper exposes a synchronous Web API (REST, ...)
	3. Calls the producer and performs all the dirty work of sending -> waiting -> handling response
	4. Example:
	
	```
	End user
	| 												^
	| REST request with command (place new order)	| Order placed successfully
	|												|
	v												|
	Wrapper
	|					^
	|					|
	v					|
	Producer
	|					^
	| New order placed	|
	|					|
	v					|
	Channel
	```
	
		1. Wrapper kept the request thread for the user running until it got response from the producer
			1. Not easy to implemenet
			2. Do it only if you absolutely need a response from the event
			3. Some channels (e.g. RabbitMQ) have built-in support for this
				1. Has support for wrappers
					1. The wrapper listens to the topic until return event is returned

### Events as Source of Truth ###
1. With traditional systems, the database holds the operational data and the events trigger actions in the system
	1. DB is the source of truth
		1. If we want to know the state of the system, we are going to the source of truth
		2. Consumers work against the database
			1. Saving data after handling event
2. With channels that retain events, the channel can funtion as the source of truth
	1. If data needs to be saved, the consumer sends an event back to the channel
		1. Relevant only if:
			1. Events are retained
			2. The channel has some kind of query language
				1. Example: Bring me all events that were received yesterday, ...
			3. Main functionality of the system is around event streaming, no complex interactions
				1. Example: Complex queries against data cannot be used
3. Implementation of events as source of truth
	1. Kafka
		1. Events are retained
		2. Has the KQL query language
			1. Kafka Query Language
				1. To run queries against events stored in Kafka
		3. Designed for event streaming
			1. KSQ - basic query language

### The Saga Pattern ###
1. Saga pattern
	1. Transaction management in distributed system is difficult
		1. Example:
			1. Two services system
			2. Each service has a DB
			3. If service A committed to its DB
			4. Service A sends request to Service B
			5. Service B tries to save the data to its own DB (to make the DBs consistent) but the transaction fails
			6. We get inconsistent data in both DBs
		2. Problem is common in distributed systems
			1. A solution: 2-Phase commit protocol
				1. But difficult to implement
	2. The Saga pattern strive to solve this problem
		1. A sequence of service-scoped transaction, triggered by events
			1. Each transaction is scoped to its service using its database
	3. When a transaction fails, a compensating transaction is triggered
		1. If service B cannot commit the data, service A does something to revert the previous commit
			1. Delete record OR
			2. Add status flag
			3. ...
	4. The services communicate with each other using events
2. Flow:

```
Service A - Commit -> DB    Runs compensating transaction (delete, flag, etc.)
|							^
| Transaction A commited	|
|							|
v
Channel
|							^
| Transaction A commited	|
|							| Transaction B failed
v							|
Service B - Commit -X-> DB (failed)
```

	1. It is not easy to implement
	2. Consistency is not ensured 
		1. Compensating transaction can fail
			1. Data is still inconsistent
	3. Quite difficult to debug
	4. Monitoring is important
3. When to use?
	1. No need to strongly-coupled transactions
		1. If we are okay with a slight inconsistency in data between services
		2. If data must be consistent, SAGA will not solve 2-Phase commit issues
	2. Compensating transactions can be defined
		1. If we can think of something that compensates for error that happened on service B

### Events on the Front-End ###
1. EDA on the Front-End
	1. So far we discussed Event Driven Architecture in the back end
	2. It can also be implemented on the front end
	3. We won't deep-dive into it
2. Two main aspects of EDA on the front end:
	1. Micro frontends
	2. Push notifications
3. Micro Frontends
	1. Brings the microservices concept to the front end
	2. The page is divided to separate, independent UI component
	3. Each component has its own UI, functionality, backend etc.
	4. Components communicate with each other using events
	5. Example:
		1. Item details
			1. Raises an event: Item added to shopping cart
		2. Shopping Cart
			1. Shpping cart acts accordingly
	6. The components themselves are platform agnostic and can use any frontend framework (or vanilla JS)
	7. The inter-component communication is done using **Browser Events** and **Custom Elements**, supported by all major browsers
4. Push notifications:
	1. Events that are sent to the browser from the server
		1. Server sends an event to browser
	2. As opposed to the more traditional Request/Response model
		1. Not exactly EDA but involves events in the clients
	3. Very useful for apps requiring streaming info from the server
		1. Example: Chats
	4. Architecture:
	
	```
	Laptop
	^
	|
	| message in chat
	|
	Server
	```
	
	5. Implementation:
		1. Libraries and frameworks:
			1. SignalR (server to client)
			2. Socket.IO
			3. gRPC
			4. ...

## Implementing Event Driven Archicture ##
### Introduction ###
1. We covered a lot of theory
2. How do we implement EDA?
	1. Mainly 4 things to consider
		1. Events approach
		2. Implementing the channel
		3. Implementing the producer
		4. Implementing the consumer

### Events Approach ###
1. Two main approaches
	1. Events are retained
		1. The channel retains the event for future handling
		2. A retention period is defined which after it expires - the event is removed (hours to years)
			1. Configurable
		3. Great for streaming events and when the channel is the source of truth
	2. Events are not retained
		1. The channel publishes the events and does not store them
			1. If a consumer missed an event - it can't be replayed
			2. Used mainly for in-system events

### Implementing the Channel ###
1. Depends on the events approach
	1. Events are retained
		1. Use a messaging / queue engine
			1. Common engines:
				1. RabbitMQ
				2. Kafka
	2. Events are not retained
		1. Use an event publisher
			1. Specific engine depends on platform used, types of interfaces and more
		2. Let's see some examples
			1. Azure Event Grid
				1. Events publisher in the cloud
					1. Fully hosted in Azure cloud, no installation required
				2. Great integration with a lot of event sources and handlers
					1. We can plug different services that can trigger events to event-grid and reveive events routed by the event-grid
		3. It can deal with thousands of events/sec
			1. Great fit for system that is expected to handle a huge load
		4. Azure Event Grid:
			1. Event sources
				1. Azure Blob Storage
				2. Azure resource groups
				3. Azure subscriptions
				4. Azure Event Hubs
				5. Azure Media Services
				6. Azure IoT Hub
				7. Azure Service Bus
				8. Azure Maps
				9. Azure Container Registry
				10. Azure SignalR Service
				11. Azure App Configuration
				12. Azure Machine Learning
				13. Azure Communication Services
				14. Azure Cache for Redis
				15. Azure Policy
				16. CloudEvents Sources
				17. Custom Events (anything)
			2. Event Grid
			3. Event Handlers
				1. Serverless Code
					1. Functions
				2. Workflow and Integration
					1. Service Bus
					2. Logic Apps
				3. Buffering and Competing Consumers
					1. Event Hubs
					2. Storage Queues
				4. Other Services and Applications
					1. Hybrid Connections (WebSockets)
					2. WebHooks (anything)
					3. Azure Automation
		5. WebHooks
			1. A standard for publishing events using REST API
			2. Consumers subscribe to the WebHook engine and register a REST API endpoint that will be called when an event occurs
				1. If there is a relevant event, call this endpoint
			3. The WebHook will call the endpoints when event is triggered
			4. Easy to implement
				1. Supported by GitHub, DropBox, PayPal, Stripe and more
			5. WebHooks flow
			
			```
			Producer
			|
			| Trigger event using REST request to controller
			|
			v
			WebHook controller
			^												|
			|												| Call receivers' endpoint using REST
			| Register callback endpoint (URL - REST API)	|
			|												v
			Receiver
			```
			
			6. Implementation
				1. Libraries for implementing WebHooks in various platforms
					1. E.g. ASP.NET WebHooks
				2. Website offering WebHooks
					1. Zapier
					2. Ifttt (if this, then, that)
					3. HostedHooks
					4. ...
		6. HTTP Push notfication
			1. Send events from the server to client(s)
			2. Great for chats, message notification and more
			3. Example:
			
			```
			Laptop
			^
			|
			| New message in chat
			|
			Server
			```
			
			4. Implementation:
				1. Quite a lot of libraries and frameworks:
					1. SignalR
					2. Socket.IO
					3. gRPC
					4. And more...
		7. How to choose event publisher?
			1. Azure Event Grid or similar
				1. Hosted in the cloud
				2. Need strong integration between backend services
					1. Example:
						1. Timer triggered
						2. Specific function was called
						3. ...
			2. WebHooks
				1. Receivers expose REST API
				2. Need something simle and quick (to develop and manage)
			3. HTTP Push Notification
				1. Need to notify the end user
					1. Less used for inter-service communication
2. Never develop your own channel
	1. Focus on business logic
		1. Don't waste time on infrastructure setup

### Implementing the Producer ###
1. Can be based on any platform
	1. Needs to be able to communicate with the channel
		1. Depends on channel implementation
			1. Example:
				1. RabbitMQ
					1. Use RabbitMQ client library for your platform
					2. There's one for almost every platform
					3. Choose from:
						1. [https://www.rabbitmq.com/devtools.html](https://www.rabbitmq.com/devtools.html)
							1. .NET
							2. Java
							3. PHP
							4. Python
							5. Go
							6. ...
				2. SignalR
					1. Install the SignalR library
					2. Configure the Hub
						1. Similar to channel
						2. It manages all notifications to and from SignalR
					3. Allow connections from clients
						1. Configure connections to the hub
					4. Define functions that will send messages to clients
					5. Optional - Construct groups to filter messaging
						1. All clients relevant to aviation chat will get messages from aviation

### Implementing the Consumer ###
1. Can be based on any platform
2. Needs to be able to communicate with the channel 
3. Depends on the channel implementation
4. Let's see some examples:
	1. RabbitMQ
		1. Use the RabbitMQ client library for your platform
		2. There's one for almost every platform
		3. Choose from:
			1. [https://www.rabbitmq.com/devtools.html](https://www.rabbitmq.com/devtools.html)
	2. WebHooks
		1. Register the consumer using the WebHook REST API
			1. Controller exposes REST API for registering the consumer (or receiver)
		2. Expose REST API that will be called by the WebHooks

## Case Study ##
### Introduction ###
1. Case study
	1. Design of event-based system for receiving and processing noise telemetry from sensors
	2. The system will utilize two types of channels
	3. After designing it - we'll actually build it

### Our System ###
1. Introducting
	1. NOP 
		1. Noise Processing system
		2. A system for receiving and processing noise data from external sensors
			1. The system should:
				1. Receive the telemetry
				2. Validate it
				3. Notify clients on new data
		3. The data is a number representing the decibals recorded
		4. Every sensor sends the data every 30 seconds
			1. If there are a lot of sensors, there's quite a lot of data
				1. 1000 sensors - 33 msgs/s
		5. Design requirements
			1. Handle load
				1. Streaming engine should be used
				2. Processors pull from the stream when possible
			2. Validate the data 
				1. The first thing that should happend after receiving the data
			3. Unknown number of clients
				1. Classic events ruquirement
					1. Scaling out an event based system is easy
						1. We simply add consumers
			4. No sync users' commands
				1. No synchronous actions required
		6. Architecture
		
		```
		Sensor
		Sensor  ---> Streaming channel (RabbitMQ) --pull--> Consumer/ Validator + SignalR (to notify user that data is received) ---> Client(s) (Subscribers)
		Sensor
		```

### Installing .NET SDK ###
1. Preparing the environment
	1. Installing some software
		1. .NET SDK
		2. VS Code with some extensions
		3. RabbitMQ (channel)
2. Installation:
	1. Download .NET SDK
		1. Install
	2. Open CMD
		1. `dotnet --version`

### Installing VS Code ###
1. Download VS Code
	1. Install
2. Install extension
	1. C# (Microsoft)

### Installing RabbitMQ ###
1. Install Erlang
	1. [https://erlang.org/download/otp_versions_tree.html](https://erlang.org/download/otp_versions_tree.html)
		1. First link 
2. Install RabbitMQ
	1. [https://www.rabbitmq.com/download.html](https://www.rabbitmq.com/download.html)
		1. Rabbit MQ Server
	2. Open: Rabbit MQ Command Prompt
		1. `rabbitmqctl status` **(M)**

### Building the Producer ###
1. Simulates noisy sensor
	1. Download and open with VS Code
2. Rabbit MQ command prompt
	1. `rabbitmqctl list_queues`
3. 

### Building the Consumer ###
### Building the SignalR Client ###
### Summary ###

## Conclusion ##
### Conclusion ###
1. Summary
	1. Event driven architecture
	2. Basics to advanced EDA
		1. Streaming
		2. Sync calls
		3. ...
	3. Practical
	4. Equipped with EDA
2. Agenda
	1. Welcome
	2. Introduction to Events
	3. Event Driven Architecture
	4. Event Sourcing and CQRS
	5. When to use EDA
	6. Stateless and Stateful EDA
	7. Streaming and EDA
	8. Logging and monitoring
	9. Implementing EDA
	10. Case study
	11. Conclusion

### BONUS: Next Steps ###
1. [Azure Solutions Architect Certification: The Ultimate Bundle](http://tiny.cc/azurecert)
2. [Azure Security Best Practices](http://tiny.cc/azseccoupon)
3. [Azure OpenAI Services - The Complete Guide](http://tiny.cc/azureopenai)
4. [Microsoft Entra ID for Developers and Architects](http://tiny.cc/azadcoupon)
5. [Azure Copilot - The Complete Guide](http://tiny.cc/azcopilotcoupon)
6. [AWS from Zero to Hero - The Complete Guide](https://tiny.cc/gcpcoupon)
7. [REST API vs GraphQL vs gRPC - The Complete Guide](https://tiny.cc/apicompcoupon)