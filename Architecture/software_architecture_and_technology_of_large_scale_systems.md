# Developer to Architect: Mastering Software Architecture #

## Introduction ##
### Introduction to Developer to Architect ###
1. How do you architect a new system?
	1. Starting with:

			Use cases
			DB Schema
			Code flow (sequence diagram)
			Class diagram
			
		1. Next step:

				user interface <-> web application <-> business service <-> database
				
			1. 3-tier or n-tier architecture
		2. Next step:
			1. Technologies and languages for implementation
				1. HTML/CSS/JS
				2. PHP
				3. Python
				4. C#
				5. Java
				6. Spring
				7. SQL
	2. We have not done any architect's job here
		1. We have never dealt with system requirements
			1. We must not just satisfy functional requirements but non-functional and system requirements (most importantly)
				1. Performance
					1. 90% of requests should be satisfied within a second
						1. To minimise latency
						2. Increase throughput
				2. Scalability
					1. System should be able to handle 1M simultaneous users
				3. Reliability
					1. How to make system resilient to failures
						1. If component has failed
						2. If data centre has failed
				4. Security
					1. How to securely transfer data
					2. How to securely store data
					3. How to authenticate and authorize
					4. What steps to take to secure our system against external and internal threats
				5. Deployment
					1. These systems are not easy to deploy (might require a lot of automation and coordination with operations team) - Due to high scalability and reliability
						1. There could be many components
						2. There could be many instances of the components
				6. Technology Stack
					1. For each layer and component
						1. Which platform or product to choose
							1. DBs
							2. Caches
							3. Queues
							4. Servers
					2. The options are chosen based on requirements of a system
						1. Performance, scalability, reliability, security, deployment requirements
					3. Products or technologies or platforms that satisfy those requirements are chosen
		2. The course is about non-functional and system requirements

## Performance ##
### Module Contents Overview ###
1. High level topics
	1. Understanding Performance
		1. Performance problems
		2. Measurement
		3. Principles
			1. The performance of a system depends on
	2. How to improve the performance of a system?
		1. Latency (How to minimize it) - Following are categories
			1. CPU - maximization
			2. Memory - minimize mem related latency
			3. Network - minimize network related latency
			4. Disk - improve utilization and minimize latency
		2. Concurrency (How to improve throughput)
			1. Locking - role played in terms of improving or degrading performance
				1. Pessimistic - where to use
				2. Optimistic - where to use
			2. Coherence - role played in terms of improving or degrading performance
		3. Caching
			1. Static Data - how to cache, challenges, how it helps us
			2. Dynamic Data - how to cache, challenges, how it helps us

### A Reference Software System for Discussing Performance ###
1. Sample System - we want to improve the performance of this system

		Web browser -SSL/TLS-> Web Application -objects-> Business App
				Pages/JSON/XML/Images
				
		Business App -Txn Data-> Database <-Report Data- Bach Processing
		
	1. Web application - accessible from web browser
	2. Web application - fetches data from a service (business application)
		1. It can be SOA
		2. It can be microservices
	3. Business application - fetches data from database
		1. Assuming database is RDBMS
	4. Back Processing - fetches data from database, processes it and puts the data back into database

### What is Performance ###
1. Performance - of software system
	1. Measure of how fast or responsive a system is under
		1. A given workload (this has to be fixed)
			1. Backend data
			2. Request volume
		2. A given hardware (this has to be fixed)
			1. Kind
			2. Capacity
	2. If we have system with huge data, that system is likely to face more performance problems compared to when we reduce the data that is there on the backend
	3. If request volume is high, the system is likely to face more performance problems
	4. This constraint is application only when we measure performance
	5. If we use superiod hardware or increase capacity of hardware
		1. Performance problems generally go away and system responds better
			1. If hardware was the reason behind any performance problems
2. Goals:
	1. Web requests
		1. How fast are we getting response
	2. Batch processing
		1. How fast the batch processes are finishing
3. Goal
	1. As we increase the workload, our performance should remain stable
		1. It should not severely degrade
			1. A little is okay (depends)
4. Hardware
	1. If we increase capacity or bring superior one
		1. System performance should improve (if it was lagging behind because of inadequate capacity or kind)

### How do Performance Problems Look Like ###
1. Performance Problems
	1. How to spot a performance problem?
	2. How does performance problem look like?
	3. How to get rid of all performance problems?
		1. We don't want them
2. Every performance problem is the result of some queue building up somewhere. (requests get queued up somewhere)
	1. Network socket queue
		1. Congestion
	2. DB IO queue
		1. Congestion
			1. A lot of requests are going to DB but it cannot respond immediately
	3. OS run queue
		1. How much CPU is available
		2. How many threads the system is able to run on the CPU(s)
		3. Congestion
			1. Too many threads
	4. ...
3. Reasons for queue build-up
	1. Inefficient slow processing
		1. Slow algorithm - inefficient code
	2. Serial resource access
		1. If only one thread needs to be executed at a time
			1. Deposit or withdraw of money
				1. All other threads should wait for the thread to finish
					1. Queue builds up
	3. Limited resource capacity
		1. Suppose we are able to execute requests in parallel
			1. We have limited number of CPUs
				1. Analogy: Traffic
					1. If we have 6 lanes instead of 2 lanes (more vehicles can pass at any given time)
4. Analogy
	1. Traffic jam
		1. There is a bottlenect somewhere - reason can be anything
5. Why is there a queue build up?
	1. Classification
6. Goal:
	1. To identify where the queue build up is happening
		1. If we can do that, we can fix the performance problem
	2. If we are architecting or building a new system
		1. We should focus on identifying the areas where this queue building can happend and try to avoid that
			1. Ensures that we have architected a system which is less likely to face any performance problems

### Performance Principles ###
1. Focus:
	1. Efficiency (improve it)
		1. Efficient Resource Utilization
			1. IO - Memory, Network, Disk
			2. CPU
		2. Efficient Logic
			1. Algorithms
			2. DB Queries
		3. Efficient Data Storage
			1. Data Structures
			2. DB Schema
		4. Caching
	2. Concurrency (increase it)
		1. Hardware
		2. Software
			1. Queueing
			2. Coherence
	3. Capacity (increase it)
2. Request types
	1. Serial requests - are processed one after another (only one request exists in the system)
		1. request goes in and response comes out
		2. Second request goes after first response
		3. ...
		4. **Efficiency is considered (single request processing)**
			1. How fast a single request gets processed in a system largely depends on the code that is executing the request
				1. Capacity: Kind of hardware
					1. We can keep this constant
			2. How efficient the code that is executing the request is governs the performance
				1. **Efficient Resource Utilization**
					1. IO, CPU
				2. **Efficient Logic** - it must use minimal amount of CPU and memory and IO (minimal work) - architect is not concerned about here
					1. Algorithms
					2. DB Queries
				3. **Efficient Data Storage**
					1. Data Structures - maps for search (instead of lists)
					2. DB Schema - indexing for search and it must be used by query
				4. **Caching** (architectural concern)
					1. It needs minimal code changes and it leads to phenomenal amount of performance improvement
			3. The above areas ensure that the response time of requests being processed serially will come down drastically (depends on efficiency)
	2. Concurrent requests - at any given time there can be multiple requests present in our system
		1. They are either processed simultaneously or serially
			1. Serial processing: Locking enforces it
		2. **We consider only concurrency and not efficiency**
		3. Concurrency is about executing multiple requests simultaneously in a system
			1. **Hardware** - It should allow our requests to be processed simultaneously
			2. **Software** - We need to code for the hardware that allows simultaneous request processing
				1. Here we don't have to be concerned about intrinsic inefficiencies within a single request (it has already been taken care of previously)
				2. Factors purely related to concurrency:
					1. **Queuing**
						1. It results from multiple requests being simultaneously present on a machine
							1. Not due to external call
						2. Blocking is because of other requests
							1. They are occupying resources (that are required by other requests and are not available)
					2. **Coherence**
	3. Capacity
		1. If we bring in better kind of hardware or increase the hardware - it can help with performance
			1. Capacity augmentation
				1. CPU
				2. Memory
				3. Disk
				4. Network
		2. Not the focus of this course
			1. Mention would be made if it can solve certain problems
				1. Identifying when this is relevant and not the other concepts (efficiency, concurrency)

### System Performance Objectives ###
1. Objectives
	1. Minimize Request-Response Latency
		1. Latency is Measured in Time Units
			1. How much time a request/ response spends within a system
				1. When it goes through, it spends time at different points in a system for processing
				2. When it goes through, it spends time waiting to be processed
			2. Total latency = wait time + processing time
				1. We are trying to minimize
					1. Wait time
					2. Processing time
		2. Depends on
			1. Wait/Idle Time
			2. Processing Time
	2. Maximize Throughput (this is our goal)
		1. Throughput is measured as Rate of Request procesing
		2. Depends on
			1. Latency - (minimizing this can increase throughput)
			2. Capacity - (increasing this can also increase throughput)
				1. This is important
2. Example: 
	1. Web-application - needs low latency
		1. Takes a request and gives response
		2. This also need throughput
	2. Batch processing - report generation say (read and write to db or file)
		1. We don't worry about request-response latency
		2. Throughput is important
3. Architect needs to learn
	1. How to bring down latency of a system - more important to focus on
		1. Capacity is next

### Performance Measurement Metrics ###
1. Metrics to measure to know the performance of a system (4 most important metrics)
	1. Latency
		1. Affects - User Experience
			1. Important
		2. Desired - As low as possible
	2. Throughput
		1. Affects - Number of users that can be supported
			1. Higher the throughput, higher the number of requests that can be supported
		2. Desired - Greater than the request rate
			1. It should be at-least higher than the peak number of users to be supported
	3. Errors (% of errors)
		1. Affects - Functional Correctness
		2. Desired - None
			1. Errors should only be related to performance - usually only timeouts
				1. Usually happens if we subject our system to very heavy workload
			2. It is not okay to have functional errors
				1. The solution cannot be used in production
	4. Resource Saturation
		1. Affects - Hardware capacity required
			1. Tells us how much capacity is completely utilized
				1. 100% CPU utilization
				2. Network is completely choked
			2. These are indications of resource saturation
			3. Unless we saturate the hardware we will not come to know if the hardware is overutilized or underutilized
				1. Based on this analysis, we can decide to whether augment the capacity or take away the capacity
		2. Desired - Efficient utilization of all system resources
		3. Tail latency - it is an indication of queuing of requests
			1. Gets worse with higher workloads
				1. Latency is key to performance exercise
				2. We need to pay attention to tail latency
					1. Y - axis - number of requests
					2. X - axis - latency
					3. Tail latency - small percentage of requests with high latency (tail through)
						1. 12000 milliseconds
						2. from 99 percentile - 1 % of requests have more than 4000 ms
							1. Every 100th request can experience a latency of more than 4000 ms (upto 12000 ms)
								1. Every 100th user might face this latency
									1. If this kind of latency for users is not acceptable, we need to pay attention to tail latency
										1. Say: 99% should be below 3000 ms
								2. Last percentile can be important to business
						3. If we increase the workload, then tail latency might become worse - more requests might shift to the right side
							1. It is worsening of performance problem
								1. Because of queuing of requests (because of other requests, they did not get queued)
						4. This measure can be a good indication of what does increase in workload do to our system
		4. Average latency hides the effects of tail latency
			1. Also measure 99 (or 99.9 - if required by business) percentile latency

### Serial Request Latency ###
1. Efficiency - related to serial request latency

### Network Transfer Latency ###
1. Two kinds of networks
	1. Browser and Web app
		1. Internet can be involved
			1. There could be multiple hops
			2. There could be multiple networks
			3. Some of the networks might not be:
				1. Fast
				2. Reliable
			4. They could be long distance in general and many networks might be involved
		2. Intranet
			1. Pretty reliable - may not be 100% reliable (better than internet)
			2. Fast (as compared to internet)
			3. Communication can be different as compared to browser to web-application
2. Sources of latency
	1. Any network is connected by wires and data phyisically travels by wires
		1. Data to reach from point A to point B - latency is involved 
			1. It is called as data transfer latency
				1. Different for internet as compared to intranet (global, regional, local network)
	2. Creation of connections
		1. TCP Connections
			1. UDP - much faster but unreliable - it is not discussed here
				1. Reliability has to be built into application
			2. Client has to first initiate a connection
				1. For that, if HTTP protocol is used - it is on top of TCP
					1. Overhead with TCP connection:
						1. Client initiates TCP connection
							1. Sends a TCP packet to server
								1. 50 ms say
						2. Server establishes connection
						3. Server sends acknowledgement to client
							1. 50 ms say
						4. Client also establishes connection, sends acknowledgement + data to server
						5. Total roundtrip time: 50 ms + 50 ms = 100 ms per connection
						6. Each subsequent request and response (if connection is already established) will take 100 ms
						7. Total communication time: 200 ms (100% overhead for connection creation)
					2. Overhead with SSL/TLS Connection
						1. Client communication will be over SSL usually
						2. Even intranet communication will be over SSL (if banking application)
						3. Steps
							1. Client initiates TCP connection (TPC SYN)
							2. Server sends acknowledgement (TCP SYN ACK)
							3. Client also sends TCP acknowledgement (TCP ACK)
							4. Client initiates SSL connection (SSL Client Hello)
							5. Server sends acknowledgement (SSL Server Hello)
							6. Client sends key (SSL Key Exchange)
							7. Server sends encyption parameters (SSL Change Cipher)
						4. Time taken for SSL connection: 300 ms
						5. Actual request/response roundtrip time
							1. 100 ms
						6. Total time: 300 ms + 100 ms = 400 ms
							1. Overhead: 300%

### Minimizing Network Transfer Latency ###
1. Approaches to address latencies
	1. Client -> Server: SSL/TLS connection over HTTP
	2. Web application -> REST API: HTTP
	3. REST API -> DB: DB specific protocol or HTTP - it is also over TCP
2. Stategy to reduce connection overhead
	1. Connection pool: Connection is created and pooled
		1. Re-using connections already created
			1. To avoid connection creation latency
				1. We cannot do anything about the latency
		2. Examples:
			1. Business application will have a connection pool for DB
			2. Web application will have a connection pool of HTTP connections to business applications
	2. Persistent Connections: External client (browser) to web application
		1. We don't have to do anything
			1. HTTP 1.1 protocol will make persistent connections
				1. The connection is not destroyed just after one call
				2. It keeps the connection for a while
					1. 5 - 6 consecutive calls - can be done over same connection (if not doing them in parallel)
				3. If client library is used for HTTP
					1. We need to ensure that client is making persistent connection
					2. example: microservices
						1. client libraries should use consistent connections
	3. **Caching**: Data transfer overhead
		1. Reduce size of data
		2. No transfer at all (avoid transfer that is not required) - cache the data
		3. Example: If HTTP service is querying DB (if data doesn't change frequently)
			1. **Data Caching**: Cache the data
		4. Example: Web app
			1. If user data needs to be stored in a session
				1. **Session Cache**: We can use session cache
		5. Browser side
			1. **Static Data Caching** - JS, images, CSS files
		6. Wherever there is an opportunity to cache data, we would cache (to avoid data transfer)
	4. **Data Format & Compression**: Efficient data formats can be used
		1. Intranet: Binary protocols can be used
			1. Instead of using HTTP - uses ASCII characters
				1. We can use RPC based protocol
					1. Examples: **gRPC**, Thrift, IIOP (old days - EJB)
				2. To make data transfer overhead minimal
				3. Cons:
					1. Reduces interoperability between applications
						1. RESTful - needs HTTP to promote inter-operability
				4. If inter-operability is not required, we can use other protocols instead of HTTP based
					1. RPC based (to overcome network data transfer related overheads)
		2. **Compression**: We should always do
			1. Server should compress the data using Zip format say
				1. It reduces size of data (reduces data transfer overhead)
				2. Cons: overhead of compression and uncompression (on client side)
			2. Client can also compress and server can uncompress
				1. Needs some CPU cycles
					1. Pros: This overhead is not that significant as compared to data transfer overhead
	5. **SSL Session Caching**
		1. If repeated SSL connection are created between client and server
			1. Data is exchanged between client and server
				1. Kinds of encryptions client supports
				2. Kinds of encryptions server supports
				3. Paremeters related to encryption (exchanged)
			2. Server can cache the parameters that client transfers to server (for server to identify the client)
				1. Server can take a shortcut to connect to client
					1. It reduces roundtrip for SSL connections
	6. If we use binary protocol for RESTful application, it will not remain a RESTful application
		1. Architecturally (technically it might be)
			1. Certain cases might not require strict RESTful applications

### Memory Access Latency ###
1. Memory Latency
	1. Finite Heap Memory
		1. Whether process is using heap or not
			1. A process can use only finite amount of heap memory
				1. Any process that tries to exceed the limit is bound to crash (problem to deal with)
		2. GC processes
			1. Java or .Net
				1. When process is about to go out of memory
					1. GC will run (aggressively)
						1. Performance will go down (may be drastically)
							1. Users might experience bad performance
	2. Large Heap Memory
		1. If a process occupies large heap memory
			1. It might be ocupying more than what is physically on the machine
		2. It might be bigger than physical memory
			1. OS might have to use hard disk to accomodate that much of extra heap memory
				1. Swapping (between physical memory and hard disk)
					1. Severely brings down the performance
		3. Even if physical memory is huge (to accomodate large heap size)
			1. Problem: Especially with those systems using GC
				1. GC has to do more work
					1. It has to sweep through large areas to clear objects no longer utilised
						1. It slows down GC algorithm
							1. Impacts performance of a system
		4. Large heap size need to be watched out for
	3. GC Algorithm
		1. Different flavors are used
			1. Each algorithms specializes for a given situation
				1. We need to identify the situation and apply appropriate GC algorithm
					1. Or else it might impact performance if dealing with large data
	4. Finite Buffer Memory - On DB side
		1. Any read/ write ops happening on DB, it happens in memory
			1. DB reads record from HDD to memory
			2. The record will be changed in memory
			3. The record is then written back to HDD
		2. Space utilization of buffer memory is critical
			1. It governs how many ops per second we can do
				1. Impacts throughput of DB
		3. If we are in shortage of buffer memory (may be due to poor memory allocation or inefficient schema)
			1. It will severly affect performance of entire system

### Minimizing Memory Access Latency ###
1. Approaches
	1. Avoid Memory Bloat
		1. Process should occupy as little memory as possible
			1. Code base
				1. If number of instructions are fewer
					1. The back and forth between ram and processor will be lesser
			2. Heap space
				1. As small as possible
					1. Lesser job for GC
					2. Chances of process going out of memory is lesser
			3. We can control the two as much as possible
				1. Unnecessary allocation
	2. Weak/ Soft References
		1. Useful where we are allocating large objects
			1. There is a chance of process going out of memory
				1. Solution: Weak or Soft References
					1. Java - this exists
						1. We can declare a reference as weak reference
							1. If runtime notices that process is running short of memory, it lets GC destroy the objects (weak references)
						2. Changes to program:
							1. It should check if the object still exists before referencing
	3. Multiple Smaller Processes
		1. This is better than one single process
			1. If a JVM process occupies huge memory (40 GB RAM say)
				1. RAM - 50 GB
			2. It is still not desirable
				1. It might be too much for GC algorithm to run efficiently
					1. GC can run really badly
		2. If we break the application into multiple processes, the work can be divided between processes
		3. Use cases:
			1. Batch process (for large amount of data)
				1. Multiple JVMs
				2. Multiple nodes
	4. Garbage Collection Algorithm
		1. many flavors are available
			1. Constantly researched and improved
		2. Broadly two kinds of GCs exist
			1. For batch processing - long pauses in-between (GC is done)
				1. GC should be efficient (good throughput)
					1. Overall time taken for GC should be as small as possible
						1. How fast the data will be processed and how soon the batch processing finishes is important (not pause times)
			2. For server processing - GC is run along with main process
				1. Pauses are small
					1. Most of the work is accomplished along with the main process
				2. Example: Server takes request and gives response
					1. If JVM pauses couple of seconds - bit performance blow
						1. Solution: GCs that run along with the application and has very low pause time
							1. Suitable
		3. There is no GC available where there is no pause at all
			1. Process is stopped from doing work
		4. There are many GCs to choose from
			1. We must choose the one appropriate for live process vs batch process
	5. Finite Buffer Memory (DB)
		1. The amount of memory allocated to buffer memory should be adequate (as large as possible)
			1. When DB is considered, it should have adequate amount of buffer memory
		2. **How the buffer memory is utilized is important**
			1. Normalization
				1. Leads to good utilization of buffer memory
				2. Used to avoid duplicate data
					1. Amount of storage for the data becomes lesser (optimal)
					2. Leads to more DB performance
				3. Denormalization:
					1. Done if there are complex joins (to speed up reads)
						1. Where there is no need to de-normalize data, it is better to keep the data normalized
							1. It saves disk space
							2. It saves memory (when loaded)
			2. Compute Over Storage
				1. A way of ensuring good utilization of buffer memory
					1. If certain data can be computed (by business logic say)
						1. We should not store it
							1. Trade-off - computation cost
								1. But might relieve database (if it is under pressure)
									1. Storage on hard disk is fine but when it is brought into memory it is unnecessary

### Disk Access Latency ###
1. Disk Latency - One of the slowest IOs (this is important to consider)
	1. Almost every component in system needs to do disk IO
		1. Example: Logging
			1. Disk penalty is not that high (?)
	2. Disk penalties are high in
		1. Web applications
			1. It needs to access web content like JS file, CSS files, image files from HDD
				1. It causes huge latency
		2. DB Disk Access
			1. Disk latency can be a challenge
				1. Data write or read is usually to and from HDD respectively

### Minimizing Disk Access Latency ###
1. Approaches
	1. Logging:
		1. Sequential IO: We write on a file
			1. It uses sequential access (not random access)
				1. Data is written one line after another sequentially
				2. Sequential IO is much faster than random IO
					1. Accessing record from DB is a random IO
						1. DB tables and records could be scattered across HDD
			2. Sequential IO is not as slow as random IO
		2. Batch IO:
			1. If we can log as much data as possible in one go, that can help in reducing context switching cost
				1. CPU needs to switch between logging and computation
					1. Efficient way: We can combile 4 logging statements into one
		3. Asynchronous Logging: Do asynchronous logging as much as possible
			1. Main thread can be involved in computation
				1. It can provide data to secondary thread and continue
					1. Main thread doesn't have to leave CPU (it can continue to occupy CPU for as much time as possible)
						1. It can make processing efficient
			2. Secondary thread can do logging
			3. Wherever possible prefer asynchronous IO over synchronous IO
				1. Cons: If application crashes somewhere, there is no guarantee that last few statements might not have been logged by async loggers
					1. Unless there is extremely critical that needs to be logged, we can prefer asynchronous logging
		4. Web Content Files:
			1. Web app can have static data stored as files (js, css, html, ...)
				1. They are stored on disk
					1. Fetching can involve IO
					2. They could be fetched frequently
					3. One way to avoid the cost
						1. We can keep the file in memory (caching)
							1. How to do this?
								1. Special components
									1. Reverse Proxy
										1. To separate the responsibility of serving static data and dynamic data
										2. Static requests are served by reverse proxy (does not hit web server)
										3. It specializes in storing the data
			2. Static is read from memory (once it is fetched into memory)
			3. Other free things we get with Reverse Proxy
				1. Page Cache - files already fetched remain in physical memory of the system
					1. Reverse proxy uses page cache efficiently
				2. Zero Copy - when copy is performed from disk over network, we can use **kernel mode** instead of user mode
				3. ...
				4. Examples: 
					1. Varnish
					2. Nginx
			4. **Any static content should be delivered by specialized component such as a reverse proxy**
		5. DB Disk Access
			1. If read only requests wants to be sent to database:
				1. We can cache the data somewhere outside the database
					1. Cache of the server say - we can avoid disk access
			2. Schema Optimization
				1. Denormalization Vs. Normalization
					1. If we find from load test, the problem is with disk IO
						1. Solution: Denormalization
							1. One can store that data in one table (instead of multiple tables)
								1. Going to multiple tables will require disk rotation and can be separate IOs - takes more time than single IO
					2. Use this if disk access is causing problem
				2. Indexes
					1. They avoid lot of data we need go through while we fetch some data
						1. If for instance we need to fetch some data from a table and a row:
							1. If not indexed, we may have to do a full scan to find the row
							2. If we can have an index (filter criteria) on that row, the db can use the index and through the index, it will know the exact disk location where it can find the record
								1. It will directly go to the record in the disk
									1. It will drastically reduce the IO
					2. There could be inefficiencies concerned with incorrect indexing
				3. Query optimization
					1. They should be optimized to fetch minimum possible amount of data
					2. Schema optimization is related to this
				4. Higher IOPS, RAID, SSD Disk
					1. SSD - Can be used if disk access is extremely critical
						1. These are much faster than regular disks
						2. Cons: A little more expensive
					2. Higher IOPS - Input/ Output Per Second
						1. If we are doing a lot of random IO (random seeks)
							1. Prefer HDDs that offer high IOPS
					3. RAID - Redundant Array of Integrated Disks
						1. Same data is replicated over multiple disks
						2. It can be partitioned
						3. Striping & Mirroring
						4. Advantages:
							1. We can read in parallel (does not reduce latency)
								1. IO will be faster
								2. Overall time will be reduced

### CPU Processing Latency ###
1. CPU Latency
	1. Inefficient Algorithms
		1. Many times quite obvious
		2. It can be handled by developers
	2. Context Switching
		1. It is not very obvious
		2. It affects entire system
		3. Issue with context switching
			1. Affects environments where (pretty much all components)
				1. Multiple processes are running
				2. Multiple threads are running
		4. Example: We are running two processes on a single CPU machine

				P1/T1 --->|    |     |    |---->|    |
				          |    |     |    |     |    |
				P2/T2     |    |---->|    |     |    |---->
							  ^
							  |
							wasted time:
				          1. save state of PCB1
				          2. restore state of PCB2

			1. If a process (P1 say) may try to do IO (access disk or network call)
				1. OS will evict the process
				2. OS will give opportunity to the other process to occupy CPU and start it's execution
					1. There is a delay between end of P1 and beginning of P2
						1. OS will save the state of P1 (PCB1) in memory
						2. OS will restore the state of P2 (PCB2) in memory
						3. OS will start P2
			2. How can we avoid incurring cost of context switch?
				1. If we can avoid IO
					1. Even after finishing IO, the process needs to wait for it's turn to execute (context switch)
						1. Overhead can be 100% (100 ms + 100 ms = 200 ms) 

### Minimizing CPU Processing Latency ###
1. Efficient Algorithms - development concern
2. Efficient Queries - development concern
	1. It gets translated to algorithms that fetch data or write data from or to database respectively
3. Context Switching
	1. Batch / Async IO - wherever possible
		1. If we are making multiple calls to DB to fetch data
			1. It is a network overhead + cpu overhead
				1. process or thread is evicted multiple times (due to IO)
					1. It incurs context switching cost
			2. If we can batch multiple calls to one call
				1. It will save network latency
				2. It will save on CPU latency
			3. Writes & reads can be combined to save context switch
		2. Async IO
			1. We write log statements (to find out what has gone wrong with the system)
				1. Separate thread can be used to do logging
					1. Even if logging thread gets evicted (since it is doing IO), the main thread is still continue to execute efficiently
	2. Single Threaded Model
		1. Example: JS Engine (Chrome browser), Node.JS, VolDB, Reverse Proxy like Nginx
		2. Efficient way to run processes is to do all processing work in CPU only through a single thread
			1. Example: All requests go to main thread
				1. If main thread wants to do IO, it delegates it to async thread
				2. Once IO completes, the result is communicated back to the main thread
				3. main thread gets the data and continues processing with the returned data
				4. Process will switch between threads (main, IO threads)
				5. Main thread will almost never leave the CPU
					1. It always has something to process
		3. If we have a large flow of requests, and if we have to do a lot of IO
			1. We can use single threaded model
				1. Appropriate if high load and high number of IOs
	3. Thread Pool Size
		1. We should not have a very large thread pool
			1. If too many thread, they may not get time to execute on CPU (thrashing)
				1. A lot of context switching can happen
		2. Have just the right number of threads for the machine
			1. Example: 2 CPUs - 10 threads (no guideline - it depends on - kind of process, how much IO it does, how CPU intensive it is)
			2. We need to find the optimal size
	4. Multi-Process in Virtual Environment
		1. If we run mutliple processes in a single machine
			1. We should run them in their own virtual environments
				1. Why?
					1. If we are running 4 processes, the processes will contend for the CPU on the machine
						1. If one of the processes continues to hog CPU (written efficiently)
						2. **Virtual environment gives dedicated quota of CPU to each process**
							1. Avoids interference between processes
		2. If it is a performance sensitive system:
			1. If machine is large size,
				1. We tend to run multiple processes on the machine
					1. Certain processes can make other processes starve for CPU (this can be avoided using virtual environments)

### Some Common Latency Figures ###
1. Latency comparison numbers (~2012)
	1. L1 cache reference	- 0.5	ns
	2. Branch mispredict	- 5		ns
	3. L2 cache reference	- 7		ns	(14x L1 cache) - proc mem - worst case
	4. Mutex lock/unlock	- 25	ns
	5. Main memory ref		- 100	ns (20x L2 cache, 200x L1 cache) - for context switch, PCBs are stored in main memory
	6. Compress 1K bytes with zippy	- 3,000 ns
	7. Send 1K bytes over 1 Gbps network	- 10,000 ns
	8. Read 4K randomly from SSD*			- 150,000 ns (~1GB/sec SSD)
	9. Read 1 MB sequentially from mem	- 250,000 ns
	10. Round trip within same datacenter - 500,000 ns (500 us)
	11. Read 1 MB sequentially from SSD* - 1,000,000 ns (~1GB/s SSD)
	12. Disk seek								- 10,000,000 ns
	13. Read 1 MB sequentially from disk - 20,000,000 ns
	14. Send packet CS->Netherlands->CS	- 150,000,000 ns
2. Disk seek - 10^5 mem reference
	1. We want to avoid disk (as much as possible)
3. Compressing and sending data
	1. 1 K - 3,000 ns + 10,000 ns (13,000 ns)
		1. Compression cost is much lesser as compared to sending data over network (3 times or so more)
	2. Significant amount of data can be compressed
4. Roundtrip within data center vs roundtrip between two continents (approximately)
	1. 500,000 ns vs 150,000,000 - 1:300 (300x)
	2. Fetching data within data center is much faster than fetching data from the internet (if it is far off)
		1. Solution: We can do caching
5. Disk access
	1. SSD vs Disk
		1. 150,000 vs 10,000,000 (might be worse for 4K for Disk)
			1. ~50x
6. Sequential IO
	1. Mem vs SSD vs Disk
		1. 250,000 ns vs 1,000,000 ns vs 20,000,000 (1:4:80)
7. Sequential vs Random access
	1. Random access
		1. Mem vs Disk: 100 ns vs 10,000,000 ns (100,000 times more)
	2. Sequential access
		1. Mem vs Disk (1 MB): 250,000 ns 20,000,000 ns (80 times more)

### Concurrency Related Latency ###
1. Parallel request concurrency
	1. If there are multiple requests in the system
		1. How do we minimize latency?
		2. How do we increase concurrency?

### Amdahl's Law for Concurrent Tasks ###
1. Assumption: We have already taken care of serial request or single request latency (minimized to whatever extant possible)
2. Concurrency here:
	1. Concurrent processing:
		1. If we have 3 requests and if we are processing one after the other (serial processing)
		2. If we have 3 requests and if we are processing all at once at the same time (parallel processing)
		3. In many systems it is neither truly serial nor parallel

			->	         ->
			-> -> -> -> -> -> -> ->
			->          ->
			
		1. If we have a synchronized block (java) or if we have taken a lock - the three processes execute serially
	2. Suppose we process serially only
		1. If we have one processor, one thread, one user
			1. 1 request / second say (rate)
				1. 3 requests in 3 seconds (serially)
		2. If we increase the number of processors to 2
			1. 1 request / second only (serial)
	3. Suppose we process in parallel
		1. If we have one processor, one thread, one user
			1. 1 request / second
		2. If we have two processors
			1. 2 requests / second
		3. If we have three processors, three threads, three users
			1. 3 requests / second
		4. If processes are perfectly parallel, the graph will be linear
	4. In general
		1. Overheads
			1. Taking locks
			2. Coordinate between threads
			3. Synchronize threads
		2. There will usually be serial parts
			1. Depending on the amount of serial parts, the graph is in-between
		3. Amdhal's law - tells how much the serial portion affects the graph
			
				C(N) = N / [1 + alpha(N - 1)]
				
			1. C - capacity
			2. N - scaling dimention
				1. like CPU or load
			3. Alpha is resource contention
				1. Alpha = 0, for linear performance
		4. Effect of locking or serialization
			1. If 95% of the process is parallel
				1. If we increase no of processors: Throughput will rise  and flatten (S curve)
					1. Amdhal's law can be used to calculate when it flattens
			2. If 90% of the process is parallel
				1. Flattens quicker
					1. Throughput - almost half of previous one
			3. If 75% of the process is serial
				1. Flattens even sooner
			4. If 50% it is almost as a serial process
			5. If 0% it will be flat
	5. If we want to make a system highly performant:
		1. We have to make it concurrent
		2. We have to make it perfectly concurrent as well
			1. Limitation: Shared resources (by taking locks)
				1. Files
				2. Shared memory
				3. Record in database
			2. Locks will introduce serial portions in the application
				1. Goal: Keep the serial portions as low as possible (< 5% is good enough)
					1. If only 50% - it could be as good as serial

### Gunther's Universal Scalability Law ###
1. Amdhal's law (deals only with queuing)
	1. When processes get serialized, it results in queuing (synchronized portion)
		1. A thread has to take a lock to enter the serialized portion
			1. Other threads which do not have the lock have to wait
		2. **Queuing limits throughput or performance of a system**
1. Universal Scalability Law (combines queuing with coherence)
	1. Queuing + Coherence - limits concurrency of the system

			C(N) = N / [1 + alpha(N - 1) + beta N (N - 1)]
			
		1. C is capacity
		2. N is scaling dimension like CPU or load
		3. alpha - represents resource contention
		4. beta - represents coherence delay
	2. Linear performance when alpha and beta are zero
	3. Coherence:
		1. Example: suppose there are 3 threads executing on 3 processors
			1. L1 & L2 are unique to the processors
			2. Suppose we use volatile variable
				1. It will be consistent across processors
					1. Other variables have copies in each processor (caches)
				2. If we want variable to have same value across all processors, it can be declared as volatile
					1. If we change the variable in one processor, it will force a refresh (of value) of the variable in other processors (caches will be refreshed)
						1. It has a performance cost
		2. If we have a lot of shared variables and we modify them a lot:
			1. The coherence cost will be high
				1. If we increase the number of threads/processors/users
					1. The throughput goes down (reverse U curve)
						1. It will bring down the throughput graph
							1. (graph flattens because of queuing, graph goes down because of coherence)

### Shared Resource Contention ###
1. Causes of Contention
	1. **Listen/ Accept Queue**
		1. Listen Queue: If a new request received by server (assuming other requests exist in the server)
			1. If server is overloaded (slowness may be):
				1. The request will get queued at listen queue itself
					1. Usually if enough processors are not available
		2. Accept Queue
			1. Request crosses listen queue but it will not be processed yet
		3. These can be thought of as network queues
		4. If queue size grows beyond certain size, the requests are rejected
			1. Client will see errors
		5. If requests are accepted
			1. If listen queue and/or accept queue are long
				1. The requests will face much more latency than of those that do not have to wait in the queue (queue time gets added)
					1. Queue is killer of concurrency (queue build up takes place)
		6. Queue is at network gate
	2. **Thread Pool**
		1. CPU - A thread has to allocated for request
			1. It processes thread
		2. There are limited threads (depending on number of processors)
		3. If system is overloaded
			1. There will be contention for thread from fixed size thread pool
		4. There could be increased context switching if we keep increasing thread pool
			1. If we keep limit on thread pool, there will not be too many requests running
		5. Context switching happens if there is any IO or locks the process is waiting for
			1. If there is contention, processes will generally be waiting for many locks (increase of context switching cost as well)
		6. There is contention for thread pool
	3. **Connection Pool**
		1. Suppose process has to make a call to the backend
			1. There is a limit on the number of connections that we can have based on the size of connetion pool
				1. The threads have to contend for connection from connection pool
		2. Backend is running slower than the rate at which threads are processing requests (contention at connection pool)
	4. **CPU/ Disk/ Network**
		1. CPU - contention in the form of contention for threads
		2. Disk - Depends on the disk controller
			1. Only a limited number of threads can be allowed to access a disk at the same time
				1. Practically - **we can assume that we have a serial access to the disk**
					1. Can be assumed for design of system
			2. It can be a source of contention if we do a lot of I/O
				1. Use case: DB access
					1. If too much data is fetched
		3. Network - If network is choked
			1. Sometimes happens in microservices architecture
				1. Internal network
			2. There can be contention for network availability
	5. **Locks**
		1. Biggest source of contention (acquiring locks)
			1. This is required for serial part of the code
				1. Locks are gatekeepers for serial portions of code
		2. If multiple threads are contending for same lock, then it becomes a source of contention
	6. **DB**
		1. Similar contention as disk but CPU, Disk and Network is heavier (?)

### Minimizing Shared Resource Contention ###
1. **CPU/Disk/Network**
	1. As we increase number of requests, the utilization goes up (including **memory**)
	2. Steps:
		1. Serial request latency should be optimized (making use of resources efficiently)
		2. Vertical scaling (for better bandwidth)
			1. Memory - increase memory (and bus speed to access)
			2. Disk
				1. Better disk
					1. RAID - Redundant Array of Independent Disks
						1. **Allows parallel access to disk**
							1. Data is copied to multiple disks
								1. If there are multiple threads looking for same data
									1. Data can be accessed by multiple threads at the same time
						2. DB performance can also be enhanced
			3. Network
				1. More bandwidth
			4. CPU
				1. Better CPU
2. **Listen Queue**
	1. Depends upon thread pool
		1. If lot of requests are coming (web app > services > db)
		2. There could be build of of the queue if web app is not able to serve the requests
			1. Listen Queue grows
	2. Don't have to do much
		1. Only causes problem if we go to extreme scales
	3. Steps:
		1. Ensure that the system is processing requests efficiently
		2. Take care of other contention issues within the system
			1. Internal optimization could minimize the size of listen queue
				1. Thread pool size
				2. Connection pool size
		3. **Tune OS to increase listen queue size**
3. **Thread Pool Size**
	1. It is a collection of threads dedicated for a single purpose
		1. Thread pool provided by container (tomcat, jetty, weblogic say - for web apps, services, (batch request thread pool is not considered here)
			1. Server thread pool for worker threads
	2. If we have smaller thread pool size, the contention will increase
		1. **Listen Queue** can grow (waiting)
	3. We can increase the thread pool size
	4. Other problem: If we increase thread pool size to too high
		1. Threads will be idle waiting for CPU (2000 threads vs 10 CPUs)
	5. Solution: **Optimal size has to be found**
		1. Using load tests
		2. Factors affecting thread pool size
			1. Wait time
				1. Processing time (web app makes call to services which takes time => threads wait for services to finish)
					1. Solution: Larger thread pool size
			2. CPU time
				1. If threads occupy CPU and not make many calls to backend (CPU intensive)
					1. CPU time will be very high
					2. We don't want to go for high thread pool size (?)
						1. More or less equal to number of CPUs
							1. If CPU utilization is 100% and wait time is 0, then number of threads = No of CPUs (ideal case)
								1. Non-ideal cases (waiting exists)
									1. Disk I/O wait
									2. Locking
									3. External calls 
						2. Thread pool size increases is proportional to the wait time
			3. Number of CPUs
4. **Connection Pool Size**
	1. Thumb rule: 1:1
		1. Suppose thread pool size is 100, connection pool size should also be at-least 100
			1. If a request comes to web app and web app wants to make a request to services
				1. 1 HTTP connection will be made to make 1 call to services (at-least)
					1. If single HTTP connection results in multiple services connections, then connection pool size will be > thread pool size
					2. If gateway is used, only one connection will be created with the gateway
	2. Services: Database connections are considered
		1. One thread will make one db connection at a time (multiple simultaneous DB calls is rare)
			1. 1:1 (thread pool size: connection pool size)
				1. Threads usually do transactions (single connection)
					1. It is different for distributed transactions (multiple connections)
5. **Vertical scaling**
		1. Increasing performance of a single machine is considered here
			1. If we are done with handling contentions in a single machine, we can think about multiple machines
		2. Increasing number of threads requires increasing number of CPUs
			1. This needs vertical scaling of the system
		3. Increasing number of db load requires
			1. Increasing number of CPUs
			2. Better disks (RAID may be)
			3. More DB memory
		4. Services
			1. Increase CPUs
			2. Better disks (RAID may be)
			3. More memory
			4. Better network
		5. Vertical scaling is
			1. Making hardware more powerful
			2. Increasing the capacity of the hardware

### Minimizing Locking Related Contention ###
1. Minimizing lock contention
	1. Reduce duration for which a lock is held
		1. Move code out of synchronization block that doesn't required lock (especially I/O)
			1. Example: logging something (I/O) (context switch for I/O)
		2. **Lock Splitting** - Split locks into lower granularity locks (that are exepriencing moderate contention)
			1. Divide scope of lock into smaller parts

					{
						{ // take lock here
							...
						} // leave lock here
						{ // take lock here
							...
						} // leave lock here
					}
					
				1. Go for lower granularity objects
					1. Contention will be reduced
						1. Contention is for two objects instead of one object
						2. Duration will also get reduced		
		3. **Lock Striping** - Split locks for each partition of data like in concurrent HashMap (concurrent data structures)
			1. Example: Concurrent HashMap

					---			(bucket 0)
					-----		(bucket 1) - lock 0
					-			(...)
					-
					-------	(bucket 4) - lock 1
					---			(...)
					--
					...
					-----		(bucket n) - lock k
					
				1. Divide buckets into partitions (16 partitions)
				2. If we want to modify a bucket entry, the lock object responsible for that partition is identified
				3. Only that lock will be used to lock the partition, rest of the partitions will be left
				4. Advantages:
					1. Performance can go up 16 times (expectation)
						1. If operations are fairly divided among the 16 partitions
	2. Replace exclusive locks with coordination mechanisms
		1. Use **ReadWriteLock**/ **Stamped** locks
			1. **ReadWriteLock**
				1. When dealing with two kinds of threads (against a data structure)
					1. One thread - reading
					2. Other thread - writing
				2. Consider a data structure shared across threads
					1. Two types of locks
						1. Readers can take read lock
							1. While reading, it should not be modified
								1. Other readers can also take the lock (not mutually exclusive) - multiple readers can read
							2. Writer needs to wait for readers to finish
						2. Writers can take write lock
							1. If no readers are reading, writer takes the lock
				3. Advantages:
					1. Readers will not block other readers
						1. If we have a lot of reader threads but small number of writer threads, it reduces contention
		2. Use **Atomic Variables** (protected by CAS)
			1. CAS - Compare and Swap (doesn't take exclusive lock)
				1. Works based on optimistic lock
2. Take away:
	1. Reduce granularity of the lock
	2. Code protected should be as small as possible
	3. Look for non-exclusie locks

### Pessimistic Locking vs Optimistic Locking ###
1. Pessimistic Locking (regular kind)
	1. Threads must wait to acquire a lock
	2. Use when contention is high
	3. May result in deadlocks
		1. One of the participating thread is backed up by receiving an exception
	4. Procedure

			Lock & Fetch Data (Simultaneous)
					| 
				Process
					|
					v
				Update
					|
					v
				Commit (Unlock)
	
2. Optimistic Locking
	1. Threads do not wait for a lock, but backup when they discover contention
	2. Use when contention is between low to moderate
	3. May result in starvation
		1. Switch to pessimistic locking
	4. Procedure

			Fetch Data <--
					|		|
				Process	| On error
					|		|
					v		|
				Lock, Fetch,
				Verify & Update
					|
					v
				Commit (Unlock)
				
		1. Lock is for shorter duration as compared to optimistic locking
			1. Shorter serial portion
				1. Better concurrency
				2. Better performance
		2. Fetch (DB or Memory)
		3. Process - if it takes long time, we can run it outside lock scope
		4. Verify - check if initially fetched data is same as the one fetched again
			1. If so, there was no contention during the last fetch and this fetch
			2. If it is not the same, then the processing was done on stale data
				1. An error is thrown, process is re-run
	5. Dis-advantage:
		1. If there is lot of contention, we may have to back off many times => lot of CPU cycles get wasted
			1. The approach is good if there is no or moderate level of contention

### Compare and Swap Mechanism ###
1. Compare & Swap
	1. CAS is an optimistic locking mechanism
		1. All modern hardware (CPU) support it (OS as well if so)
	2. Java implements support for CAS through Atomic (`java.util.concurrent.atomic.*`) classes

			AtomicInteger ai = new AtomicInteger(10);
			ai.compareAndSwap(10, 20); 
			
			// returns true if value was 10 and sets 20 as the new value (at hardware level)
			// returns false if the value was not 10 as a result of a race condition with some other thread
			// Good for counters
			
			// Cassandra, HBase has similar feature
			select * from inventory where productId = 'Test-Product-7';
			
			productid			| quantity
			---------------------------
			Test-Product-7	| 		100
			
			update inventory set quantity = 200 where productId = 'Test-Product-7' if quantity = 0;
			
			[applied]		| quantity
			------------------------
				False		|		100
				
			update inventory set quantity = 200 where productId = 'Test-Product-7' if quantity = 100;
			
			[applied]
			----------
				True
				
	3. 	NoSQL - Doesn't allow transactions
		1. The only way to ensure atomicity is through optimistic locking
2. Advantage(s):
	1. Since this feature is provided at the hardware level, the performance is good

### Deadlocks ###
1. **Lock Ordering Related** - Reason 1
	1. Result of threads trying to acquire multiple locks
		1. Simultanous money transfer from X and Y accounts by thread T1 and T2
		2. T1: from X to Y
		3. T2: from Y to X
	2. Acquire locks in a fixed global order
		1. Acquire locks only in the sort order of account numbers: X and then Y
			1. Defined: Accounts are pre-sorted
				1. T1 should take lock on X and then on Y
				2. T2 should take lock on X and then on Y
					1. If T1 has taken lock on X, then T2 will not be able to proceed and T1 will be able to take lock Y
	3. Illustration
					
				  T1
			+-----------+
			|			  |
			|			  v
			X			  Y
			^			  |
			|			  |
			+-----------+
				  T2
			
		1. T1 has acquired lock for account X and is waiting for lock for account Y
		2. T2 has acquired lock for account Y and is waiting for lock for account X
		3. Example: If we have 20 threads and two have got deadlocked, we will be left with 18 threads, and if more and more pairs get deadlocked, we will lose most of the threads
			1. Brings down the performance of the application
	
2. **Request Load Related** - Reason 2 (Load induced deadlocks)
	1. Threads waiting for connections to multiple databases
		1. May run out of enough connections resulting in deadlocks
	2. Threads waiting for other threads to be spawned and perform some work
		1. May run out of enough threads resulting in deadlocks
3. Deadlocks
	1. Can throttle performance of the system
	2. Can bring down to a standstill
	3. Illustration:

					| (1)
					v
				gateway --+
			(2)	|	^		| (4)
				v	| (3)	v
			service 1	service 2
			
		1. Request reaches Gateway
		2. Suppose service 1 wants to call service 2 (db say) and it is routed through gateway (3) and (4)
		3. Response goes in reverse order
		4. When load goes up - there can be deadlocks (?)
			1. Suppose gateway service has got thread pool of size 10
			2. Suppose 10 users send requests to gateway
				1. 10 threads get allocated
			3. 10 threads make call to service 1
				1. Suppose 10 threads are allocated to service 1
			4. 10 threads make call to gateway service
				1. But the threads are occupied
					1. The threads will be blocked
		5. If there are only 2 requests,
			1. 2 threads for user and 2 threads for service 1 => 4 threads
				1. There is no blocking
		6. Suppose we are making connection to databases (we ran out of connection pool)
			1. If there is high load
				1. Few threads make connection to certain databases but not others
				2. Few other threads make connection to other databases but not to those already made by first set of threads
4. Solution:
	1. A solution: 
		1. Make service call directly (without going through gateway)
		2. Anticipate load from internal services and increase the size of the thread pool in gateway

4. **We must guard the system from deadlocks**

### Coherence Related Delays ###
1. Coherence Delays (related to shared data)
	1. **Visibility (Volatile)**
		1. Java garantees that a volatile object is always read from main memory and written back to main memory when updated in a processor
	2. **Locking (Synchronized)**
		1. All variables accessed in a sync block are read from main memory at the start of sync block
		2. All variables modified in a sync block are flushed to the main memory when the associated thread exits the sync block
			1. **Synchronized ensures locking & visibility**
			2. **Volatile only ensures visibility**
	3. These guarantees are provided using memory barriers which may result in invalidating or flushing of caches
2. Processor architecture

			CPU				CPU
		L1 Cache		L1 Cache (5ns)
		L2 Cache		L2 Cache (7ns)
				L3 Cache
			RAM - Main Memory  (100ms)
		Hard Disk/	Network Card - NIC
		SSD
		
		L1 Cache - faster
		L2 Cache - slower, bigger, cheaper
		
	1. Suppose T1 is running on CPU1
		1. T1 will load shared data into L1 and L2 caches
		2. T1 modifies shared data, it will be modified in L1
			1. This change will not be visible to T2
				1. If T1 is running a loop and it can be stopped by T2 by setting a value
					1. If code is not guarded by `synchronized` or `volatile` - the change happens only in L1 of CPU2 and L1 of CPU1 cannot see this
	2. Suppose T2 is running on CPU2
	3. Solution: `synchronized`
		1. Suppose T1 modifies variable
			1. It will be propagated to main memory
		2. Suppose T2 wants to read the variable, the variable becomes dirty and it will be read from memory
		3. Drawbacks
			1. High latency (access to RAM - 100ns) - 15 times slower as compared to cache
	4. Solution: `volatile`
		1. Locking related penalty is avoided
		2. Reading is still from main memory
3. We cannot do much regarding these kind of delays
	1. If variable is frequently accessed among threads - coherence related delays can occur
		1. We can try to minimize sharing of data
		2. We can try to reduce the frequency of modifying or accessing the variables

### Caching ###
1. How to make requests more efficient by caching some data

### System Architecture for Performance ###
1. Architecture so far

		UI Client ---> Web Application ---> Services ---> Database
					Persistent Connections      ^      Denormalization
					Response Compression        |      Normalization
					Efficient Encoding          |      Indexing
					Web Content Caching         |      Buffer/ Page Cache
					SSL Session Caching         |
					Session Caching             | 
									^              |
									|			     |
									Thread Pool & Size
									DB Connection Pool
									Efficient Locking
									Query Optimization
									Asynchronous Logging
									Sequential & Batch I/O
									Data Caching
									
	1. Buffer/ Page Cache
		1. Caching done by database
	2. Data Caching - in services
	3. Web Content Caching - static data
	4. SSL Session Caching (SSL connection parameters)
	5. Session Caching

### Caching for Performance ###
1. Caching architecture

		UI Client -||--> Web App --> Services --> Database
			||		static		||				||
		HTTP		data		session		object
		cache		cache		cache			cache
		
	1. Object cache (dynamic data)
		1. data fetched from database
			1. For any user (not user specific)
		2. Service doesn't have to make repeated calls to db for the same data
	2. Web app
		1. Session cache (user level) (dynamic data)
			1. User related data can be stored here
	3. Static Data Cache
		1. CSS, JS, Images, HTML, ...
			1. These files cannot change very frequently
		2. Caching can be at reverse proxy or load balancer
			1. It can have a large file system (HDD space)
				1. All static content can be put here
		3. Caching can be at CDN
		4. Caching can be at public cache
	4. HTTP Cache
		1. Browser cache
			1. Images
			2. ...
2. If something changes too frequently, caching doesn't make sense
	1. If it does not change frequently, it makes sense to cache
		1. Or if many requests can be served before the data changes

### HTTP Caching of Static Data ###
1. HTTP Caching for Static Data (between browser and web-application)
	1. GET method responses are idempotent and hence good candidates for caching
	2. Headers
		1. Cache-control: If a resource can be cached
			1. `no-cache`: Do not use cache without validating with origin server
				1. Browser or intermediate server can cache but it cannot use it without validating with origin server
			2. `must-revalidate`: Like no-cache but need to validate only after its max-age (even if client is ready to accept stale data)
			3. `no-store`: Do not cache at all
			4. `public`: Any shared cache can cache
				1. Any intermediate public cache can cache the object
					1. Useful for multiple users
			5. `private`: Only a client cache can cache
				1. User specific data (profile image say)
				2. private cache can cache this data
			6. `max-age`: Maximum age of a resource in cache, relative to resource request time
				1. How long the client or intermediate servers can cache it
		2. ETAG: A hash code for indicating version of a resource
			1. Invalidates previous version cache
			2. Example: If we have an image on web application and it is labeled as version 1 using ETAG
				1. Any cache can cache or `no-cache` (to enforce e-tags)
					1. Each time browser tries to use the cached image, it validates it against the web-application (can it use or not)
						1. Steps:
							1. Browser provides ETAG value to Web app
							2. Web app looks at ETAG and if it is latest version, it responds that browser can use it
							3. Web app can label ETAG to version 2 and send the response
							4. Browser checks if ETAG sent by web app matches with the one it has
								1. If it does not match, it reloads the image from the web-application and updates ETAG to version 2
2. Caching architecture between web browser and web application

		browser cache -proxy server cache -> reverse proxy cache -> web app
		
	1. Ignoring router servers in between
	2. Reverse Proxy Cache (close to server) - **private cache**
		1. There could be multiple web applications behind the reverse proxy (all requests come to reverse proxy)
		2. This can cache static data
	3. Proxy Server Cache (close to client) - **public cache**
		1. Multiple browser trying to access the same application will converge to this (office say)
		2. It can cache all responses coming from web application
		3. Data of any user can be cached and accessible to public (in the office)
			1. An admin can see this data
	4. Browser cache - **private cache**
3. How do public and private caches know what data to cache?
	1. GET - good candidate for caching (read only)
		1. Every get request cannot be good candidate for caching
			1. If it is serving the data that changes very frequently say
			2. If it is serving data that doesn't change frequently
				1. Good candidate to cache
4. Cache control header
	1. When a web app sends response, it can put a `cache-control` header in the response
		1. Indicates two things (for intermediate caches):
			1. Indicates if the request should be cached
			2. If cached, for how much duration
5. Reverse proxy:
	1. It can exclusively host static content (no static content on web application)
		1. It is responsible for setting cache headers

### Caching of Dynamic Data ###
1. Dynamic data caching - Two approaches
	1. Exclusive Cache (cache per node)
		1. Has low latency
		2. Without routing can lead to duplication
			1. It is okay one is fetching data from any instance
				1. User request can go to any instance
					1. If the data is filled in most of the nodes, it becomes effective - request can go to any of the nodes
			2. Useful for smaller datasets
				1. Example: Currency conversion table
					1. Duplication is okay (small data)
				2. Example: User profile data
					1. Duplication is expensive
						1. We need intelligent routing
							1. Session cache can be used
		3. With routing can lead to uneven load balancing
			1. Session cache
				1. Suppose user request has come to node 1 and it is cached
				2. Next time user request comes:
					1. A cookie can be stored in user browser that tells what node the user connected to in the previous request
					2. The user can be redirected to the same node
						1. If data is present in the cache, request can be served
				3. Advantages:
					1. Duplication of data can be avoided
					2. Very fast as compared to shared cache
						1. Cache is internal
							1. It is stored at the node and fetched quickly if request comes to the node
				4. Disadvantages:
					1. Requires routing of data to specific node
					2. Scalability issues
					3. Requires additional mechanism for this to work
		4. Illustration

									Node 1 [Cache Data]
								/
				Browser - LB -	Node 2 [Cache Data]
								\
									Node 3 [Cache Data]
		
		5. Example: Web-application
			1. Each web-app node can cache data in it's own memory
				1. It resides within the instance (service data say)
	2. Shared Cache (caching is deligated to an external component)
		1. Higher latency due to an extra hop (in network)
			1. Adds some cost (ms)
		2. Can scale out to a distributed cache
			1. Memcache
			2. Redis
		3. For large datasets
		4. Illustration

									Node 1
								/ 			\
				Browser - LB -	Node 2 - [Cache Data]
								\			/
									Node 3
									
		5. Advantages
			1. Intelligent routing is not required
				1. Only one cache
			2. Easy to scale out this cache
				1. Scaling responsibility can be decoupled to caching mechanism
				2. They can be clustered easily
					1. Can cache huge data
			3. Good for large data sets
			4. No intelligent routing
			5. No duplication of data
2. Where do we need this dynamic data caching?
	1. Services
		1. If they fetch data from database
			1. If it is not changing very frequently
			2. If it is accessed more frequently
	2. Web Application
		1. User profile info (say it is from database)
			1. If user asks for user profile again
				1. Cached data can be returned
3. Dynamic data that doesn't change frequently can be cached

### Caching Related Challenges ###
1. Any caching strategy has the following two limitations:
	1. **Limited cache space results in early evictions**
		1. Data is read only
		2. Prefer caching for frequently accessed objects
			1. **Cache fast-moving consumer goods** vs slow moving goods
				1. e-commerce store
					1. Not many people will be accessing slow moving goods
					2. Many people will be accessing fast moving goods and the goods will likely be unchanged for long periods of time
		3. Average size of cached objects should be as small as possible
			1. Large sized objects results in cache getting full too soon causing evictions
				1. Small objects occupy lesser space so more number of objects can be cached
					1. Optimizes cache size as well
	2. **Cache invalidation & cache inconsistency** (if data becomes stale it becomes in-consistent with main source)
		1. Requires update/ delection of cached value upon update (of source)
			1. Not an option when a cache is outside of a system (public cache say - HTTP cache - not in our control)
				1. We cannot update or delete contents of the cache
			2. No cache inconsistency
				1. Cache is immediately updated with source data if it changed - brings down inconsistency duration to bare minimum (cache is part of the system)
		2. TTL value can be used to remove aged data (results in cache miss - HTTP caching say) - TTL is Time To Live (object based caching)
			1. High TTL results in more cache hits
				1. Inconsistency interval increases
			2. Low TTL decreases inconsistency interval
				1. Cache hits go down
			3. Cache receives TTL along with object and it cannot be changed
				1. Disadvantage:
					1. May need trial and error to figure out a good TTL value or could be based on other statistics (which needs time and data)
					2. Suppose TTL is still valid and data has changed at source
						1. Client will be receiving stale data
							1. TTL is 1 hour and data changes every 5 minutes
					3. TTL is 5 minutes and data is updated every hour
						1. We will be hitting source every 5 minutes unnecessarily
3. Cache Hit Ratio: (used to measure effectiveness of cache)

		cache hit ratio = # of cache hits / (# of cache hits + # of cache misses)
		
	1. \# of cache hits - if data is served by cache
	2. \# of cache misses - if data was not served by cache
	3. \# of requests - \# of cache hits + \# of cache misses
	4. If cache hit ratio is high - more effective
4. Caching is based on memory
	1. It is not a cheap resource
		1. Database stores data on disk - cheaper
			1. Memory cannot store this amount of data (very expensive)
				1. TB of cache (memory) is prohibitively expensive
		2. We need to decide what to cache and what need not be cached
5. We need to look at trade-off while designing caching strategy

## Scalability ##
### Module Contents Overview ###
1. System Scalability
	1. Scalability
		1. Vertical & Horizontal Scaling
	2. Horizontal Scalability (ways to achieve it)
		1. Replication
		2. Services
		3. Caching
		4. Asynchronous Process
		5. Partitioning
	3. Load Balancing (How to load balance)
		1. Load Balancers
		2. Service Discovery
		3. DNS & Geo Load Balancing (for global solutions)
	4. Micro-Services (helps in highest degree of scalability)
		1. Architecture
		2. Transactions
		3. SAGA Pattern (compensating transactions)
		4. NoSQL (for scalability)

### Performance vs Scalability ###
1. Performance - meausured for **fixed load**
	1. Low latency (request-response time is low)
	2. High throughput (rate at which system is processing requests)
		1. Concurrency (increase)
			1. Single machine - multi-threading
			2. Multi machine - multi-threading + multi-processing = distributed processing (this was not considered before)
		2. Capacity (augment)
2. Scalability - measured for **for variable load**
	1. High throughput
		1. Definition: **Ability of a system to increase its throughput by adding more hardware capacity**
			1. 1 million users or 10 million users
				1. We want to see how the system will perform if we increase and/or decrease the load
	2. Both ways - UP and DOWN
		1. We should be able to scale up or down (to save cost)
	3. Scalability is performance under variable load

### Vertical & Horizontal Scalability ###
1. Vertical (we replace smaller hardware with a more powerful hardware (4 CPU to 32 CPU, 16 GB RAM to 256 GB RAM)
	1. Easier to achieve
		1. Very costly
	2. Limited scalability
		1. Expensive to get high end machines (may be exponential)
		2. It may be infeasible (such hardware may not exist)
2. Horizontal (we add more hardware - more such machines are brought up of the same power - 3 machines of 4 CPU & 16 GB RAM - cost goes up linearly (not exponentially))
	1. Hard to achieve
		1. Software should be designed to support this (coordination is required)
	2. Unlimited scalability
		1. Practically it is high
		2. Unlike vertical scalability, we can scale down and re-purpose the machines for other uses
			1. Cloud env - we can rent out and return to scale up and down respectively

### Reverse Proxy ###
1. Reverse Proxy
	1. Client needs to know only about the address of reverse proxy
		1. If load balancer does not exist
			1. Client needs to know about all the machines to distribute requests
				1. Clients need to remember IP addresses
					1. Not practical if we scale (dynamic property - can increase or decrease)
		2. Can be used for internal clients as well (IP address can be remembered)
		3. External client - only remebers DNS name which will be resolved to IP address by DNS server(s)
			1. DNS can map one DNS name to multiple IP addresses
				1. It is not going to be used as reverse proxy
					1. It can have stale data for quite some time (instances can be dynamically changing)
	2. Reverse proxy can also act as a load balancer
		1. Reverse proxy - sits near server side
			1. Every request intended to server goes through reverse proxy
			2. It can also decide which server can serve the request
				1. Can be configured to act as a load balancer

### A Reference Software System for Discussing Scalability ###
1. System for Scalability Discussion

		Web Browser -> Web application -> Business Application -> Database
		
	1. How to scale the application? - to handle millions of users

### Scalability Principles ###
1. Principles to make a system horizontally scalable: (scalability depends on the following principles)
	1. **Decentralization** (one component is not responsible all the different kind of work) - Monolith is an anti-pattern for scalability (if there is only one component for the entire load the system is facing - the only way to scale is vertically) - there are multiple components of different kind for the work
		1. More workers - Instances, Threads
		2. Specialized workers - Services
			1. Different kind of workers for different kind of work
	2. **Independence** (benefit of lots of workers is when they can work independently) - coordination may be required if there is shared data (db access say)
		1. Multiple workers are as good as a single worker if they can't work independently
			1. They must work concurrently to maximum extent
		2. Independence is impeded by (coordinator may be required)
			1. Shared resources
			2. Shared mutable data
				1. DB
				2. File
				3. ...
		3. Coordinator becomes bottleneck
			1. If we increase number of workers, the load on coordinator also increases
				1. 100 workers to 1000 workers
					1. Load on coordinator will be up by 10 times
						1. System will fail at some point
		4. Solution:
			1. If workers can be made to work independently
			2. If requirement for coordination can be minimized

### Modularity for Scalability ###
1. Modularity (scalability can be started from here)
	1. Scalable architecture starts with modularity
		1. Provides the foundation for breaking an application into more specialized functions / services
	
				Web Browser -> Web App -> Business App -> DBMS
												- API Protocol Layer
												- Service Modules:
												  User (module)
												  Catalog (module)
												  Order
												  Inventory
												- Data Access Layer

			1. Modularity applies to Business Logic (Business App mostly, and a little with Web App)
				1. It can be dividied such that
					1. It is not coupled
					2. It must be loosely coupled
					3. Later can be made completely decoupled (if possible)
	2. First make business logic modular
	3. Make API Protocol layer decoupled from business logic
		1. This can change independently from buisness logic
	4. Make Data Access Layer decoupled from business logic
		1. This can change independently from business logic

### Replication ###
1. Replication
	1. For handling increasing workloads
		1. Stateless (no data involved)
			1. Code Replication
				1. Web application - has 3 instances (running same code) - statelss/ stateful
				2. Service application - has 3 instances (running same code) - stateless
				3. Stateful:
					1. It is used in some circumstances
		2. Stateful
			1. Code & Data Replication
				1. Database (stateful) - has 2 instances
					1. Data synchronization
						1. Data written on one instance should get propagated to other instances
	2. Why?
		1. When load on system increases and if one machine cannot handle the load, we can scale horizontally
			1. User load can be shared among multiple instances
			2. DB - depends on the kind of replication used

### Stateful Replication in Web Applications ###
1. Stateful replication is done: When low latency is required (web app)
	1. Sticky sessions/ session affinity
		1. Session data is stored in an instance identified using id
		2. Client is returned a cookie with the following info:
			1. Session id
			2. Node id
		3. Client sends request to load balancer
		4. Load balancer checks the node id sent and redirects request to the node
			1. Latency is reduced (by reducing hops)
	2. Sessions occupy memory
	3. Session clustering for reliability
2. Example: Suppose user wants to fetch user profile
	1. User sends request to web app
	2. Web app forwards request to services app
	3. Services app sends request to DB
	4. The profile goes back using the same route
3. The number of hops can be reduced by storing profile in Web-app
	1. First time, the user profile data is obtained from DB
	2. Web-app stores user profile - in the instance hit
4. Limitations related to:
	1. Scalability
		1. Each session data occupies memory
			1. Suppose it occupies 1 MB per user
			2. 500 MB of total memory
			3. => 500 connections is the limitation
			4. CPUs and threads limit actual connections to 2000 connections simultaneously
				1. But due to session limitations, it can serve only 500
					1. More machines are required to serve remaining requests (due to session memory limitation)
						1. Operation cost will go up
	2. Reliability
		1. Suppose a node goes down (Node 1)
		2. If load balancer receives a request and it has to route it to node 1, node 1 is no longer alive
			1. Load balancer route to any of the other nodes
				1. The session data needs to be fetched again (full latency is the cost)
				2. All the users whose session data was stored on node 1 will get affected
					1. All of them will experience high latency (until caches are refreshed)
		3. If user has made changes to session data (user profile data) and it has not been propagated to the database yet and node goes down
			1. The changes will be lost
			2. User will see old data
				1. Solution: Web-Logic, Web-Sphere provide clustering session feature
					1. Session data gets clustered on other machines

							node 1 -- session 101 data
							...
							node i -- session 101 data
							...
							
						1. If a machine goes down, users can be diverted to node i
						2. When user makes changes to session data, clustering logic will ensure that the changes are propagated to replica
		4. Drawback
			1. Complicated
			2. Messy to handle
	3. Not preferred approach
		1. Stateless replication is the preferred approach
	4. Where is it used?
		1. If the above are not serious limitations and do not outweigh limitation on latency side

### Stateless Replication in Web Applications ###
1. Web Stateless Replication
	1. For higher scalability at the expense of higher latency
		1. No longer store data in web-layer
		2. Each time we go to the database and fetch data
			1. Issue: Added latency
				1. Solutions:
					1. Session data can be stored on:
						1. Client side in Cookies
						2. Server side in Shared Cache
							1. Options:
								1. Memcached
								2. Redis
							2. First time, request goes to DB and stored in cache
							3. Second time, request goes to Cache
								1. Latency is saved
									1. Not as fast as web-app memory
						3. Overhead
							1. Additional component - shared cache
						4. Advantages:
							1. Good for large amounts of data
							2. If there is non client specific data
							3. If any instance goes down
								1. Data is not lost - it is there is cache
								2. If cache goes down
									1. Application nodes can fetch data from database and fill the cache again
					2. Storing session data on user side (in cookies)
						1. The request will come along with session data to the web app
							1. Limitation: Cookies cannot carry a lot of data
								1. Network cost (if multiple hops are required)
						2. Good for small amount of data
2. Go for stateful if requirements for latency is extremely critical

### Stateless Replication in Services ###
1. Stateless replication - same as web stateless
	1. Similar to web app
		1. One can go for stateless replication
			1. Data that is more frequently read than modifed can be stored in a cache (shared cache)
	2. Challenges
		1. Introduction of additional complexity with shared resources
			1. If all instances are using shared resource (file say) and writing to it in a transaction mode
				1. We cannot synchronize using locks because the instances are separate (not managed by same OS)
					1. Solution:
						1. Lock table in database
							1. Take a lock on a row
							2. Modify the file
							3. Commit the row

### Database Replication ###
1. Database Replication (considering RDBMS systems - general use cases, NoSQL - specific use cases)
	1. For higher read scalability
	2. For high availability
2. A solution: Vertical scaling
	1. There is point where it doesn't work
3. How to scale?
	1. Read replica is created (another db instance)
		1. Any change happening to master db gets replicated to read replica
			1. Some of the read load can be diverted
		2. Master can take both read and write loads
	2. Advantages:
		1. If there are large number of read requests (as compared to write requests), this approach scales
	3. Backup replica
		1. Used for high availability
			1. if master goes down, the backup can be promoted as master

					-R/W->	Master DB -> Backup DB
								|
								v
					-R-> Read Replica DB (Slave/ Secondary)

### Database Replication Types ###
1. Master-Slave (Primary-Secondary)
	1. Asynchronous (read replica)
		1. Low latency writes
		2. Eventually consistent
		3. data loss
	2. Synchronous (backup)
		1. Consistent (both dbs are in sync)
		2. High latency writes
		3. Low write availability

				Service -R+W-> Master/Primary
					|				|
					|				Uni-directional
					|				replication
					R				|
					|				v
					+---------> Slave/ Secondary
					
			1. Any changes that go to master are replicated to slave in due course of time
				1. Two ways to do this
					1. Asynchronous
						1. If client writes to database, once transaction is successful, it is acknowledged immediately (by the master)
						2. Whatever changes done are propagated to slave(s)
							1. Time delay can exist
					2. Synchronous
						1. If client writes to master db
							1. The changes are immediately propagated to secondary db
							2. When secondaries acknowledge that the changes are applied, the primary acknowledges to the client that the transaction is committed
		3. Properties - reasons we do this are
			1. High read scalability (many read replicas can be made availability)
			2. High read availability (if one of the instances goes down, other replicas can serve the requests, if master goes down, read replicas can serve the requests)
			3. No write conflicts
	3. Differences between asynchronous and synchronous replications
		1. Asynchronous
			1. Changes are propagated after transaction completes (involving only master)
				1. Faster because only master is involved
			2. Consistency - there is lag
				1. Secondary may not have the most latest data
					1. If client reads data from secondary when master is different, client gets stale data
						1. It is eventially consistent
							1. After a delay, they become consistent
			3. If master db goes down and secondary is promoted
				1. Certain changes not promoted to slave are lost
			4. Writes become unavailable only if master goes down
				1. If secondary goes down, write can still continue
					1. It can pickup when it comes back
			5. It can be used in cases where we need high read performance, low latency reads and writes
		2. Synchronous
			1. Slower because all master and slaves have to be synchronized before comitting the transaction
				1. Slower write latency as compared to asynchronous
			2. Consistency
				1. Data is always consistent (transaction takes care of that)
			3. Low write availability
				1. Suppose read replica goes down & synchronous replication is established between master and slave
					1. Since secondary is not available, transaction cannot be completed (because transaction needs to update secondary as well to complete)
						1. Writes become unavailable if any of the databases goes down
			4. This can be used for backups
				1. Not for read replicas
				2. Master and backup will be in sync with each other
					1. Brings down latency a bit (as compared to asynchronous)
					2. But if master goes down, backup will get promoted to become master (without loss of data)
2. Master-Master (No-Master/ Peer-To-Peer)
	1. Asynchronous (multi-geography)
		1. Write conflicts
		2. High availability
			1. It does not matter which database goes down (we can write to other databases)
	2. Properties
		3. High read scalability
		4. High read write availability
		5. Transaction ordering issues

				Service -R+W-> DB1
									^
									|
								Bi-directional
								replication
									|
									v
				Service -R+W-> DB2
				
	3. Client can read/write on any of the instances
		1. Replication is bidirectional
			1. Change in one is propagated to other database
		2. Flavours
			1. Asynchronous
		3. Challenge:
			1. Write conflict
				1. If changes are made in both db instances to the same record at the same time
					1. In master-slave - there is only one source of truth
						1. No write conflicts (this is popular and simple)
				2. Not easily resolved
		4. Use case:
			1. Different data exist in different databases (not same records)
				1. User writes to the db close to the user
				2. If user from one location wants to write data of another location, the data is written to the remote location.
					1. Write latency is higher of remote location
			2. Business rules need to be written to handle write conflicts
		5. Clock skew can be present between the instances
			1. May cause transaction ordering issues

### Need for Specialized Services ###
1. Need for specialized services
	1. Service modules: (they live within same application instance)
		1. User
		2. Catalog
		3. Order
		4. Inventory
		5. Notification
	2. Scalability issues
		1. Extra load - updating inventory
			1. Warehouses review and upload updated inventory
				1. Load on system goes up
			2. We want to add more instances for inventory module only
				1. But bloated app has all the modules
					1. All modules need to be scaled (all resources (db connections, ... will be required)
						1. The operational issues can be fixed if we break our monolith application into smaller services

### Specialized Services - SOAP/REST ###
1. Specialized services
	1. Partially independent development and deployment
		1. There is still some dependency
			1. Common database
			2. If SOAP schema - WSDL dependency
				1. RESTful - the dependency can be got rid of
	2. Independent scalability
		1. Any service can be scaled independently
			1. Catalog service say
				1. More instance for Catalog service
	3. Independent technology
		1. Technolgy used to develop the services can be independent of each other
			1. User Service - .Net
			2. Catalog Service - Java
			3. Order Service - C++
			4. ...
2. Consequences
	1. We can independently develop the service (partial dependency)
		1. User service developer does not need to know the inner details of catalog service
			1. But shared tables of DB (one service cannot modify the schema)
	2. We can independenty deploy the service (partially)
		1. Patch on User service can be added independently of other services
		2. But common libraries and schema cannot be deployed independently
	3. Increase in complexity of the system
		1. Web application
			1. Needs to interact with multiple services say (complex interaction)
		2. Mobile client
			1. Complexity of app
				1. They are usually external to the system (unlike web application) - difficult to locate where which service is available
		3. **Solution**:
			1. RESTful Aggregator/Gateway Service
				1. Reasons for Gateway Service
					1. Workflow complexity
						1. Single point of contact for all clients (web or mobile)
							1. Aggregation of responses are taken care by aggregator service
					2. Inter-operable interface on gateway service
						1. This is essential here but not for internal services
							1. Inter-service communication can be on gRPC or Thrift (binary protocol)
								1. Faster (performant)
						2. Clients can use REST or SOAP
							1. Thrift or gRPC can also be used by clients
3. Caveat - Single instance exists for write load
	1. Problem if load becomes very high

### Asynchronous Services ###
1. Async services effectively reduces write load from a database
	1. Message queues - 
		1. Used to integrate client and server if interfaces are different (not compatible) (?)
		2. Used to reliably deliver message from client to server
		3. Scalability - used to offload some write load on databases
			1. Where to use message queue?
				1. Suppose order booking request takes time to process
					1. Order service:
						1. Accept the order
						2. Validate the order
						3. Persist it in messaging queue (processed later)
							1. Previously this step was done synchronously
								1. Also talk to inventory
							2. Message queues are fast at accepting messages (they are designed for that)
						4. Send response to user (acceptance)
					2. Order Processing service
						1. Pulls requests from messaging queue
							1. Push requests to order processing service can also be implemented as an alternative
						2. Talks to other servicess (Inventory say)
						3. Processes requests
						4. Talks to notification service
							1. Notification service - notifies user of order creation
2. Asynchronous processing:
	1. Where to use it?
		1. Where write operation is the main operation
			1. Read operation: request goes through system (db if required) processed and displayed to user
				1. Here asynchronous processing cannot be used (we need to respond immediately and show information immediately)
			2. **Predominantly write oriented operations: Write operations where intermediate read operations dont have to be shown to user**

### Asynchronous Processing & Scalability ###
1. Async services require infrastructure for average load as opposed to peak load
2. Order requests coming to order service are processed in order processing servie are written to database
	1. If we are receiving 50000 requests/sec on order service, db is also processing 50000 requests/sec
		1. DB has to scale at the same rate as order service
		2. There could be other requests from other services coming (common db for services)
		3. Load on DB will become very high
	2. Solution: Asynchronous processing
		1. Load on system will not be constant throughout and it varies
			1. Peak periods - request rate will be high
				1. The requests coming during peak periods can be stored
				2. When load on system is lesser, we can process the stored requests
					1. Requests don't have to be rejected
				3. A threshold can be used
					1. Any requests above 10000 requests/ second cannot be handled & lower rate can be hanled by the DB
						1. The scaling gets stopped dat 10000 requests/ sec
							1. This can be changed by introducing message queue + order processing service
								1. Message queues can scale much higher than databases (100000 requests/ sec say)
									1. They are fast because very less processing
				4. DB will continue to process at it's maximum rate
					1. 10000 requests/ sec
			2. When request rate goes down below 10000 requests/ sec
				1. DB and order processing service will catch up with the backlog accumulated
				2. Backlog gets reduced during lull periods (when there is no much load)
			3. Alternative - more database is needed
				1. Problems: 
					1. Even if the rate is slightly higher, db will not be able to handle them
					2. The rate doesn't last very long and could be in multiple short bursts then DB will be underutilized (on an average)
		2. Consequence: Peak load is distributed over a period of time
3. Asynchronous processing wherever it is possible to introduce can increase the scalability of the system	

### Caching for Scalability ###
1. Caching reduces latency and reduces overall read load
	1. Recap
		1. If there is data that is very frequently read and is not modified so frequently - candidate for caching
		2. Points where we can cache
			1. Database: Object Cache
				1. Services can utilize instead of going to database (read)
			2. Web application: Session cache or regular cache
				1. Data related to user session
				2. Global data can also be cached
			3. Reverse proxy: Can cache static data
			4. Proxy: Can cache static data
			5. Browsers: Can cache static data
	2. Consequences
		1. If data is available in browser cache, call is not made to the system
			1. Load on system will reduce
		2. If static data is available on reverse proxy, call will not be made to web application
			1. Reduces load from web application and rest of the system behind
		3. Web can cache data and not make calls to services
		4. Services can cache data in object cache and avoid making calls to database
		5. If we can reduce calls using caches, we can reduce load on the system components (especially database - it is hard to scale because it is stateful)
			1. Read replicas can be created but write load is still a bottleneck
			2. If read load is offloaded to cache, db gets freed from load
				1. This gives some breathing space to the database to increase it's write load (capacity gets utilized to serve write loads)
2. Two ways to reduce load on database
	1. Asynchronous processing using message queues (reduces write load by distributing in time)
	2. Caching for read load (reduces read load by offloading it to cache)
	3. This further scales database and the entire system

### Vertical Partitioning with Micro-Services ###
1. Micro-Services completely decouples services and databases for higher scalability
	1. Suppose we need to handle more load than what has already been done
		1. Write load (cannot be distributed for RDBMS)
			1. Solutions:
				1. Depends on the kind of data we are storing
					1. Each service represents a domain in the business logic
						1. Inventory
						2. Order
						3. Catalog
						4. User
							1. User Authentication (service)
							2. User Profile (service)
					2. We can separate data based on domain, we can host the data on different databases
						1. Inventory -> Inventory DB
						2. Order -> Order DB
						3. Catalog -> Catalog DB
						4. User -> User DB
					3. Roughly the system is 4 times more scalable (or more)
					4. Challenge:
						1. We may have to get rid of common tables
							1. Each db is responsible for a particular data according to business domain it belongs to
								1. Order service talks to only Order DB
								2. If Order service wants Catalog data:
									1. It should go through Catalog service
										1. There is separation of responsibility
					5. Consequences:
						1. The DBs can be scaled independently
						2. The DBs can be deployed independently
						3. The DBs might have different load
						4. Write load is distributed among different DBs
					6. Drawback:
						1. We have sacrificed ACID transactions
							1. Suppose Order service was previously doing transactions over multiple tables
								1. The tables are distributed across databases
									1. This is no longer possible
2. Vertical Partitioning:
	1. Services & Data are vertically partitioned
		1. Inverntory -> Inventory DB
		2. Order -> Order DB
		3. ...
	2. This is microservices architecture
		1. Used for high levels of scalability
			1. If we have run out of other ways of scaling the system
			2. Good to scale for write load

### Database Partitioning ###
1. Used for extreme scalability
	1. Context:
		1. Vertical partionaing of system
			1. DB split based on domain (Catalog -> Catalog DB, ...)
			2. Limitations:
				1. 10 domains say - 10 times scalability approximately
			3. This is not sufficient for higher levels of scalability
				1. Extreme load say (after vertical partitioning)
					1. Solution: Horizontal partitioning
						1. Suppose Order db is heavily loaded
							1. Range partitioning: (id is pk) - if we increase or decrease the number of nodes, we may have to change the way we partition (complicated)
								1. Logic:
									1. ids 1-100 hosted on node 1
									2. ids 101-200 hosted on node 2
									3. ...
								2. Challenges:
									1. Re-partitioning is required if we increase or decrease the number of nodes
									2. If nodes go down, re-partitioning may be required
								3. While inserting or fetching data, we need to have the logic to send the request to the right node
								4. Issues:
									1. We cannot do ACID transaction on records
										1. Single record ACID transaction is possible
										2. If 10 records live on different nodes, we cannot do ACID transactions
											1. Same problem as with vertical partitioning
										3. Even within domain we cannot do ACID transactions
								5. This kind of partitioning is not popular with RDBMS
									1. The transaction logic needs to be in the application
									2. We have to deal with eventual consistency
									3. Recently even RDBMS are providing auto-sharding or auto-partitioning
										1. Read the docs
								6. This kind of partitioning is popular with NoSQL databases
									1. It is taken care of internally
							2. Hash partitioning:
								1. Logic:
									1. Hash(id) % N = 1
									2. Hash(id) % N = 2
									3. ...
								2. In practice - %N is not applied - consistent hashing technique is used (a variation as well is used)
									1. Sophistication
										1. If any node goes down or we add new nodes, to rebalance data, there is minimum amount of disruption in terms of moving data
										2. Updates and inserts become scalable
								3. Downside:
									1. We lose ACID transactions
									2. Overall complexity increases
										1. More hardware
										2. More complexity to architecture (and implementation)
2. Use case: Go for DB partitioning if vertical partitioning is not sufficient for scaling out

### Database Partitioning Selection ###
1. Range Partitioning

		SELECT * FROM Order WHERE id = 150
		SELECT * FROM Order WHERE id > 150 AND id < 250
		
	1. Node 2 has data between 101..200 and Node 2 has data between 201..300
		1. We need to visit both nodes for the range
	2. Use case: If we are searching data on a range, we can split the data based on range
	3. Use case: If we are searching data based on single id

2. Hash Partitioning

		SELECT * FROM Order WHERE id = 150
		
	1. We cannot do range queries (150 and 250)
		1. We have to run 100 queries for each id (they can be bached if db supports but they are separate queries)
		2. The queries may go on different nodes
			1. There is chance that each query may run on a different node (100 nodes are hit)
				1. Hash partitioning ensures that the keys are distributed evenly
		3. Range partitioning is costly with hash paritioning scheme
		4. **It is good for CRUD on records based on key**
3. Range partitioning is a superset of Hash partitioning
4. Advantages of Hash partitoining:
	1. Performance is higher for id based query as compared to range partitioning
		1. Indexes are tree based entries	 for range based partitioning
			1. Index tree may be on multiple nodes (distributed db and indexes may be kept on multiple nodes)
			2. If we want to look for a range, we have to go through the tree structure (many machines may need to be visited)
				1. Latency may get increased
		2. Hash partitioning directly identifies the node
			1. We don't have to go through any index tree on multiple nodes
			2. Client can calculate the node and server is not required
3. NoSQL DBs have their own query language
	1. RDBMSs are simple to understand and universal

### Routing with Database Partitioning ###
1. CRUD requests
	1. Considered horizontally partitioned Order table
		1. How to get data? (of id = 256)
			1. Three ways:
				1. Client library - (CouchDB, Memcache)
					1. They are cluster aware (they know how many nodes are in the cluster)
						1. When we run query
							1. The library applied hashing algorithm to determine the node and fetch the data
				2. Router Component - (MongoDB)
					1. Hosted as a server application
					2. Any client can send the request to the router
					3. The router determines node where the request can get served (hash partitioning or range partitioning)
					4. The router is cluster aware + aware of the partitioning scheme
				3. Contact any node - (DynamoDB, CassandraDB)
					1. The contacted node takes the responsibility of forwarding the request to the right node

### Methods for Horizontal Scalability ###
1. Horizontal Scaling Methods
	1. Services (breaking monolith into services)
	2. Replication (more workers)
		1. Stateful (Db are stateful always)
		2. Stateless (web apps, services, ... - more scalable)
	3. Partitioning
		1. Vertical/ Functionality Partitioning (microservices)
		2. Database Partitioning (horizontal partitioning)
	4. Asynchronous Calls (write load - peak loads can be handled better)
	5. Caching (reduces latency, reduces load and hence increases scalability)

### Dealing with Large Scale Systems ###
1. Large Scale Systems
	1. We need other services
		1. Load balancing
		2. DNS
		3. Auto-scaling

### Load Balancing Multiple Instances ###
1. Load Balancing provides
	1. Single IP address for a component
		1. Any component can have multiple instances
			1. Web app
			2. Gateway
			3. Catalog service
		2. Suppose gateway wants to call catalog service
			1. Which instance to call?
			2. How many instances exist?
			3. The number of instances can change
			4. IP addresses can change
			5. Load on the instances can change
			6. Hence, it is even hard to maintain a list of IP addresses
				1. Solution: Load balancer
					1. It takes the responsibility of routing the request to the right instance (based on load, or whatever strategy)
					2. It takes the job of distribution of requests
					3. Client can use only one IP address (of the load balancer)
2. Outermost load balancer
	1. It has public IP
		1. There are software based and hardware based load balancers
	2. This will see the highest amount of load (next one also)
	3. Rest of the load balancers are there to provide single IP address to the different components
		1. If microservices has multiple services and each service has a lot of instances
			1. Each service has load balancer (Kubernetes say)
				1. There is alternative to load balancer

### Discovery Service and Load Balancing ###
1. The load balancers can be removed for each service and put in gateway service
	1. If there are lots of services, it becomes messy to have load balancer for each of the services (Kubernetes infrastructure makes it easy to maintain)
2. Alternative
	1. Discovery Service
		1. Use case: If there are lots of services, it becomes hard to track what services are available and what instances of the services are running and what of them are healthy
			1. Solution: Discovery service
				1. Order service instances (say) registers with discovery service (when they come up)
				2. Discovery service will know what services and what instances are still serving
				3. Each service frequently updates its existance to discovery service using a heartbeat (health)
				4. Steps:
					1. Gateway service queries the discovery service for instances of Order service (say)
					2. Discovery service will provide list of healthy instances of Order service
					3. Gateway service load balancer uses a strategy to choose the instance it wants to call
					4. Gateway makes a call to the order service  
	2. Load balancer that is embedded into gateway service code
		1. If gateway service wants to make a call to backend service, it makes a call to embedded load balancer (library)
3. Suppose Order service wants to call Catelog service
	1. It can embed load balancer along with discovery service
4. Discovery Service can also be used by traditional load balancers
	1. The latest status of the services can be obtained
	2. Large scale systems typically have discovery service
		1. Otherwise it becomes difficult to manage each service through configure 
	3. Needed if Kubernetes cluster management system is not used

### Load Balancer Discovery ###
1. External Clients - Use DNS to discover the external load balancer
	1. DNS name will be resolved to external IP address
2. Internal Clients - Use a local registery/ config to discover an internal load balancer

		Client -> External LB		    Services -> Internal LB  
			|		Name: www.abc.com
			v		Ext IP: 158.26.78.80
			DNS		IP: 198.168.1.1
			
	1. Internal LB
		1. IP address is used
			1. Available to clients through configuration or
			2. Available in registry (discovery service)

### HLB vs SLB ###
1. Two kinds
	1. Hardware based load balancer
		1. Load distribution for L4 & L7
			1. 2x 14-Core Intel Xeon processors
			2. 1.6 TB of available use storage space
			3. 512 GB DDR4 RAM
			4. 4x 100G and 8x 40G fiber ports
		2. F5 Big IP i5000 series
			1. Connections: 300 million
			2. Throughput: 320/160 Gbps
			3. RPS (L7): 10 million (requests per second - only at L7)
	2. Software based load balancer
		1. Load distribution L7 (only) - application layer
		2. Features
			1. Content based routing
			2. Supports SSL termination
			3. Supports sticky sessions
		3. NGINX
			1. Connections: 225 K (sufficient for many use cases)
			2. Throughput: 70 Gbps
			3. RPS: 3 million
2. TCP/IP Model
	1. Application layer (HTTP, HTTPS, SMTP, IMAP, FTP, DNS, NNTP...)
	2. Transport (UDP, TCP, SCTP)
	3. Internet
	4. Network Access (Link)
3. OSI Model
	1. Application (Layer 7 load balancing upto session layer)
	2. Presentation
	3. Session
	4. Transport (Layer 4 Load balancing)
	5. Network
	6. Data Link
	7. Physical
4. HW LBs
	1. Can take immense amount of load
	2. Can do load balancing for L4 (Transport) and L7
	3. They are better than software based
5. Why use software based load balancers?
	1. HW based load balancers are extremely expensive
	2. SW based load balancers are free
		1. There is some cost for maintenance which is less
		2. Options
			1. Apache
			2. NGINX
			3. HAPROXY
	3. One can upgrade to HW based LB if needed

### Layer-7 Load Balancer ###
1. L7 - app level protocols are used
	1. SSL Termination
		1. HTTPS is used upto Load balancer but LB to Internal servers can be HTTP
	2. Reverse proxy (They act as reverse proxy)
		1. Breaks TCP connection
			1. Client instantiates a TCP connection to load balancer
			2. Load balancer instantiates another TCP connection to the Web-server
	3. Content based routing
		1. It can look into HTTP request (URL, Cookies, Headers, Body, ... - since it is L7)
			1. Example: https://images.hotel.com/room/standard (static content)
				1. Routed to static content servers
			2. Example: https://www.hotel.com/reserve (dynamic content)
				1. Routed to dynamic content servers
	4. Load balancing (strategies that can be used)
		1. Round Robin
		2. Least Connection
		3. Weighted RR/Least Conn
		4. Least Response Time
			1. Least Latency
				1. Considering geographic locations say
2. Dynamic content: http://www.hotel.com
3. Static content: http://images.hotel.com
4. L7 vs L4 LB
	1. L4 LB can do direct routing of requests (acts as router in between)
	2. L7 acts as proxy

### DNS as Load Balancer ###
1. Configure DNS records with multiple A records (Address records - they specify what IP addresses are serving the domain name, multiple A records (multiple IP addresses)) - the following strategies give some kind of load balancing
	1. Return single IP in a round-robin fashion
		1. Load is distributed across instances (good for browser)
	2. Return a list of IPs
		1. Load balancing can be done on client side (not for browser)
			1. Thick client can do load balancing using IPs
2. Cloud based DNS can be configured along with health checks
	1. DNS can ping a backend instance and know it's health
		1. If it is not responding, then it's IP will not be returned
			1. Client is saved from sending request to a non-live server
		2. Cloud DNSs provide this feature (Amazon, Google, ...)
3. DNS can still not be used as LB
	1. LB actively tracks instances which are down and stops traffic to those instances
		1. DNS needs lead time to make the switch
			1. DNS due to scalability reasons relies on caching
				1. In intermediate DNSs (may be stale for load balancing)
					1. Workaround: Setting TTL values
						1. Time To Live
							1. The response is valid for 1 hour/1 minute, ...
							2. We want low TTL values (0 => not caching => overloading of DNSs)
								1. DNS may need high TTL and may not be practical for LB
3. Drawbacks
	1. Indefinite caching and not respecting TTLs
	2. Low or zero TTLs can result in very high load on DNS

### Global Server Load Balancer ###
1. Scalability
	1. Routing for multi-geographic systems
		1. All users do not have to connect to a single region
			1. System can be hosted in multiple regions
				1. Scaled up
2. Performance
	1. Locality for multi-geographic users (users in NA can connect to data center in NA if available - improves performance)
		1. Client to Datacenter Latency (DNS can consider this for LB)
		2. Client to Datacenter Proximity (DNS can do LB based on this)
		3. Datacenter Geography (DNS can do LB based on this - different country or state say)
3. High Availability
	1. Multi region availability
		1. Suppose NA is down or overloaded (unavailable)
			1. DNS can detect it (in some time) and divert traffic to APAC region
				1. This is not too quick
					1. If this is done too quickly, **data will be messed up**
						1. It might corrupt data (if syncing is enabled between regions (?))
4. Disaster Recovery
	1. If region goes down, the users will be diverted to different region
		1. It is not quick
			1. It may take time to prepare system in different region
				1. The following activities may have to be performed
					1. Start applications
					2. Refresh data
5. Illustration:

					DNS            DNS
		Client --------> DNS <--------- Client
          |     Query    |     Query     |
          |              |               |
          |            Health            |
          +------------------------------+        
          |            Checks            |
          v		NA  	  |   APAC        v
          LB				  |               LB
          |				  |					 |
          v				  |					 v
		Servers			  |            Servers
		   |				  |					 |
		   v				  |					 v

	1. LB has IP addresses of the server instances
		1. Certain instances can go down (everyday say)
		2. The list of IP addresses have to be updated in the LB at a very high rate
			1. Or else
				1. Requests may get served to dead instances (high failure rate)
		3. Switch to new data is quick (it is local list)
		4. Since each LB serves only one region, and since redundancy in built into each region, it is not easy for entire region to go down
		5. Number of regions is also not that high
	2. DNS
		1. At this level, situation of something (regions say) going down is not that dynamic (fairly static)
		2. It can be used as a load balancer (globally)
			1. Data is not stale frequently
		3. If a region goes down
			1. DNS can detect that (though not frequent)
				1. LB takes time
				2. This is a very rare event
6. Suppose a user is in NA region
	1. To resolve DNS
		1. Browser will query DNS
		2. DNS can look at geographic region of the user and returns IP address accordingly
	2. DNS is not a typical load balancer in this case
		1. NA user is not directed to different regions unles NA region is overloaded (and DNS knows that) or it has gone down completely
	3. DNS as a load balancer is providing routing in this case
7. Challenge:
	1. How to keep two regions in sync? (fall-back region)

### Global Data Replication ###
1. Active-Active Setup
	1. All sites active
2. Master-Master or Peer-to-Peer replication
	1. Mostly asynchronous
3. Failover is quick
4. Some data loss is a possibility
5. Illustration:

		  Client ---------------- DNS ------------------- Client
		     |                     |                       |
		     +---------------------+-----------------------+
		     |									                  |
		     v									                  v
		     LB								                  LB
		     |									                  |
		     v									                  v
		  Web App								               Web App
		     |									                  |
		     v									                  v
		  Service								               Service
		     |									                  |
		     v									                  v
		  Master -> Replica <---------------> Replica <- Master
		     ^                                             ^
		     |                                             |
		     +---------------------------------------------+
		     
	1. Goal: Data between the two regions is in sync
		1. User will be able to access data from any data center
			1. Both data centres need to be active all the time (active-active setup) - all sites are active all the time
				1. master-master or peer-to-peer replication (to keep data in sync between data centres)
					1. Replicas
						1. Read replicas (asynchronous replication) OR
						2. Backups (synchronous replication)
					2. Used for global data replication (different geographies)
						1. To independently read and write between two geographies
							1. Can result in write conflicts
								1. Resolution:
									1. Automatic or manual
										1. Use cases:
											1. Same user will not write data to two locations at the same time (Taxi booking say)
												1. No conflict in this case
												2. If I go to the other data center, I will be writing to the other data center
													1. It will get propagated to the other data center
				3. In cases there are write conflicts, we need a system to resolve it
				4. If a region goes down, we must not switch quickly to the other region
					1. We need to absolutely ensure that it is down
						1. If we switch in quick succession, we might get write conflicts
			2. Failover is quick
				1. DNS routing works well in this case
				2. DNS if updated, it takes a few minutes to switch over
			3. Some data loss is a possibility
				1. Asynchronous replication
					1. Between two master servers
						1. There can be a data loss
					2. Synchronous replication?
						1. Not practically feasible between two geographies
							1. Latency is high (takes long time to sync up)
								1. Write performance of database will go down
							2. Connectivity might get broken
								1. We cannot complete our transaction (we need both masters for synchronization)
					3. Master-master replication is generally asynchronous
					4. Suppose a data center goes down, apac region may not get the data written in north america region
						1. User should be communicated appropriately
						2. There should be processes to handle this data loss
6. Master-master replication can be used to write data to two geographies simultaneously

### Auto Scaling Instances ###
1. Monitoring Service
	1. Monitor Load
		1. CPU
		2. Network
		3. Disk
	2. Monitor Health
		1. Ping
		2. Http
2. Auto-Saling Service
	1. Configure load threasholds
	2. Monitor load
	3. Launch New Instance
	4. Shutdown Instance
3. Description:
	1. Autoscaling application when application is under load
		1. Homegrown system
		2. Cloud
			1. Autoscaling frameworks
		3. If load is increasing, then manual process is not practically feasible (say within 5 minutes)
			1. Human error factors go away
	2. Components:
		1. Monitoring & Health Check
			1. Requests coming to instances through load balancer
			2. The monitoring & health check system monitors CPU load, network load, disk usage, ...
			3. Health check system determines how much load the system is subjected to
				1. This information is constantly related to autoscaler
		2. AutoScaler if informed that system is under load, it launches new instances
			1. Pulls out VM/Container image
			2. Registers the new instance with LB
				1. The traffic coming to LB will now get distributed to the new instance as well
			3. If load goes down and if Monitoring & Health Check system detects it, the AutoScaler deregisters one or more instances and then brings down one or more instances
		3. If as system admin, we configure that we do not want more than 70% to 80% load on an instance, we need to start new instances if that happens
		4. We don't want delay so we don't want creation of new instances but we want images loaded with requisite software and pull it (very min configuration)
			1. The only runtime configuration
				1. New IP address
					1. AutoScaler will register the new instance using the IP address (say)

### Micro-Services Architecture ###
1. Why we need to do or should not use microservices for large scale system

### Micro-Services Motivation ###
1. Micro-services architecture
	1. Sometimes, we take a middle path between SOA and microservices architecture
		1. We must be clear what microservices architecture is & what SOA is
2. Architecture
	1. How it impacts end users
		1. Performance
		2. Scalability
		3. Cost
		4. ...
	2. Benefits
		1. For team (developing or deploying)
			1. These are secondary
3. Primary impacts
	1. Motivations
		1. Very High scalability (decentralization and independence)
			1. How microservices provides this?
		2. Frequent Deployment
			1. Incremental features can be delivered to customer at a higher frequency
				1. Positive impact on the business
		3. Internal benefits
			1. 

### Service Oriented Architecture ###
### Micro-Services Architecture Style ###
### Transactions in Micro-Services ###
### Compensating Tansactions - SAGA Pattern ###
### Micro-Services Communication Model ###
1. Synchronous processing
	1. Immediate Response (better user experience)
		1. If possible
	2. For read/query loads
		1. Small amount of data from DB
		2. Small amount of processing
	3. Drawbacks
		1. Un-reliable
			1. If an instance handling a request goes down, then the client needs to re-try (user might retry)
				1. If there is high load and requests are failing due to load, retrying is not a great strategy
					1. Solution: Asynchronous processing (defers the processing)
2. Asynchronous processing
	1. Deferred response
	2. For write/transaction loads (to scale better)
		1. If it takes time
		2. If it does not require immediate response to user
	3. Higher scalability
	4. Higher reliability

### Event Driven Transactions ###
### Extreme Scalability with NoSQL and Kafka ###

## Reliability ##
### Module Contents Overview ###
### Distributed Systems and System Failures ###
### Partial System Failures ###
### Reliability Engineering Topics ###
### Reliability ###
### Availability ###
### High Availability ###
### Fault Tolerance ###
### Designing Fault Tolerance ###
### Fault Tolerant Design ###
### Redundancy ###
### Types of Redundancy ###
### Single Point of Failure ###
### Stateless Component Redundancy ###
### Stateful Component Redundancy ###
### Load Balancer Redundancy ###
### Datacentre Infrastructure as SPOF ###
### Fault Detection ###
### Fault Models ###
### Health Checks ###
### External Monitoring Service ###
### Internal Cluster Monitoring ###
### Fault Detection in a System ###
### Recovering from Failures ###
### Stateless Component Recovery ###
### Load Balancer High Availability ###
### Database Recovery with Hot Standby ###
### Database Recovery with Warm Standby ###
### Database Recovery with Cold Backups ###
### High Availability in Large Scale Systems ###
### Failover Best Practices ###
### System Stability ###
### Timeouts ###
### Retries ###
### Circuit Breaker ###
### Fail Fast and Shed Load ###

## Security ##
### Module Contents Overview ###
### Security Objectives ###
### Network Security ###
### Symmetric Key Encryption ###
### Public Key Encryption ###
### Secure Network Protocol ###
### SSL and TLS ###
### Hashing ###
### Digital Signatures ###
### Digital Certificates ###
### Chain of Trust ###
### TLS/SSL Handshake ###
### Secure Network Channel ###
### Firewalls ###
### Network Security ###
### Identity Management ###
### Authentication and Authorization ###
### Authentication ###
### Credentials Transfer ###
### Stateful Authentication ###
### Stateless Authentication ###
### Single Sign-On Within a Network Domain ###
### Token Storage ###
### Authentication ###
### Access Management ###
### Role Based Access ###
### Role Based Access Example ###
### Authorization ###
### OAuth2 Token Grant ###
### OAuth2 Token Grant - Code Flow ###
### OAuth2 Token Grant - Password Flow ###
### JSON Web Tokens ###
### Common Vulnerabilities ###
### SQL Injection ###
### Cross Site Scripting ###
### Cross Site Resource Forgery ###

## Deployment ##
### Module Contents Overview ###
### Large Scale Deployments ###
### Application Deployment ###
### Infrastructure Deployment ###
### System Operations ###
### Modern Deployment Solutions ###
### Application Deployment ###
### Component Deployment ###
### Component Deployment Parts ###
### Provisioning and Configuration ###
### Virtual Machine Deployment ###
### Isolation Through Virtual Machines ###
### Docker Containers ###
### Infrastructure Deployment ###
### Deployment with Docker Containers ###
### Deployment with Containers on Cloud ###
### Deployment with Kubernetes ###
### Kubernetes Lifecycle Management ###
### Kubernetes Naming and Addressing ###
### Kubernetes Scaling with Multiple Instances ###
### Kubernetes Load Balancing ###
### Kubernetes High Availability ###
### Kubernetes Rolling Upgrades ###
### Kubernetes Capabilities ###
### Kubernetes Deployment ###
### Kubernetes Services and Workloads ###
### Kubernetes Architecture ###
### System Upgrades ###
### Rolling Updates ###
### Canary Deployment ###
### Recreate Deployment ###
### Blue Green Deployment ###
### A/B Testing ###

## Technology Stack ##
### Module Contents Overview ###
1. Architecting Solutions with Platforms & Frameworks
	1. Platforms for:
		1. Web Apps
		2. Services
		3. Datastores
		4. Analytics
	2. Platform Functionality
		1. We will pick up a platform product
			1. We will look at its functionality
				1. Example: Database
					1. What kind of schema it supports
					2. What kind of read and write load it can handle
				2. Example: Web-server
					1. Whether the web-server can support caching
					2. Whether the web-server can act as a good reverse proxy
			2. Before selecting any product, we want to make sure that this product serves us all the functionality that we are looking for
	3. Platform Architecture (non-functional requirements)
		1. Performance (how does the product perform)
		2. Scalability (how does the product scale)
		3. Reliability (what reliability guarantees does the platform product provide)
	4. Platform Use-Cases (for what use-cases, the product is built for)
	5. Platform Alternatives (compare the product with other products that are available)
		1. Comparison (which product fits the best for our application)
	6. Architecting Solution
		1. End-to-End
2. For each of layers, we need to select certain products
	1. Database:
		1. RDBMS: Oracle, SQL Server
		2. NoSQL
			1. On what basis do we make the selection
	2. Frontend:
		1. On what basis do we choose a reverse proxy
		2. On what basis do we choose a web-server
3. How do we make those decisions?
	1. On what basis do we select a particular platform and construct a solution out of that
	2. For each of the layers, we pick a product (platform product)

### Reference System for Using Tech Platforms ###
1. Reference System
	1. Web layer
	2. Service layer
	3. Database layer
	4. Analytics layer
2. We will try to build the system using various platforms and technologies available
	1. When we have to choose a platform product, we are interested in two things:
		1. Functionality
			1. Is it providing the necessary functionality or not
		2. Non-functional aspect
			1. Is it going to scale
			2. Is it resilient
			3. Is it reliable
			4. Is it secure
			5. Is it going to perform

### Web Applications ###
1. Front-end
	1. We are concerned about the server side of the system
		1. Not user interfaces (not even scripting)
	2. Web-applications:
		1. Web-applications receive the highest amount of load that a system receives
			1. As we go down the system, the load decreases progressively
				1. The load on the databases is the least
					1. Challenging:
						1. It is hard to scale out databases
						2. We are managing state
		2. We do not manage state on the frontend side
			1. It reduces some load on the web application
		3. **Every request hits our web-application**
			1. A request may or may not go to the backend
			2. **Hence, load the a web-application is the primary challenge that any web-application needs to deal with**
		4. **They are connected with clients that are located at long distances**
			1. Clients of any other layer of the system are local clients
		5. **Communication needs to be secure**
		6. When we try to select a product for our web-application, we look for the above things
			1. How efficiently can it serve the content
			2. How much load can it efficiently handle

### Solutions for Web Applications ###
1. Solutions:
	1. Static Content (how to manage)
		1. Apache Web Server
		2. Nginx Web Server
		3. Cloud Storage (static data)
	2. Dynamic Content
		1. Web Server - Apache HTTPD, NodeJS (static content)
		2. Java Web Containers - Tomcat, Jetty (comparing with NodeJS), Spring-Boot (Java)
			1. Tomcat vs Jetty - small comparison
			2. Jetty vs NodeJS - Totally different ways of handling web-content
	3. Content Caching
		1. Nginx
			1. Varnish cache is another option
	4. Content Distribution
		1. CDN
			1. When we have large distances to cover
				1. If we have a large site in Asia but we have customers in America as well
			2. If website has a lot of static content

### Apache Web Server ###
1. Store Static Content (important function)
	1. HTML/CSS/JS Files
	2. Image files
	3. Documents
2. Generate Dynamic Content (important function)
	1. Get data & generate pages dynamically
	2. PHP, Python, Perl
	3. No JSP/Servlets
3. Act as a Reverse Proxy (important function)
	1. Not great
	
#### Store Static Content ####
1. Static content is stored on Apache server's hard disk
	1. If content is delivered from hard-disk, the delivery is quite slow
		1. Example: if a jpeg image needs to be delivered, Apache needs to fetch the image from the hard-disk and deliver to the client - This can be slow because Apache needs to do an IO from the disk
			1. Solution:
				1. When Apache is fetching the jpeg file for the first time, it stores the file in the memory of the Apache server
				2. Next time if a request comes for the same image, it will be delivered from RAM
				3. **It is important for Apache Server to have a large RAM**
					1. 32 GB, 64 GB, ...
						1. May or may not be sufficient
							1. Depends on the amount of static content
								1. Say 200 GB
									1. RAM of 32 GB is insufficient
					2. If it is a static content intensive web-site, there will be a huge static content sitting on the disk and not everything can be cached on the RAM
						1. Anything at comes from the RAM is slow but anything that comes from the hard disk will be faster

#### Generate Dynamic Content ####
1. It does it pretty well and is known for this feature
	1. We can write scripts in PHP, Python, or Perl, ...
		1. Using the scripts, Apache will fetch data from a service/ database & dynamically generates HTML page (whenever a request is received for generating a page)
	2. For generating dynamic HTML pages, the resources used by Apache:
		1. RAM - Where all the operations are performed
		2. CPU
			1. These two are overloaded
	3. It doesn't have Servlet container
		1. No JSP/Servlets
		
#### Act as a Reverse Proxy ####
1. It is not well known for
	1. We can still use it
		1. If it is not a heavily overloaded website
2. It is not a great reverse proxy as compared to others
	1. Other reverse proxies are designed to be great reverse proxies
3. It can sit in front of our web-application
	1. Suppose web-application has several instances (10-15 instances)
		1. Apache Web Server can sit in front of the web-app
		2. Clients can call Apache Web Server
			1. Apache Web Server will be a single point of contact (they just have to know the IP address of the Apache Web Server)
			2. Apache Web Server will proxy all the requests to the backend web application
				1. It acts as a reverse proxy
				2. It can do some load balancing

### Apache WebServer Architecture ###
1. The architecture is based on request/response model
	1. It is similar to the architecture of any the following which serves HTTP requests
		1. Web server
		2. App server
		3. Web container
	2. Examples: Apache Tomcat, Wildfly, JBoss, Jetty, ... 
		1. The servers are based on request/response model and they listen to HTTP requests
		2. They work pretty much the same way
			1. Apache Webserver represents them
2. Architecture
	1. Assume there are a lot of clients connecting using HTTP protocol to a web-server
		1. Each client will have a connection
			1. It can be a persistent connection if client is trying to re-connect again using the same connection
				1. Reason: It saves some latency
			2. Apache provides this feature
			3. Each connection occupies some memory (not much)
			4. Each connection will be **allocated a thread from a worker thread pool**
				1. The thread will dedicatedly work for that connection for a given client request
				2. The thread serving a client request may access the following depending on the kind of request:
					1. cpu
					2. memory
					3. network
				3. If the client has asked for a static resource, the thread will do a disk access, it will fetch a static resource file (css file, jpeg file, ...) and it will return the information back to client
					1. During the operation, the thread may write some log statements on a log file (this needs disk access as well)
				4. The thread might serve the request purely out of memory if the resource is cached in memory
			5. Request for a dynamic web-page
				1. When client requests for a dynamic web-page, a connection is established
				2. The connection will be allocated a thread
				3. The thread will spend time in CPU (because it does processing to generate a page)
					1. During this process, it needs to access network to fetch data
						1. It can be from database
						2. It can be from a service (which is available on a network)
					2. Once data is fetched, it will be processed using CPU and memory
				4. Once the processing is done, the page is generated
				5. The page is then returned to the client
				6. A thread at any given time is doing one of the following things:
					1. Processing - consuming CPU and Memory
					2. IO - accessing network, disk, and/or memory
				7. If we are using Apache server for generating dynamic content and we increase the load on Apache server (increase the number of clients, increase the load such that the server gets overloaded),
					1. Server will run out of:
						1. CPU first - for more CPU intensive requests
						2. Memory first - for more Memory intensive requests

### Apache WebServer Scalability ###
1. It depends on how it is used:
	1. Apache as Webserver (CPU Bound)
		1. Apache is fronted by a load balancer (load balancer acts as a reverse proxy, it can be any other tool, discussed later)
	2. Apache as Reverse Proxy (IO Bound)
		1. Apache is fronted by a Apache Webserver load balancer
			1. Apache is sending or proxying requests to any other web server
2. Apache as a Webserver:
	1. Apache Web server can be used to serve static content or dynamic content or a mix of both
	2. When we scale the requests to Apache web server, Apache web server may run out of CPU or Memory depending upon the nature of requests
		1. If the requests require a lot of CPU, Apache web server may run out of CPU first
		2. If the requests require a lot of Memory (because we are doing a lot of processing, caching or static content), Apache may run out of Memory first
		3. Solution:
			1. We can add more nodes of Apache webserver
				1. As we add more nodes, we will get more CPU and more Memory, and we can scale Apache webserver (if we are using Apache webserver for dynamic content or static content)
3. Apache as Reverse Proxy:
	1. Apache doesn't have to do much processing
		1. The processing per client is very limited
			1. It can choose a backend web-server and send the request to that (any of them)
	2. The thread is blocked until the response is returned by the backend web-server
	3. Once the response is received, Apache reverse proxy returns the response to the client
	4. The load is mostly on the memory (no much CPU load)
		1. If there are lots of connections tha Apache is handling, it will have to increase its thread pool (one thread per connection)
			1. If we increase the thread pool size, that will require more memory
				1. **The only way to scale Apache Web Server as a Reverse proxy is to scale it vertically**
					1. Scaling memory in one single server is pretty costly
						1. Having very large memory is not sometimes possible and may not be cost effective as well
							1. Solution: Other solutions when we are dealing with large number of connections which can optimally utilize memory
4. If we have a requirement just for a web server and we have to generate dynamic web-pages, Apache web-server is a fantastic option
	1. It is a lightweight webserver where we can make use of Perl, PHP, Python, etc. to generate dynamic web pages
		1. Even today it is used widely used to generate dyanmic web pages in PHP

### Nginx WebServer ###
1. Topics:
	1. Store Static Content (function 1)
		1. HTML/CSS/JS Files
		2. Image files
		3. Documents
	2. Generate Dynamic Content (function 2)
		1. Not the best
	3. Act as a Reverse Proxy (function 3)
		1. Excellent
	4. Cache Content (function 4)
		1. Good
2. Its functionality is same as Apache webserver
	
#### Store Static Content ####
#### Generate Dynamic Content ####
1. Apache has got a marginal edge over Nginx in terms of performance

#### Act as a Reverse Proxy ####
1. Nginx webserver was designed to be an excellent reverse proxy

#### Cache Content ####

### Nginx Architecture ###
1. Architecture:
	1. It is event-driven
		1. Uses asynchronous IO model
	2. Client can connect to Nginx using HTTP protocol (web-server)
		1. Upto the point that client forms a connection with Nginx, it works the same as Apache
			1. Difference: How the requests for each connection is fulfilled
				1. Apache: For each request that comes, Apache server allocates a thread from thread pool
				2. Nginx: There is no thread-pool
					1. There is only one single main thread (other activities have threads)
						1. The thread that processes requests is a single thread
	3. The single thread never leaves CPU on its own
		1. If a thread does not leave CPU, it can do a lot more processing efficiently, because there wont be any context switching
			1. Gives thread ample chance to do processing, **without waiting for CPU**
	4. Steps:
		1. When a connection request comes, the main thread will check if any request has come
			1. It continously polls to check if there are any TCP connections and checks for any activity
		2. The single thread reads the stream and gets the request
		3. The single thread processes the request
		4. If the single thread has nothing else to process, it will write back to the connection and response is sent to client
		5. Sometimes, we need data from a database, or a service, or sometimes we need to get a static resource file from hard-disk
			1. The thread will issue an asynchronous IO request and it will not wait for a response from IO
				1. The thread will continue to execute after issuing the request
		6. The thread will then continue to check if there is any other request
			1. If there is no other request, the thread will continue to execute
		7. The thread will then check if IO has any response
			1. If there is no response, it will again go and check if there is any activity on the connection side
				1. If there is, it will execute that
		8. The thread will then check if there is any database or service call, or disk access
			1. The thread will make an async request if there is, and then it will continue its execution
		9. During the execution, it will check if there is any new connection request
			1. If there is none, it will check if there is any IO response we got back
				1. If we have got a response from DB or service, it will process it and finds to which request it belongs to and write to the same connection
		10. The thread will continue to execute
		11. If the thread sees any response, it will take the response and write the response on appropriate connection
		12. etc.
		13. Thread never leaves the CPU, unless OS forces it to leave the CPU
			1. On its own, it will never leave the CPU
	5. Process loop:
		1. Poll for client request (continously poll)
		2. Poll for client response (continously poll)
		3. Process client request (if it is got from a connection)
		3. Process IO response (if it has come back from the OS)
		4. For processed client request Send IO Request (if required)
		5. For processed IO response send response to client (from Async IO)
	6. The Single Thread works very fast
		1. In cases, where there are a lot of IO as compared to processing
			1. If only processing needs to be done, the model doesn't work fine
			2. The model works well if there are many Asynchronous IO requests that needs to be made
				1. Hence a single thread is good enough to handle the processing load (for IO bound requests which do not have much processing)
		2. A single thread is good enough to handle a lot of connections
	7. Only one thread has thread context
		1. The memory that is consumed is only the one consumed by the single thread
			1. If there are 1 M connections, it wont construct 1 M thread contexts
			2. Only one thread context that corresponds to single worker thread
				1. **Hence, Nginx scales immensely, when it works as a reverse proxy**
					1. A reverse proxy doesn't do much processing
						1. The only processing is:
							1. It receives a request from a client
							2. The request is sent to some other service
							3. Whenever the service response comes back, the response is returned to the client
						2. There is a lot of IO but not much processing
							1. **Nginx is perfectly suitable for this kind of workload**
							2. **Nginx is also suitable for static data files also**
								1. We can read the file data asynchronously
									1. It is marginally better
										1. Reason: We cannot do too much of parallel processing on disk
								2. Any improvement that comes from static data comes from using cache memory
									1. We will store most of the data files we have accessed in cache memory (RAM) of Nginx
										1. Same as Apache
	8. Nginx is perfect for handling a lot of IO based requests, hence it is a good reverse proxy

### Nginx as Reverse Proxy and Cache ###
1. How to use Nginx as a reverse proxy and cache
	1. Web application (assuming it is written in PHP or Python, or Perl, ...) (Apache is a good candidate for web application)
		1. Apache is perfect to host a PHP web application
	2. We have placed Nginx in front of Apache
		1. If browser is looking for a static resource (Jpeg say):
			1. If the file is not in memory, it will be a cache miss
				1. The file will be fetched from the disk and response will be returned
			2. If the file is in memory, it will be a cache hit
				1. The file will be fetched from memory, and response will be returned
					1. This way, Nginx acts as a cache
						1. As there will be more requests, more and more static data files will be cached in Nginx memory
							1. Typically we use a large memory with Nginx
								1. When we want Nginx to act as a cache
									1. Static data files will build up in the memory
										1. Nginx will start serving them from its cache whenever there is a cache hit
		2. Nginx as reverse proxy
			1. It is proxying requests to backend Apache servers
				1. While it is acting as a reverse proxy, it can do a load balancing across instances
					1. The capability is built into Nginx
			2. Nginx can front any services as a reverse proxy
				1. If we have a RESTful service, Nginx can act as a reverse proxy load balancer
			3. If HTTP responses are coming from services, it can cache the responses too
				1. It can act as reverse proxy and cache as well
2. If there is a requirement in the architecture where we want a reverse proxy and we have to cache HTTP responses (In front of RESTful service, and web-application)

### Web Containers & Spring Framework ###
1. Topics:
	1. Dynamic content using Java
		1. OO Language for complex logic
	2. Web Containers
		1. Tomcat (Servlet Engine)
		2. Jetty (Servlet Engine)
	3. Application Servers
		1. Features:
			1. Servlet Engine
			2. EJB Container
			3. Session Clustering
			4. Connection Pools
			5. Caching
			6. JMX
			7. JMS
			8. OSGI
			9. ...
		2. Examples:
			1. Wildfly/JBoss
			2. Weblogic
			3. Websphere
	4. MVC Architecture
		1. Servlets for logic
		2. JSP for presentation
	5. Spring Containers
		1. Runs inside a Web container
		2. Provides
			1. IOC/DI
				1. For business logic
			2. Model View Controller
				1. For frontends
			3. JDBC Templates
				1. For accessing DB
			4. Connection Pools
				1. Http, DB

#### Dynamic content using Java ####
1. Serving dynamic web-content that has a little more complex business logic
	1. Which we do not want to express in scripting language (PHP, Python, Perl, ...) that can be easily hosted on Apache webserver or Nginx webserver
		1. We can go for web containers where we can write complex business logic using Java langauge (OOL) - suitable for more complex business logic

#### Web Containers ####
1. The web containers provide servlet engines
	1. We can write our business logic as servlets & presentation can be expressed as JSP
2. Two open source web containers (provide servlet containers, most popular)
	1. Tomcat
	2. Jetty

#### Application Servers ####
1. Application servers provide
	1. Servlet Engines
	2. EJB Containers
	3. Session Clustering
	4. Connection Pooling
	5. Caching
	6. JMX
	7. JMS
	8. OSGI
	9. ...
2. They usually come at a huge license cost
	1. Wildfly/JBoss - open source
	2. Weblogic - huge cost
	3. Websphere - huge cost
3. It is not worth paying the cost because same functionality can be achieved through web containers in combination with Spring framework (open source)

#### Spring Boot ####
1. If we are using Spring framework (any web application these days are using), then another way of running web container is:
	1. Spring Boot (runs Java application)
		1. Runs embedded web container 
			1. Runs:
				1. Tomcat
				2. Jetty (choice)
2. If we want to run our RESTful service, we can use web containers along with Spring framework
	1. If we are writing a web application, it is a common practice & best practice to use MVC framework
		1. There are frameworks available to implement MVC architecture
			1. Model-View-Controller

#### MVC Architecture ####
1. Most popular framework available to implement MVC architecture is Spring
2. Using Spring framework, we are able to separate:
	1. The model in the form of Servlet
	2. The presentation in the form of JSP
3. Passing of control from controller to model and model to JSP (view) is taken care by MVC framework in Spring
	1. Best practice to have MVC architecture and use Spring

#### Spring Containers ####
1. Spring provides many core capabilities which are important for any Web application & any services (RESTful)
2. Spring framework runs as a **container inside a web container**
	1. It provides certain key capabilities:
		1. Inversion of Control (Dependency Injection) - for business logic
		2. Model View Controller - for frontends
		3. JDBC Templates - for acessing DB
		4. Connection Pools - for HTTP, for DB
	2. The capabilities gives structure to the application
	3. The capabilities takes away a lot of work from a developer
		1. Otherwise, developers needs to write a lot of boilerplate code (taken away by Spring containers)

### Jetty & Spring ###
1. Review:
	1. Jetty can be used anywhere we have HTTP requests
		1. It can be used to host web-applications
		2. It can be used to host services (based on HTTP protocol)
			1. REST Service - uses HTTP protocol (hence Jetty container)
	2. On top of Jetty containers, we can use Spring containers
	
			+------Jetty------+
			|  +-----------+  |
			|  |  Spring   |  |
			|  | Container |  |
			|  +-----------+  |
			+-----------------+
			
		1. Whereever we are writing Java code, we can use Spring framework
			1. Spring framework provides a lot of libraries to minimize developer work while writing Java code
	3. Difference between Spring framework on RESTful side and Webapp side is:
		1. Kind of response we are generating
			1. On services side:
				1. Response: JSON/XML
			2. On webapp side:
				1. Response: HTML
					1. Because we are generating dynamic content
	4. Other things related to HTML (css, javascript, static images, ...) are hosted on Nginx reverse proxy
		1. We don't need to bring requests to dynamic content layer
			1. Since it can be served from Nginx through its memory
				1. Releaves our webapp from some of the load that Nginx can share
	5. We can use Nginx for caching RESTful services responses (reverse proxy)
		1. If the HTTP response indicates that they are cacheable, Nginx can cache the responses
			1. If there is a request from webapp for some service API, the response is cacheable and is cached in Nginx
				1. Then there is no need to go upto service
		2. Nginx reverse proxy alleviates restful services from some of the load wherever it can cache the responses

### Node.JS ###
1. Topics:
	1. HTTP Server
		1. Uses JavaScript engine to process requests
	2. Highly efficient at handling a large-number of connections
		1. For requests that are IO bound and not CPU bound
	3. Single thread to handle all connections
		1. Saves memory
		2. Avoids context switching
		
#### HTTP Server ####
1. Why use Javascript engine on Server side?
	1. Javascript engine was designed to handle a lot of I/O requests asynchronously
		1. Javascript makes call to server and gets data
		2. Javascript renders the page behind the scenes
		3. Javascript does a lot of asynchronous I/O behind the scenes
			1. It does it very efficiently
	2. Suppose we have same kind of requests on the server side
		1. The most of the work that a server has to do is:
			1. Handle IO requests to service
			2. Handle IO requests to database
		2. Then the web app has to handle IO requests
			1. **If IO requests can be handled asynchronously, that gives an opportunity to handle a very large number of connections**

#### Highly efficient at handling a large-number of connections ####
1. Requirement: The requests should be IO bound and not CPU bound
	1. Each request must not force Node.js to do a lot of computation
		1. If there are lot of computations involved in serving a request, then Node.js is not a good choice
		2. If the requests are mostly IO bound, where very little computation is required
			1. Most of the time is spent in:
				1. Making call to database
				2. Making call to a service
		3. For IO bound requests, Node.js is an excellent choice because it gives us an opportunity to handle a very large number of connections

#### Single thread to handle all connections ####
1. Single threaded model avoids context switching and it saves memory
	1. event-driven, asynchronous model
		1. Also used in Nginx reverse proxy
		2. Node.js in addition as asynchronous execution that needs to be done
			1. With Javascript, we can do a lot of asynchronous callbacks
2. The native datastructure format on the server side is JSON
	1. MongoDB supports JSON format
	2. Browser works with JSON format
	3. Web application works with JSON format (due to Node.js)
		1. **Gives an opportunity to pass messages without any transformation**
			1. End to end messages can be passed and communicated using JSON format

### Node.JS Event Loop ###
1. Architecture
	1. Node.js internally executes Javascript engine
		1. Javascript engine has got an event loop
			1. Event-loop: A single thread that continuously executes and never gives up the CPU on its own
				1. If OS wants to move out the thread for some reason, it can do that
		2. The only reason it may vacate CPU is when there is absolutely no requests
			1. Otherwise, the thread will continue to execute all the requests
				1. There are other threads
		3. Event loop processes:
			1. Incoming client requests
			2. Callbacks
			3. Outgoing calls
			4. Handling responses
		4. Rest of the activities related to the IO are managed by OS
			1. OS IO Queue (Non-Blocking) or Thread Pool (OS responsibility)
			2. Incoming Network Calls (OS responsibility)
				1. Listening to client requests for incoming calls
			3. Outgoing Network Calls (OS responsibility)
				1. Make outgoing calls to execute the outgoing calls which have been called by Node.js asynchronously
			4. Disk Access (OS responsibility)
		5. Any function executed synchronously is executed by the event loop
			1. Any function that is called synchronously is handled by the event loop
			2. Any function that the event loop will call asynchronously will be given to OS
				1. OS will execute the outgoing call asynchronously
		6. If a disk access is required (say Node.js is writing some statements in a log file), the disk access is also handled asynchronously
	2. Flow:
		1. Incoming request is handled by the OS (case with every server)
			1. All other servers which are based on request/response model, they will spawn a thread for each client request
			2. In the case of Node.js, no threads are spawned for each request
		2. Event-loop constantly polls OS IO queue
			1. Then it gets to know the incoming client requests
		4. Then if there is any incoming client requests, it will take the request
		5. Then it will execute it synchronously
		6. If there is any asynchronous call in Javascript code, the event loop is executing for the request, the asynchronous call will be put into a callback queue
			1. Example: `setTimeout` function
				1. Executed asynchronously after certain duration of time
					1. Callbacks which have to be executed after a certain duration of time, will be put into a callback queue (enqueue)
		7. Once event loop is done executing some of the requests, it can poll the callbacks
			1. If it finds that any callback needs to be executed, it will execute the callack
		8. Once the callback is executed, it will poll for any incoming requests
			1. If there is any incoming request, it will execute it in a synchronous fashion
			2. If there is any callback during the execution, it will be put into the callback queue
		9. If there is an external call that we are making synchronously, event loop will execute it synchronously
			1. It blocks the event loop
				1. **It may force it to vacate CPU**
					1. Solution: **When we make external calls in Node.js, we make them in an asynchronous fashion**
						1. Any IO needs to be done asynchronously
							1. If we cannot do it asynchronously, we must not use Node.js
		10. If there is an external call that we are making asynchronously, the call will be given to the OS
			1. OS will take care of making the external network call
		11. Event-loop will periodically poll the OS IO queue to check if we have got any response for our outgoing network call
	3. What is being polled?
		1. It is polling OS IO queue
			1. It can get:
				1. Incoming client requests
				2. Any response to outgoing network call
					1. Call made to external service and response has come
						1. It is in the OS buffer
							1. Once we poll the OS, OS will let us know that we have got a response
						2. Event-loop can take the response back and process the response synchronously
					2. Once we complete the execution, we will write the response on OS IO queue
						1. This response will go back to a network channel from where, the request has come
							1. Event-loop will track which code executed belongs to which request and which callback executed ties up to which request etc.
			2. **Any IO that happens, it happens asynchronously**
				1. **As soon as event loop sees that it has to do something asynchronously, it puts it into some queue**
					1. Once it is put in the queue, event loop will proceed with the next task which it will get from any other queue by polling
	4. Summary:
		1. Event loop constantly polls
		2. Event loop queues the work that is in callback
		3. Event loop queues the outgoing work (network calls, disk access)
		4. Event loop executes the necessary code after it gets back a response (after disk access, network call, ...)
		5. Event loop will write back on the network channel from where the request has come
	5. Client's perspective:
		1. It is a request/response model
	6. Node.JS perspective:
		1. Within Node.JS, all the requests are handled in an asynchronous fashion which gives an opportunity to continously execute single thread without giving up CPU
			1. It minimizes context switching
				1. Speeds up our process:
					1. If we continously execute single thread, we can continuously get work from clients
						1. This allows us to maintain lots of connections
							1. Reason: Very little memory overhead for maintain only one thread
								1. Thread is continously working
								2. Thread can work on multiple requests
								3. Thread can handle client load only if the work it has to do for each request is IO work
									1. If a lot of computation needs to done, event loop will do it in a synchronous fashion:
										1. **Client request will get blocked for a long time**
		2. Client doesn't get blocked (if IO bound)
			1. Node.js picks up request
			2. Node.js queues it up with OS (as an async request)
			3. Node.js moves to the next client request
2. Node.js is very efficient
	1. It does two things:
		1. To serve requests for huge number of clients
			1. It can maintain lots of connections
			2. It has very small memory footprint
				1. Everything is run on a single thread (there is only one thread context that occupies memory)
					1. Memory is required for stacks
					2. If there are million connections and we spawn million threads for them, there will be millions of thread contexts
						1. They will not fit into memory
	2. Node.js can handle a large number of connections pretty well when most of the work is asynchronous
	
### Cloud Solutions for Web ###
1. Topics:
	1. Managed Services
		1. Hardened solutions
		2. Automated deployment
		3. Built-in scalability & reliability
		4. Global deployment solutions

#### Managed Services ####
1. The solutions that work on-premises can also be used in cloud environment
	1. Especially if we use cloud as IaaS
2. Cloud has some advantages over on-premises products
	1. We get services which are self-managed services
		1. Benefits:
			1. Hardened solutions
				1. Example: Service for hosting static content
					1. The service is being used for such a long time that it is hardened solution
						1. There are hardly any issues left in the services
				2. The services are also loaded with features
			2. Automated deployment
				1. Any deployment we do will be automated
					1. Example: In certain cases, storage solutions doesn't need anything to be deployed
						1. We just need to store our content
			3. Built-in Scalability & Reliability
				1. Cloud solutions are built for scale
				2. Cloud solutions are built with inherent reliability (there will be multiple replicas to ensure that the data is safe)
					1. Be it a server hosting in cloud
					2. Be it storage solution
			4. Global deployment solutions
				1. We can deploy our solutions anywhere on the globe
					1. Asia
					2. Europe
					3. America
				2. If we decide to deploy our solution in one region (Asia region say)
					1. If we want to deliver solution to customers in Europe and America, cloud has solutions to make it possible
				3. Cloud already has a global network and global presense
					1. It is cost effective to make a global solution
					2. The performance of the solutions is much better (due to global presense)
3. Cloud solutions provided by two popular cloud vendors:
	1. AWS
	2. Google Cloud
	3. Solutions:
		1. CDN
			1. Akamai - specialized in CDN (they have global network)
			2. AWS - AWS CloudFront
				1. Integration exists with their backend
					1. We just need to do some configuration
				2. It is easy to deploy and operate
			3. Google Cloud - Google Cloud CDN
		2. Load Balancers - They come with a lot of compelling features
			1. Features:
				1. We can configure health checks to backend
					1. The health checks can check if the backend is alive or not
					2. LB can route requests to backend if it is alive or will not route requests if not
					3. We can set criterias for defining whether a particular backend is alive or not
				2. HA is already supported in cloud - we don't have to do anything
					1. In on-premise, we have to setup two load balancers (primary, secondary) and establish high availability between them so that once primary goes down, secondary can take over
				3. Load Balancers
					1. L7 Load balancer: They can inspect the contents of the request and route the requests
						1. Splitting requests based on the kind of request (URL of the request):
							1. We want to send static content request to cloud storage
							2. We want to send dynamic content request to web application
						2. Solutions:
							1. Application LB - AWS
							2. External HTTP LB - Google
					2. L4 Load Balancer: It doesn't inspect contents of the request
						1. It lets requests pass through to one of the instances of the backend
						2. Solutions:
							1. Network LB - AWS
							2. Network HTTP LB - Google
				4. Cloud Storage
					1. Any static data that we store on cloud storage gets replicated automatically:
						1. We can replicate in multiple continents:
							1. Very high reliability - content cannot be lost
							2. If a lot of clients are connecting to the application and looking for static data, then they have multiple instances they can connect to and get the content
								1. The load balancing is built into the solution
									1. If say a jpeg images is downloaded by a lot of customers, it can replicate it on multiple servers
						1. Solutions:
							1. AWS S3 (Simple Storage Service)
							2. Google Cloud Storage
					2. A network load balancer directs CDN to cloud storage service directly
					3. Application load balancer can direct CDN to web application
						1. Dynamic content is usually not stored in CDN
							1. However, there is some dynamic content that has life (2 min or 5 min, 30s is also good)
								1. If we don't want to store any dynamic data, users can reach out to LB directly (Governed through DNS)
			2. Examples:
				1. AWS - Application LB
				2. Google Cloud - External HTTP LB
		3. Application Servers (web containers)
			1. Out of the box features:
				1. Managed service
				2. Comes with automation
				3. Easy to deploy - our solution on cloud
				4. Automatic scalability
					1. Number of instances can go up and come down depending on the load
				5. Reliability
					1. Whenever an instance goes down, the cloud will bring up another instance
			2. Solutions:
				1. AWS Elastic Beanstalk
				2. Google App Engine

### Cloud Storage ###
1. Topics:
	1. Unlimited Disk Space
	2. Version Control
	3. Access Control
	4. Low Latency
		1. No overhead of Directory structure
	5. High Throughput
		1. Parallel clients
		2. Large files can be broken into smaller chunks for parallel read
	6. High Availability & Reliability
		1. Multiple copies
		2. Multiple physical locations
	7. Static Website Creation
2. Case study: Online booking system
	1. Static data files - stored in cloud storage
		1. Product images
		2. Web content
			1. CSS
			2. JS
			3. Static HTML
			4. Documents
				1. PDF
				2. Word Docs
	
#### Unlimited Disk Space ####
1. Space available on cloud storage is practically unlimited
	1. We pay for only what we use

#### Version Control ####
1. If we upload a product image and we see that we have uploaded it by mistake, we can go back to our previous version

#### Access Control ####
1. We can decide which of the users have write access and which users have a read access
	1. Employees who take care of uploading or modifying on cloud storage
		1. They can have read/write control
	2. Users of the website will have only read access
2. Fine-grained access control

#### Low Latency ####
1. The files stored are key-value kind of data (not hierarchical)
	1. No overhead of directory structure
		1. Reduces latency a lot - for large scale systems

#### High Throughput ####
1. The files are replicated over multiple servers
	1. Example: File 1 is replicated on 3 servers etc.
2. If there are more readers, the file will be replicated even more
	1. If there are k users and if file is available at k locations, they can read in parallel (they don't have to go to the same machine)
		1. Hence the throughput is increased
3. Large files can be broken into smaller chunks for parallel read
	1. Read will be faster
		1. We can parallely read multiple chunks, combine them and give them to the user

#### High Availability & Reliability ####
1. High Availability & reliability: If one of the machine goes down, there are two more machines that can serve the same file
	1. After certain time, the files hosted on the server that went down will be replicated on other servers
	2. We can extend HA and reliability by having storage in multiple locations
		1. We can store a file in a different country, continent, or region
			1. Very high amount of availability and reliability

#### Static Website Creation ####
1. Cloud storage can be used to host static websites
	1. If website does not have any dynamic content
		1. We do not need anything else

### Cloud CDN ###
1. Topics:
	1. Low latency local access for cache hits
	2. Persistent connections for cache miss
	3. Lower load on the backend
2. Solutions:
	1. AWS CloudFront
	2. Google Cloud CDN
3. Case study: e-commerce system
	1. When user is using the system, what data is transferred the most? (static data or dynamic data)
		1. User interaction
			1. User browses through a lot of products
			2. User then takes about 5 min to select a product once user has looked at multiple products
			3. User then buys the product
		2. Number of pages visited by the user is much more than the pages the user will visit for buying a product
			1. Amount of interactions that a user has for static data is far more than the interaction for dynamic data
		3. If we look at the size of static data vs dynamic data
			1. Static data is far larger than dynamic data
				1. The amount of static data transfered is much more than dynamic data
					1. Because of number of interactions
					2. Because of size of static data
				2. **Transferring static data is a big challenge**
		4. Another challenge: **Physical distances**
	2. Solution:
		1. CDN
			1. If a system is somewhere in Asia
			2. If a user connects to our system
				1. The request travels over the internet and connect to our system
					1. Latency experienced will be very high
						1. The data has to traverse over continents
			3. It has a lot of servers present in each continent in different countries
				1. Job of servers is to cache any data coming from origin server
					1. Data must be cacheable
						1. Static data is mostly cacheable
			4. CDN will make a request to origin server (system) and gets the image
				1. User will be able to download from a local server
					1. Caveat - First time, user will experience a lot of latency
						1. CDN has to first download the image from the origin server
				2. If another user comes in after some time
					1. If the user needs the same product image and if the user is in North America, the image will come from local CDN server
						
#### Low latency local access for cache hits ####
1. We minimize latency

#### Persistent connections for cache miss ####
1. We would have done some optimization
	1. CDN server in North America, while downloading an image from server in Asia will use **persistent connection**
		1. Let us say, CDN downloads product 1 image from origin server
			1. It will have to instantiate a TCP connection
				1. The connection will not be closed
		2. Let us say, user 2 requires product 2 image and it is not available on CDN
			1. If the connection is still alive, CDN will use the persistent connection and download the image (saves round-trips)
		3. It is an optimization

#### Lower load on the backend ####
1. Whenever there is a cache hit, user doesn't have to access origin server
	1. The data comes from edge server/CDN server
		1. The load on the origin server is reduced
2. CDN solves the problem of delivery of static content in case of global customers

### Services ###
1. Services layer
	1. Business logic on services
		1. Business logic can be complex & it can be the largest amount of code we write
			1. **Main challenge**
		2. Patterns used to develop services:
			1. Web-services
			2. RESTful services
				1. More light
				2. With microservices they are even more popular
	2. If we are doing RESTful services and microservices then we need to worry about
		1. Caching
		2. Asynchronous processing
			1. Messaging queues
		3. Hosting business logic
			1. Containers
				1. Jetty - web-applications
				2. The containers for web-applications and services are the same
					1. If we subtract static load, the load is pretty much the same for both
		4. Load balancing and routing
			1. Reverse proxy - Nginx
				1. For both web-applications and services

### Services Solutions ###
1. Topics:
	1. Web Containers
		1. REST & Spring Containers
	2. Object Caching
		1. Memcached
		2. Redis
	3. Asynchronous Messaging
		1. Redis
		2. RabbitMQ
		3. Kafka
	4. Service Mesh
		1. Netflix
		2. Istio
		
#### Web Containers ####
1. REST & Spring Containers
	1. We can use whatever we have used for building web-applications
		1. The considerations remain almost the same as in web-applications

#### Object Caching ####
1. Memcache
2. Redis

#### Asynchronous Messaging ####
1. Redis - for special case
2. RabbitMQ - major messaging queue
3. Kafka - major messaging queue

#### Service Mesh ####
1. Microservices deployments are difficult
	1. There are lots of services and lots of instances to be handled
		1. Mainly handled through k8s
2. Service Mesh
	1. Netflix
	2. Istio

### Memcached ###
1. Topics:
	1. Stores key value pairs
	2. Values can be
		1. Any blob
		2. Any size
			1. Preferred < 1 MB
			2. Max is configurable
			
#### Stores key value pairs ####
1. Requirements for caching can arise anywhere in the system
	1. In Web-application layer
		1. To cache session objects
	2. In Service layer
		1. To cache objects created after long computation, or created after fetching data from database
2. It makes sense to cache objects if the objects are accessed frequently and the data is not modified very frequently (The data doesn't become stale very soon)
3. Less scalable way to cache
	1. Caching in service memory itself
		1. Whenever node computes an object (which is expensive) caches it in memory because it is built using request from database
	2. If a request comes to the node, it is returned from the cache
		1. Works if it is a single node
			1. Problem with multiple nodes:
				1. We might have less cache hits
					1. If request goes to another node for the same data, the second node needs to recompute the object
				2. Key data duplication
					1. We will be storing data for the same key in multiple nodes
						1. Expensive as compared to how Memcache stores
							1. **Memcache is a centralized cache**
								1. Memcache stores as key/value pairs

#### Values can be ####
1. Stores as a blob
	1. Memcache doesn't care what we store in the cache (store anything)
		1. Usually used to store strings
2. We can store any size of data
	1. There used to be a limit of 1 MB
		1. Now it is configurable
	2. We should not use any cache for large objects
		1. Fills very soon & will store very few objects
			1. **With cache, we want to store as many keys as possible**
				1. **Cache hit goes down**
					1. If the use-case demands using large values and there are very few of them, we could go ahead to configure storing large values
3. Two more points:
	1. TTL can be set differently for each data
		1. If we are putting key-value pair in memcache, we can decide for how long the data can live in the memcache
			1. In how much time, the memcache can consider the data to be stale
	2. Eviction expunges expired data followed by LRU data
		1. First it picks expired data - knows through TTL values
		2. After that, it evicts using LRU method

### Memcached Architecture ###
1. Topics:
	1. Cache-aside pattern
	2. Sub-millisecond latency
	3. Horizontally Scalable
		1. Data is partitioned
	4. High Throughput
		1. Parallel operations
	5. Cluster Aware Client Library
		1. Consistent hashing for resolving a node
	6. Node Failure is Treated as a Cache Miss
		1. Use large number of nodes with less data
	7. Data is lost if a node crashes or restarted
2. Architecture:
	1. Memcache can be installed as cluster of nodes
		1. We can have as many nodes as we want
			1. Depending on how much data we have
	2. Each node has a number & IP address
		1. Node-1 - has IP address
		2. Node-2 - has IP address
	3. Clients of Memcache know how many nodes exist in the memcache cluster
	4. Clients also have IP addresses of the nodes
	5. Memcache Client:
		1. It uses a client library
			1. Client library will make a DNS call to get the IP address of any one of the Memcache node (we can get multiple IP addresses as well)
				1. If there are 10 nodes in the cluster, Memcache may return 2-3 addresses
			2. Client library will use any one of the IP addresses
			3. Suppose DNS has returned the IP address of node-1
			4. Client library will make a call to node-1 for getting cluster info
			5. Client library will get a response containing (the info is cached):
				1. How many nodes
				2. What are the IP addresses
	
#### Cache-Aside Pattern ####
1. Memcache follows Cache-aside pattern
	1. Client can retrieve only those keys which client itself has put into Memcache
		1. Example: Client is looking for key3
			1. There is nothing in the memcache to start with
			2. There will be a cache miss
			3. When client tries to get the value of key3, it will get nothing
			4. Client will go to database (directly), get the value of key3, and put it in Memcache cluster (in a node)
				1. Key3 will be available in Memcache cluster
			5. If client goes to Memcache cluster and asks for the value of Key3, it will get the value for key3 (DB access is not required)
2. How does the client know that it has to go to a particular node for a value?
	1. To put or get from a particular node:
	
			put(key3):
				Hash(key3) % 2 = 1 -> node-1-IP
				
			load_multi(key1, key2): // possible to load multiple values at once
				Hash(key1) % 2 = 2 -> node-2-IP
				Hash(key2) % 2 = 1 -> node-1-IP
				
		1. It works similar to Hashtable
		2. Memcache know for each node number, what is the IP address
			1. It knows where to put the key and retrieve the information
	2. To retrieve the value:
		1. Same hash is calculated and moded with number of nodes
3. **Client itself is managing the state of all the nodes**
	1. Client is responsible for storing the values in Memcache
		1. All nodes will arrive at the same information because they are using the same client library & they have the same info about the memcache cluster
4. Most caches work this way 

#### Sub-Millisecond Latency ####
1. Time required to fetch a key and value from memcache node will be < 1 ms
2. If we go to DB, it is in the order of 5 ms for NoSQL dbs
	1. 5 - 20 ms for RDBMS databases
3. Hence it improves any architecture in terms of latency
	1. **Consider using a cache if we want low latency**

#### Horizontally Scalable ####
1. Since we have partitioned the keys, each node is responsible for different keys
		1. Results in high throughput
			1. Since it is horizontally scalable (we can add any number of nodes to memcache)

#### High Throughput ####
1. Parallel operations
	1. If there are 100 clients, they can parallelly access the nodes
		1. The keys can be retrieved independently
	2. Each node can be made multi-core (increases parallel operations)

#### Cluster Aware Client Library ####
1. In reality, consistent hashing is used
	1. Consistent hashing is a variation of hashing that is more advanced
	2. If we increase or decrease the number of nodes (which affects the mod factor) will not impact the entire cluster

#### Node Failure is Treated as a Cache Miss ####
#### Data is lost if a node crashes or restarted ####
1. Drawback:
	1. If a node crashes or if we need to restart our system:
		1. **We will lose all the data that we have cached**
			1. Takes time for cache to build up again
		2. Cache restart can bring down the performance of a system

### Redis Cache & Its Architecture ###
1. Topics:
	1. Much like Memcached
	2. It is a [key -> Data structure ] store
		1. Strings
		2. Lists
		3. SortedSets
		4. Maps
		5. ...
	3. Data-Store Made for Persistence
		1. Stores data on a disk
		2. Allows backups
		3. Can be started pre-populated with a backup
	4. Data Replication
		1. Asynchronous and synchronous
		2. Read load distribution
		3. High Availability
	5. Can also be used as a Messaging Queue
	6. Data-Store Mode Requires Fixed Number of Nodes
		1. Cache mode is suitable for node scaling
2. Redis came after Memcache
	1. It filled all the gaps that were there in Memcache
	2. It has added many more features
3. Redis does what Memcache does and does much more
	1. If we are starting a new project, we could use Redis cache
		1. There is no reason to use Memcache
		
#### Much like Memcached ####
#### It is a [key -> Data structure ] store ####
1. It is a data-store (as compared to Memcache)
	1. Values can be data structures
		1. In Memcache, they are just blobs (Strings usually)
	2. Why store datastructures?
		1. Suppose we store list in Redis and has 10k elements
		2. Suppose we want to append one more element
			1. In Memcache - we retrieve the entire list, add element, put the whole list in Memcache memory
				1. High latency - retrieving and storing a lot of data
			2. In Redis - We can add an element to the list in Redis (it is not just a blob and Redis knows how to append element)
		3. Redis can perform operations on data structures

#### Data-Store Mode for Persistence ####
1. Data Store: In Redis, we can store data on disk (asynchronously)
	1. Allows backups
	2. Allows us to restart our cache nodes
		1. If we restart them, they can be pre-populated with the backup we have taken (with data stored on disk)
2. We can restart the entire Cluster
	1. The cluster will get re-populated with the backup (data on disk)

#### Data Replication ####
1. Topics:
	1. Asynchronous and synchronous
	2. Read load distribution 
	3. High Availability
2. Architecture:

		Client Lib --Cache Miss---> DB
		    |
			|        Read
			+---------------------------------+
		Read/Write                            |
			|      (key1,key3)     (key1,key3)|
			+----> Master-1 ------> Slave-1 <-+
			|            Async Replication    |
			|      (key2,key4)     (key2,key4)|
			+----> Master-2 ------> Slave-2 <-+
			             Async Replication
						 
	1. Masters are similar to Memcache
	2. If we modify or read, we can go to masters
	3. Difference: **To support more read load, we can have slaves to masters**
		1. We can have multiple slaves to master
		2. Whenever a key is added to master, it is added to slaves
			1. It is done asynchronously - to ensure good latency numbers
				1. We can do it synchronously but it degrades performance
	4. We generally use it as a cache
		1. We use datastore because we don't want to build it up once again
			1. If a node goes down
			2. If we restart the cluster
	5. If a master goes down, we can elect one of the slaves as the master
		1. It takes very little time
		2. Provides HA
	6. Read load distribution:
		1. For read load, we can go to master and slaves

#### Can also be used as a Messaging Queue ####
#### Data-Store Mode Requires Fixed Number of Nodes ####
1. We can use Redis in Cache mode or Datastore mode
	1. In Datastore mode: The number of nodes becomes fixed
2. In cache mode, we can add and remove nodes
3. Pros & Cons:
	1. Pros: It is the right option to go for whenever we have a caching requirement
	2. Cons: It is slightly more complex in terms of installation (setting up of cluster)
		1. Worth it because it is better than Memcache

### Cloud Caching Solutions ###
1. Topics:
	1. AWS Elastic Cache
		1. Memcached
		2. Redis
	2. Google Memorystore
		1. Memcached
		2. Redis
	3. Features:
		1. Fully Managed
		2. Sub-millisecond latency
		3. Scalable to 5 TB
		4. Highly available (99.9%)
2. In terms of caching it is the same as in on-premise environment
3. We can use it as IaaS - we can deploy it on our own with the infra provided by the cloud
4. We can use cloud's provided solution - fully managed
	1. We don't have to deploy
	2. We can directly use it
	
#### Fully Managed ####
1. We do not have to deploy or install Redis or Memcache on cloud
	1. They are ready to use 
	2. Just configure
		1. Tell the kind of hardware & cloud will configure accordingly
2. Another option:
	1. We deploy it as PaaS
		1. We need to manage the deployment

### RabbitMQ ###
1. Topics:
	1. Design Goals
		1. At-Least-Once Delivery
		2. Message Sequencing - FIFO
		3. Interface Decoupling
		4. Consumer Decoupling
		5. Message Rate Decoupling
	2. Consumer Mode
		1. Push
		2. Pull
	3. Use Cases
		1. Service Integration
		2. Message Buffer
2. It is a general purpose messaging queue
3. It is most widely used messaging queue
4. Use-Case:
	1. We want to pass a message from Service-1 to Service-2
		1. Service-1 doesn't expect a response OR
		2. Service-1 waits for sometime to get the response
			1. Immediate response is not expected
	2. Asynchronous one-way messaging - MQ can be used
5. Ways to use MQs:
	1. Way 1:
		1. Service-1 will put message into an MQ (instead of sending to Service-2)
		2. MQ then can push the message to Service-2 (if it is available)
	2. Way 2:
		1. MQ can deliver message to multiple services
			1. one-to-many message delivery
		2. The messages are pushed when the services become available
	3. Way 3:
		1. Subscriber pulls the message
	4. Way 4:
		1. Multiple subscribers pull the message
		
#### Design Goals ####
1. At-Least-Once Delivery:
	1. Why can't we pass directly?
		1. We want to ensure that the message is delivered at-least once (message delivery is guaranteed)
			1. Once we send a message, whenever service-2 is available the message is delivered
			2. Once the message reaches MQ, assuming the MQ is highly available, MQ can deliver the message when service-2 is available

2. Message Sequencing - FIFO
	1. Message sequence is maintained
		1. The messages are delivered in the same sequence as they come to the consumer(s)

3. Interface Decoupling
	1. Service-2 doesn't need to know the communication technology used by Service-1
		1. If Service-2 is restful service, Service-1 must be RESTful client (no other option)
			1. If we message queue
				1. Service-2 can be of any kind
					1. RESTFul
					2. EJB
					3. SOAP based Web-Service
				2. Service-2 doesn't have to worry about the nature of Service-1
					1. Service-2 just needs to understand the message

4. Consumer Decoupling
	1. Service-1 doesn't know to which service it is delivering the message
		1. Synchronous communication needs service-1 to know:
			1. Host & port
		2. Service-1 needs to know the host & port of message queue
			1. Helps in one-to-many delivery
		3. MQ will take care of delivering it to all of its consumers

5. Message Rate Decoupling
	1. Producer is producing messages at a very high rate (temporarily)
	2. Queue can absorb the messages and deliver the messages at the rate the services can process the messages
	3. Example: Suppose Service-1 is sending messages at a very high rate
		1. MQ will acknowledge the messages after receiving them
		2. MQ can deliver the messages at the rate at which service-2 can receive messages
			1. Processing of messages in service-2 may not happen at the same rate as service-1 sends
				1. If we don't have MQ in between, service-2 will go down (because it cannot process at that rate)
					1. service-2 will reject messages that it cannot process
			2. MQ can just keep the messages and acknowledge service-1
			
#### Use Cases ####
1. Service Integration
	1. MQ can be used to integrate two services (asynchronously)
		1. One way asynchronous messages
2. Message Buffer
	1. If service-1 is getting messages at a very high rate, service-2 cannot process the messages at the same rate
		1. In between MQ can act as a message buffer
		2. MQ can store all messages temporarily
		3. If service-2 is not able to cope up with the load, if load decreases on service-1, service-2 will eventually cope up with messages filled in message queue 
		4. If service-2 is not able to cope up with messages, we can add more consumers
			1. Consumption can be faster
	2. Use-case:
		1. Streaming type of workflow
			1. Messages are coming from IoT devices
				1. Coming at a very high right
					1. Kafka can be used to store messages at a very high rate
						1. Multiple consumers can process the messages
	3. RabbitMQ vs Kafka
		1. RabbitMQ - a general purpose messaging queue for all the use-cases
			1. Push or pull
			2. Push: If there are messages at times and no messages at other times, push can be used
			3. **In service integration, load is not that high (variable), push messaging works better**
				1. We can use RabbitMQ in those cases
		2. Kafka - can only be used for pull based messaging
			1. Consumers have to pull the message
			2. Streaming workloads:
				1. Incoming message flow rate is too high and queue is always full
					1. Pull makes sense
						1. Or else, service-2 will unnecessarily be poling for messages wasting its CPU cycles
				2. If messaging queue is guaranteed to be full (usually in the case of streaming workflows)
					1. There is high inflow of messages
						1. **We can do pull**
							1. Reason: It takes away some of the load of messaging queue
				3. **In streaming workloads, we want Queue to act as a message buffer**
			3. Kafka shines if:
				1. Streaming workloads for which we need message buffers
				2. Incoming message flow rate is extremely high
					1. RabbitMQ cannot scale beyond a point (in case of streaming scenario)

### RabbitMQ Architecture ###
1. Topics:
	1. General purpose message broker
	2. Messages are pushed to consumers
		1. Consumers can also pull the messages (but push is common)
	3. Message deleted once acknowledged
		1. Consumers cannot go back to the messages it has already processed
			1. It is possible with Kafka
			2. There are use-cases where we need to go back to the messages
				1. If we are trying to build reliability into consumers and if they need to redo the stuff they did before (generally in long running processes), we cannot do with RabbitMQ
					1. The use-case generally doesn't arise in service integration where we use RabbitMQ
	4. Message ordering is guaranteed
		1. The queue delivers the messages in the order they arrived at the queue
	5. Useful for asynchronous service integration
		1. Any service that has to be integrated, and it is possible to integrate them asynchronously, we can integrate with RabbitMQ
	6. Both persistent and transient messages are supported
		1. Transient messages: Messages that are not stored by RabbitMQ on disk but straight away delivers them to consumers
			1. If for some reason RabbitMQ goes down before delivering the messages, the messages are permanently lost
			2. Why do we use it?
				1. For high speed processing of messages but if some messages are not delivered, we are fine with it
		2. Persistent messages: We guarantee that message that was put into messaging queue is definitely delivered to the consumers (at-least once)
			1. If a message is delivered more than once (say due to the queue going down or the consumer going down), RabbitMQ can deliver messages multiple times (rare)
				1. Solution: Consumer should be aware of those messages by checking the id of the messages
					1. Using the id, we can ensure that the processing of the message does not affect the system
			2. Any message that comes into RabbitMQ, it is permanently stored on the disk
				1. If RabbitMQ goes down and comes up, it can retrieve the message from the disk and deliver it
	7. Uses built-in component called exchange for routing
		1. RabbitMQ uses a component called exchange for routing
			1. Exchange - a type of router
				1. It controls to which queue or topic a message has to go
				2. It applies certain routing rules looking at the message and routes it to appropriate queue or topic
			2. Flow:
				1. Step 1: Message is delivered to an exchange
				2. Step 2: Message will be stored on the hard-disk (applicable for persistent mode)
					1. Skiped for transient messaging
				3. Step 3: If we have setup replication (if MQ becomes corrupt, we can recover using replica), we have
					1. Master/Slave
						1. Master Queue
						2. Slave Queues
							1. When a message arrives to master, it is communicated to slave MQ
							2. The slave MQ will store it in its queue
						3. It adds to reliability or availability of MQ (RabbitMQ)
							1. It is not for scale
								1. Any message comes to master and message deleted is first in master
									1. No state changing operation in slave
							2. **A client can connect to either master or slave but exchange will route to the master queue**
								1. All the load is handled by the master
									1. Problem: **It doesn't scale**
				4. Step 4: Once the message is replicated and stored on the disk, an acknowledgement will be sent to the producer
				5. Step 5: MQ will then take the responsibility of delivering the message
					1. Synchronous flow
				6. Step 6: MQ takes the message from memory and tries to deliver to the consumer (if consumer is available)
					1. If the consumer is available, it pushes the message out to its consumer
				7. Step 7: The consumer sends an acknowledgement after receiving (and processing) the message to the MQ
				8. Step 8: The MQ will delete the message from its memory and from its disk
				9. Step 9: The same acknowledgement will be forwarded to the replica and replica will also delete the message from its queue and from the disk
				
2. Features:
	1. Scales to 50k messages per second (with vertical scalability)
		1. It is pretty good because it should cover most of the use-cases
			1. Except for streaming use-cases (Kafka shines with this)
	2. Scales well vertically
	3. Not horizontally scalable (not very well)
		1. Master-Slave replication for high availability
			1. Clients can connect to any side
			2. All publish, consume operations first go to master 

### Kafka Architecture ###
1. Topics:
	1. Performance
		1. Million messages per second
		2. Sequential writes and reads on log files
		3. Relies on page cache for quick reads
	2. Horizontally Scalable
		1. Topics and partitioned
	3. Order of data guaranteed only within a partition
		1. Producer can decide the partition
	4. Messages are not deleted, so can be replayed
	5. Consumers can only pull the data
		1. No push by Kafka
		2. Not designed for service integration
	6. Useful for streaming analytical workloads
		1. Where high throughput is required
		2. Click streams, Page views, Logging, Ingestion, Security
2. Kafka is ideal for streaming workloads where producers are producing data for Kafka at a very high rate
	1. RabbitMQ cannot do that
	2. Kafka's architecture supports streaming workloads
3. Architecture:
	1. Kafka is just a distributed log-file
		1. Internally, Kafka writes all its messages on a log-file (main database file for Kafka)
		2. Producers: Many producers can connect simultaneously to Kafka but the messages written are sequentially appended on a log file
			1. Append operation is extremely fast, Kafka can support lots of producers simultaneously
				1. RabbitMQ has to maintain certain data structures instead
					1. B-Tree - used by databases to write data on hard disks
						1. Allows writing to disk and fetching to memory
					2. Kafka doesn't have such navigation
					3. RabbitMQ maintains data structures in memory and on disk
						1. Write overheads are significant
							1. Not as good as sequential write overheads
								1. It is negligible as compared to RabbitMQ
			2. Producer write operations are extremely fast
		3. Consumers: They know the offset and they can start reading from the start of the file
			1. If a consumer has read upto 9th message, it knows that it has read upto the 9th message
				1. Consumer tracks (not Kafka)
					1. Zookeer helps consumer to track this
				2. Consumer can say I want to read from 9th message (using index)
				3. Consumer can read from any offset at any time
					1. Log-files stay for very long time (even forever)
						1. We can reclaim some of the old files to save disk space
				4. Kafka helps reading from the offset it decides
				5. Generally, consumers reads from the latest messages
					1. The latest messages are readily available in OS page cache
						1. Once a block of log-file is read by OS into memory, the subsequent messages are already avaialable in memory
							1. OS maintains page cache - recently written or read messages are available in the page cache
								1. Improves performance - helps reading very fast (most reads are coming from page cache)
	
#### Performance ####
1. Handls millions of messages per second
	1. Reasons:
		1. Due to sequential writes and reads on log files
			1. Relies on page cache for quick reads

#### Horizontally Scalable ####
1. Topics are partitioned
	1. If log file is partitioned
		1. Some data in partion 0, some in partion 1, etc
			1. Some producers can write on partion 0, some in partion 1, and some in partion 2
				1. 1/3 of producers on each partition
					1. Reduces load on log file by 1/3
						1. If we increase paritions, we can write in parallel
		2. If we partion into 100 partions and we keep the partions in 100 machines, we can handle more producers
			1. 100 times faster for one producer as well
2. Consumers can be scaled horizontally
	1. Consumers can be distributed on partitions
		1. Some consumers can read from partion 0, some from partion 1, etc.
	2. If the load on Kafka increases, we can increase the load on Kafka and we can increase the number of machines
		1. Horizontal scalability

#### Order of data guaranteed only within a partition ####
1. Ordering in a queue is lost to an extent
	1. If three partitions belong to a particular queue
		1. Since we are writing the messages to three separate partitions, we have lost the global order
			1. We have not lost the order within a partition
	2. Partioning control:
		1. Producer can decide on which partition to put a certain message
			1. Example: For certain set of users, partion 0 is chosen etc.
				1. For a given user, all data will come in one partion and in perfect order
					1. Local ordering is not lost
		2. We can also collapse all partitions into one partition
			1. Cannot scale

#### Messages are not deleted, so can be replayed ####
1. Kafka does not delete messages
	1. Any consumer can go back and re-read messages from a older offset
		1. With RabbitMQ, the message is immediately deleted once it recieves acknowledgement that it has read and consumed the message
	2. Use-case:
		1. **Building backups** - DBs can be rebuilt (we have all the events that have taken place in a system)
			1. If we replay all the events, we get to the final state
2. Kafka is built for **high throughput incoming data that has to be processed in real-time**

#### Consumers can only pull the data ####
1. Consumers can only pull the messages
	1. Kafka cannot push the messages to its consumers
		1. It is not a trade-off in high-throughput environment for which Kafka is designed
			1. Reason: There is no difference if the messages are pushed or pulled
				1. Responsibilities of fetching messages is offloaded to consumers
					1. Consumers can track their offsets
					2. Consumers can decide at what rates they want to process the messages
						1. They are themselves pulling messages
2. It is not designed for service integration:
	1. For service integration we need one service to communicate the message to another
		1. Message needs to be pushed
			1. Even if Kafka is used, the consumers have to continously poll for messages
				1. Kafka is not designed for such use-cases

#### Useful for streaming analytical workloads ####
1. Kafka is designed for high-throughput workloads
	1. Examples:
		1. Click streams (we want to analyze)
		2. Page views (we want to analyze)
		3. Logging (real-time)
			1. Can be injested into Kafka
				1. An analytical tool can fetch the logs and analyze them
		4. Security
	2. It is good for data that is coming into Kafka at a very high rate
		1. We need a message buffer to absorb all the load and we want consumers to process the messages at their own pace

### Redis Pub/Sub ###
1. Topics:
	1. For short lived messages with no persistence
		1. Much like a synchronous call
		2. Fire and forget
			1. No delivery guarantee
	2. Million operations per second
	3. Useful for making dashboards
		1. Leaderboard
	4. Comparison
		1. Kafka
			1. No push
			2. Writes to log
		2. RabbitMQ Transient
			1. Delivery acknowledgement
			2. Deletion of delivered messages
2. Pub/Sub
	1. Forms an excellent messaging-queue (for certain kinds of problems)
		1. **For fast messaging that does not need any persistence***
			1. To pass on messages to subscribers without any persistence
3. Architecture:

				Publisher
					|
				TCP Connection
					|
					v
				Channel 1		Channel 1
				Redis --------> Redis
					|				|
			+-------+-------+-------+-------+         
			|				|				|
		TCP Connection	TCP Connection	TCP Connection
			|				|				|
			v				v				v
		Subscriber 1   Subscriber 2		Subscriber 3
		
	1. Channel 1 - Has on Redis cluster
	2. Redis cluster - Two nodes
		1. Node 1 - Two subscribers connected
		2. Node 2 - Two other subscribers
	3. **Connections are long lived (TCP connections)**
		1. Unlike HTTP connections
			1. Disconnected after a timeout period
		2. The connection is disconnected only when it is closed by the client or server
	4. Publisher:
		1. Sends a message to its channel
		2. The message is immediately delivered to its subscribers which are connected with Redis
			1. If a subscriber is not connected to Redis at the moment, it will not get the message
				1. If the subscriber later on connects with Redis, it would have missed the message
		3. The subscribers subscribed to the channel 1 on other nodes will also get the message
			1. Node-1 will relay the message to Node-2
			2. Node-2 will deliver the message to its subscribers
		4. It is like synchronous call
			1. If subscriber is down durng delivery, the message is lost
			2. Redis will also not re-attempt to deliver the messages
		
#### For short lived messages with no persistence ####
1. Messages are delivered very much like in a synchronous call
	1. Publisher will publish a message
	2. If subscriber is connected at that time, subscriber will get the message
	3. If subscriber goes down at the time, the subscriber will not get the message
		1. Redis will not try to deliver the message (message is lost)
	4. Use cases:
		1. For short-lived messages that do not require any persistence
			1. If the messages are delivered, we can forget about them and move to the next set of messages
				1. Example: Leaderboard
					1. Constantly showing top 10 people leading in the game
						1. Suppose the position changes every second
						2. We want to communicate the leaderboard to players in realtime
					2. If we are unable to deliver the leaderboard to a particular node, it is okay
						1. Connection could be bad
						2. The node might have gone down
					3. The messaging system can move to the next message - it is more relevant
			2. Focus is to deliver the current message to the subscribers who can receive the message at the current point in time
		2. Redis is excellent solution
2. Fire and forget
	1. No delivery guarantee
		1. In return, we get millions of operations per second

#### Million operations per second ####
1. Redis is great for fire-and-forget type of use-cases but who need millions of operations per second
	1. Delivery guarantees is not important

#### Useful for making dashboards ####
1. Leaderboard
	1 Old messages are not delivered

#### Comparison ####
1. Kafka
	1. No push
		1. Doesn't work if subsribers poll Redis server (it might bring down the server)
	2. Writes to log
		1. Wherever we don't need these guarantees, the overhead is meaningless
2. RabbitMQ Transient
	1. Delivery acknowledgement
		1. **If subsriber is unavailable at the time of delivery but comes back at a later time, RabbitMQ retries delivery**
	2. Deletion of delivered messages
		1. No persistence
			1. It comes to memory and delivered to subscribers
			2. **Not written to disk**
				1. If RabbitMQ goes down and comes back, it is not going to read anything from disk and deliver (transient mode)
		2. Acknowledged messages are deleted

### Cloud MQ Solutions ###
1. Solutions:
	1. Community
		1. RabbitMQ
		2. Kafka
	2. AWS
		1. SQS 
		2. Kinesis
	3. Google Cloud
		1. Pub/Sub
2. The cloud offerings are no different from open source offerings
		
#### AWS ####
1. SQS - Simple Queue Service
	1. Very much like RabbitMQ
		1. A few features might be slightly different
	2. We can use RabbitMQ or replace it with SQS
2. Kinesis
	1. Kafka is used where there is high throughput of data
		1. Used in:
			1. Big data scenarios
			2. Streaming scenarios
			3. IoT scenarios
		2. Consumers have to pull messages from Kafka
	2. Kinesis - used in IoT and big-data scenarios where there is high throughput of data
		1. Use it if we want to replace Kafka with a managed solution provided by AWS

#### Google Cloud ####
1. Pub/Sub
	1. It can be used for both scenarios where we can use RabbitMQ and Kafka
		1. It can take exceptionally heavy loads
			1. Horizontally scalable
				1. It is a managed service
					1. We don't have to manage it
				2. With RabbitMQ and Kafka, we need to manage the cluster
	2. It works for:
		1. General messaging
		2. High throughput messaging

### Datastores ###
1. Data Storage Layer
	1. It doesn't just store files
	2. The system reads and/or modifies the same data
2. Anayltics
	1. We don't modify any data
		1. The data is in the final shape
			1. We just process the data (rarely modified)
3. Challenges:
	1. The system needs to be designed for read and write loads simultaneously
	2. Storage is done on disk
		1. We have to do disk operations if we want to do read or write
			1. High latency
	3. Load on database layer is not much as compared to frontend payer but it is big enough
		1. There is a high latency of operations involved in accessing disk storage

### Datastore Solutions ###
1. Topics:
	1. RDBMS
		1. Oracle
		2. SQL Server
	2. Distributed Databases
		1. Key-Value
			1. Dynamo
		2. Column Family
			1. Big Table
			2. Cassandra
			3. HBase
		3. Document Oriented
			1. MongoDB
		4. Graph Database (not looking into)
2. Comparing features of RDBMS with distributed databases
	1. Why do we need distributed databases?
	2. Where do the distributed databases help us?
	3. Where are they a good fit?
	4. Where are they not a good fit?
3. Goals:
	1. Functionality of the DBs
		1. Unique Features in terms of functionality
	2. Unique features in terms of non-functional requirements:
		1. Performance
		2. Scalability
		3. Reliability
	3. With the above perspectives, we look at the DBs
		1. Each DB has been designed for a particular use-case

### RDBMS ###
1. Topics:
	1. General purpose database (< 1-5 TB data, 10k connections)
		1. If we do not have any specific functional requirements, this is the right choice
		2. Generally, we will start getting into problems if data is > 1 TB
		3. We also get into scalability issues once the number of connections reach about 10k
			1. Reasons: No of nodes that we can use for RDBMS are limited
	2. ACID Transactions (possible only on a single node or else it requires 2PC/3PC)
		1. Update the multiple records or tables - Atomically
	3. Data Consistency (possible only on a single node or else it requires 2PC/3PC, leads to low availability)
		1. Data same for all readers at any given time
			1. If we bring in multiple nodes in RDBMS, **the consistency starts getting relaxed**
	4. Fixed Schema (Impedes application evolution) (well defined schema)
		1. Data analysis (we can do queries on the data - because we have well defined schema)
			1. Columns can be searched (we can select columns)
			2. Rows can be filtered (by applying different conditions)
			3. Queries can Join Tables (Joins may slow down a system)
		2. Query pattern can change or evolve
			1. Any column can be indexed
			2. Indexes can be created whenever required (on the fly)
				1. Speeds the searches
				2. Possible because, RDBS recognizes the columns
					1. Values in the columns are not black boxes (like key/value pair DBs)
						1. RDBMS know what value each column has in a table
	5. Normalized Data (Joins may slow down a system)
		1. Efficient storage and writes
			1. With denormalized data, we can avoid joins
	6. Overwrite for updates (Allows only one version of data, Old design for expensive disk space)
		1. Since disk is not expensive, a new row is created with a new timestamp
			1. It becomes the current row
			2. Allows us to store older version as well
			3. Allows versioning
2. RDBMS capabilities & their shortcomings
	1. How NoSQL tries to address them
3. We don't know what kind of queries will be supported on RDBMS
	1. We decide schema first
	2. Queries can evolve later
	3. Disadvantages:
		1. Adding/removing columns is not easy (especially if DB is in production)
			1. It might needs DB migration
		2. Application is tightly coupled with the DB
			1. If we make object changes, we need to make schema changes to DBMS
				1. It impedes application evolution
		3. Joins slow down queries
			1. However, joins make data analysis flexible
		4. Normalized data is not scalable
	4. Advantages:
		1. Data is normalized
			1. Data is not duplicated
				1. Stored efficiently
					1. No much disk space is consumed
					2. Amount of memory to load is also reduced (utilized efficiently)
				2. For large scale systems, disk space is not an issue and memory is not an issue (aggregate memory of multiple nodes is much higher for horizontally scaled systems)
4. With NoSQL
	1. We know the access patterns (how we access ata)
		1. Queries are known
	2. We then design schema applying the knowledge of the queries
	3. We can change the structure of our schema in such a way that it is optimized for our query (join is avoided)
		1. How?
			1. Aggregate objects
				1. Object in business layer are as it is put into the NoSQL DBs
	4. They try to move to denormalized schema
		1. Has its advantages and disadvantages

### RDBMS Scalability Architecture ###
1. RDBMS Scalability Architecture:
	1. RDBMS is vertically scalable
		1. Few other things can be done to make RDBMS more scalable and reliable
			1. Limitations
				1. Hence we need NoSQL databases
		2. There are limits to vertical scaling
	2. RDBMS can be partitioned vertically
		1. Three services, Catalog, Order, Inventory, were using one RDBMS Database node
			1. We can have separate node for each service
				1. Catalog service database node
					1. Exclusively hosting catalog service database
				2. Order service database node
				3. Inventory service database node
					1. Makes our application considerably scalable
						1. Load will get reduced to 1/3 on each node (assuming the load is equal for each service)
							1. Assuming we write code that works in an isolated fashion
				4. Drawbacks:
					1. We cannot have database transactions across nodes that combine catalog tables & order tables
						1. Aleternatives:
							1. 2PC/3PC
							2. Eventual consistency
	3. RDBS can have read replicas (If there is a lot of load on single database)
		1. Any change that is done to the master is replicated to the secondary databases
			1. Advantages: Allows us to share read load with master
			2. Disadvantages: Replication is asynchronous
				1. Read queries on replicas are not consistent with those in Master
					1. It will take some time for replication to happen (not instantaneously)
					2. The state of replicas will be slightly inconsistent for a brief period of time
				2. Reads are scalable
				3. Writes are not scalable
	4. RDBMS Reliability:
		1. Synchronous replication
			1. If master goes down, replica must be exactly same as the master
				1. Why not use read replicas?
					1. They are many and synchronous writes becomes slow on master
						1. We need to wait until data is written on all the replicas
2. Oracle:
	1. RAC - Real Application Cluster
		1. Processing nodes can be multiple
		2. Database shares the same disk
			1. There are still bottlenecks
				1. It is not very scalable
		3. Considering the cost of scalability, it is not a very great option
			1. If we want to spend a lot of money for a small increment in scalability

### NoSQL Objectives & Trade-Offs ###
1. Objectives & Trade-Offs
	1. Scalability (biggest design objective)
		1. Architectural Choice:
			1. Horizontal Partitioning (RDBMS cannot be horizontally scaled)
			2. Commodity Hardware (no expensive hardware required)
				1. RDBMS requires extremely reliable hardware
					1. Cost is extremely high
						1. Vertically scaled
				2. NoSQL databases build reliability into software (instead of relying on hardware)
					1. Cost of scalability comes down
						1. We can horizontally scale in cost effective manner
		2. Trade-Off
			1. ACID Transactions
				1. Due to horizontal scalability
					1. 2 PC/3 PC is possible
						1. They are not replacement of ACID in terms of:
							1. Performance
							2. Convencience
			2. Joins
				1. Due to horizontal scalability
	2. Availability (second objective, even if certain nodes are not available, there must be other nodes that are available to serve the database (important because commodity hardware run the database, we can make NoSQL databases work even if there is network partition))
		1. Architectural Choice
			1. Data Replication
			2. Eventual Consistency
		2. Trade-Off
			1. Data Consistency
				1. Transactions are no longer ACID
					1. They are eventually consistent
						1. Consistency can be tuned
							1. We trade consistency for performance
				2. We lose consistency with NoSQL
	3. Flexible Schema
		1. Architectural Choice (There is no hard requirement on columns and their data types - we can add them on the fly - if we change object schema in application the schema automatically changes (no need to run any migration))
			1. Key-Value
			2. Column Family
			3. Document-Oriented
		2. Trade-Off (We lose the flexibility of SQL because DB usually doesn't know what columns exist and their datatypes)
			1. SQL
			2. Secondary Indexes
				1. We can get objects through keys
					1. Some document databases have secondary indexes (?)
						1. But others don't have secondary indexes
						2. **Secondary indexes** - **Indexes that are not based on the key of objects**
						
			3. Integrity Constraints
				1. We lose this
					1. It is okay because we gain performance
						1. Reason: DB doesn't have to check for integrity constraints
							1. Whenever there are mutations in DB
	4. Performance
		1. Architectural Choice
			1. Aggregate Schema
				1. Highly de-normalized
					1. Works for certain queries which are looking at de-normalized structures
						1. We can get the entire de-normalized structure without doing any joins
				2. Problem: We cannot do any non-key based queries in a flexible manner
					1. In RDBMS, we can choose any columns, we can apply filters on any columns (because of the indexes present)
					2. Since schema evolves freely, we may not have indexes
						1. Some NoSQL DBs don't allow secondary indexes
							1. Hence some NoSQL DBs may not perform well
					3. With NoSQL DBs, we know the query pattern and then the schema is created based on the query pattern
						1. Any after thought queries may not perform well
							1. In certain cases, it many not even be possible to do those queries
								1. Solution: We need to know what kind of queries we are going to make and accordingly we design schema (for higher performance)
									1. We may not be able to make random queries which are not key-based
										1. This may require secondary indexes
			2. In-Memory R/W
				1. NoSQL DBs are memory based
					1. Why?
						1. Since, data is horizontally partitioned
							1. They are running on many machines so we can have a lot of aggregate memory
		2. Trade-Off
			1. Normalization
			2. Non-Key Queries
2, NoSQL DBs had some design objectives:
	1. They were trying to overcome the limitations that were there in RDBMSs (scalability related)
		1. To achieve the design objectives, there were trade-offs
			1. Architectural tradeoffs
			2. Design tradeoffs

### Amazon DynamoDB ###
1. Topics
	1. Key-Value Pair Datastore
		1. Each record in dynamo db table is identified by a key
		2. A value is associated with a key
			1. Value can be blackbox
				1. Values can be:
					1. JSON
					2. XML
					3. ...
		3. It is a free schema
			1. Java object can be transformed into JSON and stored as value
				1. Object ID can be the key
			2. Advantages:
				1. We don't have to convert Java objects into RDBMS normalized format
					1. Just convert the entire object and put it into dynamo db
		4. The schema can evolve freely
			1. We don't have to change anything in database if the object structure changes
	2. Used for High Scalability & Availability
		1. It has very high scalability & availability
	3. Table is a Hash-Map (like in Java)
		1. Persistent
			1. They can be stored on disk and retrieved from disk
		2. Distributed
			1. All key-value pairs stored get split into multiple key-value pairs
				1. Some go on some nodes and others go to other nodes
	4. API (It is a hash-table)
		1. Put
		2. Get
		3. Update
		4. Delete
		5. Query (some limited querying)
			1. Querying is based on primary key columns only
	5. Index Key - has two parts (helps retrieve a particular row if multiple rows have the same partition key)
		1. Partition Key (product id)
			1. Can have only one attribute
			2. Key is hashed to determine the partition (advanced hashing is used)
				1. Same partition key goes to one node
					1. 1001 - same node
		2. Sort Key (optional, size, if it is specified, it must be specified for everys row)
			1. Determines sort order of an item within a partition
				1. Helps us get to a particular row by doing a binary search
			2. Can be used for range query <, >, like
				1. Example: Product with id 1001 and all sizes starting from 'A' to 'D'
	6. R/W ops for a key are atomic
		1. Example: If we are updating a product with ID 1001 and size L, the change will be atomic

### DynamoDB Architecture ###
1. Topics:
	1. Suitable for storing small chunks of data (DB is for this purpose)
		1. Key values less than 1 MB
			1. Supports Big JSON, XML, String
				1. Not suitable for:
					1. Big data files
					2. Binary data files
	2. Peer-to-Peer cluster (distinctive feature)
		1. No master - write on any node
			1. Example: Node B, Node C, Node D are responsible for Key 1
				1. If client needs to do anything to Key 1, it can go to any of the three nodes
				2. The client connects to any node in the cluster
				3. The node forwards the request to any of the three nodes responsible for the key Key 1
				4. If any of the three nodes is down:
					1. We can update the key Key 1 in any of the other two nodes
						1. Even if a node is down, we can still do writes
							1. This is not possible in a master/slave architecture
		2. Each node responsible for a set of keys
		3. Consistent hashing of virtual nodes for key allocation
			1. It is an advanced form of hashing
				1. When we add or remove nodes, we don't have to disrupt the entire cluster
					1. An advanced form of consistent hashing is used
		4. Vector clocks are business rules to resolve merge conflicts
			1. Since we can write on any nodes, if two users are writing for k1 on node B and another user writing for k1 on node D - conflict
				1. Resolution techniques:
					1. Timestamps
					2. Vector Clocks (?)
					3. Business rules (if vector clocks is not possible)
	3. Highly Scalable
		1. Practically any number of nodes
		2. Petabytes of data (because of horizontal scalability)
		3. Can handle 10 million RW ops requests/second
	4. Highly Available
		1. Updates are not rejected even in case of network partitions or server failures
			1. If any node goes down, there are replica nodes where we can do read and write operations
	5. Consistency guarantee is adjustable
		1. R + W > N for strong consistency
			1. By default, dynamo db is not strongly consistent (it favors availability over consistency)
				1. When update happens to one node, it takes some time for the update to propagate
					1. For a brief period of time, the dynamo db is inconsistent
						1. During this time, we can connect to other nodes for reading or writing the key in-case some nodes are down
			2. If we don't want eventually consistent but strongly consistent system (anytime two clients read value of k1 from the system, they must read the same value)
				1. R - min no of nodes to read
				2. W - min no of nodes to write
				3. N - total number of nodes
					1. Example: If N = 3, then R = 2, W = 2 say
						1. We need to write to at-least 2 nodes
						2. We need to read from at-least 2 nodes
							1. If there is inconsistency, we will know that
2. Architecture:

		                                     K1  Key K1 (Replica 2)
		Client - Get(K1) -> Node H -> Node A -> Node B -> Node C
		                       ^                (Replica 1) |
							   |							v
							Node G <- Node F <- Node E <- Node D
		                                                (Replica 3)
														
	1. Ring represents range of values for a partition key column
	2. Machine IP/Name is hashed to occupy a position on the ring
	3. Gossip protocol:
		1. Each node randomly connects to other nodes in the cluster
		2. The node tries to get info as to what nodes are responsible for what keys
		3. The node talks to enough number of nodes to propagate the state of the cluster across the entire cluster (?)
3. We use dynamo db for very high scalability
4. We use dynamo db for free schema
	1. We can write any values
5. We use dynamo db for extreme high availability (even if there is network partition)
	1. If some nodes go down or we get disconnected from other nodes, we can still read and write to a node that is available to a client

### Google BigTable ###
1. Topics:
	1. Basis for Apache HBase
		1. Apache HBase is open source implementation of Google BigTable
			1. Interface is slightly different
				1. Google BigTable supports HBase interface now
	2. Column-Family Storage
		1. Data is grouped into column families
			1. Example:
			
					Row Key: (com.airlines.www, com.hotel.www)
						Document (CF) - contain web pages (home page)
						Lanuage (CF) - EN
						Referrer: trips.com    -|
							1. Check Flights
							2. (no entry)
						Referrer: holidays.com -|- (CF)
							1. (no entry)
							2. Your Hotel
						Referrer: news.com     -|
							1. (no entry)
							2. Venue
						
				1. Referrer - Column Family
					1. trips.com - Column Name
					2. holidays.com - Column Name
					3. news.com - Column Name
			
	3. Table is stored as a Tree-Map (Rows are in sorted order)
		1. Sparse
		2. Sorted
		3. Persistent
		4. Distributed
	4. Limited CF (<100)
	5. CFs are compressed
	6. Unlimited columns
	7. R/W ops atomic for a key
	8. Timestamps for versioning

### BigTable Architecture ###
### HBase ###
### Cassandra ###
1. What is it?
	1. It is an open source DB
	2. It came after DynamoDB and BigTable
		1. It has taken features from both DynamoDB and BigTable
			1. It is a mix of both
2. Data model:
	1. Column family data model
		1. Not exactly similar to BigTable
		2. There are similarities to DynamoDB data model
	2. Example:
	
			Product Id | Size | Col Name | Col Value
			1001         L      Name       Blue Denim
			1001         L      Quantity   150
			1001         XL     Name       Blue Denim
			1001         XL     Quantity   780
			
			1002         M      Name       Black Shirt
			1002         M      Quantity   960
			1002         M      Discount   10
			1002         L      Name       Black Shirt
			1002         L      Quantity   900
			1002         L      Discount   20
			
		1. In Cassandra, a table is called a column family
			1. All columns are included in a column family
		2. It has a partition key & sort key
			1. In DynamoDB, we could put any value
			2. In Cassandra, we have distinct columns
				1. No multiple column families
					1. Logically, it becomes an RDBMS table, but this is not how it is stored
			3. Partitition key - it decides in which partition a particular row is going to recide (like DynamoDB)
			4. Sort key - What is the order of the rows in that partition for the partition key
		3. Storage:
			1. the way it is stored is:
				1. The column names are stored as column values
					1. Name
					2. Quantity
				2. The column values are stored as column values
					1. Blue Denim
					2. 150
			2. Each column has got converted into a row
				1. Two columns become two rows
				2. Three columns become three rows
			3. Cassandra can have any number of columns
				1. Because they become rows
			4. Cassandra can store structured data & get exploded into multiple rows (like in Bigdata)
				1. Difference:
					1. Each product id goes to a different partition
						1. Each partition can go to a different node (like dynamo db)
						2. In Bigtable, all the rows will be in sorted order
							1. In Cassandra, the sorting is limited to a partition key (decided by sort key)
								1. Two partitions will not be sorted and will not be adjacent to each other
									1. They can be in any relative order depending on the hash values
			5. We can store millions of columns (column family database)
		4. Features:
			1. Cassandra is horizontally scalable
			2. Cassandra is clustered
			3. Data can be partitioned into different nodes
				1. Borrowed from Dynamo DB (exactly same)
					1. Peer-to-peer topology
						1. No master
						2. Decentralized
						3. Each node is responsible for certain set of nodes
						4. ...
					2. It achieves high availability even if there is network partition
						1. There could be conflicting writes
							1. Handles write conflicts similar to Dynamo DB
		5. Performance:
			1. Write operations: Borrowed from Big Table
				1. Steps:
					1. Write operation comes to Cassandra 
					2. Operation is logged in WAL (write ahead log) file (like BigTable)
						1. Sequential IO
							1. Extremely fast operation
								1. File is open for writes & writes are quickly appended
					3. Write is also done in Memtable (similar to BigTable) (in memory)
						1. This is fast operation
							1. It is not random access
							2. It is sequential IO
					4. Write operation is acknowledged
						1. The write operations are extremely fast
					5. If there is shortage of memory
						1. The memtables are flushed into SSTables (Similar to BigTable) (onto disk)
					6. If the node goes down during the write operation and comes back (temporary problem)
						1. The Memtable can be re-created by reading from the SSTable from the disk and applying operations there on the LOG
					7. If node completely goes down and we cannot recover the data, data is available in the replica
						1. Each time an operation is done on a particular node, it is replicated on other nodes
							1. On replica nodes responsible for a particular key
								1. For reliability
					8. Read operations:
						1. If keys are in memory, they will come out of memory
							1. If key is not in memtable, then
								1. SSTable will be loaded into memory
								2. Read will be completed
						2. Read is fast but sometimes it is slow
							1. It depends on whether the data is cached or not
			2. Use-Cases:
				1. Very high write throughput - writes are on memory

### Cassandra Features ###
1. Topics:
	1. Schema-less, Column-Family Structured Data (format)
		1. Sparse
		2. Persistent
		3. Distributed
			1. By hash partitioning
			2. It also supports range-partitioning (not known for this)
	2. Horizontally Scalable
		1. Petabytes of data
			1. For lots of data
			2. If we want to write with very high throughput
	3. Highly Available
		1. Even during network partitions
			1. Due to peer-to-peer model
				1. Nodes can be in different data centers
					1. Spread of dynamo or cassandra can spread over the entire world
	4. High throughput R/W operations
	5. Merge Conflicts
		1. Vector clocks
		2. Timestamps
		3. Business rules
2. Features Summary:
	1. Data Model - Column Family - resembles Big Table
	2. Storage - Memtable -> SSTable - inspired from Big Table
	3. Partitioning - Hash Based - Dynamo
	4. Replication - Peer-to-Peer - Dynamo
	5. Consistency Model - Eventually Consistent - Dynamo
		1. High availability at the cost of consistency
			1. It can be tuned for strong consistency (on a query basis)
				1. It increases latency (especially if nodes are located very far in different data centers)
	6. Availability - Highly Available - Dynamo
3. The features don't show any difference with a small scale database with very few nodes
	1. There may not be much difference between HBase, Cassandra, BigTable, etc.
		1. The architecture will give details that can be used to decide the usecases of the database

### MongoDB ###
1. Topics:
	1. Key -> Document (key/value pair database)
		1. In Binary JSON (bson) format (JSON document in binary format)
			1. MongoDB knows each field of the JSON document we are inserting
			2. It can store nested documents - it is the speciality of MongoDB
				1. We can update portions of a document
					1. Entire document doesn't need to be updated
	2. Columns created dynamically
	3. Columns can be indexed
	4. Documents can be queried
		1. on id and or column values
	5. An operation on a single document is atomic
		1. 2 PC for multiple documents
			1. Any operation on a single document is atomic
				1. Operations on multiple documents is done 2 PC - not scalable
					1. Only for feature completion
						1. We usually don't come to NoSQL DBs for transactions
2. Operations:

		db.inventory.insertMany([
			{ item: "journal", qty: 25, size: { h: 14, w: 21, uon: "cm" }, status: "A" },
			{ item: "planner", qty: 75, size: { h: 22.85, w: 30, uon: "cm" }, status: "D" },
			{ item: "postcard", qty: 45, size: { h: 10, w: 15.25, uon: "cm" }, status: "A" }
		]); // Insert - it allows nesting (unlike other DBs)
		
		db.inventory.find( { status: "A", qty: { $lt: 30 } } ) // Query
		
		db.inventory.find( { "size.h": { $lt: 15 } } ) // Query with nested attribute - makes it faster if we index
		
		db.inventory.updateOne(
			{ item: "paper" },
			{
				$set: { "size.uom": "cm", status: "P" },
				$currentDate: { lastModified: true }
			}
		) // Update - portions
		
		db.products.createIndex(
			{ item: 1, quantity: -1 }
		) // Index Creation - for top level columns or nested columns - it makes search fast (we can have indexes on any columns)
		
3. Recap:
	1. We can store structured data in:
		1. BigTable
		2. HBase
		3. Cassandra
	2. We can store key-value pair data in:
		1. DynamoDB

### MongoDB Architecture ###
1. Topics:
	1. Indexing for fast search
		1. It's write overhead (trade-off)
			1. Insert and update queries will be very slow (indexes need to be updated each time)
				1. Indexes are B / B+ Trees which need random access
					1. Similar to what exists in RDBMS (in terms of latencies)
			2. It is as good or as bad as RDBMS in terms of performance
				1. Where it differs is it is horizontally scalable
					1. We can keep data on several nodes
						1. It can fit much more data than what RDBMS can fit
	2. Sharding for Scalability (optional and it can be switched off)
		1. Range sharding
			1. Enabled by default (we can switch to hash sharding)
			2. Useful for range queries
				1. example: id < 10 & id > 200
		2. Hash sharding
			1. Good for even distribution
			2. Good for equality queries:
				1. example: id = 200
				2. It is a little faster for equality queries
	3. Replication
		1. Master Slave (It is primary for certain keys but secondary for other keys, other nodes can be primary for other keys but secondary for some keys - read requests get diverted to either of the nodes)
			1. No write conflicts
				1. Writes go only to primary
		2. Asynchronous (default)
			1. Eventual consistency
				1. We can change it synchronous on query basis
					1. Strong consistency is possible - latency goes high
		3. Synchronous (on demand)
	4. Works very well with Node.js
		1. Javascript -> Node.js -> Mongo (no better latency but higher scalability)
			1. JSON format
				1. Assume SPA:
					1. Objects are in JSON
						1. No transformation is required between layers
2. Architecture:
	1. Config server holds metadata
		1. Instances present and shards
		2. Data ranges on each shard
	2. Router instances
		1. Re-directing the client requests
		2. Caches config server data refreshed periodically
	3. Diagram:
	
			  Client
	             |
				 v
			Mongo Router ---Cache Config---> Config Server
			     |   |                             ^
			     |   |                             |
				 |   +----------+    +-------------+
				 |              |    |
				 Write(K1)      |    |
				 |              |    |
				 | +-----------_|_-+-+-----+  
				 v |            v  |       |
			Primary         Secondary    Secondary  Server Server
			     |              ^            ^
			     |              |            |
			     +--------------+------------+
				     Asynchronous replication

### Analytics ###
1. Last layer in the system
2. Special properties:
	1. Does not actively participate in transactions
		1. No users are actively connected to this layer
		2. Example: If we book an order
			1. It will be written into databases and response is returned back
		3. Analytics is offline:
			1. Whatever data is accumulated in the Data layer, it is used to analyse the data
				1. Historical
				2. Current
	2. Challenges:
		1. We may have structured and un-structured data
			1. Unstructured data: Applications writing log files
				1. This comes to analytics storage
		2. We are dealing with huge amount of data
		3. Realtime data
			1. IOT Systems
			2. Social media
			3. Mobiles
			4. Logs
				1. Choice:
					1. Batch processing: We can accumulate and do a batch processing (we do processing in bulk after some time)
					2. Stream processing: Processing data as it arrives
			5. Analytics deals with batch processing & stream processing (real-time processing)

### Analytics Solutions ###
1. Topics:
	1. Data Movement
		1. Logstash
		2. Fluentd
	2. Storage
		1. Hadoop HDFS
			1. Map-Reduce
		2. Elastic Search
			1. Search
	3. Stream Processing
		1. Kafka
			1. Buffer
		2. Storm, Flink
			1. Processing

#### Data Movement ####
1. Suppose services were generating a lot of log files
	1. We need to take the log files and move them to analytics
		1. Done by:
			1. Logstash
			2. Fluentd

#### Storage ####
1. After we receive the data, we need to store it
	1. Options:
		1. Hadoop HDFS
			1. Where we can do Map-Reduce
		2. Elastic Search
			1. Where we can do fast searches on data
			
#### Stream Processing ####
1. What is stream prosessing?
2. What are the challenges of stream processing?
	1. How do we deal with stream processing?
		1. We are not discussing processing using:
			1. Strom, Flink
		2. Kafka - used as buffer

### Logstash Architecture ###
1. Architecture:
	1. I/O Plugins:
		1. Collect & Move Log/stream events
			1. Input plugin collects data
	2. Queue
		1. Reliable data movement
			1. It ensures that data is delivered **at-least once**
				1. If logstash goes down before it receives the acknowledgement and it gets restarted, it may deliver the data again
					1. There may be some duplication (> 1 times)
		2. At least once delivery
			1. In any streaming solution, data is delivered multiple times at times
				1. We need to handle duplicate deliveries
		3. Tracks Acks, Applies Backpressure
			1. Supposed destination is not able to accept the load
				1. Queue will start growing in such cases
					1. **Once it goes beyond a threshold, it will stop accepting values from source**
						1. Backpressure gets applied
				2. When queue is eased out, it will start taking requests
	3. Filter Plugins
		1. Filter, Transform, Aggregate
2. Diagram:

		Push Source (Filebeat)	Pull Source (DB, Queue)
			|						^
			|						|
			| +---------------------+
			v |
		Input Plugin
			|
			v
		Queue
			|
			v
		Filter Plugin
			|
			v
		Output Plugin
			|
			v
		Destination
		
	1. Push Source:
		1. Access logs
		2. App logs
		3. System logs
		4. DB logs
		5. ...
		6. Streaming input
			1. Twitter say
	2. Input Plugin (can belong to different vendors)
		1. File
		2. Beats - provided by Logstash
			1. It is used to move around files and other sources
		3. HTTP
		4. JMS
		5. Redis
		6. Kafka
		7. ES
		8. ...
	3. Queue
		1. Memory - if we don't need persistence
			1. It will be very fast
			2. If logstash goes down, we will lose this data
		2. File
			1. Used if we cannot afford to lose some data
	4. Filter Plugin
		1. JSON
		2. CSV
		3. Grok
		4. Dissect
		5. Clone
		6. Drop
		7. Aggregate
		8. ...
	5. Output Plugin - depending on destination
		1. ES
		2. Redis
		3. Webhdfs - Hadoop
		4. S3
		5. Kafka
		6. File
		7. Email
		8. ...
	6. Destination
		1. Alerts
			1. Nagios - Monitoring tool
		2. Analysis
			1. Hadoop
			2. Elsticsearch
		3. Archives
			1. Google Cloud Storage
			2. S3
3. Example:

		127.0.0.1 - - [05/Feb/2012:17:11:55 +0000]
		"GET / HTTP/1.1" 200 140 "-" "Mozilla/5.0...
			
				|
				v
				
		{
			"host": "127.0.0.1",
			"user": "-",
			"method": "GET",
			"agent": "Mozilla/5.0 (Windows..."
		}
		
2. Problem: How to collect and move log files:
	1. Solution: Logstash
3. We can think of logstash as a pipe
	1. We can put data at one end
	2. We can receive the data at the other end
	3. Inside the pipe, we can do some transformation and/or filtering
4. Example:
	1. Apache server is logging all requests
	2. We want log statements to go to Elasticsearch
		1. Logstash will either pull from Apache server
		2. Logstash will either push for Apache server (Apache will not be able to do it but we need another software)
			1. Logstash can itself do that
	3. Steps:
		1. Input plugin accepts the input
		2. The input is then put into a queue
			1. This enables acknowledging to the source of data that logstash has taken the input data
			2. Queue:
				1. It can be memory based
				2. It can be file based
					1. This option is for high reliability
						1. If logstash crashes, if we again start logstash, then whatever data is put into queue, it will resume from where it left of
		3. Filter plugin pulls out the data from the queue and processes it
			1. Multiple processing plugins available
				1. Example: Space separated Apache log file is converted into JSON file
					1. We can use:
						1. JSON plugin
						2. Grok plugin
						3. Disect plugin
						4. ...
		4. Output plugin will take the transformed output and will communicate it to the destination
			1. Destination:
				1. Example: Elasticsearch
			2. Once it gets acknowledgement from Elasticsearch, the acknowledgement can go all the way upto the queue
				1. The data is deleted from the queue
					1. Ensures reliablity - deletes data only if it is reliablity pushed to destination
5. Logstash is an integration tool that integrates source to a destination
	1. It reliably transfers data from source to destination

### Logstash Data Streaming Architecture ###
1. Topics:
	1. Streaming log data for Real-Time Analytics
	2. Horizontally Scalable & Highly Available - Any number of Logstash nodes
	3. Fault Tolerance - Needs reliable disk storage (RAID, Cloud persistent disks)
		1. **To ensure that messages are not lost** (if there is a problem with a logstash node)
			1. Cloud persistent disks - replicated at disk level
	4. Use Kafka as buffer - For heavy load that Logstash Queue cannot handle
		1. If system is under very heavy load
2. Architecture:

		Application-1
			^
			|
		Filebeat/Logstash
			|
			v
		Kafka/Redis
			|
			v
		Logstash
			|
			v
		Elasticsearch (or HDFS - Map/Reduce)
			|
			v
		Kibana
		
	1. Data streaming of its source to an analytic engine where we can draw useful info out of the data
	2. Suppose an application is generating exceptions
		1. We want to report such exceptions asap
			1. Previously, we would need to take the log files through batch process and transport them using tools like FTP to an analytical engine which reads log files and reports the errors
			2. Requirement:
				1. We want to ship messages automatically from applications generating log messages
				2. The shipped messages should reach their ultimate destination (analytical engine)
				3. The analytical engine can anaylize and report the messages in automated fashion, in real-time
	3. How to use Logstash for streaming data real-time analytics:
		1. Suppose application-i is constantly generating log-files and appending messages to log-files
		2. We can install logstash on the same machine where the application is running
			1. Problems: **Logstash is a heavy tool in terms of memory consumption** (because it is Java application)
				1. **It also had a lot of processing logic to transform data**
					1. Solution: We use a lightweight tool called Filebeat (a lightweight version of logstash)
						1. Features of Filebeat:
							1. It ships data
							2. It has very minimal transformation capabilities
						2. It collects data and ships it
							1. It doesn't interfere much with the main application
						3. Filebeat can directly send to analytic engine (Elasticsearch say)
							1. Problem: **It doesn't scale well, when we have lots of applications generating log files on a continuous basis**
								1. Solution: Logstash engine in between
									1. **Highly Scalable**: It can be scaled to a lot of nodes
										1. 100s of nodes - it can horizontally scale
									2. **Highly Available**: If any node goes down, Filebeat can send data to other nodes
									3. **Load Balancing**: Filebeat can use Round-Robbin method to send log messages to available nodes
		3. Logstash server forwards the messages to Elasticsearch
		4. Why Kafka/Redis in-between Filebeat and Logstash?
			1. They are full fledged messaging queues & can act as very good message buffers
				1. Problem with Logstash: It doesn't have queuing capabilities of Kafka or Rabbit MQ (it doesn't take as much load)
					1. Kafka & Rabbit MQ can be horizontally scaled (unlike in Logstash)
						1. Logstash has only one queue (we can have multiple instances but each instance has a single queue)
							1. Queue inside an instance cannot be scaled horizontally
								1. Solution:
									1. Application level Filebeat instances can first send messages to Kafka/Redis
									2. The messages will be available in Kafka/Redis
									3. Logstash can pull messages from Kafka/Redis.
										1. Logstash can pull messages at a pace that it can handle
											1. The pace depends on the pace that Elasticsearch can handle
			2. Advantages:
				1. The streaming infrastructure becomes resilient
					1. It can take a lot of load (especially during peak times)

### Fluentd ###
1. Topics:
	1. Older than Logstash
		1. Plugin support that is available with fluent is much more than logstash
			1. What is in favor of logstash?
				1. It is part of ELK stack
					1. It makes sense to use Logstash if using Elasticsearch
						1. Any other use-case, we can use Fluentd (it is Logstash + other capabilities)
	2. Memory Footprint
		1. Logstash - Heavyweight (GB)
			1. Very high memory footprint
				1. Not a good solution for acting as a log agent in machines where applications are logging
		2. Filebeat - Lightweight (MB)
			1. Part of suite of products called Beats (for different interfaces)
				1. File interface - FileBeat
		3. Fluentd - Lightweight (MB)
			1. Less memory
			2. It is comparable to FileBeat
				1. However, in terms of features, it is comparable to Logstash
		4. Fluent Bit - Super Lightweight (KB)
			1. Memory footprint is extremely less
				1. If we need extremely lightweight agent
	3. All features of Logstash - similar to logstash
	4. + Routing
		1. Tags
			1. Any log events coming out of fluent can be tagged
				1. Fluent can use the tags to route the messages to different kind of destinations
	5. + Docker Logging (Fluent integrates very well with Docker)
		1. Picks log events from container console
			1. Docker provides a fluent driver (along with its runtime)
				1. If containers are running on a Docker runtime, if we enable containers for logging with fluent
					1. We can specify when running a container
			2. **Any log messages coming on the console will be diverted to fluent running on Docker runtime**
				1. When we start the containers, we can start fluent driver
					1. We can run the following command:

							fluentd -c docker-fluent.conf

						1. `docker-fluent.conf` - tells fluentd driver as to where to route the log events
							1. Elasticsearch
							2. Google Storage
							3. Amazon S3
							4. ...
			3. fluentd - fluent daemon

2. Architecture:

		Application
		    |       Fluent Bit/
			|        Fluentd    ------> Fluentd ----> Alerts 
			v        |                                Analytics
		   LOG <-----+ tail                           Archives
		   
		   
		$> docker run --log-driver=fluentd
		
		Container-1		Container-2			Alerts
		(Apache)		(MySQL)				Analytics
		    |			   |				Archives
			|			   |			       ^
			v			   v			       |
		+--------------------------------------|---------+
		|                              +---------------+ |
		|     Docker Runtime           | Fluentd Driver| |
		|                              +---------------+ |
		+------------------------------------------------+
		+------------------------------------------------+
		|                      Host                      |
		+------------------------------------------------+
		
		$> fluentd -c docker-fluent.conf
		
3. Other alternatives for logstash:
	1. Scribe - Facebook
	2. Flume - Apache

### Elasticsearch ###
1. Topics:
	1. Full-Text Search
		1. Filter
		2. Group
		3. Aggregate
	2. Stores JSON Documents
	3. Document Fetched using id
	4. Indexes JSON keys and values
	5. Structure
		1. Index -> Database
		2. Type -> Table
		3. Document -> Row
			1. JSON keys are flattened
		4. Supports data types
	6. Users can specify mapping between terms & documents
2. Structure:

		Documents				Inverted Index
		ID 	 | Document			Term     | Frequency | Documents
		Doc-1| Exception in		created  | 1         | Doc-2
		       Order module	
		Doc-2| Your Order is	delivered| 1         | Doc-3
		       created
		Doc-3| Your Order is	Exception| 1         | Doc-1
		       delivered
		                    	in       | 1         | Doc-1
		                    	is       | 2         | Doc-1, Doc-3
		                    	module   | 1         | Doc-1
		                    	Order    | 3         | Doc-1, Doc-2
		                    	                     | Doc-3
		                    	Your     | 2         | Doc-2, Doc-3

		{
			"_index": "accounts",
			"_type": "person",
			"_id": "1",
			"_source": {
				"name": "John",
				"lastname": "Doe",
				"job_description": "Systems administrator and Linux specialist"
			}
		}

		GET localhost:9200/accounts/person/1
		GET localhost:9200/_search?q=john
		GET localhost:9200/_search?q=job_description:linux
		GET localhost:9200/accounts/person/_search?q=job_description:linux

	1. Two options to store data:
		1. Elasticsearch
		2. Hadoop
	2. Two options to store unstructured data:
		1. Storing as it is as files
			1. Hadoop is this kind of storage
		2. Datastore
			1. RDBMS - not choice for storing un-structured data
			2. NoSQL - good choice for unstructured data
				1. Elasticsearch - Not often classified as NoSQL DB
					1. It is designed for doing full-text search
						1. We can use indexes for finding records in NoSQL DBs
					2. It has special kind of index called inverted index - allows us to do full-text search

#### Full-Text Search ####
1. Suppose we have 3 documents
	1. An inverted index is created and maintained by ES
		1. If we want to find out how many times a word is used & in which documents it is used:
			1. We can use inverted index
				1. All terms are extracted (string terms but other kinds of terms are also possible (dates, numbers))
				2. Each term is put in the index
				3. We store how many times the word occurs
				4. We store the documents in which the word is found
					1. This is similar to the index in a book on the back-side
						1. It is the inverted index
				5. We can look up a key
					1. If key is found, the documents can directly be fetched because they are in the inverted index
						1. **We can search any word**
				6. Procedure for creation of inverted indexes:
					1. An inverted index is created for each document
					2. The documents are merged into one cohesive inverted index
						1. Merge is run when new rows are added
							1. Merge is easy because, the indexes are in sorted order
								1. Merge sort can be used to merge the indexes
	2. If we replace strings with JSON documents, that is the format in which ES stores
		1. `_id` - JSON document id
			1. Internal field used to identify a particular document
		2. `_source` - this has the entire document that we inserted
			1. We can do full-text search on a particular field:
				1. `job_description`
					1. Finding `administrator` only in this field
			2. We can do full-text search on the entire document inserted
			3. ES understands that there are fields inside a document
		3. `_index` - index name 
			1. Similar to a database in RDBMS
				1. Logically disconnected from other indices
		4. `type`
			1. Similar to a table in RDBMS
	3. There are two ways to fetch required data
		1. Using id:

				GET localhost:9200/accounts/person/1

			1. ES behaves as a key-value store
		2. Doing query:

				GET localhost:9200/_search?q=job_description:linux

			1. Condition: `job_description` must be `linux`
			2. ES will fetch the document with `_id` `1`
			3. No restrictions search:

					GET localhost:9200/_search?q=john

			4. We can specify the db name and table name

					GET localhost:9200/accounts/person/_search?q=job_description:linux

	4. It is useful if ES is aware of the data type we are interested in
		1. Example: Finding number 0 (not text "0")
		2. ES can determine the data types of different fields
			1. Solution: We can use explicit mapping

#### Users can specify mapping between terms & documents ####
1. Mapping between the document and how we want ES to store it
2. Since ES stores JSON documents, we used Logstash or Fluentd to convert logs into JSON documents

#### Use-Cases ####
1. ES is used for full-text search on a DB
	1. We don't want to do transactions
		1. There will be write load because we add new documents
			1. **We do not use ES to modify documents**
		2. We usually use it for searching documents
			
### Elasticsearch Architecture ###
1. Topics:
	1. Document Oriented data-model
		1. It can store JSON documents
		2. We can search those documents
	2. Horizontally Scalable
		1. Petabytes of data
			1. Data we can maintain on ES can be in Petabytes
				1. Cons: Data searched cannot be of that magnitude
					1. It will be a fraction of its overall size
					2. If we want search size comparable to the stored data, ES is not a good choice
			2. How?
				1. We can shard the data on ES
					1. 3 shards say - horizontally
					2. Each node can have shards and replica shards
						1. Replicas are on different nodes
		2. Data is sharded with key as Document id
			1. ES will compute hash using Document id of the database and it will arrive at a particular node id using the hash of document id
				1. Request will be diverted to a particular node
		3. Put/Get request goes to specific shard
			1. If a request arrives any node
				1. Put Request:
					1. It will compute a hash
					2. It will forward the request to the primary shard of the document id
				2. Get Request is similar
					1. It will go to a specific shard
						1. It can go to any of the shard where document can be located
							1. For load balancing
				3. Delete request: Similar to Put request
		4. Search queries go to all shards
			1. Search request:
				1. Result can be in any document
					1. Solution: We need to search on all nodes
						1. We can connect to any node
						2. The node forwards requests to all the nodes where the documents can be
						3. Each node executes the search independently
						4. Results will be returned back to coordinator
						5. The coordinator will aggregate the results and returns to the client
				2. Performance:
					1. Latency is low - because of parallel search
					2. Throughput is high - Search requests are distributed
	3. High Availability
		1. Shards are replicated
			1. If a node goes down, copy of the primary shards are available on other nodes
				1. All of it is coordinated by the master
					1. It takes care of assigning different data to different nodes
					2. If a node goes down, master takes care of moving shards to other machines
	4. Index structure is based on merge sort
	5. Index not updated with every update or insert
		1. We can put new documents
			1. The update will not update the index
				1. There is no update in ES
					1. ES disables old document
					2. ES constructs a new document
			2. Flow:
				1. When a document arrives
				2. ES computes inverted index for the document
				3. When another document arrives
				4. ES will compute inveted index for the second document
				5. etc.
				6. Once it reaches a size of 3, ES uses Lucene
					1. Lucene merges three indices into higher level index
						1. Merge sort is used
					2. The old indices are discarded
					3. The new index is used to search documents
				7. Once we have added three more indices (due to 3 new documents, a higher level index is created and the older indices are discarded
				8. Once we add 3 more indices, a higher level index is created
				9. Once we have 3 higher level indices, they will be merged into a unified index and the 3 higher level indices are discarded
				10. The process is continued
				11. The indices are in this order:
					1. 9 documents - very big index
					2. 3 documents - intermediate index
					3. 1 document - small index
					4. 1 document - small index
				12. Logic:
					1. When we search, all the indices of different sizes are searched
						1. Majority of the data should be found in the largest index
				13. The process is repeated with every 3 indices being merged into higher level index
					1. When we insert new indices, the index structure is not altered
						1. When we add a document, a small index gets created apart from bigger indices that already exist
					2. In the background, when each index layer reaches its threshold reaches its threshold, it does a merge
						1. It is done periodically to merge newly created indices with older indices
			3. If we are adding new records to ES, it is extremely fast
				1. We don't touch older indices
			4. If we update, a record is removed and new record is added
				1. Updating a record is slightly expensive
					1. Adding is not expensive
			5. All nodes use the structure to search data
	6. Index maintained in memory (indices are specific to each node)
		1. Occassionally flushed to disk
			1. For reliability
				1. If a node goes down, it can come back and reach the changes saved on the disk
				2. Remaining changes that were not flushed onto the disk are applied from the WAL file (in memory)
2. ES architecture:

		Client1 --+          | Shard-1,2 --+
		          +-Put/Get->|             |
		                     | Shard-2,3 --+-> Master
		          +--Search->|             |
		Client2 --+          | Shard-3,1 --+

	1. Merge:

			[1] [1] [1] [1] [1] [1] [1] [1] [1] [1] [1] [1] [1] [1]
			 \   |   /   \   |   /   \   |   /   \   |   /   ^   ^
			   [ 3 ]       [ 3 ]       [ 3 ]       [ 3 ]     |   |
			     \           |           /           ^       |  []
                  \          |          /            |       +--[]
                   v         v         v             +-------+--[]
                         [   9   ]<-----------------------------[] 

#### Use-Cases ####
1. Excellent tool for reporting (similar to SQL queries can be implemented):
	1. Searching records
	2. Filter records
		1. Where
	3. Aggregate records
	4. Group records
		1. Group by

#### Non Use-Cases ####
1. Result set is huge
	1. Solution: Hadoop
		1. It can deal with a large amount of result set

### Hadoop HDFS ###
1. Topics:
	1. Distributed File Data Storage
		1. Unstructured data files
		2. Petabytes of data
		3. Large file sizes > 100MB
	2. Distributed Files
		1. Files broken into chunks
		2. For parallel reads
			1. Map-Reduce
	3. Sequential Writes - Append
		1. Large blocks of data - 64MB
	4. Replication for Reliability
2. Architecture:

		Client
			Client Lib ------> Master Node
		                            Holds directory structure
		                            Mapping of files to blocks
		                            Mapping of blocks to datanodes
		                       ^
		                       |
		        +--------------+--------------+
		        |              |              |
		    Data Node-1   | Data Node-2     |Data Node-3
			[Apple Mango  | [Mango Orange]  |[Banana Pineapple]
			 Plum]        |                 |[Pear Orange Plum]
			[Plum Grapes] | [Pear Plum      |
			              |  Graps]         |
			[Pear Orange  | [Pear Apple]    |
			 Apple]       |                 |
		    --------------+-----------------+------------------
		    [Mango Orange]|[Banana Pineapple|[Apple Mango Plum]
		    [Pear Plum    |[Pear Orange     |[Plum Grapes]
		     Grapes]      | Plum]           |[Pear Orange
			[Plum Apple]  |                 |[Pear Orange
		                  |                 | Apple]

3. Use-case:
	1. We want to store our log files into Hadoop HDFS
		1. Advantages:
			1. We can store our files as it is
			2. We can process large amounts of data
				1. Unlike in Elasticsearch - we can search small chunks of data
					1. Big data cannot be handled
				2. If we want to process petabytes of data (large fraction or entire data)
	2. It can store files
		1. But it is a distributed file storage

#### Distributed File Data Storage ####
1. Large file size > 100MB
	1. It can be broken into 64MB pieces (conigurable)
	2. Example: 1 GB file is broken into 10 pieces of 100 MB
	3. Hadoop is not the choice for small files (> 100MB)
2. Unstructured data files
	1. Log files is unstructured data - easily stored
	2. No transformation required
3. Petabytes of data
	1. Since it is horizontally scalable

#### Distributed Files ####
1. Files are broken into chunks
	1. Chunks are stored on multiple nodes
		1. Why?
			1. We can read chunks in parallel
				1. Example: If we want to count the words in the file (entire file needs to be processed)
					1. If the 10 chunks are on different machines, we can count words in each chunk in parallel - performance increases 10 times
		2. Advantages:
			1. Horizontally scalable
				1. We can have any number of nodes
2. For parallel reads
	1. Map-Reduce - it is able to process large amounts of data
		1. If a large file is broken into 100 small chunks, we can process the file 100 times faster

#### Replication for Reliability ####
1. Example: Consider a file

		Apple Mango Plum
		Plum Grapes
		Pear Orange Apple
		Mango Orange
		Pear Plum Grapes
		Plum Apple
		Banana Pineapple
		Pear Orange Plum

	1. Client contacts Master Node using Hadoop Client library
	2. Master sends data to Client library as to which data nodes, the file can be written on
	3. Client then directly works with data nodes to write the entire contents of the file
		1. Client interaction with Master is minimal
		2. Advantage: Master doesn't become a bottleneck
			1. Master node:
				1. It holds directory structure in memory 
				2. It has mapping of which file is broken into how many chunks
				3. Where are the chunks located on Data nodes
		3. If a client wants to write/read, it gets that info from master node
		4. Procedure:
			1. Client breaks data into small chunks
			2. Each chunk goes to a data node
			3. Client also replicates each chunk and each replica chunk goes to a different data node
				1. For reliability (can be controlled)
					1. If a node goes down, all the chunks are in the remaining data nodes
	4. It can store petabytes of files permanently 
		1. It can be used as long-term archive as well

#### Use-Cases ####
1. Good for storing large files
2. Good for processing large amounts of data

### Map-Reduce ###
1. Topics:
	1. Parallel file processing on Hadoop cluster
	2. Processing code executes on datanodes
	3. Input/Ouptut sources
		1. HDFS
		2. HBase
		3. Cassandra
	4. Map phase
		1. Filtering and transformation
	5. Reduce phase
		1. Shuffles map output across nodes
		2. Groups related information
		3. Computes aggregate data
2. Design

		Apple Mango Plum
		Plum Grapes
		Pear Orange Apple
		Mango Orange
		Pear Plum Grapes
		Plum Apple
			|
			+---------------+
			|               |
			split 1         Split 2
			|               |
			v               v
		Apple Mango Plum    Mango Orange
		Plum Grapes         Pear Plum Grapes
		Pear Orange Apple   Plum Apple
			|    |    | 	   |
			v    |    v		   v
		Apple,1  |  Pear,1	   Mango,1
		Mango,1  |  Orange,1   Orange,1
		Plum,1   |  Apple,1    --
		         v			   Pear,1
				Plum,1		   Plum,1
				Grapes,1  	   Grapes,1
		         |			   --
		         v			   Plum,1
		        Apple,1		   Apple,1
		        Apple,1		   |
		        Apple,1		   v
		        --			   Grapes,1
		        Orange,1	   Grapes,1
		        Orange,1	   --
		        --			   Pear,1
		        Mango,1		   Pear,1
		        Mango,1		   --
		         |			   Plum,1
		         v			   Plum,1
		        Apple,3		   Plum,1
		        Orange,2	   Plum,1
		        Mango,2		   |
							   v
							   Grapes,2
							   Pear,2
							   Plum,4

	1. Input File -Split-> File Text -Extract-> Key,Value -Shuffle,Sort-> Key,Value -Aggregate-> Result
	2. Map:
		1. Split
		2. Extract
	3. Reduce:
		1. Shuffle
		2. Sort
		2. Aggregate

#### Map-Reduce ####
1. It is a processing algorithm that runs on top of Hadoop cluster

#### Parallel fle processing on Hadoop cluster ####
1. We have stored a log data on Hadoop
2. We want to count the total number of exceptions we have received in the last one month (huge data)
	1. Procedure:
		1. We take all log files and put them in Hadoop
		2. Hadoop will split our files and put our files on different nodes
			1. Map doesn't split (Hadoop already splits)
		3. Map algorithm
			1. It will further split (based on new-line say) file chunks into smaller records (done on each node in parallel)
			2. It also parses each record (how to do it is written as part of map handler) (into different words say) and splits
			3. Key/value pairs are generate (for each word say - handler can do anything here as we define)
				1. Apple,1
				2. Mango,1
				3. ...
			4. Computations are done in memory 
			5. The result is written to disk
				1. Each node writes wherever it is doing computing
			6. Map phase ran on each node where data was
		4. Reduce algorithm
			1. We can choose the number of nodes on which we want to run reduce phase
				1. If it is one, all the key/value pairs are reduced to that machine
				2. It finds a machine that is not busy, and it will choose that machine to run the reduce logic
				3. It can choose multiple nodes
					1. Example: 2 nodes
				4. Shuffling
					1. Reduce phase shuffles all keys to the given nodes
						1. Which node to shuffle to is decided by hashing of the key
							1. Apple -> 1 - result will go on node 1
							2. Plum -> 2 - result will go on node 2
							3. ...
					2. All keys on the disk are read and transfered to the appropriate nodes based on hashing
						1. This is done by the framework
				5. We can override handler to decide what to do with each key (operation is customizable)
					1. Sum
						1. Reduce handler is executed to find sums
					2. Concatenation
					3. Average
					4. ...
				6. The results are written as files on disk
					1. The files are stored on Hadoop as output
4. What have we achieved with map-reduce?
	1. We have taken a large set of files (each file being huge)
	2. Each file spread over multiple nodes
		1. We have GBs of data or TBs or PBs
	3. Map-reduce has done parallel processing (map) on the same node and the processed data is shuffled on the number of nodes configured (reduce) (grouping and aggregation) and we get the results
5. Map job:
	1. Filtering
		1. We write handler
	2. Transformation
		1. We write handler
6. Reduce job:
	1. Shuffles the map output across nodes
	2. Groups related info
	3. Computes aggregate data
		1. Custom logic is written in handler for aggregation

#### Why is Map-Reduce successful ####
1. It executes on nodes where the data is
	1. The amount of data we deal with in map phase is far more greater than the data we deal with in the reduce phase (in general)
		1. It is true if we can condense the info
			1. Example: Each record is a huge line in a log fine and we extract a small key/value pair
			2. The job for reduce phase becomes small
				1. Shuffling work also reduces
		2. We don't have to extract the data out of the nodes to process it
			1. Example: If we do it using JDBC call interacting with an RDBMS
				1. We need to run an SQL and feetch the data into memory & process it
					1. Alternative: Procedures
						1. Drawbacks: We cannot run the procedures in a distributed fashion on multiple nodes
					2. If we have data in multiple RDBMS on multiple nodes, we have to bring data into memory of the nodes where we want to do processing (application nodes)
						1. Drawback: **It is a huge amount of effort if we want to transfer that much amount of data**
			2. Alternative: Map-Reduce
				1. Code logic goes to each node
					1. Code is moved to the data
					2. Code processes the data in the same node, condense it, and move it around
					3. We bring logic to data & not data to logic
	2. It can work on multiple kinds of input and output
		1. Example:
			1. Input: HDFS
			2. Output: HDFS
		2. We can have other parallel sources of input
			1. Input: HBase/Cassandra
			2. Output: HBase/Cassandra
				1. Whichever has the ability to split the data across multiple nodes (at-least for map phase - data is huge)
		3. If output is small, we can use any data sync
			1. We can put our results on something on a single node

#### Intermediate Results ####
1. They will always be written on Hadoop cluster (where Map-Reduce is running)
	1. We can run Hadoop map/reduce only on Hadoop cluster
		1. Initial Input: HBase
		2. Final Output: Cassandra

#### Use-Case ####
1. Permanent storage to write huge amount of data, and we want to process the data as batch process
	1. Hadoop Map/Reduce is good choice

### Apache Spark ###
1. Topics:
	1. Evolution of Map-Reduce
		1. We can install Apache Spark on HDFS of Hadoop itself
			1. Instead of running native Hadoop Map-Reduce, we would run Apache Spark
				1. Why?
					1. Hadoop run:
						1. It reads from data nodes (disk) and brings it to memory
						2. After map function is done, data is written to disk
						3. Reduce reads data into memory
						4. Reduce does operation
						5. Reduce puts data back into disk
							1. Map - reads and writes once
							2. Reduce - reads and writes once
					2. Apache Spark:
						1. It does some operations in memory
						2. Reads data from HDFS
						3. Runs map operation
							1. Output is not written to disk
							2. Result set is maintained in memory
						4. The result set will be used by reduce operation
							1. Memory data structures will be shuffled
						5. Once reduce is done, it writes back to HDFS
							1. It is possible to do more operations
								1. Other operations: (can be done my modifying map and reduce handlers in Hadoop)
									1. Union
									2. Join
									3. GroupBy
								2. We don't have to write code for typical tasks to transform data
				2. The operation of reading from and writing to disk operations are avoided (intermediate steps)
					1. Only one read for input
					2. Only one read for output
	2. In memory
		1. 10x to 100x times faster
			1. Apache Spark is used instead of Hadoop's map-reduce
	3. DAG of operations (in Hadoop we can only model map followed by reduce)
		1. Multiple operations in a DAG
			1. We can construct graphs and Spark runs the graph for us
		2. Multiple inbuilt operations
			1. We can avoid writing code
	4. Interactive
		1. Interactive shell in Scala/Python/R
			1. To test any of the workflow of DAG
				1. We can take small data sets
				2. We can interactively execute
	5. In built libraries for (libraries are provided by Spark)
		1. SQL Interface
			1. Map-Reduce also has other interfaces
				1. Hive - provides SQL interface over map-reduce
					1. We can write SQL queries on Hive 
						1. Hive runs on top of Map-Reduce framework
							1. It converts SQL queries into map-reduce code and runs on Hadoop cluster
				2. Pig - scripting language to write map-reduce
			2. The tools provide convenient interface (we don't have to write map-reduce code in Java)
				1. We can write:
					1. SQL
					2. Pig script
		2. Machine Learning (library)
			1. We can run machine learning on Apache Spark
		3. Graph Processing (library)
		4. Streaming (library)
			1. If we want to process streaming input coming from Kafka
				1. Spark can read from Kafka and constructs micro-batches
					1. Reads a small amount of data from Kafka
					2. It will construct a batch
						1. Batch - DAG of operations (or map-reduce) is run
						2. It will run map-reduce and write the results
						3. It will go back to Kafka (huge number of records - whatever we can get in little time window)
						4. It will run map-reduce and write the results
							1. It is very quick
			2. Spark does micro-batching
				1. It has some overhead
2. Architecture

		Disk
		 | (HDFS read)
		iter,1
		 | (HDFS write)
		 v
		Disk
		 | (HDFS read)
		iter,2
		 | (HDFS write)
		 v
		Disk
		 |
		 .
		 .
		 .


		Disk (Input)
		 |
		iter,1
		 |
		 v
		Memory
		 |
		iter,2
		 |
		 v
		Memory
		 |
		 .
		 .
		 .

	1. Flow:

		Data 1		Data 2		Data 3		Data 4
		 |			 |			  |			  |
		 v			 v			  v			  |
		Map			Map			Reduce		  |
		 |			 |			  |			  |
		 |			 |			  |			  |
		 +-----------+			  |			  |
		 |						  |			  |
		 v						  |			  |
		Union					  |			  |
		 |						  |			  |
		 v						  |			  |
		Join <--------------------+			  |
		 |									  |
		 v									  |
		GroupBy <-----------------------------+
		 |
		 v
		Output

#### Use-Cases ####
1. If we want to run batch-processing for huge amount of data
	1. Consider Apache Spark (not Hadoop)

### Stream Processing ###
1. Topics
	1. Low Latency
		1. Keep data moving
	2. High throughput
		1. Multiple sources
	3. Event Issues
		1. Event delay
		2. Out-of-Order
		3. Missing
	4. Fault Tolerance
		1. Event Replay
	5. High Availability
	6. Processing Engine
		1. Storm
		2. Flink
		3. Spark (Micro-Batching)
	7. Buffer
		1. Kafka
2. Architecture

		Application
			Filebeat
			|
		    <> -tail-> Log
			|
			v
		Kafka
			|
			v
		Logstash
			|
			v
		ES/HDFS
			|
			+----+
			|    |
			v    v
		Kibana   SQL


		Application
			Filebeat
			|
			<> -tail-> Log
			|
			v
		Kafka
			|
			v
		Stream Processing
			|
			v
		Kafka
			|
			+----+----+
			|    |    |
			v    v    v
		Kibana  Email Storage

2. Stream processing delivers realtime results over any streaming data
	1. Example: Log data
		1. If logs are coming out of services, we want real-time analysis
			1. Say we want to detect fraud in a bank application
				1. Batch processing takes hours and days
					1. Solution: Stream processing
						1. If we want analysis of data on a realtime basis
					2. Batch flow:
						1. Logstash or Fluentd is used
							1. They cannot do distributed stream processing
								1. They can parse log events
								2. The log events can be individually transformed or aggregated within the same node
								3. **They have a flavor of stream processing**
									1. They can continously take input data and output processed data
										1. Drawback: **If we decide to put the data in ES or HDFS, it is not a streaming workflow**
											1. If data is going into HDFS or ES, we can do bulk processing when we accumulate enough data
												1. Graphical Interface
												2. SQL interface
									2. Why is putting in ES is also batch processing?
										1. **When we store data in ES, we don't do search on data we received moments ago** (search is on overall data)
											1. More agile for small queries (low latency)
												1. Seconds / minutes
													1. HDFS takes minutes and hours
										2. **If we need data that arrived few milliseconds or seconds ago, we don't have to store it in ES**
											1. Solution: The data is taken into stream-processing engine
												1. Could be logstash or fluentd
													1. If we have to aggregate data from multiple nodes and do processing, it is not possible with logstash or fluentd
														1. Alternative tools:
															1. **Storm**
															2. **Flink**
															3. **Spark streaming**
																1. Small batch process with small amount of data (micro-batching)
																	1. It has overhead
																		1. Not as efficient as native streaming processes
																			1. **Flink is the latest and popular**
						2. Distributed processing: - **Not possible with Logstash or fluentd**
							1. We process log events on different nodes
							2. We bring them to a node
							3. We aggregate
							4. We can diverge and converge for other operations
					3. Stream flow
						1. Once stream processor processes the data, we store them in Kafka
							1. Why?
								1. Destination sources may not be able to absorb the data if the data is coming at a high rate
									1. Stream processing engine can handle data at a very high rate
									2. Kafka can buffer the data that is arriving at a very high rate
						2. Destinations (Notification, real-time dashboards, archives) can process data at their own pace if they cannot handle the rate at which data is arriving in Kafka
							1. Otherwise, Stream processing engine can put the data directly into the destination

#### Challenges and Properties ####
1. Streams processing engine has to process the data with very low latency (milliseconds)
	1. It has to keep the data continously moving
		1. We keep some buffers on the input side and output side
			1. To handle peaks
	2. They are designed to handle data with extremely low latency
	3. They are designed to handle data with extremely high throughput
	4. They are designed to handle multiple engines which are streaming data
2. Stream processing engine must handle events that come after sometime which do not come immediately (they get delayed).
3. Stream processing engine must handle out of order events
	1. If event 2 comes before event 1, it needs to decide what to do
4. Stream processing engine must handle missing data
	1. Caveat: We need to write a lot of scripting and code to take care of these issues
		1. The framework makes it easy to handle these scenarios
			1. Handles fault tolerance
				1. If a node goes down on consumer side, input side, stream processing node, etc.
					1. The events will be replayed
			2. Handles high availability
				1. The engines are distributed
					1. Requirement to be used in production

#### Log data processing ####
1. We use stream processing if we need immediate analysis of log data

### Summary ###
1. Recap:
	1. Frontend
		1. Web applications
		2. CDN
		3. Load balancers
		4. Session cache
			1. Used to store sessions in memory
				1. It is much more scalable
					1. Multiple instances of the web-application can look at the common session cache
	2. Cache
		1. Redis
			1. Preferred
				1. New solution
					1. Persistence of cache
						1. If cache goes down, there is some fault tolerance
		2. Memcached
	3. Hosting
		1. Web-applications
			1. Jetty + Spring Boot - Java
			2. Node.js - JavaScript
	4. Static content storage
		1. AWS S3
		2. Google Cloud Storage
		3. (Any cloud vendor storage solution)
			1. Reasons:
				1. They are highly scalable
				2. They can be made available at multiple locations
		4. CDN - for serving content at global scale (for static content)
			1. Akamai
			2. AWS
				1. CloudFront
			3. Google
				1. Google Cloud CDN
			4. For on-premises and cloud
	5. Load Balancers
		1. Nginx
			1. Caching static content
		2. Apache
			1. Caching static content
		3. Cloud Load Balancers
	6. Middle Tier/ Service Tier
		1. Node.js
			1. JavaScript services
		2. Jetty/Tomcat
			1. Java
		3. Spring Boot (replacement for Jetty or along with Jetty)
			1. Java
	7. Service Caches
		1. Redis
		2. Memcached
	8. Message Queues
		1. RabbitMQ
			1. If scale is not too high, it has better features
				1. If scale is too high, it cannot handle
					1. It has good scalability
		2. Kafka
			1. If RabbitMQ cannot be a choice
			2. Handles very high scale
	9. Other services
		1. Discovery service
			1. Netflix Eureka
		2. Aggregator service
			1. Netflix Zuul				
		3. Embedded load balancers
			1. Netflix Hystrix
				1. Aggregator is a client to other services so we can use Hystrix load balancer
		4. Spring Cloud
			1. Provides a good integration with Netflix services & libraries
	10. OLTP Databases (for online transactions):
		1. RDBMS
			1. When scale is not too high
			2. When we need ACID transactions
			3. Options:
				1. PostgreSQL
				2. MySQL
		2. Distributed DBs
			1. For scalability
			2. If using DBs at different geographical locations
				1. Cassandra
					1. For high scalability
					2. For different geographic locations as well
					3. It trades-off consistency with availability
						1. If certain nodes are down, it is still available but not consistent
				2. HBase
					1. For high scalability
					2. Cannot be used for DBs that span different geographic locations
				3. MongoDB
					1. Document oriented DB
					2. Provides good scalability
					3. It is a distributed database
					4. Use-cases:
						1. When we need document oriented dbs and documents are in JSON format
		3. These databases are not good for analytics
	11. Analytics
		1. Un-structured data
			1. From logs
				1. Fluentd
				2. Logstash
					1. Collect logs from different machines and components and bring the logs to an unstructured storage
						1. For further analysis
			2. Unstructured storage
				1. Elasticsearch
					1. If search is the only thing we want to do
				2. Hadoop HDFS
					1. If want to do more than search
				3. We can put in both
					1. ES
					2. Hadoop HDFS (a general purpose data storage for unstructured data)
						1. Hadoop Map-Reduce OR
						2. Spark
							1. More evolved form of Map-Reduce
								1. Works in memory
		2. Data warehouse:
			1. Processed data can be stored in data warehouse
				1. We can bring other structured data from DB through ETL processes
					1. We can have one combined data in a data warehouse
			2. Options (they can do multi-processing for queries):
				1. Oracle
				2. Teradata
2. Summary:
	1. We have different layers
	2. We have different architectural concerns for the layers
	3. How different products can address the concerns
	4. Using the products and tools, understanding their strengths and weaknesses, we can build solutions
3. Where to apply the knowledge:
	1. When we are enhancing architecture of existing system
	2. When implementing a new solution from scratch

### Technology Stack Presentation Slides ###
1. [https://www.udemy.com/course/developer-to-architect/learn/lecture/26921744#overview](https://www.udemy.com/course/developer-to-architect/learn/lecture/26921744#overview)