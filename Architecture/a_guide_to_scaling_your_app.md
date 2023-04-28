# From 0 to Millions: A Guide to Scaling Your App - Part 1 #
1. Typical architectural evolution of a website/app, how/why we make technical choices at different stages.
	1. Do we build a monolithic application at the beginning?
	2. When do we add a cache?
	3. When do we add a full-text search engine?
	4. Why do we need a message queue?
	5. When do we use a cluster?
2. Topics:
	1. Traditional approach to building an application, starting with a single server
	2. Concluding with a cluster of servers capable of handling millions of daily active users
	3. Impact of recent trends in cloud and serverless computing on application building
		1. How they changed the way we build applications
		2. Insights on how to consider the modern approaches when constructing the next big hit
	4. How a typical startup builds its first application
	5. Serverless computing makes it easier to start an application that could scale to tens of thousands of users with very little upfront investment
		1. How to take advantage of this trend
	6. How an application (Llama) is traditionally built at the start

## Llama 1.0 - Monolithic Application, Single Server ##
1. The entire application stack lives on a single server
2. The server is publicly accessible over the internet
3. It provides a RESTful API to handle the business logic (for mobile and web client applications to access)
4. It serves static contents like imags and application bundles that are stored directly on the local disk of the server
5. The application server is connected to the database which also runs on the same server
6. Benefits:
	1. It could server hundreds, or even thousands of users
		1. Actual capacity depends on the complexity of the application
7. Drawbacks:
	1. If there is growing user load, scale up to a larger server with more CPU, memory, and disk space (to buy some more time)
		1. Temporary solution
			1. Eventually, even the biggest server will reach its limit
	2. With the entire stack running on a single server, there is no failover or redundancy
		1. When the server inevitably goes down, resulting downtime could be unacceptably long
8. Next: Solving the operational issues

# From 0 to Millions: A Guide to Scaling Your App - Part 2 #
## Llama 5.0 - Add Cache ##
1. Once primary-replica architecture is implemented, most applications should scale to several hundred thousand users
	1. Some simple applications might reach a million users
2. **For some read-heavy applications, primary-replica architecture might not be able to handle traffic spikes well**
	1. Example: Flash sales events like Black Friday sales in US could overload databases
		1. If load is sufficiently heavy, users might not even be able to load the sales page
	2. **Solution**: **Add cache layer to optimize read operations**
		1. Redis: Popular in-memory cache
			1. It reduces the read load for a database by caching frequently accessed data in memory
			2. It allows for faster access to the data since it is retrieved from the cache instead of the slower database
		2. **By reducing the number of read operations performed on the database, Redis helps to reduce load on the database cluster and improve the overall scalability**
	3. Access speeds:
		1. L1 Cache: 1ns
		2. L2 Cache: 10ns
		3. RAM access: 100ns
		4. 1 us
		5. Send data over network (Memcached send data over 1 Gbps network): 10 us
		6. Read from SSD (RocksDB read): 100 us
		7. Database insert (Postgresql insert): 1 ms
		8. HDD disk seek: 10 ms
		9. Packet CA -> NL -> CA (Remote Zoom call): 100 ms
		10. 1s
		11. Retry/refresh interval (Grafana refresh interval): 1s
3. We use **read-through** strategy:
	1. Data is first checked in the cache before being read from database
	2. If data is found in the cache, it is returned immediately,
	3. If data is not found in the cache, it is loaded from the database and stored in the cache for future use
4. Other cache strategies & operational considerations (when deploying a caching layer at scale)
	1. If there is another copy of data stored in cache, we need to maintain data consistency (later)
5. Another class of application data that is highly cacheable: static contents for application (infrequently updated data)
	1. Types of files:
		1 Images
		2. Videos
		3. Style sheets
		4. Application bundles
	2. Solution: Should be served by Content Delivery Network (CDN)
		1. CDN serves static content from a network of servers located closer to the end user
			1. Reduces latency
			2. Improves the loading speed of the web pages
		2. Benefits:
			1. Better user experience (especially for users located far away from the application server)
		3. Implementation: Cloudflare

## Llama 6.0 - DB Sharding ##
1. Cache layer gives some relief for read-heavy applications
2. As we continue to scale, amount of write requests will start to overload the single primary database
	1. Solution: Shard the primary database
3. Ways of sharding:
	1. Horizontal sharding
		1. More common
		2. Divides data across multiple database servers based on the values in one or more columns of a table
		3. Example: Large user table can be partitioned based on user ID
		4. Results in multiple smaller tables stored on separate database servers
			1. Each server handles a small subset of the rows that were previously handled by the single database
	2. Vertical sharding
		1. Less common
		2. Separates tables or parts of a table into different database servers based on specific needs of the application
			1. Optimizes application based on specific access patterns of each column
4. Drawbacks:
	1. Adds complexity to the application and database layer
	2. Data must be partitioned and distributed across multiple databases making it difficult to ensure data consistency and integrity
	3. Introduces performance overhead
		1. Increases application latency
			1. **Especially if application needs data from multiple shards**
			
# From 0 to Millions: A Guide to Scaling Your App - Part 3 #
1. Topics:
	1. Impact of recent trends like cloud and serverless computing
	2. Proliferations of client application frameworks and associated developer ecosystem
	3. How the trends alter the way we build applications, especially for early-stage startups where time-to-market is critical
	4. How to incorporate the modern approaches when constructing the next big hit

## Recent Trends ##
1. Cloud computing:
	1. Basic form: Running applications on computing resources managed by cloud providers
	2. We do not have to purchase hardware ourselves
2. Serverless computing:
	1. Builds on convenience of cloud computing with more automation
	2. Enables developers to build and run applications without having to provision cloud servers
		1. Serverless provider handles the infrastructure and automatically scales computing resources up or down as needed
			1. Helps developer focus on application code without having to worry about scaling
3. Proliferation of client application frameworks and frontend hosting platforms
	1. Rides on the waves of the above two trends
	2. Makes deploying frontend applications effortless

## Modern Frontend Frameworks and Hosting Platforms ##
1. Popular applications today: Single Page Applications (SPA)
2. SPA:
	1. Provides seamless user experience
		1. Dynamically updates current page instead of loading a new one each time user interacts with the application.
		2. **Initial HTML and its resources are loaded once, and subsequent interactions with the application are handled using JavaScript to manipulate the existing page content**
	2. Loads initial HTML frame and then makes requests to server for data as needed
		1. More efficient use of server resources
			1. Since server is not sending full HTML pages
			2. Since server only focuses on serving data (via a well-defined api)
				1. Benefits of API-centric approach:
					1. Same API is often shared with mobile app
						1. This makes backend easier to maintain
	3. SPAs are often built using JavaScript frameworks like React
		1. The tools provide a set of abstractions and tools for building complex applications **optimized for performance and maintainability**
3. MPA: Multipage application
	1. Serving up new HTML pages from the server every time user clicked on a link or submitted a form
	2. Each page request involves full page refresh
		1. It could be slow and sometimes disruptive to user experience
	3. Requires server centric approach
		1. **It can be challenging to scale and maintain as application grows in complexity**
4. Popularity of client frameworks brought production-grade frontend hosting platforms
	1. Examples: **Netify**, **Vercel**
	2. The hosting platforms handle the complexity of building and deploying modern frontend applications at scale
		1. Developers check their code into repo
		2. Hosting platforms take over from there
			1. They automatically build the web application bundle and its associated resources and distribute them to the CDN
	3. Benefits:
		1. Since the hosting platforms are built on the cloud and serverless computing foundation, using best practices like serving data at the edge close to the user, **they offer practically infinite scale**
		2. There is no infrastructure to manage
	4. Modern frontend landscape:
		1. Frontend application is built with a modern framework like React
		2. Client app is served by a production-grade hosting platform for scale
		3. Client app dynamically fetches data from the backend via a well-defined API

## Modern Backend Options ##
1. The role of a modern backed is to serve a set of well-defined APIs to support the frontend web and mobile applications
2. What modern options exist to build a backend?
	1. For a small resource constrained startup
		1. When time-to-market is critical and resources are limited, startup should opffload as much non-core work as possible.
			1. Solution: Serverless computing
				1. Serverless computing manages the operational aspects of the backend
					1. Operations:
						1. Scaling
						2. Redundancy
						3. Failover
					4. Frees us startup team from managing infrastructure
				2. Serverless computing follows cost-effective pay-per-use pricing model
					1. There is no up-front commitment
				3. Serverless computing allows developers to focus on writing code and testing the backend without worrying about managing servers, leading to shorter time to market
				
# From 0 to Millions: A Guide to Scaling Your App - Final Part #
1. As traffic continues to scale, modern stack will eventually reach its limits
	1. Need to examine where the modern stack might fall apart
	2. Need to define strategies to evolve the stack to handle more traffic
2. Topics:
	1. How a hyper-growth startup can gradually migrate to a microservices architecture by leveraging cloud native strategies
	
## Scaling Modern Startup Stack ##
1. Depending on the complexity of the application, the stack should be able to handle low hundreds of thousands of daily active users

### Monitoring and Observability ###
1. We should have a robust monitoring and observability system in place before we run into performance issues
	1. Otherwise, we will not know when the application starts to fall apart due to rising traffic load
2. Buy a solution:
	1. Cloud providers have in-house offerings: AWS Cloud Operations (might be sufficient)
	2. SaaS offerings are powerful but expensive
3. The following system-wide performance metrics can be monitored
	1. For database:
		1. Read and write request rate
		2. Query response time. (Track p95 and median at the very least)
		3. Database connections
			1. Most dbs have a connection limit
				1. Track the number of connections to identify when to scale the db resources to handle increased traffic
		4. Lock contention
			1. Measures the amount of time a database spends waiting for locks to be released
				1. Helps identify when to optimize the database schema or queries to reduce contention
		5. Show queries
			1. Tracks the number of slow queries
				1. Early sign of trouble when the rate starts to increase
	2. For Application Tier
		1. Incoming request rate
		2. Response time
			1. Measures the time it takes for an application to respond to a request
			2. Track at least p95 and median
		3. Error rate
			1. Tracks the percentage of requests that result in an error
		4. Network throughput
			1. Measures the amount of network traffic the application is generating

## Scaling the Serverless Database Tier ##
1. First place that could break is the database tier
	1. As traffic grows, **combined read and write traffic could start to overwhelm the serverless relational database**
		1. The limit could be quite high
		2. The compute tier and storage tier scale independently
			1. **Compute tier transparently scales vertically to a bigger instance as load increases**
		3. Metrics would start to deteriorate and could start to overload the single serverless database
			1. **Playbook to scale the db tier is well-known and stays almost the same as in the early days**

### Read Replicas ###
1. For read-heavy applications:
	1. Migrate read load to read replicas
		1. Add a series of read replicas to primary database to handle reads
		2. We can also have **different replicas to handle different kinds of read queries to spread the load**
	2. Drawbacks:
		1. **Replication lag**
			1. It is the **time difference between when a write operation is performed on the primary database and when it is reflected in the read replica**
			2. When replication lag occurs, it can lead to stale or inconsistent data being returned to clients (when replica is queried)
				1. The slight inconstency is whether acceptable depends on case-by-case basis (tradeoff for supporting ever-increasing scale)
					1. **For a small number of reads that cannot tolerate any lags, the reads can always be directed at the primary database**

### Caching ###
1. Another approach: Add caching layer to optimize read operations
	1. Redis: in-memory cache for this purpose
		1. It reduces read load for database
			1. Caches frequently accessed data in memory
				1. **Hence enhances the dbs overall scalability**
		2. Faster access to data since it is retrieved from cache instead of slower database
		3. **Managed Redis solutions are available through many cloud providers**
			1. Reduces the burden of operating a caching tier on a day-to-day basis

### Database Sharding ###
1. A technique used to partition data across multiple database servers based on the value in one or more columns of a table
	1. Example: Large user table can be divided based on user ID
		1. Results in multiple smaller tables stored on separate database servers
		2. Each server handles a small subset of the rows that were previously managed by the sinle primary database (improved query performance as each shard handles a small subset of data)
2. Drawbacks
	1. It adds complexity to both the application and database layers
	2. Managing and maintaining an increasing number of database shards becomes more complex
	3. Application developers need to implement sharding loging in the code to ensure that correct database shard is accessed for a given query or transaction
	4. It makes is harder to perform cross-shard queries or join data from multiple shards
		1. **Restricts the types of queries that can be performed**
3. Advantages:
	1. Used when vertical scaling is not feasible
4. When to choose sharding?
	1. If the benefits of sharding outweighs its added complexity and limitations
	2. When vertical scaling is no longer feasible

### Shifting Workload to NoSQL ###
1. Instead of sharding, migrate a subset of data to NoSQL
	1. NoSQL DB offers 
		1. Horizontal scalability
		2. Hig write rates
	2. Drawbacks:
		1. No schema flexibility in the data model
			1. Migrate data to NoSQL **if the subset does not rely on the relational model**
				1. It could be an effective approach to scale the application
2. Strategy:
	1. **Relational database can focus on more complex queries**
	2. **NoSQL database can handle high-write workloads**
		1. Carefully consider which subset of data is migrated
			1. Migration process must be planned and executed carefully **to avoid data inconsistencies or loss**