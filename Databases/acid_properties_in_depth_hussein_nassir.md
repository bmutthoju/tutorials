# Relational Database ACID Transactions #
1. ACID: Atomicity, Consistency, Isolation, and Durability in RDBMS
	1. MySQL
	2. SQL Server
	3. PostgreSQL

## Properties ##
1. NoSQL: Consistency is compromised

## Agenda ##
1. What is a transaction?
2. Atomicity
3. Isolation
4. Consistency
5. Durability

## What is a Transaction? ##
1. It is a collection of queries
	1. One or more queries
2. Properties:
	1. The collection of queries is a single unit of work
		1. Example: Account deposit (SELECT, UPDATE, UPDATE)
3. We define when a transaction begins and when a transaction ends
	1. Commit - I am happy with my changes, so persist the changes
	2. Rollback - I think something went wrong so abort it in its entirety
4. Example:

		ACCOUNT_ID | BALANCE
		1          | $1000
		2          | $500
		
	1. Transaction:
		1. Send $100 from accoun 1 to account 2:
			1. BEGIN TX1
				1. SELECT BALANCE FROM ACCOUNT WHERE ID = 1;
				2. BALANCE > 100
				3. UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ID = 1
				4. UPDATE ACCOUNT SET BALANCE = BALANCE + 100 WHERE ID = 2
			2. COMMIT TX1

## Atomicity ##
1. All queries must succeed.
	1. If one fails all should rollback
2. Why is it important?
	1. Example we don't have atomicity:
		1. BEGIN TX1
			1. SELECT BALANCE FROM ACCOUNT WHERE ID = 1
			2. BALANCE > 100
			3. UPDATE ACCOUNT SET BALANCE = BALANCE - 100 WHERE ID = 1
			4. DB crashes
			5. DB is restarted
			6. After we restarted the machine the account has been debited but the other account has not been credited
				1. We have lost $100
	2. An atomic transaction is a transaction that will rollback all queries if one of the queries failed

## Isolation ##
1. Can my inflight transaction see changes made by other transactions?
	1. Is it okay?
		1. SE needs to adjust the knob
2. Read phenomena
	1. Lack of isolation gives read phenomena
3. Isolation levels
	1. DB can implement these to get rid of read phenomena

### Read Phenomena ###
1. Dirty reads
	1. I am in an in-flight transaction
	2. Some other transaction made a change
	3. The transaction did not commit the change
	4. I read the change
	5. The other transaction might roll-back the change
		1. We have read a bad/ dirty value (non-committed)
2. Non-repeatable reads:
	1. I read a value that has been committed (or not)
	2. I read the same value (with same or another query)
	3. I did not get the same result
		1. Reads are not repeatable
3. Phantom reads:
	1. Another transaction inserted a row which I picked up when it should not have been picked up
		1. Usually happens with range queries (?)
4. (Lost updates):
	1. I changed a value
	2. Another transaction over-wrote the value even before I committed by change
		1. I have lost the update
		
### Dirty Reads ###
1. Example: Sales table:

		PID			| QNT	| PRICE
		Product 1	| 10	| $5	
		Product 2	| 20	| $4
		
	1. Produce a report: With sum of sales:
		1. BEGIN TX1
			1. SELECT PID, QNT * PRICE FROM SALES
			2. ...
			3. SELECT SUM(QNT*PRICE) FROM SALES -- $155
		2. BEGIN TX2
			1. ...
			2. UPDATE SALES SET QNT = QNT + 5 WHERE PID = 1
	2. TX1 has read a dirty value that has never been committed.
		1. The result was supposed to be $130 but is $155
		
### Non-repeatable Read ###
1. There are use-cases where read needs to be repeated.
2. Example:

		BEGIN TX1					BEGING TX2
		SELECT PID QNT*PRICE
		FROM SALES					UPDATE SALES
			Product 1, 50			SET QNT = QNT + 5
			Product 2, 80			WHERE PID = 1
									COMMIT TX2
		SELECT SUM(QNT*PRICE)
		FROM SALES
			$155
			
		1. Bad result
			1. First read gave me $130
			2. Second read gave me $155
			
### Phantom Read ###
1. A new record is inserted:

		Product 3	| 10	| $1
		
		BEGIN TX1					BEGIN TX2
		SELECT PID, QNT*PRICE
		FROM SALES
			Product 1, 50			INSERT INTO SALES
			Product 2, 80			VALUES ('Product 3',10,1)
									COMMIT TX2
		SELECT SUM(QNT*PRICE)
		FROM SALES
			$140
			
	1. The first sheet of the report did not account for "Product 3" but the second sheet did
		1. We are getting extra rows
		2. A little harder to fix
			1. How to lock a new value?
				1. **Solution: Serialization isolation level**
				
## Isolation - Isolation Levels for Inflight Transaction ##
### Read uncommitted ###
	1. No isolation, any change from the outside is visible to the transaction
		1. We get dirty reads
		2. We get non-repeatable reads
		3. We get phantom reads
		4. We get lost updates
### Read committed ###
	1. Each query in a transaction only sees committed stuff
		1. Most databases implement this
		2. One of the best
			1. We are happy with committed stuff
		3. Each query sees only committed stuff at the time of the query
			1. Sometimes it is fine
### Repeatable read ###
	1. Each query in a transaction only sees committed updates at the beginning of transaction
		1. Once we begin the transaction, we see only the latest commits before we began the transaction
		2. Implementation:
			1. Some DBs implement versioning
				1. Cassandra
			2. When we start a transaction, I am in version 0
				1. Anything I read belongs to version 0 of the database
				2. Commits of other transactions will go to higher versions (version 1, 2, ...)
				3. It gives me a nice consistent view
			3. Some DBs implement it as a lock
				1. More expensive
					1. Exclusive lock: Don't allow any commits from other transactions
					2. Shared lock + Exclusive lock: Take shared lock so that no-one else can modify then acquire exclusive lock to make changes
						1. Blocks people from editing
							1. Pros: Ensures that all transactions see only the latest commits
							2. Cons: Degrades write performance
						2. Versioning comparison:
							1. Pros: Both read and write performance is higher than with the locks
							2. Cons: Transactions may not see the latest commits
					
### Serializable ###
	1. Transactions are serialized
		1. Easiest way to implement and is the slowest
		2. A transaction is followed by another transaction
			1. They mostly do not execute in parallel (even if they do, they guarantee that the changes comply with the serializable isolation level)
				1. DB does tricky things to run some of them in parallel
	2. Mostly this isolation level is implemented at the application level
		1. Application places a lock before beginning a transaction, commits it and then removes the lock.

## Performance ##
1. The performance degrades as we go down the isolation levels
	1. Read uncommitted - fastest
	2. Serializable - slowest
	
## Isolation Levels vs Phenomena ##

		Isolation Dirty reads Lost updates NR reads Phantom
		Read     
		un
		committed may occur   may occur    may occur may occur
		
		Read
		committed don't occur may occur    may occur may occur
		
		Repeatable
		reads      don't occur don't occur don't occur may
		
		Serializable don't     don't       don't       don't
		
## Consistency ##
1. Atomicity & isolation leads to consistency

### Consistency in Data ###
1. What is it?
	1. Defined by the user
		1. In table schema
		2. Example: Data in one view should be equal to the data in another view
			1. Sum of money in one table should be equal to the sum of balances in another
			2. Sum of likes of a picture must be equal to the number of users who liked the picture
	2. Referential integrity (foreign keys)
		1. Usually enforced by referential integrity
	3. Atomicity
		1. Ensured by atomicity
			1. **Lack of atomicity leads to inconsistency in data**
	4. Isolation
		1. Ensured by isolation
			1. **Lack of isolation leads to inconsistency**
				1. Sometimes lack of isolation might lead to corruption
					1. Not acceptable with bank transactions
					2. Picturs & picture likes is accepatable
						1. Pictures:
							1. ID (PK)
								1. 1
								2. 2
							2. BLOB
								1. xx
								2. xx
							3. LIKES
								1. 2
								2. 1
						2. Picture_Likes
							1. USER (PK)
								1. Jon
								2. Edmond
								3. Jon
							2. PICTURE_ID (PK)(FK)
								1. 1
								2. 1
								3. 2
					3. Based on consistency level we want, we can adjust
						1. Performance
						2. Isolation
						3. Scalability
					4. **We need to think about what we can give up**
						1. **We need to understand the requirement**

### Consistency in Reads ###
1. Sometimes it matters and sometimes it doesn't
2. What is consistency in Reads?
	1. If a transaction updates X in DB
	2. If same or another transactions reads X from DB, we must the the same result that was updated by previous transaction
3. Eventual consistency:
	1. If a transaction committed a change will a new transaction immediately see the change?
	2. Relational and NoSQL databases suffer from this
		1. The above mentioned consistency is unavailable in both relational and NoSQL databases
			1. Why?
				1. If there is only one server and we run transactions (with the best isolation level), we get consistent reads
				2. If we start adding more servers (read/write replicas)
					1. We can start pumping data to replicas
					2. We might need multiple replicas (to serve huge traffic)
					3. Let us say we implement leader/follower strategy
					4. The result is eventual consistency
						1. Why?
							1. We write to primary node
							2. Someone else reads from secondary node
								1. The new values takes time to get propagated to a secondary node
									1. Why? Network delay and hence latency	
						2. An old value might get read from a secondary node
	3. Eventual consistency
		1. NoSQL databases give up on consistency and give better scalability and performance
			1. Through horizontal scalability
		2. It is hard to implement distributed database algorithms with available relational databases so we could leverage NoSQL databases (We just add nodes and they will scale)
			1. Leader elections
			2. Replication
			3. Propagation of changes to replicas
			4. Scaling out or in
		3. Isolation is not possible with NoSQL
		4. **Both relational and non-relational databases suffer from inconsistency**

## Durability ##
1. What is it?
	1. Committed transactions must be persisted in a durable non-volatile storage
		1. If I lose power or database shut down, the value must be there
			1. Redis: Non-durable database
			2. Memcached: Non-durable database
2. Caching doesn't need to be durable


## NoSQL Databases ##
1. MongoDB, Cassandra:
	1. No Consistency
	2. No schema
		1. No Referential integrity
	3. No indexes
	4. ...
2. Redis, Memcached:
	1. No durability