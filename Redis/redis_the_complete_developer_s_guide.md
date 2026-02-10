# Redis: THe Complete Developer's Guide #
## Section 1: Get Started Here! ##
### Hello and Welcome! ###
1. Discord server

### Join Our Community! ###
1. [https://discord.gg/h2G3CbxPZA](https://discord.gg/h2G3CbxPZA)

### Course Resources ###
1. [https://www.diagrams.net/](https://www.diagrams.net/)
2. [https://att-c.udemycdn.com/2022-08-19_16-31-50-0226b21c91d5b91b8753561f7d424f20/original.zip?response-content-disposition=attachment%3B+filename%3Dredis-diagrams.zip&Expires=1768664363&Signature=6GcTX5UVZeolhmCNHu8no9NvJwcWm3gYf0nmWhORazqkdlLL0gPwz0JSbfRbkS-BOYf6CTcMzZJ75-t9T09ETvfy50qrxK38LH3LO4yspLTVOJ8HB7QpqrPTAtiREXvSY2LW0LWVmL4ykqenavKxHL80RMAtn7PBuKHqLw6KfZX2rx9IXKTYAl488zzWa8CzS85OOBgGqDMYVyeFSUrfHO873ngcMdut3-NqjhXyRk8JfonlIC--HS0v~nls46OC939dtVH4KdRp0kIE-M2f0TYkG6WQki5zYXcax8G3jLfSkY4yvhQmSeAUHrFn8Ot3v1UhxOePEMzmeXvb-Y1Z1Q__&Key-Pair-Id=K3MG148K9RIRF4](https://att-c.udemycdn.com/2022-08-19_16-31-50-0226b21c91d5b91b8753561f7d424f20/original.zip?response-content-disposition=attachment%3B+filename%3Dredis-diagrams.zip&Expires=1768664363&Signature=6GcTX5UVZeolhmCNHu8no9NvJwcWm3gYf0nmWhORazqkdlLL0gPwz0JSbfRbkS-BOYf6CTcMzZJ75-t9T09ETvfy50qrxK38LH3LO4yspLTVOJ8HB7QpqrPTAtiREXvSY2LW0LWVmL4ykqenavKxHL80RMAtn7PBuKHqLw6KfZX2rx9IXKTYAl488zzWa8CzS85OOBgGqDMYVyeFSUrfHO873ngcMdut3-NqjhXyRk8JfonlIC--HS0v~nls46OC939dtVH4KdRp0kIE-M2f0TYkG6WQki5zYXcax8G3jLfSkY4yvhQmSeAUHrFn8Ot3v1UhxOePEMzmeXvb-Y1Z1Q__&Key-Pair-Id=K3MG148K9RIRF4)

### Why Use Redis? ###
1. What is Redis?
	1. It is a database
		1. To store info
	2. How is Redis different?
		1. Redis is fast
			1. Storage and retrieval
		2. Why is Redis fast?
			1. All data is stored in memory
				1. Accessing data is fast
				2. Hard to work with dataset that is larger than the memory
			2. Redis organizes all its data in simple data structures
				1. Double linked list
				2. Sorted sets
					1. Efficient for storing unique sorted values
				3. the data structures have a very well known performance characteristics
					1. We can decide how information is organized in memory
					2. Helps efficiently query data
				4. Redis is very simple in nature (simple feature set)
					1. Very few features
						1. Other databases lay feature upon feature to make it easier to use
							1. Additional features have big performance penalties
	3. Learning Redis is different than learning other databases

### Initial Setup ###
1. Copy of Redis
	1. Two options:
		1. redis.com - free instance
			1. Recommended
				1. Sign up
					1. New subscription
						1. Fixed plans
							1. Subscription name: free-sub
							2. Create subscription 
					2. New database
						1. name: free-db
						2. Activate database
		2. Install + run on local computer

### A Touch More Setup ###
1. Run Redis commands manually
	1. Use rbook.cloud OR 
		1. Connect
			1. Copy and paste URL under Connect to free-db section
		2. Simple command:
		
		```
		SET key value
		```
		
	2. Run rbook on your local machine OR
	3. Use Redis-CLI

### Running RBook Locally ###
1. Pre-requisite: Node.JS
2. Run: `npx rbook`
3. Open: [http://localhost:3050](http://localhost:3050)
4. Any notebook created will be saved in the folder where we ran `npx rbook`

## Section 2: Commands for Adding and Querying Data ##
### Basic Commands ###
1. Commands save or retrieve data in Redis
2. Commands:

```
SET message "Hi there!"

GET message
```

	1. `message` - key
	2. `'Hi there'` - value
3. `SET` and `GET` are used to store and retrieve simple strings.
4. Other data types:
	1. String
		1. `SET`
		2. `GET`
		3. `APPEND`
	2. List - list of strings
		1. `LINDEX`
		2. `LLEN`
		3. `LINSERT`
	3. Hash 
		1. `HGET`
		2. `HSET`
		3. `HDEL`
	4. Set - set of strings
		1. `SADD`
		2. `SCARD`
		3. `SDIFF`
	5. Sorted Set - set of strings in a particular order
		1. `ZADD`
		2. `ZDIFF`
		3. `ZCOUNT`
	6. Bitmap - collection of booleans
		1. `BITOP`
		2. `BITCOUNT`
		3. `BITPOS`
	7. Hyperloglog - collection of booleans
		1. `PFADD`
		2. `PFCOUNT`
		3. `PFMERGE`
	8. JSON - nested json structure
		1. `JSON.SET` 
		2. `JSON.GET`
		3. `JSON.DEL`
	9. Index - internal data used for searching
		1. `FT.SEARCH`
		2. `FT.CREATE`
		3. `FT.PROFILE`

### Documentation on Commands ###
1. Commands for handling strings
	1. Getters (retrieve a value)
		1. `GET`
		2. `GETDEL`
		3. `GETRANGE`
		4. `GETEX`
		5. `MGET`
		6. `LCS`
		7. `SUBSTR`
	2. Setters (set a value)
		1. `MSETNX`
		2. `GETSET`
		3. `MSET`
		4. `SET`
		5. `APPEND`
		6. `SETEX`
		7. `SETNX`
		8. `SETRANGE`
		9. `STRLEN`
		10. `DEL`

### Quiz 1: Essentials of Commands ###
### Variations of SET ###
### Use Case of Expiration Options ###
### Setting Multiple Keys ###
### GET and MGET ###
### String Ranges ###
### Are These Commands Even Useful? ###
### Dealing with Numbers ###
### Again... Why do These Commands Exist? ###
### Completed Notes ###
### Using a Completed Notebook ###
### Exercises ###
### A Few Exercises ###
### Exercise Solutions ###

## Section 3: E-Commerce App Setup ##
### E-Commerce App Source Code Download ###
### Don't Skip This Video ###
### Redis Client Libraries ###
### First Implementation Task ###
### Redis Design Methodology ###
### Key Naming Methodology ###
### Adding Page Caching ###
### Better Key Generation ###

## Section 4: Local Redis Setup ##
### Installing on MacOS ###
### Installing on Windows ###

## Section 5: Hash Data Structures ##
### Hashes in Redis ###
### Storing and Retrieing Hashes ###
### Deleting Hash Data ###
### Numbers in Hashes ###
### Completed Notes ###

## Section 6: Redis Has Gotcha's! ##
### Slightly Unpredictable HSET and HGETALL ###
### Issues with HSET ###
### Issues with HGETALL ###

## Section 7: Powerful Design Patterns ##
### App Overview ###
### Reducing the Design to Queries ###
### What Data Type for Each Resource ###
### Quiz 2: When to use Hashes ###
### Construct User Implementation ###
### Serialization and Deserialization ###
### Adding Serialize ###
### Fetching a User ###
### Implementing Sessions ###
### Fetching a Saved Session ###
### Instantiating Sessions ###
### Serializing Data Times ###
### Storing Items ###
### Fetching a Single Item ###

## Section 8: Pipelining Commands ##
### Batching Commands with Pipelines ###
### Running Multiple Commands at the Same Time ###
### Executing a Pipeline ###

## Section 9: Enforcing Uniqueness with Sets ##
### Basics of Sets ###
### Union of Sets ###
### Intersection of Sets ###
### Difference of Sets ###
### Store Variations ###
### Checking for an Element in a Set ###
### Scanning a Set ###
### Completed Notes ###
### Most Common Use Cases of Sets ###

## Section 10: A Little Set Implementation ##
### Requiring Unique User Names ###
### Adding a Like System ###
### How to Count the Number of Likes? ###
### Updating Like Quantities ###
### Showing Liked Items ###
### Showing Common Liked Items ###

## Section 11: Organizing Data with Sorted Sets ##
### Sorted Sets ###
### Adding and Removing Members ###
### Finding a Range of Scores ###
### Removing the Highest and Lowest Members ###
### Updating Scores ###
### Querying a Sorted Set ###
### Completed Notes ###

## Section 12: Practice Time with Sorted Sets! ##
### Sorted Set Use Cases ###
### Reminder on the Auth Flow ###
### Storing Usernames ###
### Kind of Storing Strings in Sorted Sets ###
### Convering User IDs ###
### Plan for Showing Most Viewed Items ###
### Initializing Views on Item Creation ###
### Incrementing View Counters ###
### Items by Ending Soonest ###
### Querying for Ending Soonest ###

## Section 13: From Relational Data to Redis ##
### Loading Relational Data ###
### Relational Data with SORT ###
### The Sort Command ###
### Terminology Around Sort ###
### Specifying the BY Argument ###
### Joining Data with Sort ###
### A Few More Arguments ###
### Parsing SORT Output ###
### Completed Notes ###

## Section 14: HyperLogsLogs Structures ##
### HyperLogsLogs ###
### When to use HyperLogsLogs ###
### HyperLogsLogs in Action ###

## Section 15: Storing Collections with Lists ##
### Lists ###
### Reading and Writing Data to a List ###
### Ranges and Searches ###
### Trimming Lists ###
### Removing Elements ###
### List Use Cases ###
### Using Lists in Our App ###
### Serializing and Deserializing Bids ###
### Retrieving Bid Histories ###

## Section 16: More Practice with the E-Commerce App ##
### More on Bids ###
### Validating Bids ###
### Updating Items with Bids ###
### Issues with Bids ###
### Understanding Concurrency Issues ###
### Applying Atomic Updates ###
### Transactions ###
### Watching a Key with Transactions ###
### Isolated Connections for Transactions ###
### Solving Multiple Bids with a Transaction ###
### Items by Price ###
### More on Items by Price ###

## Section 17: Extending Redis with Scripting ##
### Lua Scripting ###
### Basics of Lua ###
### Handling Arrays ###
### Handling Tables ###
### Loading and Executing Scripts ###
### Providing Arguments ###
### Providing Key lists ###
### When to Use Scripts ###
### Custom Scripts with Node-Redis ###
### Lua Script Itegration ###
### Constructing a View-Incrementing Script ###
### Code Cleanup ###

## Section 18: Understanding and Solving Concurrency Issues ##
### Concurrency Revisited ###
### Issues with WATCH ###
### Overview of a Lock ###
### Understanding the Goal ###
### Implementing WithLock ###
### Using WithLock ###
### It Works! ###
### Automatically Expiring Locks ###
### Another Lock Issue ###
### Solving Accidental Unlocks ###
### Adding an Unlock Script ###
### One Last Issue ###
### Providing Expiration Signals ###
### Alternate Expiration Solution ###

## Section 19: Querying Data with RediSearch ##
### Redis Modules ###
### Redis Core vs Redis Stack ###
### Using Modules in Production ###
### Overview on Search ###
### Constructing an Using an Index ###
### Details on Indexes ###
### Index Field Types ###
### Numeric Queries ###
### Tag Queries ###
### Text Queries ###
### Fuzzy Search ###
### Prefix Search ###
### Pre-Processing Search Criteria ###

## Section 20: Search in Action ##
### Search Implementation ###
### The Constructing Index Function ###
### When to Construct the Index? ###
### Parsing the Search Term ###
### Executing the Search ###
### Seeding Some Fake Data ###
### RediSearch and TF-IDF ###
### Applying Weights to Fields ###
### Understanding Queries with EXPLAIN ###
### Query Performance with PROFILE ###
### Sorting and Searching ###
### Updating an Existing Index ###
### Executing the Search ###
### Deserializing Search Results ###

## Section 21: Service Communication with Streams ##
### Streams ###
### Use Case of Streams ###
### Adding Messages to a Stream ###
### Consuming Streams with XREAD ###
### Blocking Reads ###
### An XREAD Shorcut ###
### A Little Gotcha Around Streams ###
### Reading Streams with XRANGE ###
### Issues with Standard Streams ###
### Consumer Groups ###
### Constructing Groups in Action ###
### Claiming Expired Messages ###

## Section 22: Bonus! ##
### Bonus! ###