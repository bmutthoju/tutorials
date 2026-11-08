# Fundamentals of Database Engineering
## Section 1: Course Updates
### Welcome to the Course
1. Practical application of the concepts
2. Deep into DB engineering
3. Topics:
	1. ACID
	2. Indexing
	3. Concurrency control
	4. Partitioning
	5. Sharding
	6. Deep indexing ideas
	7. Application of the concepts - DB system design
	8. DB Engines (how is it different from DB systems)
	9. DB choices based on application
	10. QUIC
	11. Bloom Filter (own vs out of the box)
	12. System design
4. Intermediate to advanced

### Course Note 1
1. New section:
	1. DB application
	2. Advanced indexing
		1. Key vs non-key
	3. DB replication
		1. Examples

### Course Note 2
1. More content added
2. Content:
	1. Updates
	2. ACID
	3. Database Indexing
		1. Postgres EXPLAIN
	4. Partitioning
	5. Sharding
	6. Concurrency control
		1. Deadlock
		2. 2PC
	7. Replication
		1. Master, replicas
			1. Horizontal scalability
	8. B-Tree engines
	9. LSM Tree engines
	10. DB engines demos
	11. DB cursors
		1. Stateful vs stateless
		2. Client vs server
	12. DB security
	13. Homomorphic Encryption - Performing DB queries on encrypted data
		1. Store encrypted
		2. Key is with the user
		3. DB operations on encrypted data
	14. DB dicussions
		1. Distributed transactions
		2. SQL vs NoSQL

### Course Note 3
1. Prerequisites
	1. SQL
	2. Application development with DBs
2. Layer-by-layer
	1. Page
	2. Document
	3. ...
3. Efficient storage and retrieval
4. Q&A section

### Note about Docker
1. Two methods to connect
	1. Expose port to the host machine
		1. `-p 5555:80`
			1. Exposes port 80 in the container to the host machine
			2. It can be accessed as: `<hostname>:5555`
	2. Access docker container IP directly (not on mac)
		1. `docker inspect pg` (pg is the name of the container)
			1. Shows the IP address of the container
			2. Connection: `<ip>:80`

### Slides
1. Downloadable from 1st lecture of each section

## Section 2: ACID
### Introduction to ACID
1. ACID
	1. Atomicity
	2. Consistency
	3. Isolation
	4. Durability
2. Must understand the building blocks
3. Each property is critical to build DBs
4. Agenda
	1. What is a transaction?
	2. Atomicity
		1. Most important thing to guarantee consistency
	3. Isolation
		1. If we have multiple transactions at the same time
			1. What can they see?
			2. What should they not see?
	4. Consistency
		1. Unexpected result affects consistency
	5. Durability
		1. Some DBs sacrifice it for performance
		2. We we commit a transaction, it should be persisted in a non-volatile place
			1. Even if DB crashed
			2. Even if we lost power

### What is a Transaction?
1. Transaction:
	1. A collection of queries
		1. Treated as one unit work
		2. Example: Account deposit
			1. SELECT
				1. Read account
			2. UPDATE
				1. Deduct from account
			3. UPDATE
				1. Deposit money
	2. Transaction Lifespan
		1. `BEGIN` - starts new transaction
			1. None of the queries update the db here
		2. `COMMIT` - persists to disk
			1. How to do it?
				1. Run the queries in memory?
				2. Persist in disk temporarily?
		3. `ROLLBACK`
			1. Undoes all the work
				1. If we write in memory, we can flush the memory
			2. Transaction unexpected ending = `ROLLBACK` (e.g. crash)
				1. When the DBs are back, it must rollback
					1. DBs do them differently
						1. Each one optimizes for something
							1. COMMITs
								1. PostgreSQL
									1. They are fast
								2. If commits are slow, it can crash
							2. Crashes
	3. Nature of transactions
		1. usually transactions are used to change and modify data
		2. However, it is perfectly normal to have a read only transaction
			1. Example, you want to generate a report and you want to get consistent snapshot based at the time of transaction
				1. We will learn more about this in the isolation section

### Atomicity
### Isolation
### Consistency
### Durability
### ACID by Practical Examples
### Phantom Reads
### Serializable vs Repeatable Read
### Eventual Consistency
### Quiz 1: ACID Quiz

## Section 3: Understanding Database Internals
### How tables and indexes are stored on disk (MUST WATCH before continue)
### Row-Based vs Column-Based Databases
### Primary Key vs Secondary Key - What you probably didn't know
### Databases Pages (Article)

## Section 4: Database Indexing
### Construct Postgres Table with a million Rows (from scratch)
### Getting Started with Indexes
### Understanding The SQL Query Planner and Optimizer with Explain
### Bitmap Index Scan vs Index Scan vs Table Scan
### Key vs Non-Key Column Database Indexing
### Index Scan vs Index Only Scan
### Combining Database Indexes for Better Performance
### How Database Optimizers Decide to Use Indexes
### Construct Index Concurrently - Avoid Blocking Producting Database Writes
### Bloom Filters
### Working with Billion-Row Table
### How UUIDs in B+Tree Indexes affect performance
### Article - The Cost of Long running Transactions
### Article - Microsoft SQL Server Clustered Index Design
### Quiz 2: Indexing Quiz

## Section 5: B-Tree vs B+Tree in Production Database Systems
### B-Tree Section's Introduction & Agenda
### Full Table Scans
### Original B-Tree
### How the Original B-Tree Helps Performance
### Original B-Tree Limitations
### B+Tree
### B+Tree DBMS Considerations
### B+Tree Storage Cost in MySQL vs Postgres
### B-Tree Section's Summary

## Section 6: Database Partitioning
### Introduction to Database Partitioning
### Waht is Partitioning?
### Vertical vs Horizontal Partitioning
### Partitioning Types
### The Difference Between Partitioning and Sharding
### Preparing: Postgres, Database, Table, Indexes
### Execute Multiple Queries on the Table
### Construct and Attach Partitioned Tables
### Populate the Partitions and Construct Indexes
### Class Project - Querying and Checking the Size of Partitions
### The Advantages of Partitioning
### The Disadvantages of Partitioning
### Section Summary - Partitioning
### How to Automated Partitioning in Postgres

## Section 7: Database Sharding
### Introduction to Database Sharding
### What is Database Sharding?
### Consistent Hashing
### Horizontal partitioning vs Sharding
### Sharding with Postgres
### Spin up Docker Postgres Shards
### Writing to a Shard
### Reading from a Shard
### Advantages of Database Sharding
### Disadvantages of Database Sharding
### Database Sharding Section Summary
### When Should you consider Sharding your Database?

## Section 8: Concurrency Control
### Shared vs Exclusive Locks
### Dead Locks
### Two-phase Locking
### Solving the Double Booking Problem (Code Example)
### Double Booking Problem Part 2 (Alternative Solution and explanation)
### SQL Pagination with Offset is Very Slow
### Database Connection Pooling

## Section 9: Database Replication
### Introduction to Database Replication
### Master/Standby Replication
### Multi-master Replication
### Synchronous vs Asynchronous Replication
### Replication Demo with Postgres 13
### Pros and Cons of Replication

## Section 10: Database System Design
### Twitter System Design Database Design
### Building a Short URL System Database Backend

## Section 11: Database Engines
### Introduction
### Waht is a Database Engine?
### MyISAM
### InnoDB
### XtraDB
### SQLite
### Aria
### BerkeleyDB
### LevelDB
### RocksDB
### Popular Database Engines
### Switching Database Engines with mySQL

## Section 12: Database Cursors
### What are Database Cursors?
### Server Side vs Client Side Database Cursors
### Inserting Million Rows with Python in Postgres using Client Side Cursor
### Querying with Client Side Cursor
### Querying with Server Side Cursor
### Pros and Cons of Server vs Client Side Cursors
### Article - Server Side Cursor Types in SQL Server

## Section 13: NoSQL Architecture
### SQL vs NoSQL and how MongoDB Revolutionized NoSQL
### MongoDB internals
### MongoDB Clustered Collections
### MemCached In-Memory database Architecture
### Memcached NoSQL Architecture
### NoSQL Redis Internals
### CAP Theorem Explained

## Section 14: Database Security
### How to Secure Your Postgres Database by Enabling TLS/SSL
### Deep Look into Postgres Wire Protocol with Wireshark
### Deep Look Into MongoDB Wire Protocol with Wireshark
### What is the Largest SQL Statement that You can Send to Your Database
### Best Practices Working with REST & Databases
### Database Permissions and Best Practices for Building REST API

## Section 15: Homomorphic Encryption - Performing Database Queries on Ecrypted Data
### Introduction to Homomorphic Encryption
### What is Encryption?
### Why Can't we always Encrypt?
### What is Homomorphic Encryption
### Homomorphic Encryption Demo
### Clone and Build the Code
### Going Through the Code and the Database
### Searching The Encrypted Database
### Is Homomorphic Encryption Ready?

## Section 16: Answering your Questions
### Head Index scan instead of Index only scan why?
### What is the unit of the Cost in Postgres Planner?
### All Isolation Levels - Explained Details
### Snapshot and Repeatable Read isolation difference?
### I have an Index why is the database doing a full table scan?
### Why Databases Read Pages instead of Rows?
### How does Indexing a column with duplicate values work?
### Should I drop unused indexes?
### Why use serializable Isolation Level when we have SELECT FOR UPDATE?
### Can I use the same database connection for multiple clients?
### Do I need a transaction if I'm only reading?
### Wny does an update in Postgres touches all indexes?
### What is the value of bitmap index scan?
### What does Explain Analyze actually do?
### Postgres vs MySQL (The fundamental differences)
### Does Create Index block writes and Why?
### Postgres Process Architecture
### Index Scan vs Index Seek

## Section 17: Database Discussions
### WAL, Redo and Undo logs
### SELECT COUNT (*) can impact your Backend Application performance, here is why
### How Shopify Switched from UUID as Primary Key
### How does the Database Store Data On Disk?
### Postgres Architecture
### Is QUIC a Good Protocol for Databases?
### What is a Distributed Transaction?
### Hash Tables and Consistent Hashing
### Indexing in PostgreSQL vs MySQL
### Why Uber Moved from Postgres to MySQL (Discussion)
### Can NULLs Improve your Database Queries Performance?
### Write Amplification Explained in Backend Apps, Database Systems and SSDs
### Optimistic vs Pessimistic Concurrency Control
### Avoid SELECT *, even on a single-column tables
### Postgres Locks - A Deep Dive
### How Slow is select * in row store
### MySQL InnoDB Advanced Locking Techniques