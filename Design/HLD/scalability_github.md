## System Design Topics ##
1. Client
2. DNS
3. CDN
4. Load Balancer
5. Web Server
6. Read API
7. Write API
8. Timeline Service
9. Fan Out Service
10. Memory Cache
11. Search API
12. User Graph Service
13. Search Service
14. Notification Service
15. Tweet Info Service
16. User Info Service
17. Memory Cache
18. SQL Read Replicas
19. SQL Write Master-Slave
20. Object Store
21. Notification Service

## System Design Concepts ##
1. Performance vs Scalability
2. Latency vs Throughput
3. Availability vs Consistency
	1. CAP Theorem
		1. CP - Consistency and Partition Tolerance
		2. AP - Availability and Partition Tolerance
4. Consistency Patterns
	1. Weak consistency
	2. Eventual consistency
	3. Strong consistency
5. Availability Patterns
	1. Fail-over
	2. Replication
	3. Availability in numbers
6. Domain Name System
7. Content Delivery Network
	1. Push CDNs
	2. Pull CDNs
8. Load Balancer
	1. Active-Passive
	2. Active-Active
	3. Layer 4 Load Balancing
	4. Layer 7 Load Balancing
	5. Horizontal Scaling
9. Reverse Proxy (Web Server)
	1. Load Balancer vs Reverse Proxy
10. Application Layer
	1. Microservices
	2. Service Discovery
11. Database
	1. Relational Database Management System (RDBMS)
		1. Master-Slave Replication
		2. Master-Master Replication
		3. Federation
		4. Sharding
		5. Denormalization
		6. SQL Tuning
12. NoSQL
	1. Key-Value Store
	2. Document Store
	3. Wide-Column Store
	4. Graph Database
13. SQL or NoSQL
14. Cache
	1. Client Caching
	2. CDN Caching
	3. Web Server Caching
	4. Database Caching
	5. Application Caching
	6. Caching at the Database Query Level
	7. Caching at the Object Level
	8. When to Update the Cache
		1. Cache-Aside
		2. Write-Through
		3. Write-Behind (Write-Back)
		4. Refresh-Ahead
15. Asynchronism
	1. Message Queues
	2. Task Queues
	3. Back Pressure
16. Communication
	1. Transmission Control Protocol (TCP)
	2. User Datagram Protocol (UDP)
	3. Remote Procedure Call (RPC)
	4. Representational State Transfer (REST)
17. Security
18. Appendix
	1. Powers of Two Table
	2. Latency numbers every programmer should know
	3. Additional system design interview questions
	4. Real world architectures
	5. Company architectures
	6. Company engineering blogs
19. Under development
20. Credits
21. Contact Info
22. License

## Performance vs Scalability ##
1. Scalability: Increase of performance proportional to resources added
2. **Performance problem**:
	1. System is slow for single user
3. **Scalability problem**:
	1. System is fast for single user but slow under heavy load

## Latency vs Throughput ##
1. **Latency**: Time to perform an action or produce some result.
2. **Throughput**: Number of actions performed per unit of time.
3. Tip:
	1. **Aim for maximal throughput with acceptable latency**

## Availability vs Consistency ##
1. CAP Theorem
	1. Consistency
	2. Availability
	3. Partition Tolerance
2. Only two of the following guarantees can be supported in a computer system
	1. **Consistency**: Every read receives most recent write or an error
	2. **Availability**: Every request receives a response, without guarantee that it contains the most recent version of the information
	3. **Partition Tolerance**: System continues to operate despite arbitrary partition due to network failures
		1. Networks aren't reliable, so we'll need to support partition tolerance
			1. So we have only two options with distributed systems
				1. **CP**: Consistency and Partition Tolerance
					1. Waiting for response from partitioned node might result in timeout error
					2. Good if system needs atomic reads and writes
				2. **AP**: Availability and Partition Tolerance
					1. Response returns most readily available version of the data on a node (might not be the latest)
						1. Writes might take some time to propagate when partition is resolved
						2. Good choice if business needs to allow eventual consistency or when system needs to continue working despite external errors

## Consistency Patterns ##
1. Problem: If we have multiple copies of data, how do we synchronize them so that clients can have a consistent view of the data? (every read receives the most recent write or an error)

### Weak Consistency ###
1. After a write, reads may or may not see it
	1. Best effort approach
2. Usecases:
	1. Memcached
	2. Real-time use-cases
		1. VoIP
			1. If we lose reception for a few seconds, and if we regain connection, we do not hear what was spoken during connection loss
		2. Video chat
		3. Realtime multiplayer games

### Eventual Consistency ###
1. After a write, reads will eventually see it (typically within milliseconds)
	1. Data is replicated asynchronously
2. Use-cases:
	1. DNS
	2. Email
3. Works well with highly available systems

### Strong Consistency ###
1. After a write, reads will see it
	1. Data is replicated synchronously
2. Usecases:
	1. Files systems
	2. RDBMSs
3. Works well in systems that need transactions

## Availability Patterns ##
1. Two complementary patterns to support HA
	1. Failover
	2. Replication

### Fail-Over ###
#### Active-Passive ####
1. Heartbeats are sent between active and passive server on standby
	1. If heartbeat is interrupted, passive server takes over active's IP address and resumes service
2. Length of downtime
	1. Determined by 
		1. Whether passiver server is already running in 'hot' standby or
		2. Whether it needs start up from 'cold' standby
3. **Only the active server handles traffic**
4. AKA Master-Slave failover

#### Active-Active ####
1. Both servers are managing traffic
	1. Load is spread between them
2. If servers are public facing, DNS would need to know about the public IPs of both servers
3. If servers are internal facing, application logic would need to know about both servers
4. AKA Master-Master failover

#### Disadvantage(s): Failover ####
1. Fail-over adds more hardware and additional complexity
2. There is a potential for loss of data if the active system fails before any newly written data can be replicated to the passive

### Replication ###
#### Master-Slave and Master-Master ####
1. [Master-Slave Replication](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#master-slave-replication)
	1. Master: Serves reads and writes
		1. Replication writes to one or more slaves
		2. **If master goes offline, system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned**
	2. Slaves: Serves reads only
		1. Can replicate to additional slaves in a tree-like fashion
	3. Disadvantages:
		1. Additional logic is required to promote a slave to master
2. [Master-Master Replication](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#master-master-replication)
	1. Masters: All serve both reads and writes
		1. They need to coordinate with each other on writes
		2. If a master goes down, system can continue to operate with another master
	2. Disadvantages
		1. Need load-balancer or update application logic to decide where to write
		2. Systems can be:
			1. Loosely consistent (violating ACID)
		3. Conflict resolution may be required
			1. More so if more nodes are added
			2. If latency increases

## Availability in Numbers ##
1. Availability: Uptime (or downtime) as a percentage of time the service is available
	1. Usually measured in number 9s
		1. 99.99% - four 9s
	2. 99.9%:
		1. Downtime per year: 8h 45m 57s
		2. Downtime per month: 43m 49.7s
		3. Downtime per weak: 10m 4.8s
		4. Downtime per day: 1m 26.4s
	3. 99.99%
		1. Downtime per year: 52min 35.7s
		2. Downtime per month: 4m 23s
		3. Downtime per weak: 1m 5s
		4. Downtime per day: 8.6s

### Availability in Parallel vs Sequence ###
1. A service's availability depends on whether components are in sequence or in parallel
	1. Availability decreases if two components with avaialability < 100% are in sequence

			Availability (Total) = Availability (Foo) * Availability (Bar)

		1. Example: 99.9% x 99.9% = 99.8%
	2. Availability increases when two components with availability < 100% are in parallel

			Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar))

		1. 1 - (1 - 0.999) * (1 - 0.999) = 1 - 0.001 * 0.001 = 1 - 0.000001 = 0.999999 = 99.9999%

## Domain Name System ##
### How does DNS Work? ###
1. DNS translates domain name to IP address
2. DNS is hierarchical
	1. Authoritative servers are at the top level
	2. ISP provides info about which DNS servers to contact when doing a lookup
	3. Lower level DNS servers cache mappings
		1. They becomes stale due to DNS propagation delays
	4. DNS results can be cached by browser or OS
		1. Determined by TTL (Time to Live)
3. Config
	1. NS record (Name server): Specifies DNS servers for domain/subdomain
	2. MX record (mail exchange): Specifies mail servers for accepting messages
	3. A record (address) - points a name to an IP address
	4. CNAME (canonical) - points a name to another name or `CNAME`
		1. Example: to `www.example.com` or to an `A` record
4. Routing methods:
	1. Weighted round robin
		1. Prefent traffic from going to servers under maintenance
		2. Balance between varying cluster sizes
		3. A/B testing
	2. Latency-based
		1. Example:
			1. DNS routes query to a Route53 server
			2. Route53 refers to its data on latency between London and the Singapore Region, and between London and Oregon Region
			3. If latency is lower between the London and Oregon Regions, Route 53 responds to query with IP address for the Oregon load balancer. If latency is lower between London and Singapore Region, Route 53 responds with the IP address for the Singapore load balancer
		2. Measurements are taken over a period of time to reflect changes in latency.
	3. Geolocation-based
		1. Routing is based on location that DNS queries originate from (location of users)
			1. Example: All queries from Europe to be routed to an ELB in Frankfurt region
		2. Advantages:
			1. Localization of content
			2. Presenting some or all our website in languge our users
			3. Restrict distribution of content to only locationsin which we have rights.
			4. Helps balance load across endpoints in a predictable way
5. Disadvantages of using DNS:
	1. Accessing a DNS server introduces slight delay
		1. Mitigated by caching
	2. DNS server management is complex
		1. Generally managed by governments, ISPs, large companies
	3. DNS servers can be vulnerable to DDoS attack
6. [DNS Architecture](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197427(v=ws.10)?redirectedfrom=MSDN)

## Content Delivery Network ##
1. CDN: Globally distributed network of proxy servers
	1. They serve content from locations closer to a user
	2. Content:
		1. Static files:
			1. HTML/CSS/JS
			2. Photos
			3. Videos
		2. Dynamic content: Amazon's CloudFront
2. Advantages:
	1. Improves performance
		1. Users receive content from data centers closer to them
		2. Servers do not have to serve requests that CDNs fulfill

### Push CDNs ###
1. CDNs receive new content whenever changes occur on server
	1. We take responsibility for providing content, uploading directly to CDN & **rewriting URLs** to point to CDN
		1. We can configure when content **expires** and when it is **updated**
			1. Content is updated only when it is **new** or **changed** (minimizes traffic, but maximizes storage)
2. Use-cases: (if content is placed once on CDNs and not re-pulled at regular intervals)
	1. Sites with small traffic
	2. Sites with content that is not often updated

### Pull CDNs ###
1. CDNs grab content from server when first user requests the content
	1. We leave content on server and rewrite URLs to point to CDN
		1. Problems: Slower request until content is cached on the CDN (first-request)
2. A TTL determines how long content is cached
3. Pros and Cons:
	1. Pull CDNs minimize storage space on CDN
	2. Redundant traffic if files expire and they are pulled before they change
4. Use-cases:
	1. Sites with heavy traffic
		1. Traffic is spread out more evenly
			1. Only recently-requested content remain on CDN

### Disadvantage(s): CDN ###
1. CDN costs could be significant (depending on traffic)
	1. Must be weighed with additional csts we would incur not using a CDN
2. Content might be stale if it is updated before TTL expires it
3. CDNs require changing URLs for static content to point to the CDN
4. [Globally distributed content delivery](https://figshare.com/articles/Globally_distributed_content_delivery/6605972)

## Load Balancer ##
1. They distribute incoming client requests to computing resources (application servers, databases)
	1. Load balancer returns response from computing resource to appropriate client
2. Load balancers are effective at:
	1. Preventing requests from going to unhealthy servers
	2. Preventing overloading resources
	3. Helping to elimintate single point of failure
3. LBs can be
	1. Hardware (expensive)
	2. Software (HAProxy)
4. Additional benefits
	1. SSL termination:
		1. Decrypts incoming requests & encrypts server responses
			1. Backend servers are freed from this responsibility
			2. Removes the need to install X.509 certificates on each server
	2. Session persistence:
		1. Issues cookies and routes specific client's requests to same instance if web apps do not keep track of sessions
5. HA & FT
	1. Multiple load balancers are set up
		1. Active-Active mode
		2. Active-Passive mode
6. Load balancing can be done based on the following metrics
	1. Random
	2. Least Loaded
	3. Session/cookies
	4. Round Robin or Weighted Round Robin
	5. Layer 4
	6. Layer 7

### Layer 4 Load Balancing ###
1. They look at info at the transport layer & decide how to distribute requests
	1. Info looked in the Headers:
		1. Source IP
		2. Destination IP
		3. Ports
	2. **It does not look at the content of the packet**
2. They perform [Network Address Translation (NAT)](https://www.nginx.com/resources/glossary/layer-4-load-balancing/)
	1. NAT converts private IP addresses to public IP address and back
		1. Host IP is converted to the public IP (masks the host's IP)
	2. NAT also converts port numbers
		1. Host port is converted to another port (masks the host's port)
	3. NAT maintains a NAT table

### Layer 7 Load Balancing ###
1. They look at application layer to decide how to distribute requests
	1. Contents looked at:
		1. Header
		2. Message
		3. Cookies
2. Inner working
	1. It termintates network traffic
	2. It reads the message
	3. It makes a load-balancing decision
	4. It opens a connection to selected server
3. Use-cases:
	1. L7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers
4. Comparison with L4 LB:
	1. L4 load balancing requires less time & computing resources than L7 load balancer
	2. Performance difference is minimal with modern commodity hardware

### Horizontal Scaling ###
1. LBs can help with horizontal scaling
	1. Improves performance & availability
2. Advantages:
	1. Scaling out is cost effective compared to scaling up with more expensive hardware (vertical scaling)
	2. It is easier to hire talent that can work on commodity hardware than it is for specialized enterprise systems

### Disadvantages of Horizontal Scaling ###
1. Introduces complexity
2. Involves cloning servers
	1. Servers should be stateless:
		1. They should not contain user-related data like sessions & profile pictures
			1. Sessions can be stored in centralized data store
				1. Database (SQL, NoSQL)
				2. Cache (Redis, Memcached)
3. Caches & databases need to handle more simultaneous connections as upstream servers scale out

### Disadvantages of Load Balancer ###
1. LB can be a performance bottleneck if it does not have resources or it is not configured properly
2. Increased complexity
3. Single LB is a single-point of failure
	1. Configuring multiple LBs further increases complexity

...
### Service Discovery ###
1. Examples:
	1. Consul
	2. Etcd
	3. Zookeeper
2. The systems keep track of:
	1. Registered names
	2. Addresses
	3. Ports
3. **Health checks verify service integrity**
	1. Usually done using HTTP endpoint
4. Systems (Consul, Etcd) have built in key-value store
	1. They can be used to store config values & other shared data

## Databases ##
1. ACID:
	1. Atomicity: Each transaction is all or nothing
	2. Consistency: Any transaction will bring database from one valid state to another
	3. Isolation: Executing transactions concurrently has the same results as if transactions were executed serially
	4. Durability: Once a transaction has been committed, it will remain so

### Scaling a DB ###
#### Master-Slave Replication ####
#### Master-Master Replication ####
### Federation ###
1. Federation: Functional partitioning
	1. Splits DB by function
		1. Example: Three DBs for:
			1. forums
			2. users
			3. products
	2. Advantages:
		1. **Less read & write traffic per database**
		2. **Less replication lag**
		3. **Smaller databases result in more data that can fit in memory**
			1. Results in more cache hits due to improved cache locality
		4. We can write in parallel
			1. Increases throughput

### Sharding ###
1. Distributes data across dbs
	1. Each DB manages only a subset of the data
		1. Advantages:
			1. If users increase, more shards can be added to the cluster
			2. Less read & write traffic
			3. Less replication
			4. More cache hits
			5. **Index size is reduced**
				1. Improves performance with faster queries
			6. If a shard goes down, other shards are operational
				1. Can be overcome by adding some replication to avoid data loss
			7. We can write in parallel
				1. Incrases throughput
		2. Disadvantages:
			1. Need to update application logic to work with shards
				1. Complex SQL queries
			2. A set of power users on a shard could result in increased load to that shard compared to others
				1. Rebalancing adds additional complexity
					1. A sharding function based on consistent hashing can reduce the amount of transferred data
			3. Joining data from multiple shards is more complex
			4. Sharding adds more hardware and additional complexity

### Denormalization ###
1. **Denormalization attempts to improve read performance at the expense of write performance**
	1. Redundant copies of the data are written in multiple tables to avoid expensive joins
		1. PostgreSQL & Oracle support [materialized views](https://en.wikipedia.org/wiki/Materialized_view)
			1. **They store redundant information and keep redundant copies consistent**
2. Denormalization circumvents the needs for joins (which are complex)
	1. In most systems, reads outnumber writes (100:1 or 1000:1)
		1. Read resulting in complex database join can be very expensive
			1. We will end up spending significant amount of time on disk operations

#### Disadvantage(s): Denormalization ####
1. Data is duplicated
2. Constraints can help redundant copies of information stay in sync which increases complexity of db design
3. **A denormalized database under heavy write load might perform worse than its normalized counterpart**
	1. We need to keep the redundant data in sync

### SQL Tuning ###
1. [Books](https://www.amazon.com/s/ref=nb_sb_noss_2?url=search-alias%3Daps&field-keywords=sql+tuning)
2. Benchmark & Profile to uncover bottlenecks
	1. **Bechmark** - Simulate high-load situations with tools such as [ab](http://httpd.apache.org/docs/2.2/programs/ab.html)
	2. **Profile** - Enable tools such as [slow query log](http://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html) to help track performance issues
3. The above step might point us to the following optimizations
	1. Tighte up the schema
		1. MySQL dumps to disk in contiguous blocks for fast access
		2. Use `CHAR` instead of `VARCHAR` for fixed-length fields
			1. `CHAR` - Effectively allows for fast, random access
			2. `VARCHAR` - We must find the end of a string before moving onto the next one
		3. Use `INT` for larger numers up to 2^32 or 4 billion
		4. Use `DECIMAL` for currency to avoid floating point representation errors
		5. Avoid storing large `BLOBS`
			1. Store the location of where to get the object instead
		6. `VARCHAR(255)`
			1. Larger number of chars that can be counted in an 8 bit number
				1. Maximizes use of byte in some RDBMS
		7. Set the `NOT NULL` constraint where applicable to improve search performance
			1. [Improve search performance](http://stackoverflow.com/questions/1017239/how-do-null-values-affect-performance-in-a-database-search)
				1. `NULL` values are not indexed
					1. Will use full table scan
	2. Use good indices
		1. Columns that we are querying could be faster with indices
			1. `SELECT`, `GROUP BY`, `ORDER BY`, `JOIN`
		2. Indices are usually represented as self-balancing B-Tree
			1. B-Tree
				1. Keeps data sorted
				2. It allows searches
				3. It allows sequential access
				4. It allows insertions in logarithmic time
				5. It allows deletions in logarithmic time
			2. Placing an index can keep the data in memory
				1. Requires more memory
			3. **Writes can be slower since index needs to be updated**
				1. Solution: When loading large amounts of data, it might be faster to disable indices, load the data, and rebuild the indices
	3. Avoid expensive joins
		1. Denormalize where performance demands it
	4. Partition tables
		1. Break up table by putting hot spots in separate table to help keep it in memory
	5. Tune the query cache
		1. Query cache can lead to performance issues
			1. Query cache:
				1. It stores text of `SELECT` statement along with the corresponding result that was sent to a client.
					1. If identical statement is received, server retrieves the result from the query cache instead of parsing and executing the statement again

### NoSQL ###
1. Collection of items represented in **key-value store**, **document store**, **wide column store**, or a **graph database**
	1. Data is denormalized
		1. Joins are usually done in application code
2. Most NoSQL stores lack true ACID transactions and favor eventual consistency
3. BASE - describes properties of NoSQL databases - It chooses availability over consistency
	1. **Basically available**: System guarantees availability
	2. **Soft state** - the state of the system may change over time, even without input
	3. **Eventually consistent**: System will become consistent over a period of time
		1. Given that the system will not recieve any input during that time.
4. Types of NoSQL stores:
	1. Key-Value stores
	2. Document stores
	3. Wide column stores
	4. Graph databases

#### Key-Value Store ####
1. Allows O(1) reads and writes
	1. It is usually backed by memory or SSD
2. Data stores usually maintain keys in lexicographic order
	1. Allows efficient retrieval of key ranges
3. Usecases:
	1. For storing metadata with a value
	2. For high performance
	3. For simple data models
	4. **For rapidly-changing data**
		1. **In-memory cache layer**
4. Cons:
	1. They have limited set of operations
		1. **Complexity is shifted to application layer if additional operations are needed**
5. It is the basis or more complex systems
	1. Document store
	2. Graph database

#### Document Store ####
1. Abstraction: Key-value store with documents stored as values
2. It is centered around documents
	1. XML
	2. JSON
	3. Binary
	4. ...
3. Document stores provide APIs or query language to query based on internal structure of the document
	1. Many key-value stores include features for working with a value's metadata
		1. **Blurs the lines between the two storage types**
4. Documents are organized by:
	1. Collections
	2. Tags
	3. Metadata
	4. Directories
5. Documents can have fields that are completely different from each other
6. Some document stores (MongoDB, CouchDB) provide SQL-like language to perform complex querids
	1. DynamoDB supports both key-values and documents
7. Use-cases:
	1. Document stores provide high-flexibility
	2. Used for working with occasionally changing data

#### Wide Column Store ####
1. Abstraction: nested map `ColumnFamily<RowKey, Columns<ColKey, Value, Timestamp>>`
2. It stores basic unit of data as a column (name/value pair)
3. A column can be grouped in column families (analogous to SQL table)
	1. Each column can be independently accessed with a row key
	2. Columns with same fow keys form a row
	3. Each value contains timestamp
		1. Why? For versioning or conflict resolution
4. Examples:
	1. [Bigtable](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
	2. [HBase](https://www.edureka.co/blog/hbase-architecture/)
		1. Used in hadoop ecosystem
	3. [Cassandra](https://docs.datastax.com/en/archived/cassandra/3.0/cassandra/architecture/archIntro.html)
5. BigTable, HBase, and Cassandra maintain keys in lexicographic order
	1. Allows efficient retrieval of selective key ranges
6. Advantages:
	1. High availability
	2. High scalability
7. Use-cases:
	1. Very large datasets

#### Graph Database ####
1. Abstraction: Graph
2. Graph database:
	1. Each node is a record
	2. Each arc is a relationship between two nodes
3. **They are optimized to represent complex relationships with:**
	1. **Many foreign keys** or 
	2. **Many-to-many relationships**

### SQL or NoSQL ###
1. SQL:
	1. Relational data model
		1. Highly-structural table organization with rigidly-defined data formats and record structure
2. NoSQL
	1. Collection of complex documents with arbitrary, nested data formats, and varying "record" format

3. Reasons for SQL:
	1. Structured data
	2. Strict schema
	3. Relational data
	4. Need for complex joins
	5. Transactions
	6. Clear patterns for scaling
	7. More established: developers, community, code, tools, etc.
	8. Lookups by index are very fast
4. Reasons for NoSQL:
	1. Semi-structured data
	2. Dynamic or flexible schema
	3. Non-relational data
	4. No need for complex joins
	5. Store many TB (or PB) of data
	6. Very data intensive workload
	7. Very high throughput for IOPS
5. Sample data well-suited for NoSQL
	1. Rapid ingest of clickstream and log data
	2. Leaderboard or scoring data
	3. Temporary data, such as a shopping cart
	4. Frequently accessed ('hot') tables
	5. Metadata/lookup tables

## Cache ##
1. Advantages:
	1. Improves page load times
	2. Reduces load on servers and databases
	3. Putting cache in front of database can help absorb uneven loads and spikes in traffic

### Client Caching ###
1. OS cache
2. Browser cache

### CDN Caching ###
1. A type of cache

### Web Server Caching ###
1. Reverse proxies & caches (like Varnish)
	1. They can serve
		1. Static content
		2. Dynamic content
2. Web servers can cache requests
	1. They can return responses without contacting application servers

### Database Caching ###
1. DB has cache optimized for a generic use-case
	1. We can tweek settings for specific usage patterns can boost performance

### Application Caching ###
1. In-memory caches
	1. Memcached
	2. Redis
2. Caches can be between application and data storage
	1. RAM is much faster than disk
		1. Limited in storage capacity
			1. Cache invalidation policies like LRU can be used to invalidate cold entries to keep 'hot' data in RAM
3. Redis:
	1. Features:
		1. Persistance
		2. Built-in datastructures
			1. Sorted sets
			2. Lists
4. Levels of caching
	1. Row level (database)
	2. Query level (database)
	3. Fully-formed serializable objects
	4. Fully-rendered HTML

### Caching at the database query level ###
### Caching at the object level ###
### When to update the cache ###

#### Cache-Aside ####
1. Look for entry in cache
	1. If cache miss
		1. Load entry from database
		2. Add entry to cache
		3. Return entry
	2. If hit
		1. Return entry
2. Lazy loading strategy

#### Write-Through ####
1. Cache is the main datastore
	1. Read and write are done to it
2. Flow:
	1. Application adds/updates entry in cache
	2. Cache synchronizes writes to data store
	3. Return
3. Pros:
	1. Cache will never have stale data
4. Cons:
	1. Writes are slow because of synchronization
		1. Good if we can tolerate write latency but not read latency
	2. If cache node fails, we lose data

#### Write-Back ####
1. Flow:
	1. Add/Update entry in cache
	2. Return to user
	3. Asynchronously write entry to data store
2. Pros
	1. Improves write performance
3. Cons
	1. Data loss if cache goes down before contents hit the data store
	2. **More complex as compared to implementing cache-aside or write-through**

#### Refresh Ahead ####
1. Cache automatically refreshes recently accessed cache entry prior to its expiration
	1. Reduced latency (as compared to read-through) if cache can accurately predict which items are likely to be needed in the future.
2.Disadvantages:
	1. Not accurately predicting which items are likely to be needed in the future can result in reduced performance than without refersh-ahead

### Disadvantage(s): cache ###
1. Need to maintain consistency between caches and source of truth
	1. Database through cache invalidation
	2. Cache invalidation is a difficult problem
		1. Additional complexity associated with when to update cache

## Asynchronism ##
1. Advantages:
	1. Asynchronous workflows help reduce request times for expensive operations (which would otherwise be performed in line)

			Request -> Web Server -> Message Queue -> Queue Consumer
						|								|
						+------------->	DB <------------+

	2. They can help doing time-consuming work in advance
		1. Periodic aggreation of data

### Message Queues ###
1. MQs receive, hold, and deliver messages
	1. If an operation is too slow to perform inline, use MQ with followin workflow
		1. Application publishes a job to the queue, and notifies user of job status
		2. A worker picks up the job from the queue, processes it, then signals job is complete
2. Pros:
	1. User is not blocked & job is processed in the background
		1. During this time, client can perform a small amount of processing to make it seem like the task has completed
			1. Example: Tweet could be instantly posted on my timeline, but could take some time before tweet is actually delivered to all the followers
3. Examples:
	1. Redis:
		1. Pros: Simple message broker
		2. Cons: Messages can be lost (in-memory)
	2. RabbitMQ:
		1. Pros: Popular
		2. Cons:
			1. Need to use AMQP protocol
			2. Need to manage our own nodes
	3. Amazon SQS:
		1. Pros:
			1. Hosted
		2. Cons:
			1. Messages can get delivered twice

### Task Queues ###
1. They receive
	1. Tasks
	2. Data (related to tasks)
2. Features:
	1. Support scheduling
	2. Can be used to run computationally intensive jobs in the background
3. Examples:
	1. [Celery](https://docs.celeryproject.org/en/stable/)
		1. Supports scheduling
		2. Primily Python support

### Back Pressure ###
1. If queues grow significantly, queue size can become larger than memory
	1. This might result in cache misses, disk reads, slower performance
2. Back pressure
	1. Limits queue size
		1. Maintaining high throughput rate & good response times for jobs already in queue
		2. Once queue fills up, clients get server busy HTTP 503 status code & try again
			1. Clients can retry the request at a later time
				1. We can retry with [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)

### Disadvantage(s): Asynchronism ###
1. Not suitable for following use-cases
	1. Inexpensive calculations
	2. Realtime workflows
2. Introducing queues can add delays and complexity

### Source(s) and Further Reading ###
1. [It's all a numbers game](https://www.youtube.com/watch?v=1KRYH75wgy4)
2. [Applying back pressure when overloaded](http://mechanical-sympathy.blogspot.com/2012/05/apply-back-pressure-when-overloaded.html)
3. [Little's law](https://en.wikipedia.org/wiki/Little%27s_law)
4. [What is the difference between a message queue and a task queue?](https://www.quora.com/What-is-the-difference-between-a-message-queue-and-a-task-queue-Why-would-a-task-queue-require-a-message-broker-like-RabbitMQ-Redis-Celery-or-IronMQ-to-function)

## Communication ##
1. OSI (Open Systems Interconnection) 7 Layer Model
	1. Application (7): Serves as the window for users and application processes to access network services
		1. Application/Example:
			1. End User Layer:
				1. Program that opens what was sent or constructs what is to be sent
		2. Functions:
			1. Resource sharing
			2. Remote file access
			3. Remote printer access
			4. Directory services
			5. Network management
		3. User applications: SMTP
	2. Presentation (6): Formats the data to be presented to the Application layer. It can be viewed as a translator for the network
		1. Application/Example:
			1. Syntax layer: encrypt & decrypt (if needed)
		2. Functions:
			1. Character code translation
			2. Data conversion
			3. Data compression
			4. Data encryption
			5. Charater Set Translation
		3. JPEG/ASCII/EBDIC/TIFF/GIF/PICT
	3. Session (5): Allows session establishment between processes running on different stations
		1. Application/Example:
			1. Synch & send to ports (logical ports)
		2. Functions:
			1. Session establishment
			2. Maintainance and termination
			3. Session support
				1. Perform security
				2. Name recognition
				3. Logging
				4. Etc.
		3. Central Device/Protocols
			1. RPC/SQL/NFS
			2. NetBIOS names
	4. Transport (4): Ensures that messages are delivered error-free, in sequence, and with no losses or duplications
		1. Application/Example:
			1. TCP: Host to Host, Flow Control
		2. Functions
			1. Message segmentation
			2. Message acknowledgement
			3. Message traffic control
			4. Session multiplexing
		3. Central Device/Protocols
			1. TCP/SPX/UDP
	5. Network (3): Controls the operations of the subnet, deciding which physical path the data takes
		1. Application/Example:
			1. Packets ("letter", contains IP address)
		2. Functions
			1. Routing
			2. Subnet traffic control
			3. Frame fragmentation
			4. Logical-physical address mapping
			5. Subnet usage accounting
		3. Central Device/Protocols
			1. Devices:
				1. Routers
			2. Protocols:
				1. IP/IPX/ICMP
	6. Data Link (2): Provides error-free transfer of data frames from one node to another over the physical layer
		1. Application/Example:
			1. Frames ("envelopes", contains MAC address)
				1. NIC Card - Switch - NIC Card
		2. Functions
			1. Establishes & terminates the logical link between nodes
			2. Frame traffic control
			3. Frame sequencing
			4. Frame acknowledgement
			5. Frame delimiting
			6. Frame error checking
			7. Media access control
		3. Central Device/Protocols
			1. Devices:
				1. Switch 
				2. Bridge 
				3. WAP
			2. Protocols:
				1. PPP/SLIP
	7. Physical (1): Concerned with the transmission and reception of the unstructured raw bit stream over the physical medium
		1. Application/Example:
			1. Cables, hubs, etc
		2. Functions
			1. Data encoding
			2. Physical medium attachment
			3. Transmission technique
			4. Baseband or Broadband
			5. Phyisical medium transmission Bits & Volts
		3. Central Device/Protocols
			1. Devices:
				1. Hub

### Hypertext Transfer Protocol (HTTP) ###


#### Source(s) and Further Reading: HTTP ####

## Transmission Contrl Protocol (TCP) ##
## User Datagram Protocol (UDP) ##
## Remote Procedure Call (RPC) ##
### Disadvantage(s): RPC ###

## Representational State Transfer (REST) ##
### Disadvantage(s): REST ###
### RPC and REST Calls Comparison ###

## Security ##
1. Unless we have considerable experience with security, we just need to know the basics
	1. Encrypt in transit and at rest
	2. Sanitize all user inputs or any input parameters exposed to user to prevent XSS and SQL injection
	3. Use parameterized queries to prevent SQL injection
	4. Use the principle of least privilege

### Source(s) and Further Reading ###
1. [API Security Checklist](https://github.com/shieldfy/API-Security-Checklist)
2. [Security Guide for Developers](https://github.com/FallibleInc/security-guide-for-developers)
3. [OWASP Top Ten](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)

## Appendix ##
### Powers of Two Table ###

		Power           Exact Value         Approx Value        Bytes
		---------------------------------------------------------------
		7                             128
		8                             256
		10                           1024   1 thousand           1 KB
		16                         65,536                       64 KB
		20                      1,048,576   1 million            1 MB
		30                  1,073,741,824   1 billion            1 GB
		32                  4,294,967,296                        4 GB
		40              1,099,511,627,776   1 trillion           1 TB

### Latency Numbers every Programmer Should Know ###
1. L1 Cache Reference: 0.5ns
2. Branch mispredict: 5 ns
3. L2 Cache Reference: 7 ns
4. Mutex Lock/Unlock: 25 ns
5. Main memory reference: 100 ns
6. Compress 1K bytes with Zippy: 10,000 ns (10 u)
7. Send 1KB over 1 Gbps network: 10,000 ns (10 u)
8. Read 4KB randomly from SSD: 150,000 ns (150 u)
9. Read 1MB sequentially from memory: 250,000 ns (250 u)
10. Round trip within same datacenter: 500,000 ns (500 u)
11. Read 1MB sequentially from SSD: 1,000,000 ns (1,000 u) (1 ms)
12. HDD seek: 10,000,000 ns (10,000 u) (10 ms)
13. Read 1MB sequentially from HDD: 30,000,000 ns (30,000 us) (30 ms)
14. Send packet CA-> Netherlands -> CA: 150,000,000 ns (150,000 u) (150 ms)

#### Handy Metrics ####
1. Read sequentially from HDD at 30 MB/s
2. Read sequentially from 1Gbps Ethernet at 100 MB/s
3. Read sequentially from SSD at 1 GB/s
4. Read sequentially from main memory at 4 GB/s
5. 6 - 7 world-wide round trips per second
6. 2,000 round tris per second within a data center

### Source(s) and Further Reading ###
1. [Latency numbers every programmer should know - 1](https://gist.github.com/jboner/2841832)
2. [Latency numbers every programmer should know - 2](https://gist.github.com/hellerbarde/2843375)
3. [Designs, lessons, and advice from building large distributed systems](http://www.cs.cornell.edu/projects/ladis2009/talks/dean-keynote-ladis2009.pdf)
4. [Software Engineering Advice from Building Large-Scale Distributed Systems](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/stanford-295-talk.pdf)

## Additional System Design Interview Questions ##
## Real-World Architectures ##
1. Articles on how real world systems are designed
2. Don't focus on nitty gritty details.
	1. Tips
		1. Identify shared principles
		2. Identify common technologies
		3. Identify patterns within the articles
		4. Study what problems are solved by each component
		5. Where it works
		6. Where it doesn't work
		7. Review the lessons learned
3. Types:
	1. Data Processing
		1. MapReduce - Distributed data processing from Google
			1. [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/mapreduce-osdi04.pdf)
		2. Spark - Distributed data processing from Databricks
			1. [slideshare.net](http://www.slideshare.net/AGrishchenko/apache-spark-architecture)
		3. Storm - Distributed data processing from Twitter
			1. [slideshare.net](http://www.slideshare.net/previa/storm-16094009)
	2. Data Store
		1. Bigtable: Distributed column-oriented database from Google
			1. [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/chang06bigtable.pdf)
		2. HBase: Open source implementation of Bigtable
			1. [slideshare.net](http://www.slideshare.net/alexbaranau/intro-to-hbase)
		3. Cassandra: 
			1. [slideshare.net](http://www.slideshare.net/planetcassandra/cassandra-introduction-features-30103666)
		4. DynamoDB
			1. [harvard.edu](http://www.read.seas.harvard.edu/~kohler/class/cs239-w08/decandia07dynamo.pdf)
		5. MongoDB
			1. [slideshare.net](http://www.slideshare.net/mdirolf/introduction-to-mongodb)
		6. Spanner
			1. [research.google.com](http://research.google.com/archive/spanner-osdi2012.pdf)
		7. Memcached
			1. [slideshare.net](http://www.slideshare.net/oemebamo/introduction-to-memcached)
		8. Redis
			1. [slideshare.net](http://www.slideshare.net/dvirsky/introduction-to-redis)
		9. Google File System (GFS)
			1. [research.google.com](http://static.googleusercontent.com/media/research.google.com/zh-CN/us/archive/gfs-sosp2003.pdf)
		10. Hadoop File System (HDFS)
			1. [apache.org](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html)
	3. Misc
		1. Chubby
			1. [research.google.com](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/chubby-osdi06.pdf)
		2. Dapper
			1. [research.google.com](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf)
		3. Kafka
			1. [slideshare.net](http://www.slideshare.net/mumrah/kafka-talk-tri-hug)
		4. Zookeeper
			1. [slideshare.net](http://www.slideshare.net/sauravhaloi/introduction-to-apache-zookeeper)

## Company Architectures ##
## Company Engineering Blogs ##
## Under Development ##
## Credits ##