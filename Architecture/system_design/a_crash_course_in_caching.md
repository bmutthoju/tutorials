# A Crash Course in Caching - Part 1 #
## Introduction ##
1. It is a fundamental technique in computing that enables quick retrieval of frequently accessed data.
2. By storing frequently accessed data in faster storage (memory say), caching improves data retrieval speed and improves overall system performance.
3. Purpose:
	1. Impacts user experience => business success
4. List of topics:
	1. Cache
		1. What is cache?
			1. In memory storage
			2. Cache hit & miss
		2. Where is caching used?
			1. L1, L2, L3
			2. Page cache
			3. CDN
			4. Buffer cache
			5. Memcached
			6. Redis
		3. Cache deployment
			1. In-process cache
			2. Inter-process cache
			3. Remote cache
		4. Why do we need to cache?
			1. Improve performance
			2. Reduce latency
			3. Amdahl's law
			4. Pareto distribution
		5. Distributed cache
			1. Modules sharding
			2. Range-based sharding
			3. Consistent hashing
		6. Cache replacement and invalidation
			1. Cache replacement
				1. LRU
				2. LFU
				3. Allowlist policy
			2. Cache invalidation
				1. Active invalidation when modifying
				2. Active invalidation when reading
				3. TTL
		7. Cache strategies
			1. Cache-aside
			2. Read-through
			3. Write-around
			4. Write-through
			5. Write-back
		8. Caching challenges
			1. Thundering herd
			2. Cache penetration
			3. Big key
			4. Hot key
			5. Data consistency
		9. Monitoring & alerts

## What is a cache ##
1. Definition: In computing, a cache is a hardware or software component that stores data so that future requests for that data can be served faster; the data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere (Wikipedia)
2. Example:
	1. If there is no cache, client sends request to the service
	2. Service retrieves data from storage and sends it back to the client
		1. Problem: Retrieving data from storage can become slow and overloaded with high volumes of traffic
		2. Solution: Adding a cache
			1. When data is requested, service first checks cache for data
			2. If data is present in the cache, it is quickly returned to the service
			3. If data is not found in the cache, service retrieves it from storage, stores it in the cache, and responds to the client
				1. Allows for faster retrieval of frequently accessed data since cache usually stores data in memory in a **data structure optimized for fast access**
			4. Difference between cache systems and storage systems
				1. Cache system:
					1. Stores frequently accessed data in memory
					2. Have much smaller data capacity than storage systems (due to cost)
						1. => Cache systems can store only a subset of the total data set
					3. Data stored are not designed for long-term data persistence and durability
						1. Trade-off: Performance over durability
					4. Optimized for supporting heavy traffic and high concurrency
						1. Since data is stored in memory, cache server can respond quickly to incoming requests
							1. Crucial for high traffic websites
				2. Storage system:
					1. Stores data on disk
					2. Provide long term data persistence and durability (data is always available when needed)
						1. Trade-off: Durability over performance
					3. Better suited for durably storing and managing large amounts of data
			5. If data that is requested is available in the cache, it is called as a cache hit
				1. Otherwise a cache miss
				2. System overall operates more efficiently when there are more cache hits
					1. Effectiveness is measured by **cache hit ratio**
						1. cache hit ratio = number of cache hits / number of cache requests
							1. Higher the ratio, better the performance

## Where is caching used ##
1. Caching is used in modern computer & software systems
	1. Modern computers have multiple levels of cache (L1, L2, L3)
		1. These provide fast access to frequently used data for the CPU
	2. Memory Management Unit (MMU): Used to map virtual memory addresses to physical memory addresses
		1. MMU contains specialized cache called Translation Look Aside Buffer (TLB)
			1. It stores most recently used address translations to speed up address translation process
	3. OS uses page cache in the main memory (enhances overall system performance)
		1. Page cache stores frequently accessed data pages and reduces the number of disk accesses
2. Software systems
	1. Used to enhance performance & reduce network latency
		1. Browsers: Use cache to store frequently accessed website images, data, and documents
			1. Results in faster load times and smoother browsing experience
				1. Known as Browser Cache
	2. Content Delivery Networks (CDNs)
		1. A form of caching used to deliver static resources (images, videos, CSS files, other multimedia content)
		2. It is a geographically distributed network of proxy servers
			1. They work together to deliver content from the nearest server to the user's location
		3. Advantages: Reduces time taken to access the content, resulting in a faster-loading website
	3. Databases:
		1. Why caching? To improve performance, reduce execution overhead
		2. Caches:
			1. Buffer cache
			2. Result cache
			3. Query cache
			4. Metadata cache
			5. Session cache
		3. The caches store frequently accessed data blocks, query results, metadata, and session-specific information in memory
			1. Reduces disk reads
			2. Reduces query execution time
		4. Advantages:
			1. Faster query response times
				1. Better user experience
	4. Caching systems:
		1. Memcached & Redis
			1. Open-source, high performance, distributed caching systems
			2. Used to store and retrieve data quickly
		2. Use-cases:
			1. Storing historical emails locally (to avoid repeatedly pulling same data from server)
			2. Caching popular tweets on social media websites like Twitter
			3. Preloading & caching product information for flash sale systems (to prevent excessive database pressure)
3. Summary:
	1. Caching is effective for scenarios where:
		1. Data changes infrequently
		2. Data is accessed multiple times
		3. Same output is produced repeatedly
		4. Results of time-consuming queries or calculations
4. Topics:
	1. General caching use cases in system design
	2. Principles
	3. Strategies
	4. Problems
	
## A Crash Course in Caching - Part 2 ##
## Distributed Cache ##
1. A distributed cache stores frequently accessed data in memory across multiple nodes
	1. Cached data is partitioned across many nodes
		1. Each node stores only a portion of the cached data
	2. The nodes store data as key-value pairs
		1. **Each key is deterministically assigned to a specific partition or shard**
	3. When a client requests data, cache system retrieves data from appropriate node (reduces load on backing storage)
2. **There are different sharding strategies**
	1. Modulus
	2. Range-based
	3. Consistent hashing

### Modulus Sharding ###
1. Assigning of a key to a shard based on the hash value of the key modulo the total number of shards
	1. shard_no = h(key) % total_shards
2. Advantages:
	1. Simple
3. Disadvantages:
	1. Many cache misses when the number of shards is increased or decreased
		1. Why? Most of the keys will get re-distributed to different shards when the pool is re-sized

### Range-Based Sharding ###
1. Assigns keys to specific shards based on predefined key ranges
	1. System can divide the key space into specific ranges and then map each range to a particular shard
2. Use-cases:
	1. Useful in certain business scenarios where **data is naturally grouped or partitioned in specific ranges**
		1. Examples: Geolocation-based data, data related to specific customer segments
3. Disadvantages:
	1. Challenging to scale
		1. Number of shards is pre-defined and cannot be changed
			1. If the number of shards is changed, it requires redefining the key ranges and remapping the data

### Consistent Hashing ###
1. A widely-used sharding strategy
2. Advantages:
	1. It provides
		1. Better load balancing
		2. Better fault tolerance
3. Method:
	1. Both keys and nodes are mapped to a fixed-size ring using a hash function (to assign each key and node a position on the ring)
	2. When a key is requested, the system uses the same hash function to map the key to a position on the ring
	3. System then traverses the ring clockwise from that position until it reaches the first node
	4. The node is responsible for storing the data associated with the key
	5. Adding or removing nodes from the system only requires remapping keys that were previously stored on the affected nodes (instead of re-distributing all the keys)
		1. Easier to change the number of shards with a limited amount of data rehashed
4. [More about consistent hashing](https://www.toptal.com/big-data/consistent-hashing)

## Cache Strategies ##
1. Various cache strategies, characteristics, suitable use-cases
2. Classification:
	1. Read Strategies: Cache-Aside, Read-Through
	2. Write Strategies: Write-Around, Write-Through, and Write-Back

### Read Strategies ###
#### Cache-Aside ####
1. Lazy loading (popular)
	1. Application directly communicates with both the cache and storage systems
	2. Workflow:
		1. The application requests a key from the cache
		2. If the key is found in the cache (cache hit), the data is returned to the application
		3. If the key is not found in the cache (cache miss), the application proceeds to request the key from storage
		4. The storage returns the data to the application
		5. The application writes the key and correspoinding data into the cache for future reads
2. Advantages:
	1. Versatile
		1. Accommodates various use cases
		2. Adapts well to read-heavy workloads
3. Pros:
	1. System can tolerate cache failures, as it can still read from the storage
	2. Data model in the cache can differ from that in the storage (flexibility for a variety of use cases)
4. Cons:
	1. Application must manage both cache & storage (complicates the code)
	2. Ensuring data consistency is challenging due to lack of atomic operations on cache and storage
5. Dealing with data-consistency issues:
	1. If data is written to cache, and value in storage is updated afterward
	2. If data is written to storage, and data is written to cache afterward
		1. Stale data is read
			1. Solution: Set acceptable Time-to-Live (TTL) for each cached record
				1. Ensures that stale data becomes invalid after a certain period
			2. Solution: Stringent data freshness requirements
				1. Combine cache-aside with a write strategy

#### Read-Through ####
1. Cache serves as an intermediary between application and storage system (handles all read requests)
	1. Advantages: Simplifies application's role by delegating data retrieval responsibilities to cache
	2. Use cases: Read heavy workloads
		1. Implemented in cache libraries
		2. Implemented in standalone cache providers
2. Workflow:
	1. The application requests to read a key from the cache
	2. If the key is found in the cache (cache hit), the data is returned to the application
	3. If the key is not foud in the cache (cache miss), the cache requests the key from the storage
	4. The cache writes the key and associated data into the cache, and returns the data to the application
	
			Application
				|    ^
			read	 |
			request  |
				|    |
				v    |
				Cache



				Storage



				Application
				|			^
			1. read			|
			request			4. read from cache
				|			|
				v			|
					Cache		
				|			^
				|			|
			2. cache miss	3. read from storage
				|			|	& write to cache
				|			|
				v			|
					Storage
					
# A Crash Course in Caching - Final Part #
## Managing Operational Challenges in Caching ##
1. Tradeoff: Best caching strategy vs operational challenges
2. Topics:
	1. Common caching problems by category
		1. Insight into how to tackle the challenges effectively

### Reliability Challenges ###
1. Reliability is important to maintain stable system performance
	1. Reliability issues:
		1. Cache avalanche
		2. Cache stampede
		3. Cache penetration

#### Mitigating Cache Avalanche and Cache Stampede ####
1. Databases: Caching system maintains **high cache hit ratio** and **reducing traffic to storage systems**
	1. Under normal conditions, most read requests result in cache hits with small portions leading to cache misses
		1. By design, cache handles majority of the traffic
			1. Hence storage system experiences significantly less load
2. Cache avalanche & cache stampede:
	1. Those can occur in large-scale systems
		1. **Those can cause significant performance degradation or system-wide outages**
	2. **Cache avalanche**:
		1. Happens when multiple or all cache entries expire simultaneously or within a short time window. This condition can lead to a sudden surge in requests to the underlying data store
	3. **Cache stampede** (aka thundering herd):
		1. Occurs in large-scale systems when a sudden influx of requests overwhelms the system, causing performance degradation or system-wide outages
		2. Reasons:
			1. Cache misses on popular systems
			2. Sudden spike in user traffic
			2. Service restarts after maintenance
		3. What is the thundering herd problem?
			1. The "thundering herd problem" is a term used in computer networking to describe **a situation where a large number of client processes, such as user requests or network queries, all attempt to access a resource or server at the same time, overwhelming the server with traffic and causing a bottleneck or even a system crash**.
			2. This **problem can occur when multiple processes or applications are waiting for the same event or resource, such as a file, database record, or network service, and all try to access it simultaneously when it becomes available. As a result, the server may be unable to handle the sudden surge in traffic, leading to poor performance or even failure**.
			3. The term "thundering herd" is often used to describe the noise and chaos that ensues when a large number of animals, such as elephants or buffalo, stampede together in the wild. Similarly, in the context of computer networks, the sudden surge of traffic caused by a thundering herd can be highly disruptive and difficult to control.
3. When a cache or part of it fails, large number of read requests result in cache misses
	1. This can result in a massive influx of traffic to the storage system
		1. Sudden increase in traffic can reduce storage performance or even system crashes
			1. Failue of the cache serves as a trigger that combines elements of both cache avalanche and cache stampede => high stress situation for storage system
	2. High traffic events such as Black Friday sales on e-commerce sites in the US can also trigger the phenomena
		1. A single cache node might crash due to increased demand for popular keys
			1. This might cause the keys in the cache to be rehashed to another node
			2. This can result in the crash of another node as well
			3. This phenomena can eventually crash the entire cache system
4. **Solution**:
	1. To maintain stability and efficiency of large scale systems, implement strategies that mitigate the risks of both cache avalanche and cache stampede.
	2. The following techniques can alleviate the impact of cache avalanche and cache stampede

##### Staggered Expiration #####
1. Prevention of cache avalanche:
	1. Use **staggered expiration**: combine base time-to-live (TTL) value with a random delta
		1. Advantage: The approach spreads out the expiration times of cached entries
			1. Reduces likelihood of many items expiring at once
			
					k1 (TTL: 5 min + 20s)
					k2 (TTL: 5 min + 14s)
					k3 (TTL: 5 min + 28s)
					k4 (TTL: 5 min + 41s)
					k5 (TTL: 5 min + 3s)

##### Consistent Hashing #####
1. Can be used to distribute cache entries across multiple cache servers evenly
	1. Technique reduces the impact fo cache avalanche and cache stampede
		1. How? **Shares load among remaining servers and prevents single point of failure**

##### Circuit Breakers #####
1. Circuit breakers can help prevent cache avalanche & cache stampede from escalating into severe issues
	1.**They monitor system health and prevent overloading by stopping excessive requests to the cache and data store if system is under high stress**

##### Request Rate Limiting and Load Shedding #####
1. Request rate limiting & load shedding:
	1. They can address **cache stampede** by controlling the rate at which requests are processed and preventing the system from being overwhelmed
	2. Strategies (to maintain stability during high-load situation):
		1. Per-User
		2. Per-client
		3. System-wide

#### Addressing Cache Penetration Issues ####
1. Cache penetration:
	1. **Occurs when an application attempts to access non-existing data, bypassing the cache and leading to potential performance issues**
		1. How? When an application requests a non-existing key, it results in a cache miss, followed by a request to the storage system
			1. The storage system also returns empty result
		2. The above mentioned bypassing of the cache to readh the backing storage is called **cache penetration**
	2. If a large number of non-existent key requests occur, it can impact the performance of the storage layer and destabilize the overall system
	3. Use-case: If numerous users try to query non-existent orders on a website within a short period
2. Solution:
	1. Store a placeholder value in the cache to represent non-existent data
	2. Subsequent requests for the same non-existent data will hit the cache instead of data store
	3. Specify TTL for the placeholder entries to prevent them from occupying cache space indefinitely
	
						Application
			|			^			^			|
			1. read k3	|			|			|
			|			2. cache 	4. not		5. write k3 
			|				miss	|  found 	with null
			v			|			|			|
			Cache					|			v
			k1:v1						Storage
			k2:v2
			
	4. Advantage: Simple & effective
	5. Disadvantages: **It can consume significant cache resources if the application frequently queries a large number of non-existent keys**
		1. Solution: Bloom filter (a space efficient probabilistic data structure that tests whether an element belongs to a set)
			1. System can quickly identify non-existent data
				1. Reduces cache penetration & unnecessary data store requests
			2. Procedure:
				1. When a record is added to storage, its key is also recorded in bloom filter
				2. When fetching a record, the application first checks whether the key exists in the bloom filter
				3. If the key is absent, it wont exist in both cache and storage
				4. The application can return null value directly
				5. If the key is present in the boom filter, the application proceeds to read the key from the cache and storage
			3. Bloom filter sometimes returns a false positive
				1. A small number of cache reads will result in cache miss
			4. Challenge:
				1. Capacity limitations
					1. 1 billion keys with 1% false positive rate would require aprox 1.2 GB of capacity
						1. Suited for smaller data sets

### Traffic Pattern Challenges ###
#### Hot Key Problem ####
1. Hot key problem: When high traffic on a single key results in excessive traffic pressure on the cache node (potentially leading to performance issues)
	1. Keys are shared across different nodes based on a sharding strategy
		1. Traffic for each key can vary greatly, with some keys experiencing exceptionally high traffic
			1. Excessive traffic for keys could potentially exceed resource capacity of a node
		2. Use cases:
			1. Operational emergencies
			2. Festivals
			3. Sports games
			4. Flash sales
			5. ...
	2. Example: Tweets are distributed in the cache system by their IDs and a few of them become popular quickly
		1. The corresponding cache node experiences increased traffic (possibly surpassing its resource capacity)
2. Solution: Two steps
	1. Identify the hot keys
		1. For predictable events (important holidays, online promotions, ...)
			1. It is possible to evaluate potential hot keys beforehand
		2. For emergencies
			1. Advanced evaluation is not feasible
				1. Solution: Conduct real-time traffic analysis to promptly detect emerging hot keys
	2. Implement special measures for the keys to reduce traffic pressure
		1. Potential solutions:
			1. Distribute traffic pressure across the entire cache system
				1. Split "key12" into "key12-1", "key12-2",...,"key12-N"
				2. Distribute the N keys across multiple nodes
				3. When an application requests for a hot-key, it randomly selects one of the suffixed keys
					1. Enables traffic to be shared across many nodes and prevents a single node from becoming overloaded
				4. If many hot keys exist:
					1. Real-time monitoring can enable the cache system to expand quickly (reducing traffic impact)
				5. Last resort:
					1. Applications can store hot keys in **local cache**
						1. Decreases traffic to the remote cache system
							1. Alleviates pressure on the cache nodes & helps maintain overall system performance

#### Large Key Problem ####
1. What is large key problem?
	1. When value size of a key is significantly large, it can result in access timeouts, leading to the large key problem
2. Impact is very severe:
	1. Frequent access to large keys can consume significant network bandwidth, leading to slow lookup performance
	2. Any partial update of a large key will result in the modification of the entire value, contributing to performance issues
	3. If a large key becomes invalid or is evicted from the cache, **reloading it from storage can be time-consuming**, leading to additional slow query performance
