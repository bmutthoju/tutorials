# Event-Sourcing #
## What is event-sourcing? ##
Event sourcing is **a software design pattern** **used in building complex and scalable systems**. It **involves storing the changes made to an application's state as a sequence of events in a time-ordered log**. This **log of events can be used to reconstruct the state of the application at any point in time**.

In event sourcing, the **state of the application is not stored directly in a database or other persistent storage**. Instead, the **state is derived by replaying the sequence of events that led to the current state**. This **makes it easy to track changes made to the system over time, as well as to audit and debug the application**.

Event sourcing also **provides a way to handle concurrency and distributed systems**, as **each event represents a discrete unit of work that can be processed independently**. Additionally, event sourcing **enables event-driven architectures, where events can be used to trigger actions or updates in other parts of the system**.

Overall, event sourcing is a powerful technique for building complex, scalable, and fault-tolerant systems, particularly in domains with high data volumes and frequent updates.

## Give an example of event-sourcing. ##
Let's consider an example of a banking application that uses event sourcing to track account transactions.

In a traditional system, the account balance would be updated in a database each time a transaction occurs. However, in an event-sourced system, the **transaction itself is recorded as an event in a time-ordered log, without directly updating the balance**.

For instance, let's say a user transfers $100 from their checking account to their savings account. In an event-sourced system, this would be recorded as a transaction event, which might look like:

		{
		  "type": "transfer",
		  "timestamp": "2022-04-16T10:15:00Z",
		  "amount": 100,
		  "source_account": "checking",
		  "destination_account": "savings"
		}

This **event is appended to the log of events, and the account balances are derived by replaying the sequence of events**. In this case, the balance of the checking account would be reduced by $100, and the balance of the savings account would be increased by $100.

By using event sourcing, the system can easily track changes made to the accounts, and **it can also handle concurrency and fault tolerance**. **If two transactions are initiated simultaneously, they can be processed independently as separate events, ensuring that there are no conflicts or inconsistencies in the account balances**.

## How are invariants satisfied with event-sourcing? ##
Invariants are logical rules or constraints that must hold true in a system. Invariants can be simple, such as "an account balance cannot be negative," or they can be complex, involving multiple entities or data elements.

Event-sourcing can help to ensure that invariants are satisfied in a system by providing a way to validate the events before they are committed to the event log. **When an event is processed, the system can perform checks to ensure that the event does not violate any invariants**.

For example, let's consider the invariant that "an account balance cannot be negative." **When a "withdrawal" event is received, the system can validate that the account balance will not become negative as a result of the withdrawal**. **If the withdrawal would cause the balance to become negative, the system can reject the event and prevent it from being committed to the event log**.

Additionally, event-sourcing **can provide a way to roll back events that violate invariants**. **If an event is discovered to violate an invariant after it has been committed to the log, the system can roll back the event and any subsequent events that depend on it, effectively undoing the invalid state**.

By using event-sourcing to enforce invariants, the system can ensure that data is always consistent and valid, even in the face of complex interactions and concurrent updates.

## How are conflicts handled with event-sourcing? ##
In a distributed system with event-sourcing, **conflicts can occur when two or more nodes attempt to modify the same piece of data simultaneously**. **Conflicts** can arise **when events are created concurrently**, or **when events are applied to the system in a different order on different nodes**.

To handle conflicts, event-sourcing provides **a way to resolve conflicts by merging conflicting events**. This is **typically done by defining a set of conflict resolution rules that determine how to merge events with conflicting data**.

For example, let's say two users initiate a transfer from the same account, but they transfer different amounts. If both transfers are processed concurrently, there will be two conflicting events in the event log. The system can resolve this conflict by defining a conflict resolution rule that takes the larger of the two transfer amounts and applies that amount to the account.

In addition to conflict resolution rules, **event-sourcing systems can use optimistic concurrency control techniques to detect conflicts early and prevent them from occurring in the first place**. **Optimistic concurrency control involves associating a version number or timestamp with each event**. **When an event is applied to the system, the version number or timestamp is checked to ensure that it matches the expected value**. **If the version number or timestamp does not match, it indicates that a concurrent modification has occurred, and the system can reject the event**.

By using conflict resolution rules and optimistic concurrency control, event-sourcing systems can ensure that data remains consistent and conflicts are handled effectively, even in a distributed and highly concurrent environment.

## Give an example of optimistic concurrency control. ##
Sure! Let's continue with the banking example we used earlier.

In an event-sourced banking system, **each transaction is recorded as a separate event in a time-ordered log**. **When a transaction is initiated, the system checks to ensure that the account balance is sufficient to cover the transaction amount**. **If** the **balance is sufficient, a "withdrawal" event is added to the log, and the account balance is updated accordingly**.

**To prevent conflicts, the system can use optimistic concurrency control by associating a version number or timestamp with each event**. **When a transaction is initiated**, the **system checks the current version number or timestamp of the account**. **If** the **version number or timestamp has not changed since the transaction was initiated**, the **system can proceed with adding the withdrawal event to the log**.

However, **if another transaction has been initiated in the meantime and has updated the account balance, the version number or timestamp will have changed**. **In this case**, the **system can detect the concurrent modification and reject the withdrawal event, preventing it from being added to the log**.

For example, let's say User A initiates a withdrawal of $50 from their checking account. The system checks the version number of the account and finds it is at version 10. Since no other transactions have been initiated, the system adds a "withdrawal" event to the log and increments the version number to 11.

If User B initiates a withdrawal of $100 from the same checking account at the same time, the system will check the current version number, which is now 11. Since the version number has changed, the system knows that a concurrent modification has occurred and will reject User B's transaction, preventing it from being added to the log.

By using optimistic concurrency control, the system can prevent conflicts and ensure that only one transaction is processed at a time, ensuring data consistency and avoiding race conditions.

## How to implement event sourcing in a Spring Boot application? ##
Implementing event sourcing in a Spring Boot application involves several steps, including **setting up the event store**, **defining aggregates and events**, and **implementing event handlers**.

Here is a high-level overview of the steps involved in implementing event sourcing in a Spring Boot application:

1. **Set up the event store**: The **event store is the system that stores and manages the event log**. There are several open-source event store **implementations** available, such as **Axon**, **Eventuate**, and **Apache Kafka**. Choose an event store that suits your application's requirements and integrate it with your Spring Boot application.
2. **Define aggregates and events**: **Aggregates are the domain objects that encapsulate the state of the system**. **Events are** the **immutable records that represent changes to the state of the aggregates**. Define **aggregates and events that represent the domain objects and operations in your application**.
3. **Implement command handlers**: **Command handlers are responsible for processing incoming commands and generating events**. **Commands represent requests to perform an operation on an aggregate**. Implement **command handlers that validate the commands and generate the appropriate events**.
4. **Implement event handlers**: Event handlers are **responsible for updating the state of the aggregates in response to events**. Implement event **handlers that apply the events to the aggregates and persist the new state to the event store**.
5. **Implement projections**: **Projections are read models that represent the current state of the system**. Implement **projections that listen for events and update the read model accordingly**.
6. **Configure the application**: Configure the Spring Boot application to **use the event store, define beans for command handlers, event handlers, and projections**, and wire up the dependencies between the components.
7. **Test and deploy**: Test the application to ensure that it behaves as expected and deploy it to your production environment.

Implementing event sourcing in a Spring Boot application can be complex, but there are several open-source libraries and frameworks available that can simplify the process, such as Axon Framework and Eventuate. These frameworks provide abstractions and conventions that make it easier to implement event sourcing in a Spring Boot application.

## Give an example of an event-source implementation using the Eventuate framework. ##
Sure, here's an example of an event-source implementation using the Eventuate framework:

Let's consider a simple e-commerce application that allows users to purchase items from a catalog. When a user places an order, we want to publish an event that reflects that order.

1. First, we'll define the event that will be published when an order is placed:

		public class OrderPlacedEvent implements Event {
		  private final String orderId;
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
		
2. Next, we'll create a command that represents the action of placing an order:

		public class PlaceOrderCommand implements Command {
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
	
3. We'll then define a service that handles the PlaceOrderCommand and publishes the OrderPlacedEvent:

		@Service
		public class OrderService {
		  
		  @Autowired
		  private EventuateAggregateStore eventStore;
		  
		  public String placeOrder(PlaceOrderCommand command) {
			Order order = new Order(command.getCustomerId(), command.getLineItems());
			List<Event> events = Collections.singletonList(new OrderPlacedEvent(order.getId(), order.getCustomerId(), order.getLineItems()));
			EntityWithIdAndVersion<Order> savedOrder = eventStore.save(Order.class.getName(), events, Optional.empty());
			return savedOrder.getEntityId();
		  }
		  
		}
		
4. Finally, we'll create a projection that subscribes to the OrderPlacedEvent and updates the application state accordingly:

		@Service
		public class OrderProjection {

		  @EventHandlerMethod
		  public void orderPlacedEventHandler(OrderPlacedEvent event) {
			// update application state with new order
		  }
		  
		}
		
That's it! With this implementation, when a user places an order, the PlaceOrderCommand is handled by the OrderService, which publishes an OrderPlacedEvent to the event store. The OrderProjection subscribes to the OrderPlacedEvent and updates the application state accordingly.

## Give an example of an event-sourcing implementation using the Axon framework. ##
Sure, here's an example of an event-sourcing implementation using the Axon framework:

Let's consider a simple e-commerce application that allows users to purchase items from a catalog. When a user places an order, we want to publish an event that reflects that order.

1. First, we'll define the event that will be published when an order is placed:

		public class OrderPlacedEvent {
		  private final String orderId;
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
		
2. Next, we'll create a command that represents the action of placing an order:

		public class PlaceOrderCommand {
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
		
3. We'll then define an aggregate that handles the PlaceOrderCommand and publishes the OrderPlacedEvent:

		@Aggregate
		public class OrderAggregate {

		  @AggregateIdentifier
		  private String orderId;

		  private String customerId;

		  private List<OrderLineItem> lineItems;

		  public OrderAggregate() {}

		  @CommandHandler
		  public OrderAggregate(PlaceOrderCommand command) {
			apply(new OrderPlacedEvent(command.getCustomerId(), command.getLineItems()));
		  }

		  @EventSourcingHandler
		  public void on(OrderPlacedEvent event) {
			this.orderId = event.getOrderId();
			this.customerId = event.getCustomerId();
			this.lineItems = event.getLineItems();
		  }
		  
		}
		
4. Finally, we'll create a projection that subscribes to the OrderPlacedEvent and updates the application state accordingly:

		@Projection
		public class OrderProjection {

		  @EventHandler
		  public void on(OrderPlacedEvent event) {
			// update application state with new order
		  }
		  
		}
		
That's it! With this implementation, when a user places an order, the `PlaceOrderCommand` is handled by the `OrderAggregate`, which publishes an `OrderPlacedEvent` to the event store. The `OrderProjection` subscribes to the `OrderPlacedEvent` and updates the application state accordingly. The Axon framework takes care of persisting the events to the event store, and replaying them to rebuild the application state if necessary.

## Give an end-to-end implementation example of the Eventuate framework. ##
Sure! Here's an end-to-end implementation example of the Eventuate framework using Java and Spring Boot:

Suppose we have a simple application that allows users to place orders for products. When a user places an order, we want to publish an event that reflects that order.

1. First, we'll add the eventuate-client and eventuate-local-java-jdbc dependencies to our pom.xml file:

		<dependency>
		  <groupId>io.eventuate.client</groupId>
		  <artifactId>eventuate-client</artifactId>
		  <version>0.7.2.RELEASE</version>
		</dependency>

		<dependency>
		  <groupId>io.eventuate.local</groupId>
		  <artifactId>eventuate-local-java-jdbc</artifactId>
		  <version>0.7.2.RELEASE</version>
		</dependency>

2. Next, we'll create a command that represents the action of placing an order:

		public class PlaceOrderCommand implements Command {
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
		
3. We'll then define an event that represents the order that was placed:

		public class OrderPlacedEvent implements Event {
		  private final String orderId;
		  private final String customerId;
		  private final List<OrderLineItem> lineItems;
		  // constructor, getters
		}
		
4. We'll create a service that handles the PlaceOrderCommand and publishes the OrderPlacedEvent:

		@Service
		public class OrderService {

		  @Autowired
		  private EventuateLocalProducer producer;

		  public String placeOrder(PlaceOrderCommand command) {
			String orderId = UUID.randomUUID().toString();
			OrderPlacedEvent event = new OrderPlacedEvent(orderId, command.getCustomerId(), command.getLineItems());
			String eventTopic = "OrderPlacedEvent";
			producer.send(eventTopic, event);
			return orderId;
		  }

		}
		
5. We'll create a REST controller that exposes an endpoint for placing orders:

		@RestController
		@RequestMapping("/orders")
		public class OrderController {

		  @Autowired
		  private OrderService orderService;

		  @PostMapping
		  public ResponseEntity<String> placeOrder(@RequestBody PlaceOrderCommand command) {
			String orderId = orderService.placeOrder(command);
			return ResponseEntity.status(HttpStatus.CREATED).body(orderId);
		  }

		}
		
6. Finally, we'll create a projection that subscribes to the OrderPlacedEvent and updates the application state accordingly:

		@Service
		public class OrderProjection {

		  @Autowired
		  private JdbcTemplate jdbcTemplate;

		  @EventHandlerMethod
		  public void orderPlacedEventHandler(OrderPlacedEvent event) {
			jdbcTemplate.update("INSERT INTO orders (order_id, customer_id, line_items) VALUES (?, ?, ?)",
			  event.getOrderId(),
			  event.getCustomerId(),
			  JSON.toJSONString(event.getLineItems()));
		  }

		}
		
And that's it! With this implementation, when a user places an order, the `PlaceOrderCommand` is handled by the `OrderService`, which publishes an `OrderPlacedEvent` to the Eventuate local event store using the `EventuateLocalProducer`. The `OrderProjection` subscribes to the `OrderPlacedEvent` and updates the application state by inserting the order into the `orders` table in the database. The `OrderController` exposes an endpoint for placing orders via HTTP.