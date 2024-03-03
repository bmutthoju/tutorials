# GraphQL Spring Boot #
## GraphQL Spring Boot #1 - Introduction ##
1. Topics:
	1. What is GraphQL?
	2. GraphQL vs REST vs gRPC
	3. How GraphQL works?
	4. Setting up Spring Boot project for GraphQL
	5. Constructing Controller and Repository
	6. Constructing a schema.graphqls file
	7. Executing a query
	8. Executing a mutation
	9. More into GraphQL schema and type
	10. Querying nested objects
	11. How data fetching works in GraphQL?
	12. Arguments and variables 
	13. Non null and list tokens
	14. Fragments and Directives
	15. Using Interface Type 
	16. Constructing a custom GraphQL scalar type
	17. Asynchronous data fetchers
	18. N+1 problem with data fetchers
	19. Using Java data loader to tackle N+1 problem
	20. Subscription in GraphQL

## GraphQL Spring Boot #2 - What is GraphQL ##
1. GraphQL
	1. Official definition:
		1. GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more.
			1. Important points from this definition:
				1. GraphQL is a query language for APIs & not a tool or a framework for designing APIs
				2. A client gets exactly what it wants from an API and nothing more than that
2. GraphQL is a collection of three things:
	1. Schema definition language or SDL
	2. Runtime environment
	3. Query language

### Schema definition language (SDL) ###
1. Schema definition language is used to define a GraphQL schema
2. A GraphQL schema is used to expose the functionalities that are available in an application to its users.
	1. For example: Virtual Library
		1. Adding a new book to a virtual library
		2. Getting a list of all books from that library
3. A GraphQL schema contains:
	1. Types which are similar to classes in Java
		1. Types can have fields
			1. Fields are similar to instance variables in Java
	2. Operations which can be performed on these Types. Similar to methods in Java
	
			type Query { // read only operations
				getBook(id:Int):Book
				getBooks:[Book]
			}
			
			type Mutation { // manipulate data on server
				createBook(name:String, pages:Int):Int
			}
			
			type Book { // Object type - used for user defined type
				id:Int
				name:String
				pages:Int
			}
			
### Runtime Environment ###
1. Runtime environment performs two major operations:
	1. Parsing the GraphQL schema file and constructing an 'In memory schema' from it
	2. Executing the operation specified in the client's request
2. Parsing the GraphQL schema file:
	1. Reading information from the schema file again & again will be inefficient
		1. So the runtime environment constructs an in memory representation of the schema file
			1. The in-memory representation contains all the information (types and operations) defined in that schema file
3. Executing the operations
	1. A user can use any of the operations that were defined in the schema file.
	2. Runtime environment is responsible for handling the user's request.
		1. It looks for the operation specified in the request
		2. It uses the in memory schema to check if that operation exists in the schema or not (validation)
		3. If it exists, then runtime will execute it and will perform the specified action
			1. Reading data at server OR
			2. Manipulating data at server
	3. Client passes queries to the runtime environment

### Query Language ###
1. Query language (offered by GraphQL) is used by clients to use operations that are defined in the GraphQL schema
2. QL enables a client to select only the required fields from a set of fields
	1. Examples:
	
			{
				getBooks {
					name
				}
			}
			
					|
				Runtime Environment
					|
					v
			
			{
				"data": {
					"getBooks": [
						{
							"name": "My latest book"
						},
						{
							"name": "My oldest book"
						}
					]
				}
			}
			
		1. It only returns names and not other fields

### Data Fetcher ###
1. A data fetcher is a call back function
2. It is linked to every query, mutation, and field.
	1. Every query or mutation is linked to a data fetcher
		1. The callback function is required by teh runtime environment to perform the required action
3. When a client uses an operation defined in the schema file then runtime environment invokes the data fetcher linked to that operation in order to perform the specified action

		// getBook(id:Int):Book
		public DataFetcher<Book> getBook() {
			return environment -> bookRepository.findById(environment.getArgument("id")).map(Function.identity()).orElse(null);
		}
		
		// getBooks:[Book]
		public DataFetcher<List<Book>> getBooks() {
			return environment -> bookRepository.findAll();
		}
		
		// createBook(name:String, pages:Int):Int
		public DataFetcher<Integer> createBook() {
			return environment -> bookRepository.save(new Book(environment.getArgument("name"), environment.getArgument("pages"))).getId();
		}
		
### Preparing in Memory Schema ###

		GraphQL schema file --+
		                      +--> Runtime Env --> In memory schema
		Data fetchers --------+
		
	1. Both are fed into runtime environment to get the in memory schema

### Executing the operation ###

		Client 
			|
			getBooks:[Book]
			|
			v
		Server 
			|
			Request body
			|
			v
		Runtime
			|
			I have parsed the query, now tell me
			is there anything like "getBooks" in schema
			v
		Schema
			|
			Yes, take the associated data fetcher
			and execute it for performing the action
			(returns the associated data fetcher)
			|
			v
		Runtime (executes the data fetcher)
			|
			Result
			|
			v
		Server
			|
			Response
			|
			v
		Client
		
### GraphQL in Action ###
1. Example:

		type Query {
			getBook(id: Int): Book
		}
		
		type Mutation {
			createBook(book: BookInput): Book
		}
		
		input BookInput {
			name: String
			pages: Int
			author: AuthorInput
		}
		
		type Book {
			id: Int
			name: String
			pages: Int
			author: Author
		}
		
		type Author {
			id: Int
			name: String
			age: Int
		}
		
	1. Request:
	
			POST: http://localhost:8080/graphql
			
			{
				getBook(id: 1) {
					name
					pages
					id
				}
			}

## GraphQL Spring Boot #3 - GraphQL vs REST vs gRPC ##
### Introduction ###
1. GraphQL
	1. GraphQL is a collection of:
		1. SDL
		2. Runtime environment
		3. Query Language
	2. GraphQL provides a mechanism through which:
		1. A client can request exactly what it wants from an API
			1. Nothing more or less
		2. A server can send only the required data specified by the client in the request
	3. It is not a tool or a framework for designing an API. It's all about querying an API and getting the exact data from it
		1. Example: API that returns a list of books
			1. Each book has several fields like - id, name, author, pages
			2. Author contains - id, name, age, address
			3. Case 1: If a client A wants to construct a web-page
				1. The client will be displaying a list of books will all fields
					1. API is suitable - it returns all the fields
			4. Case 2: If a client B wants to construct a web-page but he wants to display only the names of the books
				1. The API is not suitable - it returns all the information that is useless to the web-page
					1. Solution: GraphQL
						1. Client can request exactly what it wants from the API
							1. Server sends only the required data specified by the client in the request
	4. GraphQL is developed at Facebook
	5. In GraphQL first, we define types and the operations in a schema file using the SDL
	6. Later this file is parsed by the GraphQL runtime environment and it constructs an in-memory schema from it to handle the incoming requests
	7. GraphQL runtime environment does not interact with the clients directly, a controller has to be created that handles the client's request.
		1. It passes the request body the the GraphQL runtime environment
		2. The runtime environment performs the required action
			1. It fetches the operation from the request
			2. It validates the request (if it exists in the schema)
			3. If it exists, it will perform the action and returns the result to the controller
		3. The runtime environment returns the result to the Controller
		4. The controller constructs a response from the result
	8. GraphQL is **potocol independent** as it doesn't communicate with clients directly.
		1. There is a controller between the client and the GraphQL runtime environment.
		2. The controller expses the functionality offered by the GraphQL runtime
			1. There will always be a layer in between the client and the GraphQL runtime environment
	9. When to use it?
		1. In case of over-fetching: When a client is getting too much data from an API that is useless to it at the moment.
		2. In case of under-fetching: **When a client is not getting the required information from an Endpoint at once, and it has to request different Endpoints again and again to get the required information**
			1. It has support for batching using data loaders (?)
		3. When you prefer to use a single Endpoint overs multiple Endpoints
			1. Only one endpoint does all the work
2. REST
	1. REST is a group of six constraints (Architectural style):
		1. Client-server architecture
		2. Uniform interface
		3. Layered system
		4. Cache
		5. Stateless
		6. Code-on-demand - optional
	2. These constraints govern the scalability of the web.
	3. REST is not a tool or a framework
		1. It is an architectural style in which we satisfy all the above-mentioned constraints uniformly
	4. REST is commonly applied to the design of APIs for web services.
	5. It was the idea of Roy Fielding who is the co-founder of the Apache HTTP Server Project
		1. Web scalability depends on key constraints defined above
			1. Approach: to uniformly satisfy the above constraints so that web could expand or grow continously without any problem
	6. In REST, we construct resources
		1. Resource: It is usually (not always, it can be an HTML page, video, photo, document, etc.) mapped to a database row
			1. It provides a set of operations that can be performed on the row
			2. A resource is identified by a URI
			3. An operation is identified by a URI, HTTP method, and Media type
			4. Resources are called endpoints
				1. An endpoint exposes a set of data and functions to facilitate interactions between client and server
					1. It allows them to exchange information
				2. It is one end of the communication channel
	7. The web's scalability depends on how better we use the HTTP. REST is a solution to the Web's scalability problem so it is **tightly coupled with HTTP**.
		1. It depends on HTTP
	8. When to use it?
		1. When you want a simple solution or constructing an API
			1. We don't have to maintain any schema file or proto file
		2. When you want your APIs to be easily scalable
			1. HTTP is a very scalable protocol 
				1. Hence REST is scalable
		3. When you want to allow your clients to get different representations of the same resource as XML, JSON, HTML, etc.
			1. GraphQL supports only JSON so far
			2. gRPC supports only binary and JSON so far
			3. REST supports multiple formats of serialization and deserialization
		4. When you prefer to divide responsibilities into multiple enpoints
		5. When you want default support for caching in browsers
			1. Default support for HTTP caching
				1. GraphQL needs additional setup for caching
3. gRPC
	1. gRPC is a modern open-source high-performance RPC framework that can run in any environment
	2. In gRPC, a client application can directly call a method on a server application on a different machine as if it were a local method
		1. Making it easier for developers to construct distributed applications and services.
			1. Client invokes a function reciding on a server remotely
	3. gRPC is developed at Google
	4. Procedure:
		1. In gRPC, we construct services that contain methods that can be called remotely with their parameters and return types
		2. On the server side, server:
			1. Implements the interface
			2. Runs a gRPC server to handle client calls
				1. At specific IP and port number
		3. On the client side, the client:
			1. Has a stub (fake object that contains same methods as the object on the server side) that provides the same methods as the server
		4. The services are defined in a proto file that is created using Protocol Buffers
			1. Protocol Buffers: Flexible, efficient, automated mechanism for serializing structured data
				1. Like XML, but smaller, faster, and simpler
		5. Client uses stub to call a method implemented at server, remotely
		6. gRPC uses HTTP/2 as it provides support for the **bidirectional streaming of data**.
			1. It depends on HTTP/2
		7. When to use it?
			1. When you want a high-performance communication channel in your microservices for exchanging information
				1. Protocol buffer with binary is very fast
					1. Leaves a small footprint
			2. When you want out of the box support for bi-directional streaming of data
				1. It also has pluggable support for:
					1. Authentication
					2. Load balancing
					3. ...
			3. When your primary client is not a browser
				1. Browser cannot invoke a remote procedure directly
4. Examples:
	1. GraphQL Schema File:
	
			type Query {
				getBook(id:Int):Book
				getBooks:[Book]
			}
			
			type Book {
				id:Int
				name:String
				pages:Int
				author:Author
			}
			
			type Author {
				id:Int
				name:String
				age:Int
				address:String
			}
			
		1. Two types are defined: Book, Author
		2. Two operations: getBook, getBooks
	2. REST Endpoint (In Java using JAX-RS)
	
			/**
			 *
			 */
			@Path("books")
			public class BookEndpoint {
				@Inject
				private BookService bookService;
				
				@GET
				@Path("bookId")
				@Produces(MediaType.APPLICATION_JSON)
				public Book getBook(@PathParam("bookId") int bookId) {
					return bookService.getBook(bookId);
				}
				
				@GET
				@Produces(MediaType.APPLICATION_JSON)
				public List<Book> getBooks() {
					return bookService.getBooks();
				}
			}
			
		1. Two operations on the endpoint: "books"
			1. GET: getBook, Media type: application/json
			2. GET: getBooks, Media type: application/json
	3. gRPC Proto file
	
			syntax = "proto3";
			import "google/protobuf/empty.proto";
			package MicroservicesLab;
			option java_package = "com.microserviceslab.grpc";
			option java_outer_classname = "BookService";
	
			service BookService {
				rpc GetBook (Request) returns (Book);
				rpc GetBooks (google.protobuf.Empty) returns (Response);
			}
			
			message Request {
				int32 id = 1;
			}
			
			message Response {
				repeated Book book = 1;
			}
			
			message Book {
				int32 id = 1;
				string name = 2;
				int32 pages = 3;
				Author author = 4;
			}
			
			message Author {
				int32 id = 1;
				string name = 2;
				int32 age = 3;
				string address = 4;
			}
			
		1. Protofile is used as the interface definition language & as serialization format

## GraphQL Spring Boot #4 - How GraphQL works in Java? ##
1. How GraphQL works in Java?

		Schema file                            Data Fetchers
			|                                        |
			v                                        v
		SchemaParser                            TypeWiring
			|                                        |
			v                                        v
		TypeDefinitionRegistry					RuntimeWiring
			|                                        |
			+-------------------+--------------------+
			                    |
								v
							SchemaGenerator
								|
								v
							GraphQLSchema
								|
								v
							GraphQL
							
	1. Schema file - contains types and operations that can be performed on the types
	2. SchemaParser - Class provided by GraphQL Java API
		1. An object of `SchemaParser` class is created to parse the schema file
	3. TypeDefinitionRegistry - We get an instance of this class as a result of parsing Schema file
		1. It is an in-memory representation of the schema file
	4. Data Fetchers: Each data fetcher is associated with an operation or a field
		1. To represent the link between operation and data fetcher or field and data fetcher, we need to construct an instance of `TypeWiring`
			1. `TypeWiring` - Represents link between field/operation and a data fetcher
				1. It can be more than one instance of TypeWiring (multiple linkins)
			2. `RuntimeWiring` - All instances of `TypeWiring` are fed into `RuntimeWiring` class to construct an instance of the `RuntimeWiring` class
	6. `ScemaGenerator` - The `SchemeGenerator` class combines `TypeDefinitionRegistry` and `RuntimeWiring` instances, to construct `GraphQLSchema` class instance
	7. `GraphQL` - `GraphQLSchema` is used to construct the `GraphQL` instance
		1. It is used to handle the client requests

### How GraphQL works in Java? ###

		Client
			^	|
			|	v
		Controller
			^	|
			|	v
		GraphQL
			^	|
			|	v
		Data Fetcher
			^	|
			|	v
		DB / API
		
	1. In Controller, there is always a method that uses `GraphQL` object to manage the request body
		1. The method is usually mapped to teh URI path `/graphql`
			1. Example: "http://localhost:8080/graphql"
	2. Whenever a client sends a request to the URI path, then Controller passes the request body to `GraphQL` object
		1. The `GraphQL` object performs the following steps:
			1. Fetch the query from the request body
			2. Fetch the variables (if provided from the request body)
			3. Fetch the operation name (if provided from the request body)
			4. Execute the Data Fetcher associated with the query and return the result
				1. It fetches data from database or from API
		2. Controller prepares response once data is obtained from `GraphQL` object and sends it back to the client
2. Code:
	1. GraphQL Schema:
	
			type Query {
				getBook(id: Int): Book
				getBook: [Book]
			}
			
			type Book {
				id: Int
				name: String
				pages: Int
				author: Author
			}
			
			type Author {
				id: Int
				name: String
				age: Int
			}
			
	2. Instance of GraphQL class
	
			@Bean
			public GraphQL graphQL() IOException {
				SchemaParser parser = new SchemaParser();
				TypeDefinitionRegistry typeDefinitionRegistry = parser.parse(new ClassPathResource("schema.graphql").getInputStream());
				
				RuntimeWiring runtimeWiring = RuntimeWiring.newRuntimeWiring()
					.type("Query", typeWiring -> typeWiring.DataFetcher("getBook", bookService.getBook()))
					.type("Query", typeWiring -> typWiring.DataFetcher("getBooks", bookService.getBooks()))
					.type("Book", typeWiring -> typeWiring.dataFetcher("author", typeWiring -> authorService.getAuthor())) // to map field, we use its name and map it with the associated data fetcher, and the author field is in the Book type
					.build();
					
					SchemaGenerator generator = new SchemaGenerator();
					GraphQLSchema graphQLSchema = generator.makeExecutableSchema(typeDefinitoinRegistry, runtimeWiring);
					GraphQL graphQL = GraphQL.newGraphQL(graphQLSchema).build();
					
					return graphQL;
			}
			
	3. Data fetchers:
	
			@Service
			public class BookService {
				
				@Autowired
				private BookRepository repository;
				
				public DataFetcher<CompletableFuture<Book>> getBook() {
					return env -> repository.getBook(env.getArgument("id")).toFuture();
				}
				
				public DataFetcher<CompletableFuture<List<Book>>> getBooks() {
					return env -> repository.getBooks().collectList().toFuture();
				}
			}
			
			@Service
			public class AuthorService {
				
				@Autowired
				private AuthorRepository repository;
				
				public DataFetcher<CompletableFuture<Author>> getAuthor() {
					return env -> {
						Book book = env.getSource();
						return repository.getAuthor(book.getId()).toFuture();
					}
				}
			}
			
	4. Controller
	
			@RestController
			public class GraphQLController {
				
				@Autowired
				private GraphQL graphQL;
				
				@PostMapping(value = "graphQL", consumes = MediaType.APPLICATION_JSON_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
				public Mono<Map<String, Object>> execute(@RequestBody GraphQLRequestBody body) {
					return Mono.fromCompletionStage(graphQL.executeAsync(builder -> builder.query(body.getQuery()).variables(body.getVariables()).operationName
				}
			}

## GraphQL Spring Boot #5 - Setting up a Spring Boot Project for GraphQL ##
1. Steps:
	1. Install IDE
		1. STS or Eclise
			1. STS: spring.io/tools
				1. Download and install
					1. Execute the jar file
			2. Eclipse: eclipse.org/downloads
	2. Spring Boot Starter project:
		1. start.spring.io
		2. STS
			1. Group: com.microserviceslab
			2. Artifact: graphql
			3. Name: graphql
			4. Description: Just a demo project for GraphQL
			5. Package name: com.microserviceslab.graphql
			6. Java: 11
			7. Dependencies:
				1. Spring Reactive Web
				2. H2 Database
				3. Spring Data R2DBC
			8. Generate
		3. Extract and import in STS
			1. File
			2. Import
			3. Maven
				1. Existing Maven Projects
					1. Browse
						1. graphql
			4. Finish
		4. Adding a dependency:
			1. pom.xml
			
					<dependency>
						<groupId>com.graphql-java</groupId>
						<artifactId>graphql-java</artifactId>
						<version>15.0</version>
					</dependency>
					
		5. Right click on project
			1. Maven
				1. Update the project
	3. GraphQL Client
		1. Altair - easy to use
			1. altair.samuel.design
		2. Open

## GraphQL Spring Boot #6 - Constructing a Controller and a Repository ##
1. Package: controller
	1. GraphQLController.java
	
			@RestController
			public class GraphQLController {
			
				@Autowired
				private GraphQL graphQL;
				
				@PostMapping(value = "graphql", consumes = MediaType.APPLICATION_JSON_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
				public Map<Map<String, Object>> execute(@RequestBody GraphQLRequestBody body) {
					return Mono.fromCompletionStage(
						graphQL.executeAsync(ExecutionInput
						.newExecutionInput()
						.query(body.getQuery())
						.operationName(body.getOperationName())
						.variables(body.getVariables())
						.build()
					)
					.map(ExecutionResult::toSpecification);
				}
			}
			
		1. `ExecutionResult::toSpecification` - converts the data and errors returned by GraphQL java API into the format of GraphQL

2. Package: model
	1. GraphQLRequestBody.java (clients send the following fields)
	
			private String query;
			private String operationName;
			private Map<String, Object> variables;
			
			// getters and setters
			
	2. Book.java
	
			@Table("Books")
			public class Book {
			
				@Id
				private int id;
				private String name;
				private int pages;
				
				// Constructor from fields, removing the id field
				// Default constructor
				// Getters and setters
			}
			
	3. BookRepository.java
	
			@Repository
			public class BookRepository {
			
				@Autowired
				private DatabaseClient databaseClient;
			
				public Mono<Book> getBook() {
					return databaseClient
					.select()
					.from(Book.class)
					.matching(Criteria.where("id").is(id))
					.fetch()
					.one();
				}
			}

3. Package: repository
4. pom.xml
	1. Remove runtime scope from the io.r2dbc dependency
		1. Spring Data R2DB doesn't instantiate a table as Spring Data JPA. A table needs to be created manually
			1. SQL file: src/main/resources/schema.sql
			
					CREATE TABLE books (
						id INT PRIMARY KEY AUTO_INCREMENT,
						name VARCHAR(255),
						pages INT
					);
					
			2. GraphqlApplication.java
			
					@Bean
					public ConnectionFactoryInitializer connectionFactoryInitializer(ConnectionFactory factory) {
						ConnectionFactoryInitializer initializer = new ConnectionFactoryInitializer();
						initializer.setConnectionFactory(factory);
						
						ResourceDatabasePopulator populator = new ResourceDatabasePopulator(new ClassPathResource("schema.sql"));
						initializer.setDatabasePopulator(populator);
						
						return initializer;
					}

## GraphQL Spring Boot #7 - Constructing a GraphQL Schema ##
1. Schema file: src/main/resources/schema.graphql

		type Query {
			getBook(id: Int): Book
			getBooks:[Book]
		}

		type Book {
			id: Int
			name: String
			pages: Int
		}
		
	1. `[<type>]` - list of `types`s

2. Data Fetchers: service.BookService.java

## GraphQL Spring Boot #8 - Executing a Query ##
## GraphQL Spring Boot #9 - Executing a Mutation ##
## GraphQL Spring Boot #10 - Mutating a nested object ##
## GraphQL Spring Boot #11 - Querying nested object. ##
## GraphQL Spring Boot #12 - Enums in GraphQL ##
## GraphQL Spring Boot #13 - Variables in GraphQL ##
## GraphQL Spring Boot #14 - GraphQL Non Null ##