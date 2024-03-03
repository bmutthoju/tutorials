# Aerospike #
## Architecture Overview ##
1. It is a **distributed**, **scalable** database
2. Objectives of the architecture:
	1. Flexible, scalable platform for web-scale applications
	2. **Robustness** and **reliability** (as in ACID) expected from traditional db
	3. **Operational efficiency** with minimal manual involvement
3. It has three layers:
	1. **Client layer**:
		1. Cluster-aware layer
		2. Includes open-source client libraries
			1. The libraries implement Aerospike APIs
			2. The libraries track nodes
			3. The libraries know where data resides in the cluster
	2. **Clustering and Data Distribution Layer**:
		1. The layer manages **cluster communications** and **automates** 
			1. fail-over
			2. replication
			3. **Cross-datacenter replication (XDR)**
			4. Intelligent re-balancing
			5. Data migration
	3. **Data Strorage Layer**:
		1. The layer reliably stores data **in DRAM** and **Flash** **for fast retrieval**

### Client Layer ###
1. Aerospike Smart Client is designed for speed
2. Implemented as open-source linkable library in
	1. C
	2. C#
	3. Java
	4. Node.js
	5. ... ([https://aerospike.com/download/#clients](https://aerospike.com/download/#clients))
3. Client layer:
	1. Implements 
		1. Aerospike API
		2. Client-server protocol
		3. Talks directly to cluster
	2. Tracks nodes & knows where data is stored
		1. It instantly learns of changes to cluster config or when nodes go up or down
	3. Implements its own TCP/IP connection pool for efficiency
		1. It also detects transaction failures not risen to the level of node failures in the cluster
			1. It re-routes the transactions to nodes with copies of the data
	4. Transparently sends requests directly to node with the data
		1. It re-tries or re-routes requests as needed
			1. Example: During cluster re-configurations
	5. Advantages of the architecture:
		1. Reduces transaction latency
		2. Offloads work from the cluster
		3. Eliminates work for the developers
		4. Ensures that applications do not have to restart when nodes are brought up or down
		5. We don't have to waste time with cluster setup or add cluster management servers or proxies

### Distribution Layer ###
1. "Shared nothing" architecture is used
	1. It is used to store terabytes of data with
		1. Automatic fail-over
		2. Automatic Replication
		3. Automatic Cross-Datacenter Replication (XDR)
2. The layer scales linearly
3. It is designed **to eliminate manual operations with systematic automation of all cluster management functions**
4. It has three modules:
	1. **Cluster Management Module:**
		1. Tracks nodes in the cluster
		2. The algorithm is **Paxos-based gossip-voting** process
			1. The algorithm determines which nodes are considered part of the cluster
		3. It implements special heartbeat (active & passive) to monitor inter-node connectivity
	2. **Data Migration Module**
		1. When we add or remove nodes, DB membership is assertained
		2. Each node **uses a distributed hash algorithm** to divide primary **index space into data slices** and **assign owners**
		3. The module intelligently balances data distribution across all nodes in the cluster
			1. **It ensures each bit of data replicates across all cluster nodes and datacenters**
				1. Specified in **system replication factor configuration**
		4. Division is purely algorithmic
			1. The system scales **without a master** and eliminates the need for additional configuration (as required in a sharded environment)
	3. **Transaction Processign Module**
		1. Reads and writes data on request
		2. **Provides consistency and isolation guarantees**
		3. The module is responsible for:
			1. **Sync/Async Replication**
				1. For writes with immediate consistency, it **propagates changes to all replicas before comitting the data and returning the result to the client**
			2. **Proxy**
				1. Used for rare cases
					1. During cluster re-config when client layer may be briefly out of date
						1. **Transaction processing module transparently proxies the request to another node**
			3. **Resolution of Duplicate Data**
				1. If clusters are recovering from partitioned (when restarting nodes say), the **module resolves conflicts between different copies of data**
					1. Resolution strategies:
						1. Based on generation count (version)
						2. Last update time
				2. We can setup [cross-datacenter replication](https://aerospike.com/docs/server/architecture/xdr) after the first cluster is up
					1. **Ensures that if a datacenter goes down, remote cluster takes over the workload with minimal or no interruption to users**

### Data Storage Layer ###
1. Aerospike is a key-value store with schemaless data model [https://aerospike.com/docs/server/architecture/data-model](https://aerospike.com/docs/server/architecture/data-model)
	1. Namespaces - similar to databases in RDBMS
	2. Sets - Data is subdivided into sets into each namespace (similar to tables in RDBMS)
	3. Records - (similar to RDBMS rows)
		1. Each record has a unique key which is indexed
	4. Bins - Each record has one or more bins (similar to RDBMS columns)
		1. Each bin holds a value associated with a record
	5. Sets and bins can be added at runtime (we don't have to pre-define them)
		1. **Values in bins are strongly typed**
			1. They can include support for any [data-type](https://aerospike.com/docs/server/guide/data-types/overview)
		2. **Bins are not typed**
			1. **Different records can have the same bin with values of different types**
2. **Indexes**
	1. For ultra-fast access, the following are stored by default in DRAM:
		1. [primary index](https://aerospike.com/docs/server/architecture/primary-index)
			1. It can also be configured to be stored in Persistent Memory or NVMe flash device
		2. Optional [secondary indexes](https://aerospike.com/docs/server/architecture/secondary-index)
3. Values can be stored in DRAM or cost-effectively on SSDs
	1. **Each namespace can be configured separately**
		1. Small namespaces can be stored in DRAM
		2. Large namespaces can be stored in SSDs (for cost benefits)
4. Data layer was designed for speed and provide dramatic reduction in hardware costs
	1. It can operate all in-memory
		1. Eliminates the need for caching layer
	2. **It can also take advantage of unique optimizations for flash storage**
		1. In both cases **data is never lost**
5. Advantages:
	1. 100 million keys take only upto 6.4 GB
	2. Keys have nto size limitations
		1. Each key is efficiently stored in 64 bytes
	3. **Native, multi-threaded, multi-core Flash I/O** & **Aerospike log structured file-system** take advantage of low-level SSD read and write patterns
		1. **To minimize latency, writes to disk are performed in large blocks**
			1. Mechanism bypasses standard file system (historically tuned to rotational disks)
	4. **Smart Defragmenter** and **Evictor** work together to ensure that **there is space in DRAM** and **data is never lost and always safely written to disk**
		1. **Smart Defragmenter**: Tracks the number of active records in each block and **reclaims blocks that fall below a minimum level of use**
		2. **Evictor**: Removes expired records and reclaims memory if the system gets beyond a set high-water mark
			1. Expiration times are configured per namespace
			2. Record age is calculated from the last modification
			3. Application can override the default lifetime and speicify that a record should never be evicted

### Operating Aerospike ###
1. Data is divided (distributed) between all servers in the cluster
	1. We cannot log onto a server to access all your data
2. We construct and manage the database
	1. Aerospike DB is the namespace

### Building Applications ###
1. Aerospike tools can be used to verify that the database is storing data correctly
	1. In prod dbs, data is distributed over the cluster
2. **We use smart client**
	1. It instantiates the application
	2. It is location aware and knows how to store and retrieve data without affecting performance
	3. After application compilation, Aerospike API libraries are included along with the Smart Client
		1. **Smart client is separate thread/process that monitors cluster state to determine data location**
			1. It **ensures that data is retrieved in a single hop**
	4. It allows application to ignore data distribution details

## Cross-Datacenter Replication (XDR) Architecture ##
1. XDR feature **asynchronously replicates cluster data over higher-latency links** (typically WANs)
2. Following is a high level architectural overview of Aerospike XDR

### Terminology ###
1. A remote destination is refered to as a datacenter
	1. Abbreviation used: DC (DC1, DC2, DC3, ...)
2. **The process of sending data to a remote datacenter is known as shipping**

### Configuring XDR ###
1. [Configure Cross-Datacenter XDR](https://aerospike.com/docs/server/operations/configure/cross-datacenter)

#### Replication Granularity: namespace, set, or bin ####
1. Replication is defined per datacenter
2. We can configure granularity of the data to be shipped
	1. Granularity:
		1. A single namespace or multiple namespaces
		2. All sets or only specific record sets
		3. All bins or a subset of bins

##### Shipping namespaces #####
1. Nodes can have multiple namespaces
	1. We can configure multiple namespaces to ship to different remote clusters
		1. DC1 -NS1,NS2-> DC2
		2. DC1 -NS3-> DC3
	2. We can configure different replication rules for different data sets

##### Shipping Specific Sets #####
1. We can configure XDR to ship certain sets to a datacenter
	1. Record shipping: Determined by a combination of namespace and set
2. **Use-case**
	1. **Sets are used if not all data in a namespace in a local cluster needs to be replicated in other clusters**

##### Shipping Bins #####
1. Only certain bins can be shipped (and ignore the rest)
	1. All bins are shipped by default
2. We can use `bin-policy` to decide which bins will be shipped

##### Shipping Record Deletes #####
1. From
	1. Clients
	2. Expiration or eviction by namespace supervisor (nsup)
2. Record deletes by clients are shipped by default
	1. Durable deletes are always shipped
3. Record deletes from expiration or eviction by nsup are not shipped by default

## Compression Disabled by Default ##
1. XDR does not compress shipment data by default
	1. Compression can be enabled to save bandwidth if necessary

## General Mechanism of XDR: Comparison of LUT and LST ##
## XDR Topologies ##
### Active-Passive Topology ###
### Mesh Topology (active-active) ###
### Star Topology ###
### Linear Chain Topology ###
### Hybrid Topologies ###
### Local Destination and Availability Zones ###
### Cluster Heterogeneity and Redundancy ###
## Failure Handling ##
### Local Node Failure ###
### Communications Failure ###
### Combination Failure ###

## Consistency ##
### Overview ###
1. Two possible configurations
	1. Available and Partition-Tolerant (AP)
	2. Consistent and Partition-Tolerant (CP)
		1. Referred to as Strong-consistency
			1. [Configuring Strong Consistency](https://aerospike.com/docs/server/operations/configure/consistency)

### High Availability Mode ###
### Strong Consistency Mode ###
1. **All writes to a single record will be applied in a specific order (sequentially)**, and **writes will not be re-recorded or skipped**
	1. Writes acknowledged as committed have been applied & exist in transaction timeline as opposed to other writes to the same record
		1. Applies even during network failures, outages, partitions
	2. Writes designated as "timeouts" (or "InDoubt" from client API) may or may not be applied
		1. If they are applied, they will be observed as such
2. Strong consistency guarantee is per-record
	1. **No multi-record transaction semantics**
	2. **Each record's write or update will be atomic and isolated**
		1. Ordering is guaranteed using a hybrid lock
3. Modes:
	1. **Full linearizable mode**
		1. It provides a single linear view among all clients that can observe data
	2. **Session Consistency mode**
		1. Guarantees that an individual process sess the sequential set of updates
	3. The policies can by chosen on read-by-read basis
		1. Allows few transactions that require a higher guarantee to pay extra synchronization price

...

#### Roster of Nodes ####
1. It is the list of nodes that are part of the cluster in steady state
	1. When all roster nodes are present & all partitions are current, cluster is in its steady state and provides optimal performance
2. Master and replica partitions are assigned to nodes in a cluster using a random assignment of partitions to nodes
	1. For strong-consistency:
		1. The partitions are referred to as roster-master and roster-replica
3. Replication factor of 2:
	1. One master
	2. One replica
4. **roster-replica**
	1. This refers to the node that would house the replica of a partition if all nodes in the roster were part of the singler cluster (cluster was whole)
5. **roster-master**
	1. This refers to the node that would house the master of a partition if all nodes in the roster were part of the single cluster (cluster was whole)
6. Rules applied to the visibility of partitions:
	1. ...

#### Full Partitions Versus Subsets ####
#### Strong Consistency for Reads ####
1. **With strong consistency setting, reads are always sent to the master partition**
2. ...

#### Linearizing Reads ####
1. To linearize reads at the server, every read to master partition needs to verify that the partition regimes are in sync for the partition in which the key is located
	1. If regimes agree, then read is guaranteed to be current
	2. If regimes do not agree, the cluster change may be in process and it is important to redo/retry the read from the client
2. **For every write, all copies of the partition written to need to have the same regime**

#### Session/Sequential Consistency ####
1. Read from master is the one needed (on server-side)
2. Client (library) stores
	1. Partition regime
	2. 32-bit partition counter

#### Relaxed Consistency ####
1. Two relaxed consistency modes: (**client will continue to read only committed records but reads will no longer be strictly monotonic**)
	1. **Allow replica**
		1. It is very rare that this policy will violate session consistency
		2. Applications won't see read timeouts which may occur when a node (or rack) goes down
		3. It enables clients to make use of the 'preferred rack' policy
			1. To reduce cross-zone network utilization in various cloud environments
	2. **Allow unavailable**
		1. Relaxes consistency further
			1. Allows clients to read previously committed records on partitions marked as unavailable
				1. Allows applications which are sensitive to read unavailability to continue to function during a major network/cluster disruption
				2. When partitions are available, the policy behaves exactly like 'allow replica'

## Understanding Asynchronous Operations ##
1. Topics:
	1. Asynchronous operations
	2. Why are asynchronous operations used
	3. The architecture
	4. How to program with async operations
2. Pre-requisites
	1. Aerospike DB running locally with Java Kernel & Aerospike Java Client
	2. For docker container: [https://github.com/aerospike-examples/interactive-notebooks](https://github.com/aerospike-examples/interactive-notebooks)

### Introduction ###
1. Topics:
	1. Benefits, design, and specifics of programming with asynchronous operations in Aerospike
2. **Aerospike provides asynchronous APIs for many operations**
3. Notebook tutorial
	1. Architecture and concepts
	2. Coding examples
4. Main topics:
	1. Execution models in Aerospike
	2. Benefits of async
	3. Key concepts
	4. Framework for async programming
	5. Coding examples

### Prerequisites ###
1. [Aerospike Notebooks - Readme and Tips](https://aerospike.com/developer/tutorials/python/readme_tips)
2. [Hello World](https://aerospike.com/developer/tutorials/java/hello_world)

### Initialization ###
#### Ensure Database is Running ####
1. Notebook code:

		import io.github.spencerpark.ijava.IJava;
		import io.github.spencerpark.jupyter.kernel.magic.common.Shell;
		IJava.getKernelInstance().getMagics().registerMagics(Shell.class);
		%sh asd

#### Download and Install Additional Components ####
1. Aerospike Java Client
2. Java Netty Package

		%%loadFromPOM
		<dependencies>
			<dependency>
				<groupId>com.aerospike</groupId>
				<artifactId>aerospike-client</artifactId>
				<version>5.0.0</version>
			</dependency>
			<dependency>
				<groupId>io.netty</groupId>
				<artifactId>netty-all</artifactId>
				<version>4.1.53.Final</version>
				<scope>compile</scope>
			</dependency>
		</dependencies>

#### Constants and Convenience Functions ####
1. Convenient functions:
	1. test
	2. async-ops

			final String Namespace = "test";
			final String Set = "async-ops";
			
			// truncate data, close client and event loops - called multiple times to initialize with different options
			// described in greater detail later
			void Cleanup() {
			    try {
			        client.truncate(null, Namespace, Set, null);
			    }
			    catch (AerospikeException e) {
			        // ignore
			    }
			    client.close();
			    eventLoops.close();
			};

#### Open a Terminal Tab ####
1. Executing shell commands:
	1. [aql](https://aerospike.com/docs/tools/aql)
	2. [asadm](https://aerospike.com/docs/tools/asadm)
2. File > Open > New > Terminal (in notebook)

### Synchronous, Asynchronous, and Background Operations ###
1. Application uses Aerospike client library (aka client) to interact with Aerospike Database
	1. Client sets up a connection to appropriate server node & sends in a request for execution in one of the following modes:
		1. **Synchronous**
			1. Request thread makes the request
			2. Request thread waits for the response
			3. Request thread processes the response upon arrival
		2. **Asynchronous**
			1. Request thread submits one or more requests
			2. Results are processed in one or more callback thread(s) as they arrive
		3. **Background**
			1. Request thread submits the request
			2. Operation (or task) is completed in the background
			3. Submission returns immediately
			4. Actual opation executes separately
			5. Application can check the completion status
				1. After it is completed, it may examine the results in the database with one or more separate requests
2. Background operation is a special type of asynchronous operation
	1. It is applicable only for updates in Aerospike

### Asynchronous Operations for Better Resource Efficiency ###
1. During the time when request is sent to a server and result arrives ("request latency"), client and application need not wait idly if a high throughput is the goal
	1. Solution: Concurrent requests can be sent for higher throughput
2. **Synchronous**
	1. Application can spawn multiple threads and process multiple requests in parallel
		1. One thread at a time
3. **Asynchronous**
	1. Application can process requests asynchronously by submitting them in parallel without waiting for the results
	2. Results are processed as they arrive in a different "callback" thread
	3. **Async request uses a dedicated connection to the server**
4. **Pipeline**
	1. Multiple requests could be sent over the same connection to the same server node
	2. Results can be received over the same connection
	3. Advantages:
		1. There is greater sharing of threads and connections across multiple requests
			1. **No support currently**
5. Advantages of Asynchronous model: **Asynchronous processing can be more resource efficient and can deliver better throughput than multi-threaded synchronous processing**
	1. Reasons: Threads have memory and CPU (context-switch) overhead
		1. Hence their number may be limited by the OS
6. Disadvantages of Asynchronous model: **It is more complex to program and debug**
7. Clients can perform different types of commands in a single instance
8. Advantages of Background operations:
	1. Superior throughput especially in a non-UDF invocation (?)

### Supported Asynchronous Operations ###
1. Most CRUD operations have async variant
	1. Single Record Operations
		1. add
		2. append
		3. delete
		4. apply(udf)
		5. get
		6. getHeader
		7. operate
		8. prepend
		9. put
		10. touch
	2. Batch operations
		1. exists (array listener and sequence listener)
		2. get (batch list and batch sequence listener)
		3. get (record array and record sequence listener)
		4. getHeader
	3. Query/Scan: Callback handles a series of records, a single record at a time
		1. query
		2. queryPartitions
		3. scanAll
		4. scanPartitions
	4. Metadata
		1. createIndex
		2. dropIndex
	5. Operational: info

### Execution Model ###
#### Application Call Sequence ####
### Understanding Event Loops ###
#### Event Loop Variants: Netty, NIO, EPOLL ####
### Async Framework ###
#### Initialize Event Loops ####
#### Initialize Client ####
#### Initialize Event Loop Throttles and Atomic Operation Count ####
#### Define Listener and Handlers ####
#### Submit Async Requests Using Throttling ####
#### Closing ####
### Nested and Inline Async Operations ###
### Misc Examples ###
#### Delay Queue Full Error ####
### Comparing Different Settings ###
### Takeaways and Conclusion ###
### Clean Up ###
### Further Exploration and Resources ###
#### Nest Steps ####