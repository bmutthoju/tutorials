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
	1. Use [https://rbook.cloud](https://rbook.cloud) OR 
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
			1. Returns a sequence of characters from an existing string
				1. Return all characters between first and 4th
				
				```
				SET model "toyota"
				GET model
				GETRANGE model 0 3
				```
				
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
			1. Change the string at 'color'
			2. Start replacing characters at index 2 with this string
			
			```
			SETRANGE color 2 blue
			```
			
			```
			SETRANGE model 2 blue
			GET model
			```
			
		9. `STRLEN`
		10. `DEL`
			1. Deletes a key (and all data associated with the key)
				1. Works with any data type (not just strings)
				
				```
				GET color
				DEL color
				GET color
				```

### Quiz 1: Essentials of Commands ###


### Variations of SET ###
### Use Case of Expiration Options ###
### Setting Multiple Keys ###
### GET and MGET ###
### String Ranges ###
### Are These Commands Even Useful? ###
1. Question:
	1. Why would we ever want to replace part of a string?
		1. Is it practical?
	2. Remember, one of the big draws of Redis is its performance (fast databse)
	3. We can use these basic operations to make much more complicated strings
		1. We can use them in creative ways
			1. To make systems extremely fast
2. Example:
	1. App is running extremely slow
		1. Your job: Use Redis to make accessign and updating data as fast as possible
			1. List of furniture products:
				1. id, type, color, material
					1. 1, couch, brown, leather
					2. 2, table, red, wood
					3. 3, chair, green, plastic
		2. Assume that there are incredibly many users writing and reading to Redis
	2. How are people accessing data?
		1. User interacts with the list in four ways
			1. Fetch one to three properties of a single item
			2. Update one to three properties of a single item
			3. Fetch all properties related to several items
			4. Construct several items
		2. We have come to know that there are a limited number of types, colors (10), and material (5)
			1. The data is repetetive
				1. We can encode each value
					1. red -> a
					2. green -> b
					3. ...
				2. Repeat for types and materials
					1. We get an encoded datasets
		3. Store them as plain strings in Redis
			1. `item:1` -> `aqg`
			2. `item:2` -> `gbo`
			3. `item:3` -> `eec`
		4. Implementing operations:
			1. Fetch one to three properties of a single item:
				1. `GETRANGE item:1 0 2`
					1. Returns `aqg`
			2. Update one to three properties of a single item
				1. `SETRANGE item:1 0 0 bcd`
			3. Fetch all properties related to several items
				1. `MGET item:1 item:2 item:3`
			4. Construct several items
				1. `MSET item:4 trq item:5 nzq`
		5. The operations run extremely fast
			1. Compared to traditional DB

### Dealing with Numbers ###
1. We can use the same commands for numbers
	1. `SET <num>`
2. Specific commands for numbers:
	1. `DECR` - decrease
	2. `DECRBY` - decrease by
	3. `INCRBYFLOAT` - increase by
	4. `INCRBY` - increase by
	5. `INCR` - increase
3. Using number-specific commands on strings throws error
4. Storage:

```
SET age 20
```

	1. Stored as "20" (string)
		1. Needs parsing string to a number
5. Commands:
	1. `INCR`
		1. Adds 1 to the number stored at key
	2. `DECR`
		1. Subtracts 1 from the number stored at key
	3. Examples:
	
	```
	SET age 20
	INCR age
	DECR age
	```
	
	4. `INCRBY`
		1. Adds an integer to the number stored at key
		2. Example: `INCRBY age 10`
	5. `DECRBY`
		1. Subtracts an integer from the number stored at key
		2. Example: `DECRBY age 10`
	6. `INCREBYFLOAT`
		1. Adds a float to the number stored at key
		2. Example: `INCRBYFLOAT age 6.34534`

### Again... Why do These Commands Exist? ###
1. What do the commands do?
	1. `INCR` - It is doing three things simultaneously (atomic)
		1. If we use multiple commands:
			1. `GET upvotes`
				1. Comments, say
			2. Parse it into a number
			3. Add 1 in app
			4. `SET upvotes`
		2. Problems:
			1. Making two roundtrips to Redis (latency is twice)
			2. If we recieve two requests at exactly the same time
				1. To upvote a post (two simultaneous requests)
					1. Race-condition
						1. Two servers read the same value
						2. Both servers increase the value
						3. Both servers store the updated value
				2. Solution:
					1. Use a Redis transaction with 'WATCH'
					2. Use a lock
					3. Use `INCR`
						1. Simplest solution
							1. Redis processes all commands synchronsously - one at a time (it is single-threaded)
								1. One request is processed at a time
								2. No need for synchronization

### Completed Notes ###
1. [Basic Strings - Completed](https://www.udemy.com/course/redis-the-complete-developers-guide-p/learn/lecture/32529060#content)

### Using a Completed Notebook ###
1. RBook - we can make notes
	1. File has notes and extra documentation.
	2. Drag and drop

### Exercises ###
### A Few Exercises ###
### Exercise Solutions ###

```
SET shape triange NX
GET shape
SET news "Today's Headlines" EX 3
SET news "Today's Headlines" PX 3000
```

## Section 3: E-Commerce App Setup ##
### E-Commerce App Source Code Download ###
1. rbay.zip
	1. Download

### Don't Skip This Video ###
1. Setup
	1. App Setup
		1. We are going to build an ecommerce app throughout the course.
		2. I built the frontend portion for you
		3. The frontend needs to be installed
	2. Installation:
		1. Node JS setup: [nodejs.org/en/download/](nodejs.org/en/download/)
		2. Extract the **rbay.zip** file (download from the lecute right before this)
		3. At the terminal, run `npm install` inside the project directory
		4. Add connection info to the **.env** file (from redis.com)
		5. Start the project up by running `npm run dev`

### Redis Client Libraries ###
1. Architecture:

```
App Server
[Language-Specific Redis Client Library]
  |
  v
Redis
```

	1. Language-Specific Redis Client Library
		1. Gives you a set of functions to call instead of writing commands manually
		2. Examples: Node JS 'node-redis' library
			1. `GET color`
				1. `client.get('color');`
			2. `SET color red`
				1. `client.set('color', 'red');`
			3. `SET color red EX 2 GET`
			
			```
			client.set('color', 'red', {
			  EX: 2,
			  GET: true
			});
			```
			
	2. Many SQL libraries let you use a DB without really understanding the underlying DB
		1. We don't need SQL
	3. Redis client libs
		1. The exact underlying command is being executed
		2. The official command docs are frequently more helpful than the library docs
			1. [redus.io/commands](redus.io/commands)
				1. Raw commands must be understood to use the libraries
		3. Some libraries have zero docs on individual commands
2. [redis.js.org](redis.js.org)
	1. node-redis
3. Jedis - Java client library
	1. `set(String key, String value, SetParams params)`
		1. There is Javadocs
			1. Need to refer to official docs to understand the details

### First Implementation Task ###
1. Architecture:

```
// SwelteKit Server
User - Request -> [Figure out what page the user is trying to view]
                  [Run a bunch of JS code to generate HTML] // relatively slow
				  [Send response back to user]
	<- HTML document -
```

	1. Server-side rendering
2. Architecture - improved

```
User - Request -> [Figure out what page the user is trying to view]
                  [See if this page has already been rendered and stored in Redis] -> Redis
				  [Yes? Send response] [No? Render page]
                  [Store result in Redis for future use]
				  [Send response back to user]
	<- HTML document -
```

	1. HTML page stored in Redis
		1. Rendering will not be repeated
			1. key: page 
			2. value: `<html>...</html>`

### Redis Design Methodology ###
1. SQL Database Design Methodology
	1. Put the data in tables.
	2. Figure out how we will query it.
2. Redis Design Methodology (reverse)
	1. Figure out what queries we need to answer
		1. Example: Store and lookup a page
	2. Structure data to best answer those queries
3. Design considerations:
	1. What type of data are we storing?
		1. Strings
	2. Should we be concerned about the size of data?
		1. One per user?
		2. Every page?
		3. etc.
			1. There is an upper-bound (for a single instance)
				1. Data is stored in memory
		4. Pages:
			1. Custom pages (different pages for different users and for the same user at different times)
				1. Each user sees something different or new content every view (user might want different data for each page)
					1. Landing
					2. Auction creation
					3. Auction search (data might change)
					4. Dashboard
					5. Auction show (data might change)
					6. User profile
				2. Not good candidates for caching
			2. Static pages
				1. Every user sees same content and page doesn't change often
					1. Contact
					2. About us
					3. Sign in
					4. Sign up
				2. Good candidates for caching
			3. Size requirements:
				1. 57.1 kb per page
					1. Custom pages: .334 MB per user
					2. Static pages: .22 MB for all users
		5. YES
			1. Only cache certain pages
	3. Do we need to expire this data?
		1. Yes, expire after some number of minutes/hours/days
	4. What will the key naming policy be for this data?
		1. Next
	5. Any business-logic concerns?
		1. No

### Key Naming Methodology ###
1. Key naming
	1. Keys should be unique
	2. Other engineers should understand what a key is for
	3. Tip - use functions to generate your key names so you never make a typo
	4. Extremely common practice is to use a ':' to separate different parts of the key
		1. `users:45` (45 - id)
		2. `items:19`
		3. `users:posts:901` (901 - id)
		4. `posts:jqip25jnm`
	5. Small twist on common practice
		1. We are going to use a # before unique ID's to make implementing search easier
			1. `users#45`
			2. `items#19`
			3. `users:posts#901`
			4. `posts#jqip25jm`
				1. Makes search easier
2. Convention
	1. `pagecache#/about` - route
	2. `pagecache#/privacy`
	3. `pagecache#/auth/signin`
	4. `pagecache#/auth/signup`

### Adding Page Caching ###
1. `getCachedPage`
	1. Is the 'route' argument in the list of routes we want to cache?
	2. If so, get the cached page from redis
	3. If not, return null
		1. List of routes to cache
			1. ['/about', '/privacy', '/auth/signin', '/auth/signup']
2. `setCachedPage`
	1. Is the 'route' argument in the list of routes we want to cache?
	2. If s, store the page in Redis
3. Code:

```typescript
import { client } from '$services/redis';

const cacheRoutes = ['/about', '/privacy', '/auth/signin', '/auth/signup'];

export const getCachedPage = (route: string) => {
	if (cacheRoutes.includes(route)) {
		return client.get('pagecache#' + route);
	}

	return null;
};

export const setCachedPage = (route: string, page: string) => {
	if (cacheRoutes.includes(route)) {
		return client.set('pagecache#' + route, page, {
			EX: 2
		});
	}
};
```

### Better Key Generation ###
1. Generating keys using functions
2. src/services/keys.ts

## Section 4: Local Redis Setup ##
### Installing on MacOS ###
1. Two different versions:
	1. Redis
		1. Redis database
	2. Redis Stack
		1. Redis database
		2. Additional modules that extend the functionality of Redis
2. Redis Labs: `Redis stack`
3. Install directions:
	1. [https://redis.io/docs/stack/get-started/install/mac-os/](https://redis.io/docs/stack/get-started/install/mac-os/)
		1. Install homebrew: [https://brew.sh/](https://brew.sh/)
		2. Run: `brew tap redis-stack/redis-stack`
		3. Start Redis: `redis-stack-server`
		4. Run CLI: `redis-cli`
4. Connecting app to local instance:
	1. `.env`
	
	```
	REDIS_HOST=localhost
	REDIS_PORT=6379
	REDIS_PW=
	```
	
5. To connect RBook to local copy of Redis:
	1. Run RBook locally
		1. `npx rbook`
		2. Open: localhost:3050
		3. Open connection settings window
		4. Host: localhost
		5. Port: 6379
		6. Password: 
	2. Notebooks will be saved in the directory where `npx rbook` was executed

### Installing on Windows ###
1. Installation steps:
	1. [https://redis.io/docs/stack/get-started/install/docker/](https://redis.io/docs/stack/get-started/install/docker/)
		1. Install Docker Desktop: [https://docs.docker.com/desktop/windows/install/](https://docs.docker.com/desktop/windows/install/)
		2. Run: `docker run -d --name redis-stack-server -p 6379:6379 redis/redis-stack-server:latest`
		3. CLI: `docker exec -it redis-stack-server redis-cli`

## Section 5: Hash Data Structures ##
### Hashes in Redis ###
1. It is a nested key-value structure
2. Use-cases:
	1. Information about records or entitites inside the application
		1. name: alex
		2. password: ...
		3. post#9:
			1. title: A Blog Post
			2. content: Everything about...
		4. image#1:
			1. url: http://...
			2. createdAt: 2000-02-02
3. We cannot have deeply nested key-value pairs
4. The values can be only strings or numbers
5. Commands:
	1. `HSET`
	2. `HGET`
	3. `HDEL` **(M)**
	4. `HEXISTS` **(M)**
	5. `DEL`
	6. `HGETALL`
	7. `HINCRBY`
	8. `HINCRBYFLOAT`
	9. `HMSET`
	10. `HSETNX`
	11. `HSTRLEN`
	12. `HVALS`

### Storing and Retriveing Hashes ###
1. Example:
	1. `HSET`
		1. `company` -> Name of the key to store this hash at
			1. `name`: First k-v pair
			2. `Company Co`: Value of first k-v pair
			3. `age`: Name of second k-v pair
			4. `1915`: Value of second k-v pair
2. Commands:
	1. `HSET company name 'Concrete Co' age 1915`
		1. `HSET <hash-name> <key> <value> <key> <value> ...`
	2. `HGET company name`
	3. `HGETALL company` **(M)**
		1. We get back: `["name","Concrete","age",1985]`
			1. Programming language may have to parse the array

### Deleting Hash Data ###
1. `HEXISTS` **(M)**
	1. If key exists
	2. Returns 1 or 0
2, `DEL` - Deletes a hash stored at a key
	1. `DEL company`
3. `HDEL` - Deletes a single key-value pair stored in a hash
	1. `HDEL company age`

### Numbers in Hashes ###
1. `HINCRBY`
	1. Allows us to add an integer to an existing number in a hash
	2. `HINCRBY company age 10` (add 10 to `age` value)
	3. If a key doesn't exist, it will be created and the value specified is stored
	4. `-15` - decrements
2. `HINCRBYFLOAT`
	1. `HINCRBYFLOAT company age 1.004`
3. `HSTRLEN` **(M)**
	1. Get the length of a string stored in a hash. Returns 0 if no string is set
		1. Use-case: ?
4. `HKEYS` **(M)** - get all keys of a hash
5. `HVALS` **(M)** - get all values of a hash

### Completed Notes ###
1. [https://www.udemy.com/course/redis-the-complete-developers-guide-p/learn/lecture/32529100#content](https://www.udemy.com/course/redis-the-complete-developers-guide-p/learn/lecture/32529100#content)

## Section 6: Redis Has Gotcha's! ##
### Slightly Unpredictable HSET and HGETALL ###
1. Topics:
	1. Most common commands - `HGETALL`, `HSET`
	2. Some behaviors are a little unexpected
2. Code:
	1. `sandbox/index.ts`
	
	```
	const run = async () => {
	  await client.hSet('car', {
	    color: 'red',
		year: 1950
	  });
	  
	  const car = await client.hGetAll('car');
	  console.log(car);
	}; // HSET car color red year 1950
	```
	
	2. Terminal
		1. `npm run sandbox`

### Issues with HSET ###
1. Code:

```
  engine: { cylinders: 8 };
  owner: null,
  service: undefined
```

	1. Error message:
		1. `Cannot read properties of null ...`
			1. For `owner: null`
				1. Why?
					1. `HGETALL car color 'red' year 1950 engine '{cylinders:8}' ...
						1. `'red'.toString()` (method is called on each value)
						2. `1950.toString()`
						3. ...
						4. `{cylinders:8}.toString()` - (Object object)
						5. `null.toString()` - error
	2. Solution:
		1. Workaround:
		
		```
		owner: null || '',
		service: undefined || '',
		```

### Issues with HGETALL ###
1. Let us say we don't have a car with an id
	1. It doesn't return `null`
		1. `HGETALL` returns an empty object
			1. We cannot check of object or null

## Section 7: Powerful Design Patterns ##
### App Overview ###
1. Topics:
	1. Deep walkthrough of the ecommerce app we're building
	2. Do some design work on how we're going to store data in Redis
	3. Figure out what data should be stored as hashes
	4. Write code!
2. Basic auction rules
	1. Users add 'items' to sell
	2. Items have a starting price and an ending time
	3. Other users can 'bid' on an item. A bid must be higher than all previous bids
	4. At the ending time, the user with highest bid wins the item
3. Mock ups
	1. Carousels
		1. If a user logs in an views an item, only one view is counted (even after refreshes)
		2. Types:
			1. Most expensive items to least expensive
			2. Types
			3. Most views
	2. Sign-in page
	3. Sign-up page
	4. Links:
		1. Dashboard
		2. New
		3. Logout
	5. Auction:
		1. Item name
		2. Description
		3. Duration
	6. Item show page
		1. Image
		2. Title
		3. Link to seller's profile page
		4. Product description
		5. Like the item
		6. Highest bid
		7. Number of bids
		8. Time left
		9. Form to place a bid
		10. Chart to show how the price has changed over time
		11. Similar items
	7. Seller profile
		1. Items the other user is selling
		2. Items the user liked
		3. Items both liked
	8. Dashboard
		1. to view all the items we are selling
4. We assume that millions of products will be actively sold
	1. We need pagination

### Reducing the Design to Queries ###
1. Design:
	1. SQL Database Design Methodology
		1. Put the data in tables
		2. Figure out how we will query it
	2. Redis Design Methodology
		1. Figure out what queries we need to answer
			1. What data do we need to fetch?
			2. What changes do we need to make?
		2. Structure data to best answer those queries
2. SQL Database
	1. users
	2. views
	3. likes
	4. bids
	5. items
3. What queries do we need to answer?
	1. Landing page:
		1. items sorted by price
		2. items sorted by ending time
		3. items sorted by views
		4. Search for items by name
	2. Sign in
		1. Find a user with given user name
		2. Instantiate a session (auth)
		3. Find a session (auth)
		4. Get a user with a given ID (auth)
	3. Sign up
		1. Construct a user
	4. Item
		1. Construct an item
	5. Item show
		1. Fetch an item with a given ID
		2. Find the # of likes tied to an item
		3. Like an item
		4. Unlike an item
		5. See if current user likes an item
		6. Construct a bid tied to an item
		7. Find the bid history of an item
		8. Find items similar to an existing item
		9. Increment the number of views for an item
	6. Seller profile
		1. Find items a user likes
		2. Find items two different users both like
	7. Dashboard
		1. Find items instantiated by a user, sorted by various criteria
4. SQL database gives more flexibility than Redis
5. Operations:
	1. Reads
		1. Find items a user likes
		2. Items sorted by price
		3. Items sorted by ending time
		4. Items sorted by views
		5. Search for items by name
		6. Find items added by a user, sorted by various criteria
		7. Find items similar to an existing item
		8. Find a session (auth)
		9. Fidn a user with given user name
		10. Find items two different users both like
		11. Find the bid history of an item
		12. Fetch an item with a given ID
		13. Fetch the # of likes tied to an item
		14. See if current user likes an item
		15. Find a user with a given ID
	2. Writes
		1. Unlike an item
		2. Like an item
		3. Instantiate a session (auth)
		4. Instantiate a big tied to an item
		5. Increment the number of views for an item
		6. Construct an item 
		7. Construct a user
6. Things in our app
	1. users
	2. sessions
	3. items
	4. bids
	5. views
	6. likes

### What Data Type for Each Resource ###
1. When to use a hash?
	1. Reasons to store as hash
		1. The record has many attibutes
			1. item
				1. image url
				2. title
				3. description
				4. price
				5. ...
		2. A collection of these records have to be stored many different ways (sorting)
			1. items
		3. Often need to access a single record at a time
			1. item
				1. All info with fewer queries (1 query)
	2. Don't use hashes when
		1. The record is only for counting or enforcing uniqueness
			1. Views
			2. Likes
			3. Bids
		2. Record stores only one or two attributes
		3. Used only for constructing relations between different records
		4. The record is only used for time series data
			1. Values changing over time
2. Hashes:
	1. users
	2. items
	3. sessions

### Quiz 2: When to use Hashes ###
### Construct User Implementation ###
1. `services/keys.ts`

```typescript
export const userKey = (userId: string) => `users##{userId}`;
```

2. `services/queries/users.ts`
	1. New user with a username and password

```typescript
export const createUser = async (attrs: CreateUserAttrs) => {
	const id = genId();
	await client.hSet(usersKey(id), {
		username: attrs.username,
		password: attrs.password
	});
	return id;
};
```

### Serialization and Deserialization ###
1. Why not pass `attr`?
	1. Suppose we save an object in Redis
		1. By default, node Redis converts other types to string
			1. Date to string say
			2. Hard to query
		2. We don't have to store id
			1. We can embed id in the keyname
				1. `company#<id>`
	2. Fetching
		1. Problems
			1. We probably want the ID included in this object
			2. We probably want 'revenue' as a number, not a string
			3. We probably want 'createdAt' as a Date object not a string
2. Solution:
	1. Serialize and deserialize
		1. `serialize()`
			1. Takes the data we're trying to save, returns a new object with the correct fields + correct values
		2. `deserialize()`
			1. Turns strings into numbers
			2. Adds the ID
			3. Turns createdAt into a Date object
	2. We control the formatting (instead of default behavior)
		1. Date is encoded as per our decision
		2. ...
3. Procedure
	1. Serialize
		1. Gets an object ready to go INTO Redis as a hash
		2. Removes ID
		3. Turns dates into a queryable format
	2. Deserialize
		1. Formats data coming OUT of Redis
		2. Add in ID
		3. Parse string numbers into plain numbers

### Adding Serialize ###
1. `src/services/queries/users.ts`

```typescript
import type { CreateUserAttrs } from '$services/types';
import { genId } from '$services/utils';
import { client } from '$services/redis';
import { usersKey } from '$services/keys';

export const getUserByUsername = async (username: string) => {};

export const getUserById = async (id: string) => {};

export const createUser = async (attrs: CreateUserAttrs) => {
	const id = genId();

	await client.hSet(usersKey(id), serialize(attrs));

	return id;
};

const serialize = (user: CreateUserAttrs) => {
	return {
		username: user.username,
		password: user.password
	};
};
```

### Fetching a User ###
1. `src/services/queries/users.ts`

```typescript
export const getUserById = async (id: string) => {
	const user = await client.hGetAll(usersKey(id));

	return deserialize(id, user);
};
...
const deserialize = (id: string, user: { [key: string]: string }) => {
	return {
		id,
		username: user.username,
		password: user.password
	};
};
```

### Implementing Sessions ###
1. Sessions: Authentication system
2. Sign-up
	1. username+password -> Redis
		1. Random id is generated
		
		```
		id -> username: username
		      password: password
		```
		
	2. A session is created
		1. Session token is generated
		2. Session token is stored
		
		```
		session#551 -> userId: id
		               username: username
		```
		
	3. A unique session token is sent to browser
		1. If additional requests are made, session token in included
	4. If session token is sent with request, application verifies the token with Redis
		1. Checks for stored session
3. Sign-in
	1. username+password
		1. Redis cannot find `username` and `password` values with this data structure

### Fetching a Saved Session ###
1. `npm i`
2. `npm run dev`
3. `http://localhost:3000`
4. `src/services/queries/session.ts`

```typescript
import type { Session } from '$services/types';
import { sessionsKey } from '$services/keys';
import { client } from '$services/redis';

export const getSession = async (id: string) => {
	const session = await client.hGetAll(sessionsKey(id));

	// console.log(session); // returns an empty object if it does not exist
	if (Object.keys(session).length === 0) {
		return null;
	}

	return deserialize(id, session);
};

export const saveSession = async (session: Session) => {};

const deserialize = (id: string, session: { [key: string]: string }) => {
	return {
		id,
		userId: session.userId,
		username: session.username
	};
};
```

### Instantiating Sessions ###
1. `src/services/queries/session.ts`

```typescript
export const saveSession = async (session: Session) => {
	return client.hSet(sessionsKey(session.id), serialize(session));
};
...
const serialize = (session: Session) => {
	return {
		userId: session.userId!,
		username: session.username
	};
};
...
```

### Serializing Date Times ###
1. Formats
	1. String (ISO, ...)
		1. Redis can't (by default) search for or sort these
	2. Unix time: Seconds since Jan 1 1970 - Redis can search for or sort
	3. Unix time as milliseconds - Redis can search for or sort
		1. More fine-grained

### Storing Items ###
1. `src/services/queries/items/serialize.ts`

```typescript
import type { CreateItemAttrs } from '$services/types';
import { client } from '$services/redis';
import { serialize } from './serialize';
import { genId } from '$services/utils';
import { itemsKey } from '$services/keys';

export const getItem = async (id: string) => {};

export const getItems = async (ids: string[]) => {};

export const createItem = async (attrs: CreateItemAttrs, userId: string) => {
	const id = genId();

	const serialized = serialize(attrs);

	await client.hSet(itemsKey(id), serialized);

	return id;
};
```

2. New > Submit
	1. `http://localhost:3000/items/491909` (id of the item)
		1. `HGETALL items#491909`

### Fetching a Single Item ###
1. `items.ts`

```
import type { CreateItemAttrs } from '$services/types';
import { client } from '$services/redis';
import { serialize } from './serialize';
import { genId } from '$services/utils';
import { itemsKey } from '$services/keys';
import { deserialize } from './deserialize';

export const getItem = async (id: string) => {
	const item = await client.hGetAll(itemsKey(id));

	if (Object.keys(item).length === 0) {
		return null;
	}

	return deserialize(id, item);
};

export const getItems = async (ids: string[]) => {};

export const createItem = async (attrs: CreateItemAttrs, userId: string) => {
	const id = genId();

	const serialized = serialize(attrs);

	await client.hSet(itemsKey(id), serialized);

	return id;
};
```

2. `src/services/queries/items/deserialize.ts`

```typescript
import type { Item } from '$services/types';
import { DateTime } from 'luxon';

export const deserialize = (id: string, item: { [key: string]: string }): Item => {
	return {
		id,
		name: item.name,
		description: item.description,
		imageUrl: item.imageUrl,
		highestBidUserId: item.highestBidUserId,
		ownerId: item.ownerId,
		createdAt: DateTime.fromMillis(parseInt(item.createdAt)),
		endingAt: DateTime.fromMillis(parseInt(item.endingAt)),
		views: parseInt(item.views),
		likes: parseInt(item.likes),
		bids: parseInt(item.bids),
		price: parseFloat(item.price)
	};
};
```

## Section 8: Pipelining Commands ##
### Batching Commands with Pipelines ###
1. `getItems`
	1. Example: Give me details of cars with IDs x, y, z, ...
		1. How to fetch many hashes?
			1. One option: Loop over Id's, fetch one at a time (you probably don't want this)
				1. Downside: Separate requests
					1. Latency
			2. Option 2: Pipelining
				1. Take many commands and batch them to Redis
					1. Example: We set all commands using for loop
						1. Send all of them to Redis in one request
							1. Redis will execute each command one-by-one and return all the results at once

### Running Multiple Commands at the Same Time ###
1. `sandbox`
2. Pipelineing in most Redis clients

```python
client = redis.Redis(...)

pipe = client.pipeline()
pipe.set('foo', 'bar')
pipe.get('bing')
pipe.execute()
```

3. Pipelining in node-redis (the client we are using)

```typescript
const results = await Promise.all([
  client.get('color'),
  client.get('name')
]);
```

	1. No await on each command
		1. The commands are batched to Redis
4. We can mix commands in a pipeline
5. `sandbox/index.ts`

```typescript
import 'dotenv/config';
import { client } from '../src/services/redis';

const run = async () => {
	await client.hSet('car1', {
		color: 'red',
		year: 1950
	});
	await client.hSet('car2', {
		color: 'green',
		year: 1955
	});
	await client.hSet('car3', {
		color: 'blue',
		year: 1960
	});

	const commands = [1, 2, 3].map((id) => {
		return client.hGetAll(`car${id}`);
	});

	const results = await Promise.all(commands);

	console.log(results);
};
run();
```

### Executing a Pipeline ###
1. `items.ts`

```typescript
export const getItems = async (ids: string[]) => {
	const commands = ids.map((id) => {
		return client.hGetAll(itemsKey(id));
	});

	const results = await Promise.all(commands);

	return results.map((result, i) => {
		if (Object.keys(result).length == 0) {
			return null;
		}

		return deserialize(ids[i], result);
	});
};
```

## Section 9: Enforcing Uniqueness with Sets ##
### Basics of Sets ###
1. A set is a collection of strings where each string is unique
	1. Example: colors -> set(red, green, blue, orange)
2. Set commands:
	1. `SADD`
		1. Adds a string to a set
		2. Returns `1` if element added, `0` if not
		3. `SADD colors red`
			1. `colors` - Add to the set stored at this key
				1. Automatically created if it doesn't exist
			2. `red` - Add this string to the set
		4. `SADD numbers 3`
	2. `SREM`
	3. `SRANDMEMBER`
	4. `SCARD`
	5. `SMOVE`
	6. `SPOP`
	7. `SMEMBERS`
		1. Returns all the strings stored in a set
		2. `SMEMBERS colors`
			1. Get keys from this set
	8. `SSCAN`
	9. `SUNION`
	10. `SUNIONSTORE`
	11. `SINTER`
	12. `SINTERSTORE`
	13. `SINTERCARD`
	14. `SMISMEMBER`
	15. `SISMEMBER`
	16. `SDIFF`
	17. `SDIFFSTORE`

### Union of Sets ###
1. Union - Returns all unique elements from all sets
2. Examples:

```
SADD colors:1 red blue orange
SADD colors:2 blue green purple
SADD colors:3 blue red purple
```

```
SUNION colors:1 colors:2 colors:3
```

### Intersection of Sets ###
1. Intersect - Return elements that exist in all sets

```
SINTER colors:1 colors:2 colors:3
```

### Difference of Sets ###
1. Diff - Return elements that exist in the first set, but not any others

```
SDIFF colors:1 colors:2 colors:3
```

### Store Variations ###
1. `SUNIONSTORE` - stores the union with a new key
2. `SINTERSTORE`
	1. `SINTERSTORE colors:results colors:1 colors:2 colors:3` (returns 1 - only one color)
	2. Use-case: to run only once and store the results to re-use them for large sets
3. `SDIFFSTORE`

### Checking for an Element in a Set ###
1. `SISMEMBER`
	1. Return 1 if the element exists in the set, 0 if not
	2. `SISMEMBER colors:1 red` - returns 1
	3. `SISMEMBER colors:1 purple` - returns 0
2. `SMISMEMBER`
	1. Runs multiple `SISMEMBER` at the same time
	2. `SMISMEMBER colors:1 red green blue` - returns an array of 1s and 0s

### Scanning a Set ###
1. `SCARD` - Return the number of elements in a set (cardinality)
	1. `SCARD colors:1` - returns 3
2. `SREM` - Remove an element from a set
	1. `SREM colors:1 red`
3. `SMEMEBERS` will give all the members (even they are thousands or millions)
	1. Solution: `SSCAN`
		1. `SSCAN` - Scan through all the elements in a set
			1. `SSCAN colors:1 0 COUNT 2`
				1. `0` - cursor ID
					1. Pointer to the next page
						1. Returns the next cursor ID
							1. `SSCAN colors:1 3 COUNT 2`
						2. `0` - no more elements
				2. `COUNT 2` - # of elements to return
4. `SINTERCARD` - intersection and cardinality
5. `SRANDMEMBER` - returns a random member
6. `SMOVE` - moves member from one set to another

### Completed Notes ###
1. [Sets_-_Complete.json](https://att-c.udemycdn.com/2022-06-10_17-49-48-48dbb307d52882a370ebafe6a02f43c8/original.json?response-content-disposition=attachment%3B+filename%3DSets_-_Complete.json&Expires=1785277368&Signature=u2IrWcrQWQTBCWXmqzAsd8xuRHHOVxvXWX8eRPN4HGDv9mRKXmFReex97gCYGc6KgiqUgkj2Dgk7ARY2HQZkj6aV-sMdqQqL2D9DRyywU09xMQOVnNvXJ30meTTUaCLIQteCxKrRixsbduTk0u0rpuDD7RSTGyM~mxF5QecCpL9q6tSpcP3SKHxla4WMm04ykKF03PZBUufNexLcVQ2b9L4L8tzHvFrkeRrFOcam487aOtNsAeM2bIVUc~ccdlN4svuCiDrCBN6h1Ao5eEbdfkB9e5EOplhwplm9itRr2UA7~74102bjhs-3WW9cx6LM37QRWo19ZafFqspxvbTQPw__&Key-Pair-Id=K3MG148K9RIRF4)

### Most Common Use Cases of Sets ###
1. Set Use Cases
	1. Enforcing uniqueness of any value
		1. Example: Each user can use a unique username
			1. API checks to see if the username is already in use
				1. If no, username is available
				
				```
				SISMEMBER usernames powershell1
				```
				
	2. Constructing a relationship between different records
		1. Example: Users can like products
			1. `users#45:likes` - user 45 likes products
				1. Which items do user with ID 45 like?
					1. `SMEMEBERS users#45:likes`
				2. How many items does user with ID 45 like?
					1. `SCARD users#45:likes`
				3. Does user with ID 45 lik th item with ID 123?
					1. `SISMEMBER users#45:likes 123`
	3. Finding common attributes between different things
		1. Example: `users:45:likes` and `users:32:likes`
			1. Which items do both user 45 and user 32 like?
				1. `SINTER users#45:likes users#32:likes`
	4. General list of elements where order doesn't matter
		1. Example: Limit IP addresses or domains our application can connect to
			1. `domains:banned`
				1. `ezmail.com`
				2. `freemail.com`
				3. `scammail.com`

## Section 10: A Little Set Implementation ##
### Requiring Unique User Names ###
1. Check if username is not already used
2. `src/services/queries/users.ts`

```typescript
export const createUser = async (attrs: CreateUserAttrs) => {
	const id = genId();

	// See if the username is already in the set of usernames
	const exists = await client.sIsMember(usernamesUniqueKey(), attrs.username);
	// If so, throw an error
	if (exists) {
		throw new Error('Username is taken');
	}
	// Otherwise, continue

	await client.hSet(usersKey(id), serialize(attrs));

	// Add the new username to the set
	await client.sAdd(usernamesUniqueKey(), attrs.username);

	return id;
};
```

3. `src/services/keys.ts`

```
export const usernamesUniqueKey = () => 'usernames:unique';
```

4. If we try to sign-up with the same username, the application throws an error

### Adding a Like System ###
1. `keys.ts`

```
export const userLikesKey = (userId: string) => `users:likes#${userId}`;
```

2. `src/services/queries/likes.ts`

```typescript
export const likeItem = async (itemId: string, userId: string) => {
	await client.sAdd(userLikesKey(userId), itemId);
};

export const unlikeItem = async (itemId: string, userId: string) => {
	await client.sRem(userLikesKey(userId), itemId);
};
```

### How to Count the Number of Likes? ###
1. `src/services/queries/likes.ts`

```
export const userLikesItem = async (itemId: string, userId: string) => {
	return await client.sIsMember(userLikesKey(userId), itemId);
};
```

2. Problem: We don't have a good way to query all sets at the same time!
	1. Ahead computation
		1. When a user likes an item, we store total number of likes
			1. `items#45` -> `name: Chair, description: ..., likes: likes + 1`
				1. Upfront work
				2. Reading is fast

### Updating Like Quantities ###
1. `likes.ts`

```typescript
import { client } from '$services/redis';
import { userLikesKey, itemsKey } from '$services/keys';

export const userLikesItem = async (itemId: string, userId: string) => {
	return await client.sIsMember(userLikesKey(userId), itemId);
};

export const likedItems = async (userId: string) => {};

export const likeItem = async (itemId: string, userId: string) => {
	const inserted = await client.sAdd(userLikesKey(userId), itemId);
	if (inserted) {
		return await client.hIncrBy(itemsKey(itemId), 'likes', 1);
	}
};

export const unlikeItem = async (itemId: string, userId: string) => {
	const removed = await client.sRem(userLikesKey(userId), itemId);
	if (removed) {
		return await client.hIncrBy(itemsKey(itemId), 'likes', -1);
	}
};

export const commonLikedItems = async (userOneId: string, userTwoId: string) => {};
```

### Showing Liked Items ###
1. `likes.ts`

```typescript
export const likedItems = async (userId: string) => {
	// Fetch all the item IDs from this user's liked set
	const ids = await client.sMembers(userLikesKey(userId));

	// Fetch all the item hashes with those ids and return as n array
	return getItems(ids);
};
```

### Showing Common Liked Items ###
1. `likes.ts`

```typescript
export const commonLikedItems = async (userOneId: string, userTwoId: string) => {
	const ids = await client.sInter([userLikesKey(userOneId), userLikesKey(userTwoId)]);

	return getItems(ids);
};
```

## Section 11: Organizing Data with Sorted Sets ##
### Sorted Sets ###
1. Sorted set:
	1. A mix of a hash and a set
	2. No 'keys' and 'values'. There are 'members' and 'scores'
	3. Members are unique
	4. Scores don't have to be unique
		1. Always a number
		2. -ve or +ve
		3. Floats or integers
	5. Scores are sorted from least to greatest
	6. Example:
	
	```
	member | score
	peanut butter | -4
	chocolate | 1.04
	vanilla | 2.004
	strawberry | 5.32
	```
	
	7. Very flexible and useful data structure
2. Commmands:
	1. `ZADD`
	2. `ZCARD`
	3. `ZCOUNT`
	4. `ZINCRBY`
	5. `ZCORE`
	6. `ZRANK`
	7. `ZLEXCOUNT`
	8. `ZREM`
	9. `ZRANGE`
	10. `ZREVRANK`
	11. `ZREVRANGE`
	12. `ZREVRANGEBYLEX`
	13. `ZREVRANGEBYSCORE`
	14. `ZSCAN`
	15. `ZRANGEBYLEX`
	16. `ZRANGEBYSCORE`
	17. `ZRANGESTORE`
	18. `ZMSCORE`
	19. `ZRANDMEMBER`
	20. `ZDIFF`
	21. `ZDIFFSTORE`
	22. `ZUNION`
	23. `ZUNIONSTORE`
	24. `ZINTER`
	25. `ZINTERCARD`
	26. `ZINTERSTORE`
	27. `BZMPOP`
	28. `BZPOPMAX`
	29. `BZPOPMIN`
	30. `ZMPOP`
	31. `ZPOPMIN`
	32. `ZPOPMAX`
	33. `ZREMRANGEBYRANK`
	34. `ZREMRANGEBYLEX`
	35. `ZREMRANGEBYSCORE`
		1. Many commands are deprecated

### Adding and Removing Members ###
1. `ZADD`
	1. Add a member-sore pair to a sorted set
	2. `ZADD products 45 monitor`
		1. `products` - Sorted set we want to add data to
		3. `45` - score
		4. `monitor` - member
2. `ZSCORE`
	1. `ZSCORE products monitor`
		1. Get the score of a member
3. rbook

```
ZADD products 45 monitor

ZSCORE products monitor
```

4. `ZREM`
	1. Remove a member from a sorted set
	2. `ZREM products monitor`
	
```
ZREM products monitor
ZSCORE products monitor
```

5. `NX`
	1. If not already set
6. `XX`
	1. If not already exists

### Finding a Range of Scores ###
1. `ZCARD` (cardinality)
	1. Get the number of members in a sorted set
	2. `ZCARD products`
2. `ZCOUNT`
	1. Get the number of members in a sorted set within a range of scores
	2. `ZCOUNT products 0 50`
		1. `0` - Minimum score to consider
		2. `50` - Maximum score to consider
3. rbook

```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZCARD products
```

```
ZCOUNT products 0 50
```

	1. `min` and `max` are inclusive
4. Variations:
	1. `ZCOUNT products (0 (50`
		1. `0 < products < 50`
	2. `ZCOUNT products -inf +inf`
		1. `-Infinity < products < Infinity`
			1. For open-ended range
		2. Example:
		
		```
		ZCOUNT products -inf 40
		```

### Removing the Highest and Lowest Members ###
1. `ZPOPMIN`
	1. Remove and return some number of the lowest score pairs
	2. `ZPOPMIN products 2`
		1. `2` - (Optional) Remove the 2 lowest member-score pairs
			1. Defailt: 1
2. `ZPOPMAX`
	1. Remove and return some number of the highest score pairs
	2. `ZPOPMAX products 2`
		1. `2` - (Optional) Remove the 2 highest member-score pairs
			1. Default: 1
3. Examples:

```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZPOPMIN products 2
```

```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZPOPMAX products 2
```

### Updating Scores ###
1. `ZINCRBY`
	1. Adjust a member's score by the given amount
	2. `ZINCRBY products 15 keyboard`
		1. `15` - Amount to add to the score
			1. Resort will occur
2. Example:

```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZINCRBY products 15 cpu
```

```
ZSCORE products cpu
```

### Querying a Sorted Set ###
1. `ZRANGE`
	1. Retrieve a range of members and (optionally) scores
		1. `ZRANGE products 1 2 WITHSCORES`
			1. `1` - Find members with this minimum index
				1. Index - default
					1. Start: 0
			2. `2` - Find members with this maximum index
			3. `WITHSCORES` - Include the score of each member in the response
2. Examples:

```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZRANGE products 1 2 WITHSCORES
```

3. Variations:
	1. `ZRANGE products 0 50 BYSCORE WITHSCORES`
		1. `BYSCORE` - Tream the min and max as scores
		
```
DEL products

ZADD products 45 cpu
ZADD products 10 keyboard
ZADD products 55 power

ZRANGE products 0 50 BYSCORE WITHSCORES

ZRANGE products 0 (55 BYSCORE WITHSCORES

ZRANGE products -inf +inf BYSCORE WITHSCORES
```

4. Variation:
	1. `ZRANGE products 1 2 REV LIMIT 1 2`
		1. `REV` - Reverse the order [before any comparisons]
		2. `LIMIT 1 2` - Skip the first element, then give the next two
		3. Example:
	
		```
		DEL products
		
		ZADD products 45 cpu
		ZADD products 10 keyboard
		ZADD products 55 power
		
		ZRANGE products 1 2 REV
		```
		
	2. `ZRANGE products 0 55 BYSCORE LIMIT 1 2`

### Completed Notes ###
1. [Sorted_Sets_-_Complete.json](https://att-c.udemycdn.com/2022-06-10_17-49-50-c6cb76bf5c2544699ac2c5f013876b0d/original.json?response-content-disposition=attachment%3B+filename%3DSorted_Sets_-_Complete.json&Expires=1785331982&Signature=OI4FWslReZ9b~U4yjx5FchLSa83aRmkTHfxFSpUG4l8m32CK9guyUPFWCsQcCvg8CY7lpA~BiE2OTnv9XnG7jqgp-svYeLCoKlbPUgTaPAR23CFlFKvQye8WvPY2x6IzPEpEtN19NQUn2xGhyRzvAKDLtnIKl37oksK9pyTPNdvrgGf93eiH5mDH~-FbP1~TYjOR52fbsvB9bV4kpA4LhkBCTfrbiAt9a-TNm9-J3-NZbAqeDKEX0UrWVYS7Zw5HHfGFsAIVFTBD5CrK-YsSpsEMe9vh7hxS3lBQ9J6Ct322mauzEDbi1l9Y5Ks1sH1KD~ewTyzAawC-njZF6LljiQ__&Key-Pair-Id=K3MG148K9RIRF4)

## Section 12: Practice Time with Sorted Sets! ##
### Sorted Set Use Cases ###
1. Tabulating 'the most' or 'the least' of a collection of hashes
	1. Example: Book purchasing application
		1. Store info about each book
		2. Each book has a separate hash
		3. We want to list books with most reviews, ratings, or purchases
			1. Each one has a sorted set
				1. `books:reviews`
				2. `books:ratings`
				3. `books:purchases`
2. Constructing relationships between records, sorted by some criteria
	1. Example: Authors write books
		1. Multiple authors can work on a single book
			1. Each author has a hash
			2. Each book has a hash
			3. Relationships
				1. Sorted set for each author and the book they have authored
					1. Sorting by number of copies sold
						1. We can find the most sold book by the author
				2. Sorted set for each author and the book they have authored by AUTHOR DATE
					1. We can fetch the latest books written by the author

### Reminder on the Auth Flow ###
1. A hash is stored for each user on sign up
2. Sign-in
	1. We don't have id (only username)
		1. Fix: Sorted set (hash can also be used)
			1. Stores:
				1. member: username
				2. score: id
			2. We lookup username and return id
			3. We use id to return hash

### Storing Usernames ###
1. `keys.ts`

```typescript
export const usernamesKey = () => 'usernames';
```

2. `genId()` - returns hexadecimal value as string
	1. Can be converted to base 10 number

### Kind of Storing Strings in Sorted Sets ###
1. `users.ts`

```typescript
export const createUser = async (attrs: CreateUserAttrs) => {
	const id = genId();

	// See if the username is already in the set of usernames
	const exists = await client.sIsMember(usernamesUniqueKey(), attrs.username);
	// If so, throw an error
	if (exists) {
		throw new Error('Username is taken');
	}
	// Otherwise, continue

	await client.hSet(usersKey(id), serialize(attrs));

	// Add the new username to the set
	await client.sAdd(usernamesUniqueKey(), attrs.username);

	await client.zAdd(usernamesKey(), {
		value: attrs.username,
		score: parseInt(id, 16)
	});

	return id;
};
```

### Convering User IDs ###
1. `users.ts`

```typescript
export const getUserByUsername = async (username: string) => {
	// Use the username argument to look up the persons User ID
	// with the usernames sorted set
	const decimalId = await client.zScore(usernamesKey(), username);

	// make sure we actually got an ID from the lookup
	if (!decimalId) {
		throw new Error('User does not exist');
	}

	// Take the id and convert it back to hex
	const id = decimalId.toString(16);

	// use the id to look up the user's hash
	const user = await client.hGetAll(usersKey(id));

	// deserialize and return the hash
	return deserialize(id, user);
};
```

### Plan for Showing Most Viewed Items ###
1. Most views
	1. Hashes store number of views
	2. Sorted set
		1. `items:views`
			1. member: item id
			2. score: views
	3. Duplication of data
		1. Traded of for quick retrieval (instead of joining)
2. Plan
	1. On item creation
		1. Initialize the item's hash 'views' property to 0
		2. Add the item's ID to the sorted set with an initial score of 0
	2. On item view... (only if this user is viewing the item for the first time (implement later))
		1. Increment the item hash's 'views' property by 1
		2. Increment the sorted set's score for this item by 1

### Initializing Views on Item Creation ###
1. `keys.ts`

```typescript
export const pageCacheKey = (id: string) => `pagecache#${id}`;
export const usersKey = (userId: string) => `users#${userId}`;
export const sessionsKey = (sessionId: string) => `sessions#${sessionId}`;
export const usernamesUniqueKey = () => 'usernames:unique';
export const userLikesKey = (userId: string) => `users:likes#${userId}`;
export const usernamesKey = () => 'usernames';

// Items
export const itemsKey = (itemId: string) => `items#${itemId}`;
export const itemsByViewsKey = () => 'items:views';
```

2. `src/services/queries/items/items.ts`

```typescript
export const createItem = async (attrs: CreateItemAttrs, userId: string) => {
	const id = genId();

	const serialized = serialize(attrs);

	await Promise.all([
		client.hSet(itemsKey(id), serialized),
		client.zAdd(itemsByViewsKey(), {
			value: id,
			score: 0
		})
	]);

	return id;
};
```

### Incrementing View Counters ###
1. `src/services/queries/views.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByViewsKey } from '$services/keys';

export const incrementView = async (itemId: string, userId: string) => {
	return await Promise.all([
		client.hIncrBy(itemsKey(itemId), 'views', 1),
		client.zIncrBy(itemsByViewsKey(), 1, itemId)
	]);
};
```

### Items by Ending Soonest ###
1. Steps:
	1. Set up a sorted set for items by 'Ending Soonest'
		1. Bidding ends after some time
		2. `items:endingAt`
			1. `member`: item ids
			2. `score`: Unix times in milliseconds
		3. Ending times are stored in each item hash
		4. Steps:
			1. On item creation:
				1. Initialize the item's hash 'views' property to 0
				2. Add the item's ID to the sorted set with an initial score of 0
			2. On item view: Only if this user is viewing the item for the first time (implement later)
				1. 
	2. Work on displaying 'Most Views' and 'Ending Soonest'
		1. Steps:
			1. On item creation
				1. Initialize the item's hash 'endingAt' property to a unix timestamp
				2. Add the item's ID to the sorted set with an initial score of the timestamp
2. `services/keys.ts`

```typescript
export const itemsByEndingAtKey = () => 'items:endingAt';
```

3. `services/queries/items/items.ts`

```typescript
import { itemsByViewsKey, itemsByEndingAtKey } from '$services/keys';
...
export const createItem = async (attrs: CreateItemAttrs, userId: string) => {
	const id = genId();

	const serialized = serialize(attrs);

	await Promise.all([
		client.hSet(itemsKey(id), serialized),
		client.zAdd(itemsByViewsKey(), {
			value: id,
			score: 0
		}),
		client.zAdd(itemsByEndingAtKey(), {
			value: id,
			score: attrs.endingAt.toMillis()
		})
	]);

	return id;
};
```

4. `New` item

### Querying for Ending Soonest ###
1. Ending Soonest
	1. Item IDs
		1. `endingAt`
			1. Example: Two items ending soonest, if current time is 130
				1. Ignore items with `endingAt` < 130
				2. `ZRANGE items:endingAt 130 +inf BYSCORE LIMIT 0 2` **(M)**
					1. Only returns Item IDs
	2. `queries/items/by-ending-time.ts`
	
	```typescript
	import { client } from '$services/redis';
	import { itemsKey, itemsByEndingAtKey } from '$services/keys';
	import { deserialize } from './deserialize';

	export const itemsByEndingTime = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
		const ids = await client.zRange(itemsByEndingAtKey(), Date.now(), '+inf', {
			BY: 'SCORE',
			LIMIT: {
				offset,
				count
			}
		});

		console.log(ids);
	};
	```
	
	3. Testing:
		1. New item
		2. Duration: Ten Minutes
		3. New item
		4. Duration: Ten Minutes
		5. New item
		6. Duration: Ten Minutes
			1. Open home page
2. Most Views

## Section 13: From Relational Data to Redis ##
### Loading Relational Data ###
1. Strategies
	1. Loading Relational Data
		1. Construct a simple pipeline that does a bunch of 'HGETALL's
		2. Use the 'SORT' command in a very clever way
			1. Another command
				1. Example: Most Views
2. `by-ending-time.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByEndingAtKey } from '$services/keys';
import { deserialize } from './deserialize';

export const itemsByEndingTime = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
	const ids = await client.zRange(itemsByEndingAtKey(), Date.now(), '+inf', {
		BY: 'SCORE',
		LIMIT: {
			offset,
			count
		}
	});

	const results = await Promise.all(ids.map((id) => client.hGetAll(itemsKey(id))));

	return results.map((item, i) => deserialize(ids[i], item));
};
```

### Relational Data with SORT ###
1. `SORT`
	1. Sorts data and also joins data from different sources into a single structure
2. `queries/items/by-views.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByViewsKey } from '$services/keys';
import { deserialize } from './deserialize';

export const itemsByViews = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
	const results = await client.sort(itemsByViewsKey(), {
		GET: ['#', `${itemsKey('*')}->name`, `${itemsKey('*')}->views`],
		BY: 'score'
	});

	console.log(results);
};
```

### The Sort Command ###
1. `npx rbook`
2. SORT
	1. Probably the trickiest command to understand
	2. used on sets, sorted sets, and lists
		1. How can we sort a sorted set?
	3. Calling this command 'SORT' is misleading!!!!
		1. It can be used for usecases where sorting is not required
	4. Terminology we use with 'sort' conflicts with terms we use for sorted sets!!!!!
		1. `score` is paired with `member` in sorted set
			1. In `SORT`, it is different
3. Example:
	1. ID, Title, Year Published
		1. good, Good Book, 1950
		2. bad, Bad Book, 1930
		3. ok, OK Book, 1940
	2. List the ID of each book, sort by year published
		1. List the ID of each book - Data we are looking for
		2. Sorted by year published - Sorting criteria
			1. It is not included in the result set

### Terminology Around Sort ###
1. Data: Same as before

```
books:good
  title, Good Book
  year, 1950

books:bad
books:ok

books:likes:
  bad, 0
  ok, 40
  good, 50
```

2. Commands:

```
HSET books:good title 'Good Book' year 1950
HSET books:bad title 'Bad Book' year 1930
HSET books:ok title 'OK Book' year 1940

ZADD books:likes 999 good
ZADD books:likes 0 bad
ZADD books:likes 40 ok
```

```
SORT books:likes # Error: ERR One or more scores can't be converted into double
```

	1. SORT operates on the MEMBERS of a sorted set, not the scores!
		1. Example: members are strings in our case (good, bad, ok)
			1. Solution: Sort them alphabetically
			
			```
			SORT books:likes ALPHA
			```
			
	2. SORT refers to these members as scores!!! (confusing!!!)
		1. good, bad, and ok - scores (instead of members)
		
3. Variation:

```
SORT books:likes LIMIT 1 2 ALPHA
```

	1. `LIMIT 1 2`: Skip 1 and give next 2

### Specifying the BY Argument ###
1. List the ID of each book, sorted by year published

```
SORT books:likes BY books:*->year
```

	1. Step 1: Extract all the members from the sorted set
		1. `books:*->year`
	2. Step 2: Loop through each member. Insert the member into the 'BY' template. If this points at a hash, retrieve the field
		1. `books:bad->year`
			1. Redis looks at all the structures to find `books:bad`
				1. At the structure `books:bad` get the `year` field
				2. Use it as the sorting criterion
			2. Output:
			
			```
			bad -> 1930
			ok -> 1940
			good -> 1950
			```
			
	3. Step 3: Sort each member based on the 'BY' field
	4. Step 4: Return only the members (discard sorting criterion)

### Joining Data with Sort ###
1. Example: List the Title of each book, sorted by year published

```
SORT books:likes BY books:*->year GET books:*->title
```

	1. Step 1: Extract all the members from the sorted set
	2. Step 2: Loop through each member. Insert the member into the 'BY' template. If this points at a hash, retrieve the field
		1. `books:bad->year`
		2. ...
	3. Step 3: Same thing, but put the 'GET' field on teh LEFT side
		1. `books:*->title`
			1. `books:bad->title`
			2. `books:ok->title`
			3. `books:good->title`
		2. Result:
		
		```
		bad, Bad Book -> 1930
		ok, OK Book -> 1940
		good, Good Book -> 1950
		```
	
	4. Step 4: Sort each member based on the 'BY' field
	5. Step 5: Return only the fields specified in 'GET'
	
	```
	Bad Book
	OK Book
	Good Book
	```
	
2. Variation:

```
SORT books:likes BY books:*->year
  GET #
  GET books:*->title
  GET books:*->year
```

	1. `#` - insert the original member
		1. `bad`, `ok`, `good`
	2. `BY nosort`
		1. Sorting is not done
			1. Uses implicit sorting in case of sorted set
		2. It is only used for joining
		
3. Variation:

```
SORT books:likes BY nosort
  GET #
  GET books:*->title
  GET books:*->year
```

### A Few More Arguments ###
1. `nosort` is convention
	1. Any text can be used
		1. Disables sort
			1. Example: `BY: 'score'` - `sort` key doesn't exist
				1. Disables sorting
2. Explanation:

```
	const results = await client.sort(itemsByViewsKey(), {
		GET: ['#', `${itemsKey('*')}->name`, `${itemsKey('*')}->views`],
		BY: 'score'
	});
```

	1. `GET`
		1. Returns original members
		2. Returns `items:<item-id>->name`
		2. Returns `items:<item-id>->views`
	2. Returns in least views to most views in this case
		1. We want to flip the order
			1. Solution
			
			```
			SORT books:likes BY nosort DESC
			  GET #
			  GET books:*->title
			  GET books:*->year
			```
			
3. `by-views.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByViewsKey } from '$services/keys';
import { deserialize } from './deserialize';

export const itemsByViews = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
	const results = await client.sort(itemsByViewsKey(), {
		GET: ['#', `${itemsKey('*')}->name`, `${itemsKey('*')}->views`],
		BY: 'score',
		DIRECTION: order,
		LIMIT: {
			offset,
			count
		}
	});

	console.log(results);
};
```

4. Testing:
	1. Refresh product page for the items
		1. New item: Newest Chair
			1. 10 minutes
			2. Refresh a few times

### Parsing SORT Output ###
1. We want to parse array of strings into array of objects
2. We need to get other properties, too (image, etc.)
3. `by-views.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByViewsKey } from '$services/keys';
import { deserialize } from './deserialize';

export const itemsByViews = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
	let results: any = await client.sort(itemsByViewsKey(), {
		GET: [
			'#',
			`${itemsKey('*')}->name`,
			`${itemsKey('*')}->views`,
			`${itemsKey('*')}->endingAt`,
			`${itemsKey('*')}->imageUrl`,
			`${itemsKey('*')}->price`
		],
		BY: 'score',
		DIRECTION: order,
		LIMIT: {
			offset,
			count
		}
	});

	const items = [];
	while (results.length) {
		const [id, name, views, endingAt, imageUrl, price, ...rest] = results;
		const item = deserialize(id, { name, views, endingAt, imageUrl, price });
		items.push(item);
		results = rest;
	}

	return items;
};
```

	1. Tradeoff: `SORT` is a single request to Redis, but needs more code and more logic in the application

### Completed Notes ###
1. [Sort_-_Completed.json](https://att-c.udemycdn.com/2022-06-10_17-49-49-29616d953d3e4ec2c13214af603e7c5c/original.json?response-content-disposition=attachment%3B+filename%3DSort_-_Completed.json&Expires=1785967040&Signature=09Pd9yD16i5yF9PNRbJp1oYUOHOcSwZsMBk2WO86TUqrQ8FVxbhIfx-FqqGzvT8wnhpx-WqBykuNwEQUw9Ypt-Ezwf484KLWwCrMj2H8iVOSa3ckW0lCGmooWQhirbSeTXCJzEA4sdb--K7mxrMA2JTkPC7kjb0nQv5zv4Tb70jjKqilBHqbtHGGoXtrvRxP81Xlgnc27X8X0oQCYtIjRud9asvPwCRCgMJF~qvEcZsLLIJJluZSW~GIhr4ZYy8pFlcUOS4QT8RGv-O3GEG7WOgUcuhnU5WU-XswRDDMUps8YxIhyWaKVtbngPsJnqth48BecxCP~S~yDTbqtcUoFA__&Key-Pair-Id=K3MG148K9RIRF4)

## Section 14: HyperLogsLogs Structures ##
### HyperLogsLogs ###
1. HyperLogLog
	1. Algorithm for approximately counting the number of unique elements
	2. Similar to a set, but doesn't store the elements
	3. Will seem useless at first glance
2. Two commands
	1. `PFADD`
		1. `PFADD asdf` - it doesn't get stored but does some complex math and remembers it without storing it
			1. It keeps track of unique set of items without storing them
			2. If `asdf` is already added, we get back a 1
			3. If `asdf` is new, we get back a 0
	2. `PFCOUNT`
		1. Returns an approximate count of the unique elements that were added
3. `npx rbook`

```
PFADD vegetables celery # returns 1
PFADD vegetables potato
```

```
PFCOUNT vegetables
```

	1. Returns 2

### When to use HyperLogsLogs ###
1. We want each 'view' to be unique per user
	1. One way:
		1. One set per item
			1. item:5 -> views:5
				1. username1
				2. username2
				3. ...
			2. item:6 -> views:6
				1. ...
		2. Downside
			1. Each username - 40 bytes
				1. 10 million views = 40b * 1000000 / 1024 / 1024 = 38 MB
	2. Another way: HyperLogLog
		1. User views an item
			1. `PFADD views:5 username1`
				1. It returns 1 if it is new
				2. Did this return a 1?
					1. New view, so increment views
				3. Did this return a 0?
					1. User already viewed
		2. HyperLogLog doesn't store actual usernames
			1. It is always constant space
				1. 12kb no matter how many elements are added
					1. Even for a million views
		3. Downside:
			1. Approximation
				1. `PFCOUNT views`
					1. 0.81% error, so 991 to 1008 for 1000 actual value (slightly incorrect)
						1. Slight error in total number of views is not very significant

### HyperLogsLogs in Action ###
1. `keys.ts`

```typescript
export const itemsViewsKey = (itemId: string) => `items:views#${itemId}`;
```

2. `views.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByViewsKey, itemsViewsKey } from '$services/keys';

export const incrementView = async (itemId: string, userId: string) => {
	const inserted = await client.pfAdd(itemsViewsKey(itemId), userId);

	if (inserted) {
		return await Promise.all([
			client.hIncrBy(itemsKey(itemId), 'views', 1),
			client.zIncrBy(itemsByViewsKey(), 1, itemId)
		]);
	}
};
```

3. Testing:
	1. Refresh page multiple times
		1. Views is incremented only once

## Section 15: Storing Collections with Lists ##
### Lists ###
1. Lists
	1. Collection of strings in a particular order
		1. Example: Temperature recording each day
	2. Store an ordered list of strings
	3. Not an array!
	4. Implemented as a doubly-linked list
	5. Often used for time-series data
	6. You should probably use this less often than you think (?)
2. Less useful commands exist

### Reading and Writing Data to a List ###
1. Commands:
	1. GET data
		1. `LINDEX` - Get the value stored at the provided index
			1. `LINDEX temps 0`
				1. `temps` - Find the key 'temps'
				2. `0` - Get the value at the provided index
		2. `LLEN` - Get the number of elements in the list
			1. `LLEN temps` - Find the key 'temps'
		3. `LPOS`
		4. `LRANGE`
	2. Add/remove/Update Data
		1. `LPOP`
		2. `LINSERT`
		3. `LMOVE`
		4. `LREM`
		5. `LPUSH` - Add an element to the left side (start) of the list
			1. `LPUSH temps 20`
				1. `temps` - Find the key `temps`
				2. `20` - Adds this value
		6. `LPUSHX`
		7. `LMPOP`
		8. `RPOP`
		9. `RPUSHX`
		10. `LSET`
		11. `LTRIM`
		12. `RPUSH` - Add an element to the right side (end) of the list
			1. `RPUSH temps 25`
				1. `temps` - Find the key `temps`
				2. `25` - Adds this value
	3. Probably Not Needed
		1. `BLMOVE`
		2. `BLMPOP`
		3. `BLPOP`
		4. `BRPOP`
		5. `BRPOPLPUSH`
		6. `RPOPLPUSH`
2. `npx rbook`

```
LPUSH temps 25
```

```
RPUSH temps 27
```

```
LLEN temps
```

```
LINDEX temps 0
LINDEX temps 1
LINDEX temps -1 # last element
LINDEX temps -2 # last but one
```

### Ranges and Searches ###
1. `LRANGE` **(M)** - Get a range of elements from a list
	1. `LRANGE temps 0 3`
		1. `temps` - Find the key 'temps'
		2. `0` - Take all elemetns from this index...
		3. `3` - Up to (and indlucing!) this one
		
```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24
```

```
LRANGE temps 0 3
LRANGE temps 1 3
LRANGE temps 0 5455234234
LRANGE temps 0 -1 # up to last element (inclusive)
```

2. `LPOS` - Get the index of a value stored in a list
	1. `LPOS temps 25`
		1. `25` - Look for the value '25'
	2. `LPOS temps 25 RANK 2 COUNT 2 MAXLEN 10`
		1. `RANK 2` - Find the 2nd instance of '25' (skips first)
		2. `COUNT 2` - Retrieve the index of the first 2 matches
		3. `MAXLEN 10` - Only search the first 10 elements
			1. If there are too many elements
		
```
LPOS temps 27
LPOS temps 30
LPOS temps 3534343
```

```
LPOS temps 27 RANK 2
LPOS temps 27 RANK 1 COUNT 2
LPOS temps 27 RANK 1 COUNT 2 MAXLEN 10
```

### Trimming Lists ###
1. `LPOP` - Remove and return some number of elements from the left side (start)
	1. `LPOP temps 2`
		1. `2` - (Optional) Remove the first 2 elements
2. `RPOP` - Remove and return some number of elements from the right side (end)
	1. `RPOP temps 2`
		1. `2` - (Optional) Remove the last 2 elements
		
```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24

LPOP temps
LINDEX temps 0

LPOP temps 2
LINDEX temps 0

RPOP temps
LINDEX temps -1
```

3. `LSET` - Change the value stored at the given index
	1. `LSET temps 2 32`
		1. `2` - Update the value stored at index 2
		2. `32` - Store the value '32'
		
```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24

LSET temps 0 35
LINDEX temps 0

LSET temps -1 35
LINDEX temps -1
```

4. `LTRIM` **(M)** - Remove all elements outside of this range
	1. `LTRIM temps 2 5`
		1. `2` - Only keep elements from index 2
		2. `5` - Up to (and including) index 5
		
```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24

LTRIM temps 1 3
LINDEX temps 0
LINDEX temps -1
```

### Removing Elements ###
1. `LINSERT` **(M)** - Find an element in a list, then insert a value before or after it
	1. `LINSERT temps BEFORE 25 15`
		1. `25` - the value 25
		2. `15` - insert the number 15
		
```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24

LINSERT temps BEFORE 30 15
LINDEX temps 3

LRANGE temps 0 -1

LINSERT temps AFTER 30 15
LRANGE temps 0 -1
```

2. `LREM` - Remove some elements from a list
	1. `LREM temps -2 25`
		1. `-2` - Moving from right to left, remove 2 instance of
			1. `-` - right to left
			2. positive - left to right
			3. `0` - Remove all copies
		2. `25` - the value 25

```
DEL temps

RPUSH temps 25
RPUSH temps 27
RPUSH temps 27
RPUSH temps 30
RPUSH temps 24

LREM temps 0 27
LRANGE temps 0 -1

LREM temps 1 25
LRANGE temps 0 -1
```

### List Use Cases ###
1. List Use Cases:
	1. Append-only or prepend-only data
		1. Temperature readings
		2. Stock values
			1. (data added non-stop)
	2. When you only need the last/first N values of something
		1. Social media posts
			1. Keep ids in a list
				1. Alternative: Sorted set (timestamp sorted)
	3. Your data has no sort order besides the order it was inserted
		1. In chronological order (posts)
2. Don't use lists if you have many items AND
	1. You need to apply some filtering criteria
		1. `>`, `<`, ...
	2. Your data is sorted by some attribute (other than time or insertion order)
3. Scenarios
	1. Example: Book reviewing platform
		1. Need to get the titles of the 2 most recently reviewed books
			1. Find ids
			2. Get book reviews from hashes
		2. `SORT`
		
		```
		DEL reviews

		RPUSH reviews b2
		RPUSH reviews a1

		HSET books:a1 title 'Good Book'
		HSET books:b2 title 'Bad Book'

		SORT reviews BY nosort GET books:*->title
		```
		
	2. Example: Temperature Station
		1. Record the temperature, but the time between readings is variable
			1. Today 4 AM
			2. Yesterday 8 AM
			3. ...
		2. Encoding:
		
		```
		25:103453434 -> 30:125343433 -> 30:135344342
		```
		
			1. <Temperature> : <Timestamp> [: <Location>]
				1. But, cannot use it as a key to join in some cases

### Using Lists in Our App ###
1. Bid History
	1. Trend over time
2. `services/queries/bids.ts` - `history#a1` (list for each item), `25:1423232323`
	1. `createBid()` - Adds a new record into the bid history list
	2. `getBidHistory()` - Returns bid history for a single item in order of increasing time
		1. String to object

### Serializing and Deserializing Bids ###
1. `keys.ts`

```typescript
export const bidHistoryKey = (itemId: string) => `history#${itemId}`;
```

2. `services/queries/bids.ts`

```typescript
...
const serializeHistory = (amount: number, createdAt: number) => {
	return `${amount}:${createdAt}`;
};

const deserializeHistory = (stored: string) => {
	const [amount, createdAt] = stored.split(':');
	return {
		amount: parseFloat(amount),
		createdAt: DateTime.fromMillis(parseInt(createdAt))
	};
};
```

### Retrieving Bid Histories ###
1. `services/types.ts` - `CreateBidAttrs`
2. Equation: `LRANGE history#a1 -3 -1`
	1. Ending index: `(-1 - offset)`
	2. Starting index: `(-1 * offset - count)`
3. `bids.ts`

```typescript
export const getBidHistory = async (itemId: string, offset = 0, count = 10): Promise<Bid[]> => {
	const startIndex = -1 * (offset + count);
	const endIndex = -1 * offset - 1;

	const range = await client.lRange(bidHistoryKey(itemId), startIndex, endIndex);

	return range.map((bid) => deserializeHistory(bid));
};
```

4. Testing: Place bids

## Section 16: More Practice with the E-Commerce App ##
### More on Bids ###
1. More bid related implementation
2. On bid creation:
	1. Does the item exist?
	2. Is the item still open for bids?
	3. Is the bid amount greater than the existing highest bid?
	4. Add the bid to bid history list (done)
	5. Update the # of bids the item has
	6. Update the item's price
	7. Update the item's highestUserBidId
	8. Update the item's score in the item price sorted set
3. Most expensive: To do

### Validating Bids ###
1. Validations:
2. `bids.ts`

```typescript
import { getItem } from './items';

export const createBid = async (attrs: CreateBidAttrs) => {
	const item = await getItem(attrs.itemId);

	if (!item) {
		throw new Error('Item does not exist');
	}

	if (item.price >= attrs.amount) {
		throw new Error('Bid too low');
	}

	if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
		throw new Error('Item closed to bidding');
	}

	const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());
	return await client.rPush(bidHistoryKey(attrs.itemId), serialized);
};
```

### Updating Items with Bids ###
1. `bids.ts`

```typescript
export const createBid = async (attrs: CreateBidAttrs) => {
	const item = await getItem(attrs.itemId);

	if (!item) {
		throw new Error('Item does not exist');
	}

	if (item.price >= attrs.amount) {
		throw new Error('Bid too low');
	}

	if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
		throw new Error('Item closed to bidding');
	}

	const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

	return await Promise.all([
		client.rPush(bidHistoryKey(attrs.itemId), serialized),
		client.hSet(itemsKey(item.id), {
			bids: item.bids + 1,
			price: attrs.amount,
			highestBidUserId: attrs.userId
		})
	]);
};
```

2. Developer tools

```
for (let i = 0; i < 15; i++) {
  $0.click();
}
```

	1. `$0` - element select in element picker
		1. Bid history shows many entries (multiple requests succeeded)

### Issues with Bids ###
1. What's happening?
	1. Server
		1. Get item from Redis
		2. Deserialize it
		3. Run validations
		4. Make updates + save (this takes time)
			1. If multiple requests are made:
				1. Both can get the same item
				2. Both can then save at the same time

### Understanding Concurrency Issues ###
1. General concurrency problem
	1. This is an issue any time we fetch data then use it to make an update
		1. Data changes as result of some other request
	2. When not a problem
		1. Example: Todo list
			1. One request marks todo as 'complete'
			2. One request marks todo as 'started'
				1. We might be okay to run into an issue
					1. Most recent request will succeed
2. Options for handling concurrency
	1. Use an atomic update command (like `HINCRBY` or `HSETNX`)
	2. Use a transaction with the 'WATCH' command
	3. Use a lock
	4. Use a custom LUA update script

### Applying Atomic Updates ###
1. Time between reading + writing data
2. Example: Selling cars
	1. car -> inStock
		1. We want to update the stock
			1. One way:
				1. Retrieve hash
				2. Add 1
				3. Save the hash
			2. Second way:
				1. Don't read
				2. `HINCRBY car instock 1` (atomic)
	2. car -> color
		1. We want set if it has not been set before
			1. One way:
				1. Read hash
				2. Set the property (if not set) - two requests can set the property (red, blue)
			2. Another way:
				1. `HSETNX` - only if it has not exists (not set before)
					1. `HSETNX car color red`
3. The two commands do not work in our case

### Transactions ###
1. Transactions
	1. Groups together one or more commands to run sequentially
		1. Nothing else should be executed in between them
	2. Similar to pipelining, but some big differences!
		1. No guarantee that they will be executed one after another (without any other commands in between)
	3. Transactions cannot be undone/rolledback/reversed!
		1. Unlike other databases
2. What are they?
	1. `MULTI` - start a new transaction
	2. `SET color red`, `SET count 5` - Queue up this command to run
	3. `EXEC` - Run all the queued commands
3. `npx rbook`

```
MULTI
```

```
SET color red
SET count 5
```
	
	1. `"QUEUED"`
	
```
EXEC
```

### Watching a Key with Transactions ###
1. `WATCH color`
	1. Watch the key 'color' until the next transaction is executed. If it changes, cancel the transaction
		1. If the value changes before we run a transaction, then fail the transaction
			1. If `SET color blue` is run by another client
				1. The following transaction will fail
					1. `MULTI`
					2. `SET color red`
					3. `EXEC`
						1. Returns `null`
						
```
MULTI

SET color blue

MULTI
SET color red
SET count 5
EXEC
```

	1. Returns `null`

### Isolated Connections for Transactions ###
1. Patterns:
	1. Server
	
	```
	WATCH color
	
	GET color
	GET count
	
	MULTI
	SET color red
	SET count 5	
	EXEC
	```
	
		1. Transaction can get cancelled
		
2. Bids

```
WATCH item:a1

HGETALL item:a1

MULTI
HSET item:a1 amount 10 bids 1
RPUSH items
EXEC
```

	1. If any other request modifies the item, the transaction will be cancelled
3. We might make multiple connections to Redis
	1. `WATCH` and `MULTI` - Connection only to be used for the transaction
		1. A separate connection can be used for the transaction only and close it
			1. The other connection is used for regular commands

### Solving Multiple Bids with a Transaction ###
1. `bids.ts`

```typescript
export const createBid = async (attrs: CreateBidAttrs) => {
	return client.executeIsolated(async (isolatedClient) => {
		await isolatedClient.watch(itemsKey(attrs.itemId));

		const item = await getItem(attrs.itemId);

		if (!item) {
			throw new Error('Item does not exist');
		}

		if (item.price >= attrs.amount) {
			throw new Error('Bid too low');
		}

		if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
			throw new Error('Item closed to bidding');
		}

		const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

		return await isolatedClient
			.multi()
			.rPush(bidHistoryKey(attrs.itemId), serialized)
			.hSet(itemsKey(item.id), {
				bids: item.bids + 1,
				price: attrs.amount,
				highestBidUserId: attrs.userId
			})
			.exec();
	});
};
```

### Items by Price ###
1. `items:price` - sorted set
	1. On item create
		1. Add itemID to sorted set with score of 0
	2. On bid create
		1. Update score in sorted set
2. `keys.ts`

```typescript
export const itemsByPriceKey = () => 'items:price';
```

3. `queries/items/items.ts`

```typescript
export const createItem = async (attrs: CreateItemAttrs, userId: string) => {
	const id = genId();

	const serialized = serialize(attrs);

	await Promise.all([
		client.hSet(itemsKey(id), serialized),
		client.zAdd(itemsByViewsKey(), {
			value: id,
			score: 0
		}),
		client.zAdd(itemsByEndingAtKey(), {
			value: id,
			score: attrs.endingAt.toMillis()
		}),
		client.zAdd(itemsByPriceKey(), {
			value: id,
			score: 0
		})
	]);

	return id;
};
```

4. `queries/bids.ts`

```typescript
export const createBid = async (attrs: CreateBidAttrs) => {
	return client.executeIsolated(async (isolatedClient) => {
		await isolatedClient.watch(itemsKey(attrs.itemId));

		const item = await getItem(attrs.itemId);

		if (!item) {
			throw new Error('Item does not exist');
		}

		if (item.price >= attrs.amount) {
			throw new Error('Bid too low');
		}

		if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
			throw new Error('Item closed to bidding');
		}

		const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

		return await isolatedClient
			.multi()
			.rPush(bidHistoryKey(attrs.itemId), serialized)
			.hSet(itemsKey(item.id), {
				bids: item.bids + 1,
				price: attrs.amount,
				highestBidUserId: attrs.userId
			})
			.zAdd(itemsByPriceKey(), {
				value: item.id,
				score: attrs.amount
			})
			.exec();
	});
};
```

### More on Items by Price ###
1. `queries/items/by-price.ts`

```typescript
import { client } from '$services/redis';
import { itemsKey, itemsByPriceKey } from '$services/keys';
import { deserialize } from './deserialize';

export const itemsByPrice = async (order: 'DESC' | 'ASC' = 'DESC', offset = 0, count = 10) => {
	let results: any = await client.sort(itemsByPriceKey(), {
		GET: [
			'#',
			`${itemsKey('*')}->name`,
			`${itemsKey('*')}->views`,
			`${itemsKey('*')}->endingAt`,
			`${itemsKey('*')}->imageUrl`,
			`${itemsKey('*')}->price`
		],
		BY: 'score',
		DIRECTION: order,
		LIMIT: {
			offset,
			count
		}
	});

	const items = [];
	while (results.length) {
		const [id, name, views, endingAt, imageUrl, price, ...rest] = results;
		const item = deserialize(id, { name, views, endingAt, imageUrl, price });
		items.push(item);
		results = rest;
	}

	return items;
};
```

## Section 17: Extending Redis with Scripting ##
### Lua Scripting ###
1. Example:
	1. Sorted set
		1. a -> 1
		2. b -> 2
		3. ...
	2. Find all members with score that is a multiple of 2
	3. Get all members / scores
		1. Too much data (data overfetching)
	4. Apply filter on server (takes time)
2. Solution: Lua scripts
	1. Access sorted set
	2. Find members with scores > 4
	3. Return result
		1. The script is sent to Redis
		2. Redis runs LUA script
		3. Filtered results are sent back
3. Lua scripts
	1. Has full access to all Redis commands
	2. It can run multiple commands
	3. Only the final results are returned (no data overfetching)

### Basics of Lua ###
1. Search: online lua
	1. Tutorialspoint
	2. [https://onecompiler.com/lua](https://onecompiler.com/lua)
	
2. Lua examples:

```lua
print(123)
print('Hi there')
print("Hi there!")

local sum = 1 + 1
print(sum)

if sum > 0 then
  print('sum is greater than 0')
end

if sum ~= 0 then
  print('sum is not equal to 0')
end

if sum == 0 then
  print('sdfsdf')
end

if 0 and '' then
    print('0 is truthy')
end

if false or not true then
    print('adgsdf')
end

if nil then
    print('wont run')
end
```

### Handling Arrays ###
1. Examples:

```lua
local colors = {'red', 'green', 'blue'}
print(colors[1])
print(#colors)

table.insert(colors, 'orange')

print(colors[4])

for i, v in ipairs(colors) do
  print(i, v)
end
```

### Handling Tables ###
1. Examples:

```lua
for i = 5, 10 do
  print(i)
end
```

2. Objects are tables in lua (similar)

```lua
local user = {id = 'a1', name = 'samantha'}

print(user['id'])

for k, v in pairs(user) do
    print(k, v)
end
```

### Loading and Executing Scripts ###
1. Steps:
	1. Write the script
	2. Load the script
		1. Redis stores the script so it can be ran in the future, then sends back an ID for the script
	3. Hold onto script ID
		1. To tell redis to run the script with the id
	4. Time to run the script
		1. `EVALSHA <ID>`
			1. Run script
			2. Get returned value
			3. Send value back to server
	5. Use value for something
2. `npx rbook`

```
SCRIPT LOAD 'return 1 + 1'
```

	1. `return` - value is sent back to user

```
EVALSHA c301e0c5bc3538d2bad3fdbf2e281887e643ada4 0
```

	1. A new id per script

### Providing Arguments ###
1. Example: We want to add one
	1. One way: Multiple scripts (one for each variation)
	2. Second way: Arguments
	
	```
	return 1 + ARGV[1]
	```
	
		1. `ARGV` - global variable. An array.
			1. `EVALSHA <ID> 0 '1'`
				1. `1` - Argument to script - always a string
			2. Redis defines the array with the passed arguments
2. `npx rbook`

```
SCRIPT LOAD 'return 1 + tonumber(ARGV[1])'

EVALSHA f54696c104acb23787e4d627c487221c6f79ace7 0 '100'
```

```
SCRIPT LOAD 'return 1 + tonumber(ARGV[1]) + tonumber(ARGV[2])'

EVALSHA c64fe48b79aa91f6624b133ff9f588642817d8e4 0 '100' '200'
```

### Providing Key lists ###
1. Running a command
	1. `return redis.call('GET', 'color')`
	2. `EVALSHA <ID> 0`
		1. This script has a huge issue! Don't use this! (?)
2. `npx rbook`

```
SET color red
SCRIPT LOAD 'return redis.call("GET", "color")'

EVALSHA 5c319cc258f79a4a2387edac10122cb4ee3770ea 0

EVALSHA 5c319cc258f79a4a2387edac10122cb4ee3770ea 1 color
```

3. `EVALSHA <ID> 1 color`
	1. `1` - # keys we are about to list
	2. `color` - key we want to access
		1. Redis needs to know exactly which keys we want to access ahead of time (?)
	3. Alternative: `return redis.call('GET', KEYS[1])`
		1. `1` - # keys we are about to list (we are giving one key)
			1. `EVALSHA <ID> 1 color`
				1. The key is `color`
			2. To distinguish between keys are arguments
				1. First one is key, the subsequent ones are arguments
	4. We cannot have Redis look up dynamic keys
		1. Each key must be provided explicitly

### When to Use Scripts ###
1. When to use scripts?
	1. Limiting the amount of data exchanged between server + redis
		1. Filter in redis and return
	2. Solving some concurrency issues (more on this later)
	3. Minimizing the number of round trips between server + redis
		1. chaining commands and returning final result (fewer round-trips)
	4. ...
2. Script down sides
	1. Keys must be known ahead of time
		1. Limits use-cases
	2. Tough to test scripts
		1. Additional tooling is required
	3. Loss of language features (e.g. type checking with Typescript)
		1. Lua: Dynamic weakly typed language
	4. Another language to deal with (Lua)
3. Single round-trip: `views.ts`

### Custom Scripts with Node-Redis ###
1. `node-redis` library
	1. `SCRIPT LOAD`, `EVALSHA` - tedious to use yourself (extra work)
		1. Solution: Advanced features to automate them
			1. Goal:
				1. Calling: `client.addOneAndStore('books:count' 5)`
					1. Should add 1 to the argument '5' and store the result at the key 'books:count'
					2. Steps:
						1. Name of function (how do we call this our JS code?)
							1. `addOneAndStore`
						2. The script itself
						3. `#` of keys that will be provided (for the evalsha command)
						4. Instructions on how to pass arguemnts to the script
						5. Instructions on how to parse the response form the script (deserialization)

### Lua Script Integration ###
1. `services/redis/client.ts`

```typescript
import { createClient, defineScript } from 'redis';

const client = createClient({
	socket: {
		host: process.env.REDIS_HOST,
		port: parseInt(process.env.REDIS_PORT)
	},
	password: process.env.REDIS_PW,
	scripts: {
		addOneAndStore: defineScript({
			NUMBER_OF_KEYS: 1,
			SCRIPT: `
			  return redis.call('SET', KEYS[1], 1 + tonumber(ARGV[1]))
			`,
			transformArguments(key: string, value: number) {
				return [key, value.toString()];
			},
			transformReply(reply: any) {
				return reply;
			} // No additional parsing required
		}) // EVALSHA <ID> 1 'books:count' '5'
	}
});

// client.addOneAndStore();

client.on('connect', async () => {
	await client.addOneAndStore('books:count', 5);
	const result = await client.get('books:count');
	console.log(result); // Should print 6
});

client.on('error', (err) => console.error(err));
client.connect();

export { client };
```

### Constructing a View-Incrementing Script ###
1. Scripting Design Pattern
	1. Identify all the keys and arguments you want to access
	2. Assign the keys (KEYS) and arguments (ARGV) to well-labeled variables at the top of the script
	3. Write your logic
	4. Don't forget to return a value if you need to
2. `Views.ts`

```typescript
// Keys I need to access
// 1) itemsViewsKey -> 
// 2) itemsKey -> items#sadfsdf
// 3) itemsByViewsKey
// EVALSHA ID 3

// Arguments I need to accept
// 1) itemId
// 2) userId
```

3. `client.ts`

```typescript
import { createClient, defineScript } from 'redis';
import { itemsKey, itemsByViewsKey, itemsViewsKey } from '$services/keys';

const client = createClient({
	socket: {
		host: process.env.REDIS_HOST,
		port: parseInt(process.env.REDIS_PORT)
	},
	password: process.env.REDIS_PW,
	scripts: {
		addOneAndStore: defineScript({
			NUMBER_OF_KEYS: 1,
			SCRIPT: `
			  return redis.call('SET', KEYS[1], 1 + tonumber(ARGV[1]))
			`,
			transformArguments(key: string, value: number) {
				return [key, value.toString()];
			},
			transformReply(reply: any) {
				return reply;
			}
		}),
		incrementView: defineScript({
			NUMBER_OF_KEYS: 3,
			SCRIPT: `
			  local itemsViewsKey = KEYS[1]
				local itemsKey = KEYS[2]
				local itemsByViewsKey = KEYS[3]
				local itemId = ARGV[1]
				local userId = ARGV[2]

				local inserted = redis.call('PFADD', itemsViewsKey, userId)

				if inserted == 1 then
				  redis.call('HINCRBY', itemsKey, 'views', 1)
					redis.call('ZINCRBY', itemsByViewsKey, 1, itemId)
				end
			`,
			transformArguments(itemId: string, userId: string) {
				return [itemsViewsKey(itemId), itemsKey(itemId), itemsByViewsKey(), itemId, userId];
			},
			transformReply() {}
		})
	}
});

// No additional parsing required
// EVALSHA <ID> 1 'books:count' '5'
// client.addOneAndStore();

client.on('connect', async () => {
	await client.addOneAndStore('books:count', 5);
	const result = await client.get('books:count');
	console.log(result); // Should print 6
});

client.on('error', (err) => console.error(err));
client.connect();

export { client };
```

4. `views.ts`

```typescript
import { client } from '$services/redis';

export const incrementView = async (itemId: string, userId: string) => {
	return await client.incrementView(itemId, userId);
};

// Keys I need to access
// 1) itemsViewsKey ->
// 2) itemsKey -> items#sadfsdf
// 3) itemsByViewsKey
// EVALSHA ID 3

// Arguments I need to accept
// 1) itemId
// 2) userId
```

### Code Cleanup ###
1. Remove: `client.on('connect', ...)`

## Section 18: Understanding and Solving Concurrency Issues ##
### Concurrency Revisited ###
1. Issue: Request to add a bid amount: 15
	1. Make sure the bid in request is > bid in item hash
		1. Multiple bids can cause a race condition (can accidentally decrease the bid value)
			1. If we first process lower amount and then higher amount, it will be cancelled (a valid bid)
		2. One solution:
			1. Re-try mechanism
				1. Problems: Doesn't scale well (`WATCH` slows down Redis)
					1. Additional load on Redis

### Issues with WATCH ###
1. Testing setup
	1. Suppose many bids for a single item
		1. Three copies of node server
		2. Three bidder scripts
	2. We want all bids to succeed (every valid bid)

### Overview of a Lock ###
1. Two processes are reading and writing at the same time (race condition)
	1. If process 1 goes first or process 2
		1. Solution: Only one process can modify a value at a time using lock
			1. Example: `lock:item:a1` (any name)
				1. `SET lock:item:a1 hi NX`
					1. `NX` - only set if it isn't already set
						1. If it is set, it will return null
				2. `SET lock:item:a1 bye NX`
					1. Returns `null`
						1. Process 1 gets exclusive access to the hash `item:a1`
						2. Process 2 will retry until it succeeds
				3. `DEL lock:item:a1`
					1. The value is removed
						1. Process 2 will succeed (the value doesn't exist)

### Understanding the Goal ###
1. Note
	1. Our concurrency system will implement a simplified version of the Redlock algorithm (production grade)
		1. Many languages have Redlock algorithm implementations
			1. Redis documentation
	2. On any serious project, use Redlock instead of what we're building here
2. Note 2:
	1. We will build our lock in Typescript
	2. This will involve some heavy-duty Typescript code
	3. If you don't want to write TS just skip ahead
3. `bids.ts`

```typescript
export const createBid = async (attrs: CreateBidAttrs) => {
	return withLock(attrs.itemId, () => {
		// 1) Fetching the item
		// 2) Doing validation
		// 3) Writing some data
	});
	...
```

### Implementing WithLock ###
1. `services/redis/lock.ts`

```typescript
import { client } from '$services/redis';
import { randomBytes } from 'crypto';

export const withLock = async (key: string, cb: () => any) => {
	// Initialize a few variables retry behavior
	const retryDelayMs = 100;
	let retries = 20;

	// Generate a random value to store at the lock key
	const token = randomBytes(6).toString('hex');

	// Generate the lock key
	const lockKey = `lock:${key}`;

	// Set up a while loop to implement the retry behavior
	while (retries >= 0) {
		retries--;
		// Try to do a SET NX operation
		const acquired = await client.set(lockKey, token, {
			NX: true
		});

		if (!acquired) {
			// ELSE brief pause (retryDelayMs) and then retry
			await pause(retryDelayMs);
			continue;
		}

		// IF the set is successful, then run the callback
		const result = await cb();
		return result;
	}

	// Unset the locked key
	await client.del(lockKey);
};

const buildClientProxy = () => {};

const pause = (duration: number) => {
	return new Promise((resolve) => {
		setTimeout(resolve, duration);
	});
};
```

### Using WithLock ###
1. `bids.ts`

```typescript
import type { CreateBidAttrs, Bid } from '$services/types';
import { bidHistoryKey, itemsKey, itemsByPriceKey } from '$services/keys';
import { client } from '$services/redis';
import { DateTime } from 'luxon';
import { getItem } from './items';
import { withLock } from '$services/redis/lock';

export const createBid = async (attrs: CreateBidAttrs) => {
	return withLock(attrs.itemId, async () => {
		// 1) Fetching the item
		// 2) Doing validation
		// 3) Writing some data

		const item = await getItem(attrs.itemId);

		if (!item) {
			throw new Error('Item does not exist');
		}

		if (item.price >= attrs.amount) {
			throw new Error('Bid too low');
		}

		if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
			throw new Error('Item closed to bidding');
		}

		const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

		return Promise.all([
			client.rPush(bidHistoryKey(attrs.itemId), serialized),
			client.hSet(itemsKey(item.id), {
				bids: item.bids + 1,
				price: attrs.amount,
				highestBidUserId: attrs.userId
			}),
			client.zAdd(itemsByPriceKey(), {
				value: item.id,
				score: attrs.amount
			})
		]);
	});

	// return client.executeIsolated(async (isolatedClient) => {
	// 	await isolatedClient.watch(itemsKey(attrs.itemId));

	// 	const item = await getItem(attrs.itemId);

	// 	if (!item) {
	// 		throw new Error('Item does not exist');
	// 	}

	// 	if (item.price >= attrs.amount) {
	// 		throw new Error('Bid too low');
	// 	}

	// 	if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
	// 		throw new Error('Item closed to bidding');
	// 	}

	// 	const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

	// 	return await isolatedClient
	// 		.multi()
	// 		.rPush(bidHistoryKey(attrs.itemId), serialized)
	// 		.hSet(itemsKey(item.id), {
	// 			bids: item.bids + 1,
	// 			price: attrs.amount,
	// 			highestBidUserId: attrs.userId
	// 		})
	// 		.zAdd(itemsByPriceKey(), {
	// 			value: item.id,
	// 			score: attrs.amount
	// 		})
	// 		.exec();
	// });
};

export const getBidHistory = async (itemId: string, offset = 0, count = 10): Promise<Bid[]> => {
	const startIndex = -1 * (offset + count);
	const endIndex = -1 * offset - 1;

	const range = await client.lRange(bidHistoryKey(itemId), startIndex, endIndex);

	return range.map((bid) => deserializeHistory(bid));
};

const serializeHistory = (amount: number, createdAt: number) => {
	return `${amount}:${createdAt}`;
};

const deserializeHistory = (stored: string) => {
	const [amount, createdAt] = stored.split(':');
	return {
		amount: parseFloat(amount),
		createdAt: DateTime.fromMillis(parseInt(createdAt))
	};
};
```

### It Works! ###
1. 100% - 10 tims longer

### Automatically Expiring Locks ###
1. Testing:
	1. Add an item
	2. Valid bid
	3. Invalid bid
	4. Valid bid
		1. Hangs
		2. Shows old high bid
2. Unlocking
	1. `withLock` must handle errors
		1. There could be unrecoverable error (server crashes) before we unlock
			1. Solution: `SET lock:item:a1 hi NX PX 2000`
				1. `PX` - automatically unset this key after this many MS
					1. if `DEL` is not called
					
					2. `lock.ts`
					
					```typescript
					const acquired = await client.set(lockKey, token, {
					  NX: true,
					  PX: 2000
					});
					```
		2. Error-handling
		
		```typescript
		export const withLock = async (key: string, cb: () => any) => {
			// Initialize a few variables retry behavior
			const retryDelayMs = 100;
			let retries = 20;

			// Generate a random value to store at the lock key
			const token = randomBytes(6).toString('hex');

			// Generate the lock key
			const lockKey = `lock:${key}`;

			// Set up a while loop to implement the retry behavior
			while (retries >= 0) {
				retries--;
				// Try to do a SET NX operation
				const acquired = await client.set(lockKey, token, {
					NX: true,
					PX: 2000
				});

				if (!acquired) {
					// ELSE brief pause (retryDelayMs) and then retry
					await pause(retryDelayMs);
					continue;
				}

				// IF the set is successful, then run the callback
				try {
					const result = await cb();
					return result;
				} finally {
					await client.del(lockKey);
				}
			}

			// Unset the locked key
		};
		```

### Another Lock Issue ###
1. Issue:
	1. Process 1: Acquires a lock
		1. Processes and sends a `DEL`
			1. Suppose process takes time to process (with auto expiry)
	2. Process 2: Acquires the lock
2. Issue:
	1. We don't know how long it takes for a command to send to redis and get it processed
	2. Process 1: takes time to process
		1. Lock expires before `DEL` command executes
	3. Process 2: Acquires the lock
		1. Process 1's `DEL` deletes the lock
		2. Process 2 loses the lock
	4. Process 3: Acquires the lock
3. Solution:
	1. P 1 should `DEL` only if the token matches (not another process's token)
		1. Problem: Lock expires before we run `DEL` again

### Solving Accidental Unlocks ###
1. Lua Script solution - The entire script will get executed atomically (no other commands in between)
	1. Solution: Pseudocode
	
	```lua
	if GET(KEYS[1]) == ARGV[1] then
	  DEL(KEYS[1])
	end
	```

### Adding an Unlock Script ###
1. `client.ts`

```typescript
import { createClient, defineScript } from 'redis';
import { itemsKey, itemsByViewsKey, itemsViewsKey } from '$services/keys';

const client = createClient({
	socket: {
		host: process.env.REDIS_HOST,
		port: parseInt(process.env.REDIS_PORT)
	},
	password: process.env.REDIS_PW,
	scripts: {
		unlock: defineScript({
			NUMBER_OF_KEYS: 1,
			transformArguments(key: string, token: string) {
				return [key, token];
			},
			transformReply(reply: any) {
				return reply;
			},
			SCRIPT: `
			  if redis.call('GET', KEYS[1]) == ARGV[1] then
				  return redis.call('DEL', KEYS[1])
				end
			`
		}),
		addOneAndStore: defineScript({
			NUMBER_OF_KEYS: 1,
			SCRIPT: `
			  return redis.call('SET', KEYS[1], 1 + tonumber(ARGV[1]))
			`,
			transformArguments(key: string, value: number) {
				return [key, value.toString()];
			},
			transformReply(reply: any) {
				return reply;
			}
		}),
		incrementView: defineScript({
			NUMBER_OF_KEYS: 3,
			SCRIPT: `
			  local itemsViewsKey = KEYS[1]
				local itemsKey = KEYS[2]
				local itemsByViewsKey = KEYS[3]
				local itemId = ARGV[1]
				local userId = ARGV[2]

				local inserted = redis.call('PFADD', itemsViewsKey, userId)

				if inserted == 1 then
				  redis.call('HINCRBY', itemsKey, 'views', 1)
					redis.call('ZINCRBY', itemsByViewsKey, 1, itemId)
				end
			`,
			transformArguments(itemId: string, userId: string) {
				return [itemsViewsKey(itemId), itemsKey(itemId), itemsByViewsKey(), itemId, userId];
			},
			transformReply() {}
		})
	}
});

// No additional parsing required
// EVALSHA <ID> 1 'books:count' '5'
// client.addOneAndStore();

client.on('connect', async () => {
	await client.addOneAndStore('books:count', 5);
	const result = await client.get('books:count');
	console.log(result); // Should print 6
});

client.on('error', (err) => console.error(err));
client.connect();

export { client };
```

2. `lock.ts`

```typescript
        ...
		try {
			const result = await cb();
			return result;
		} finally {
			await client.unlock(lockKey, token);
		}
		...
```

### One Last Issue ###
1. Lock is not truly secure
	1. Nothing is preventing a write to a hash
		1. We are only setting lock varible
	2. Example: `cb` takes a long time to run
		1. We are automatically expiring before that
		2. It can still write after expiration
			1. Nothing preventing writing to hash
2. Fix:
	1. Abort if lock has expired

### Providing Expiration Signals ###
1. `bids.ts`

```typescript
import type { CreateBidAttrs, Bid } from '$services/types';
import { bidHistoryKey, itemsKey, itemsByPriceKey } from '$services/keys';
import { client } from '$services/redis';
import { DateTime } from 'luxon';
import { getItem } from './items';
import { withLock } from '$services/redis/lock';

export const createBid = async (attrs: CreateBidAttrs) => {
	return withLock(attrs.itemId, async (signal: any) => {
		// 1) Fetching the item
		// 2) Doing validation
		// 3) Writing some data

		const item = await getItem(attrs.itemId);

		if (!item) {
			throw new Error('Item does not exist');
		}

		if (item.price >= attrs.amount) {
			throw new Error('Bid too low');
		}

		if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
			throw new Error('Item closed to bidding');
		}

		const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

		if (signal.expired) {
			throw new Error('Lock expired, cant write anymore data');
		}

		return Promise.all([
			client.rPush(bidHistoryKey(attrs.itemId), serialized),
			client.hSet(itemsKey(item.id), {
				bids: item.bids + 1,
				price: attrs.amount,
				highestBidUserId: attrs.userId
			}),
			client.zAdd(itemsByPriceKey(), {
				value: item.id,
				score: attrs.amount
			})
		]);
	});

	// return client.executeIsolated(async (isolatedClient) => {
	// 	await isolatedClient.watch(itemsKey(attrs.itemId));

	// 	const item = await getItem(attrs.itemId);

	// 	if (!item) {
	// 		throw new Error('Item does not exist');
	// 	}

	// 	if (item.price >= attrs.amount) {
	// 		throw new Error('Bid too low');
	// 	}

	// 	if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
	// 		throw new Error('Item closed to bidding');
	// 	}

	// 	const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

	// 	return await isolatedClient
	// 		.multi()
	// 		.rPush(bidHistoryKey(attrs.itemId), serialized)
	// 		.hSet(itemsKey(item.id), {
	// 			bids: item.bids + 1,
	// 			price: attrs.amount,
	// 			highestBidUserId: attrs.userId
	// 		})
	// 		.zAdd(itemsByPriceKey(), {
	// 			value: item.id,
	// 			score: attrs.amount
	// 		})
	// 		.exec();
	// });
};

export const getBidHistory = async (itemId: string, offset = 0, count = 10): Promise<Bid[]> => {
	const startIndex = -1 * (offset + count);
	const endIndex = -1 * offset - 1;

	const range = await client.lRange(bidHistoryKey(itemId), startIndex, endIndex);

	return range.map((bid) => deserializeHistory(bid));
};

const serializeHistory = (amount: number, createdAt: number) => {
	return `${amount}:${createdAt}`;
};

const deserializeHistory = (stored: string) => {
	const [amount, createdAt] = stored.split(':');
	return {
		amount: parseFloat(amount),
		createdAt: DateTime.fromMillis(parseInt(createdAt))
	};
};
```

2. `lock.ts`

```typescript
import { client } from '$services/redis';
import { randomBytes } from 'crypto';

export const withLock = async (key: string, cb: (signal: any) => any) => {
	// Initialize a few variables retry behavior
	const retryDelayMs = 100;
	let retries = 20;

	// Generate a random value to store at the lock key
	const token = randomBytes(6).toString('hex');

	// Generate the lock key
	const lockKey = `lock:${key}`;

	// Set up a while loop to implement the retry behavior
	while (retries >= 0) {
		retries--;
		// Try to do a SET NX operation
		const acquired = await client.set(lockKey, token, {
			NX: true,
			PX: 2000
		});

		if (!acquired) {
			// ELSE brief pause (retryDelayMs) and then retry
			await pause(retryDelayMs);
			continue;
		}

		// IF the set is successful, then run the callback
		try {
			const signal = { expired: false };
			setTimeout(() => {
				signal.expired = true;
			}, 2000);

			const result = await cb(signal);
			return result;
		} finally {
			await client.unlock(lockKey, token);
		}
	}

	// Unset the locked key
};

const buildClientProxy = () => {};

const pause = (duration: number) => {
	return new Promise((resolve) => {
		setTimeout(resolve, duration);
	});
};
```

### Alternate Expiration Solution ###
1. `locks.ts`

```typescript
import { client } from '$services/redis';
import { randomBytes } from 'crypto';

export const withLock = async (key: string, cb: (redisClient: Client, signal: any) => any) => {
	// Initialize a few variables retry behavior
	const retryDelayMs = 100;
	const timeoutMs = 2000;
	let retries = 20;

	// Generate a random value to store at the lock key
	const token = randomBytes(6).toString('hex');

	// Generate the lock key
	const lockKey = `lock:${key}`;

	// Set up a while loop to implement the retry behavior
	while (retries >= 0) {
		retries--;
		// Try to do a SET NX operation
		const acquired = await client.set(lockKey, token, {
			NX: true,
			PX: 2000
		});

		if (!acquired) {
			// ELSE brief pause (retryDelayMs) and then retry
			await pause(retryDelayMs);
			continue;
		}

		// IF the set is successful, then run the callback
		try {
			const signal = { expired: false };
			setTimeout(() => {
				signal.expired = true;
			}, timeoutMs);

			const proxiedClient = buildClientProxy(timeoutMs);
			const result = await cb(proxiedClient, signal);
			return result;
		} finally {
			await client.unlock(lockKey, token);
		}
	}

	// Unset the locked key
};

type Client = typeof client;
const buildClientProxy = (timeoutMs: number) => {
	const startTime = Date.now();

	const handler = {
		get(target: Client, prop: keyof Client) {
			if (Date.now() >= startTime + timeoutMs) {
				throw new Error('Lock has expired.');
			}

			const value = target[prop];
			return typeof value === 'function' ? value.bind(target) : value;
		}
	};

	return new Proxy(client, handler) as Client;
};

const pause = (duration: number) => {
	return new Promise((resolve) => {
		setTimeout(resolve, duration);
	});
};
```

2. `bids.ts`

```typescript
import type { CreateBidAttrs, Bid } from '$services/types';
import { bidHistoryKey, itemsKey, itemsByPriceKey } from '$services/keys';
import { client } from '$services/redis';
import { DateTime } from 'luxon';
import { getItem } from './items';
import { withLock } from '$services/redis/lock';

export const createBid = async (attrs: CreateBidAttrs) => {
	return withLock(attrs.itemId, async (lockedClient: typeof client, signal: any) => {
		// 1) Fetching the item
		// 2) Doing validation
		// 3) Writing some data

		const item = await getItem(attrs.itemId);

		if (!item) {
			throw new Error('Item does not exist');
		}

		if (item.price >= attrs.amount) {
			throw new Error('Bid too low');
		}

		if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
			throw new Error('Item closed to bidding');
		}

		const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

		if (signal.expired) {
			throw new Error('Lock expired, cant write anymore data');
		}

		return Promise.all([
			lockedClient.rPush(bidHistoryKey(attrs.itemId), serialized),
			lockedClient.hSet(itemsKey(item.id), {
				bids: item.bids + 1,
				price: attrs.amount,
				highestBidUserId: attrs.userId
			}),
			lockedClient.zAdd(itemsByPriceKey(), {
				value: item.id,
				score: attrs.amount
			})
		]);
	});

	// return client.executeIsolated(async (isolatedClient) => {
	// 	await isolatedClient.watch(itemsKey(attrs.itemId));

	// 	const item = await getItem(attrs.itemId);

	// 	if (!item) {
	// 		throw new Error('Item does not exist');
	// 	}

	// 	if (item.price >= attrs.amount) {
	// 		throw new Error('Bid too low');
	// 	}

	// 	if (item.endingAt.diff(DateTime.now()).toMillis() < 0) {
	// 		throw new Error('Item closed to bidding');
	// 	}

	// 	const serialized = serializeHistory(attrs.amount, attrs.createdAt.toMillis());

	// 	return await isolatedClient
	// 		.multi()
	// 		.rPush(bidHistoryKey(attrs.itemId), serialized)
	// 		.hSet(itemsKey(item.id), {
	// 			bids: item.bids + 1,
	// 			price: attrs.amount,
	// 			highestBidUserId: attrs.userId
	// 		})
	// 		.zAdd(itemsByPriceKey(), {
	// 			value: item.id,
	// 			score: attrs.amount
	// 		})
	// 		.exec();
	// });
};

export const getBidHistory = async (itemId: string, offset = 0, count = 10): Promise<Bid[]> => {
	const startIndex = -1 * (offset + count);
	const endIndex = -1 * offset - 1;

	const range = await client.lRange(bidHistoryKey(itemId), startIndex, endIndex);

	return range.map((bid) => deserializeHistory(bid));
};

const serializeHistory = (amount: number, createdAt: number) => {
	return `${amount}:${createdAt}`;
};

const deserializeHistory = (stored: string) => {
	const [amount, createdAt] = stored.split(':');
	return {
		amount: parseFloat(amount),
		createdAt: DateTime.fromMillis(parseInt(createdAt))
	};
};
```

## Section 19: Querying Data with RediSearch ##
### Redis Modules ###
1. Additional capabilites are added through modules
	1. Modules: Separate programs we load into Redis
		1. We are adding additional data structures + commands to work with them
			1. Adding advanced features - we can add ourselves
	2. Popular modules
		1. RedisJSON
			1. JSON storage + manipulation
				1. Hashes don't allow deeply nested data
				2. This can store true JSON
		2. RediSearch
			1. True search + querying (and filtering of different keys)
				1. Multiple hashes can be searched

### Redis Core vs Redis Stack ###
1. Steps:
	1. Raw source code
	2. Compile
		1. Challenging
	3. Load using MODULE LOAD
2. Alternative Steps:
	1. Redis Stack - Includes several modules by default
		1. RediSearch
		2. RedisJSON
		3. RedisGraph
		4. RedisTimeSeries
		5. RedisBloom
	2. redis.io
		1. Redis Stack

### Using Modules in Production ###
1. Why didn't we just use modules at the start?
	1. Depending on how you deploy your app, you might not be able to use modules!
		1. Example: AWS, Google Cloud
			1. Redis instance
				1. Options:
					1. Option 1: AWS/GC runs Redis for you. Can't use modules here! (managed Redis)
						1. Setup
						2. Security updates
						3. Backup updates
						4. ...
							1. Solution: Basic data types
					2. Option 2: VM/Container you start
						1. Redis
							1. RedisJSON
							2. RediSearch
						2. Additional setup
							1. Install modules
							2. Security updates
							3. Backups
							4. ...
					3. Option 3: Redis Labs runs a copy of Redis for you on AWS/GC/Azure with a few modules preinstalled (happy medium)
						1. Redis cloud instance
							1. It was created on AWS/GC/Azure
								1. Managed instances
									1. No security, backups, etc. from us
						2. Support:
							1. RedisJSON
							2. RediSearch
							3. ...

### Overview on Search ###
1. RediSearch
	1. Why do we need it?
		1. Query on hash is challenging
			1. Needs accessory data structures (extra work)
				1. Solution: RediSearch allows us to run arbitrary search on hashes
					1. Examples:
						1. A price less than 45
						2. Color of 'green'
	2. Steps:
		1. Creation of Index
			1. Datatype that points to all different records we want to be able to search
				1. Once per hash
			2. We need to specify two things
				1. For which records we want to build the search for
					1. We provide a prefix.
						1. Example: Find all the keys that start with `items#` (all hashes with that key prefix)
					2. Index records some info about the fields
				2. Run a query
					1. Example: Using the index, find items with a particular name, color, price
	3. Commands:
		1. `FT.CREATE` **(M)**
		2. `FT.SEARCH` **(M)**

### Constructing and Using an Index ###
1. Redis cloud: https://cloud.redis.io/?_gl=1*1v11aa3*_gcl_au*NDgyODI0NjYyLjE3ODcwNzQxMTE.#/databases/14553603/subscription/3383742/view-bdb/configuration
2. Hashes:

```
HSET cars#a1 name 'fast car' color red year 1950
HSET cars#b1 name 'car' color red year 1960
HSET cars#c1 name 'old car' color blue year 1970
HSET cars#d1 name 'new car' color blue year 1990
```

```
FT.CREATE idx:cars ON HASH PREFIX 1 cars#
    SCHEMA name TEXT year NUMERIC color TAG
```

```
FT.SEARCH idx:cars '@name:(fast car)'
```

```
FT.SEARCH idx:cars '@color:{blue}'
```

```
FT.SEARCH idx:cars '@year:[1955 1980]'
```

### Details on Indexes ###
1. Discussion
	1. Querying - Gives the exact results you ask for
		1. Get all cars made in 1955 with a color of red
		2. Get all cars made before 1960 with a name of 'fast car'
		3. Get all cars with a color of blue
	2. Searching - Gives results that best answer your questions (close enough guess)
		1. Get all cars with a name like 'car that goes fast'
			1. Semantic search
		2. Get all cars related to '90 blue fast'
			1. year: 1990, color: blue, name: fast
		3. Get all cars related to 'gast var'
			1. Typos
2. `FT.CREATE`
	1. `idx:cars` - Name of the index
		1. Indexes usually follow the naming convention `idx:<thing>`
	2. `ON HASH`
		1. We want to build an index for searching hashes
			1. Specify the kind of records we want to search
				1. `HASH`
				2. `JSON`
	3. `PREFIX 1 cars#`
		1. Find all the keys that start with 'cars#' and index them
		2. Multiple prefixes can be used - the number indicates how many prefixes we are about to provide
	4. `SCHEMA`
		1. Describe the fields that should be indexed for each hash
		2. Don't have to list hte schema of every field in a hash - only the ones we want to search
	5. `name TEXT`
		1. `<name> <type>`
	6. `year NUMERIC`
	7. `color TAG`
3. `FT.DROPINDEX` - Delete an index

### Index Field Types ###
1. Types: `<name> <type>`
	1. `NUMERIC` - This field contains numbers
		1. For number based query over index
			1. Find all cars between 1950 and 2000
	2. `GEO` - Geographic coordinates
		1. For geographic queries
	3. `VECTOR` - Similarity queries
		1. Semantic search
	4. `TAG` - Used for exact string lookups
		1. Querying
			1. ID reference to another record
			2. Color of a product
				1. Strict set of colors
			3. Country that a product is made in
		2. Example: Cars with color 'red' (exact match)
	5. `TEXT`
		1. Searching
			1. Product names
			2. Product descriptions
			3. Review of a product
		2. Supports fuzzy search, typos, etc.
2. Example: Website
	1. Text field
		1. Can be marked as `TEXT`
			1. Any text
				1. With typos
				2. Anything
	2. Select dropdown
		1. Can be marked as `TAG`

### Numeric Queries ###
1. `FT.SEARCH` - [https://redis.io/commands/ft.search](https://redis.io/commands/ft.search)
	1. Query syntax
		1. Go through
		2. `@name:(fast)` - Do a text search on 'name'
		3. `@color:{red}` - Do a tag search on 'color'
		4. `@year:[1955 1960]` - Do a numeric search on 'year'
	2. Combining queries
	
	```
	FT.SEARCH idx:cars '@year:[1955 1960] @color:{blue}'
	```
	
	3. Quotes
		1. Single or double
		2. If we need quotes inside, use the other quote (single or double)
	4. Numeric queries:
		1. `@year:[1955 1980]` - Inclusive
		2. `@year:[(1955 (1980]` - Exclusive
		3. `@year:[1955 +inf]`
		4. `@year:[-inf 1955]`
		5. `-@year:[1955 1980]` - Not indluding 1955-1980

### Tag Queries ###
1. Tag queries:
	1. `@color{blue}` - Color equal to blue
	2. `-@color{blue}` - not equal to blue
	3. `@color{red | blue}` - or
	4. `@color{light\ blue}` - Escape spaces with `\`
2. Examples:

```
FT.SEARCH idx:cars '-@color:{blue}'
FT.SEARCH idx:cars '@color:{red | blue}'
```

3. All stop words are removed from tag and text queries
	1. `a`, `is`, `the`, `an`, `and`, ...
		1. They don't add much value in a query
	2. `@cities:{to | a | or}` is same as `@cities:{}`

### Text Queries ###
1. rbook

```
FT.SEARCH idx:cars '@name:(car)'
```

2. Query text + text in hash field go through pre-processing
	1. All stop words, spaces, and punctuation are removed
	2. Stemming is used to reduce words down to a base form
		1. fasting, fastly, fasts -> fast
			1. snowballstem.org/demo.html
			2. Even if suffix is added, it will match
3. Text Queries
	1. `@name:(fast car)` - Name contains 'fast' and 'car'
	2. `@name:(fast | car)` - Name contains 'fast' or 'car'
	3. `-@name:(fast)` - Name does not include 'fast'
	4. `fast` - Search all text fields for 'fast'
4. Example:

```
FT.SEARCH idx:cars 'fast'
FT.SEARCH idx:cars 'fastly'
FT.SEARCH idx:cars '@name:(fast | car)'
```

### Fuzzy Search ###
1. Typo

```
FT.SEARCH idx:cars '@name:(dar)'
```

	1. Wrap a term with '%' to include strings that have a slight difference in characters
		1. It is to account for how many characters of mismatch is allowed
		
		```
		FT.SEARCH idx:cars '@name:(%dar%)'
		```
		
			1. One character mismatch
		2. Two character mismatch
		
		```
		FT.SEARCH idx:cars '@name:(%%daar%%)'
		```
		
			1. Upto 3 chars mismatch allowed

### Prefix Search ###
1. Add `*` to a string to do a prefix search
	1. `fa*`
		1. `fast`, `far`, `fact`, `fawn`, `fantastic`, ...
	2. Min 2 chars
2. Examples:

```
FT.SEARCH idx:cars '@name:(fa*)'
FT.SEARCH idx:cars '@name:(ca*)'
```

### Pre-Processing Search Criteria ###
1. How to use the techniques?
	1. How to take plain text and convert them to query?
		1. Two steps:
			1. For autocomplete, we probably want to do prefix searches
				1. Do prefix search
			2. For the actual search implementation, we probably want to do a fuzzy search
				1. Use fuzzy search
					1. What if they enter multiple strings? What if they have typos
2. Prefix Search Pre-Processing
	1. user entered: `fast ca`
	2. Split on space: `['fast', 'ca']`
	3. Append a `*` to last term: `['fast', 'ca*']`
		1. We might want to append to all terms
	4. Maybe append a `*` to other terms? `['fast*', 'ca*']`
	5. Join with a space or a `|`: `fast* | ca*`
		1. Depends on what we are searching
3. Fuzzy Search Pre-Processing
	1. user entered: `fast dar`
	2. Split on space: `['fast', 'dar']`
	3. Wrap both terms with `%`? `['%fast%', '%dar%']`
		1. We can use more `%`
			1. Depends on our application
	4. Join with a space or a `|`: `%fast% | %dar%`

## Section 20: Search in Action ##
### Search Implementation ###
1. Example: `chair` - in name and description
	1. Full text search of item names + descriptions
2. Index Creation in Apps
	1. Figure out what prefix the index will use
		1. Example: `items#`
	2. Decide one the fields/types the index will look at
		1. Example: `name`, `description`
			1. Type: `TEXT`
	3. Make a function to construct the index
		1. Code: `src/services/redis/construct-indexes.ts`
		
		```typescript
		client.ft.create(
		  itemsIndexKey(), // Key to store this index at
		  {...} // Object describing the fields we want to index and their types
		  { ON: 'HASH', PREFIX: 'items#' } // Additional options
		)
		```
		
		2. Code: `src/services/keys.ts`
		
		```typescript
		export const itemsIndexKey = () => 'idx:items';
		```
		
	4. Decide when to construct the index
		1. Separate discussion

### The Constructing Index Function ###
1. `create-indexes.ts`

```typescript
import { SchemaFieldTypes } from 'redis'; // To designate the type of each field in the index
import { client } from '$services/redis';
import { itemsIndexKey, itemsKey } from '$services/keys';

export const createIndexes = async () => {
	return client.ft.create(
		itemsIndexKey(),
		{
			name: {
				type: SchemaFieldTypes.TEXT
			},
			description: {
				type: SchemaFieldTypes.TEXT
			}
		},
		{
			ON: 'HASH',
			PREFIX: itemsKey('') // This will match all keys that start with 'items#'
		}
	);
};
```

2. When do we make indexes?
	1. If we try re-creation of index, it throws error that the index is already created

### When to Construct the Index? ###
1. We need to check when the application starts up
	1. When the app first connects to redis
	2. Get a list of all the different indexes that exist
		1. How to get indexes?
		
		```
		FT._LIST
		```
		
	3. Does the index we're trying to construct already exist?
		1. Yes - Do nothing
		2. No - Construct the index
2. `create-indexes.ts`

```typescript
import { SchemaFieldTypes } from 'redis'; // To designate the type of each field in the index
import { client } from '$services/redis';
import { itemsIndexKey, itemsKey } from '$services/keys';

export const createIndexes = async () => {
	const indexes = await client.ft._list();

	const exists = indexes.find((index) => index === itemsIndexKey());

	if (exists) {
		return;
	}

	return client.ft.create(
		itemsIndexKey(),
		{
			name: {
				type: SchemaFieldTypes.TEXT
			},
			description: {
				type: SchemaFieldTypes.TEXT
			}
		},
		{
			ON: 'HASH',
			PREFIX: itemsKey('') // This will match all keys that start with 'items#'
		}
	);
};
```

3. `redis/client.ts`

```typescript
client.connect();

client.on('connect', async () => {
	try {
		await createIndexes();
	} catch (err) {
		console.error('Error creating indexes:', err);
	}
});

export { client };
```

### Parsing the Search Term ###
1. `services/items/search.ts`

```typescript
import { client } from '$services/redis';
import { deserialize } from './deserialize';
import { itemsIndexKey } from '$services/keys';

export const searchItems = async (term: string, size: number = 5) => {
	const cleaned = term
		.replaceAll(/[^a-zA-Z0-9\s]/g, '')
		.trim()
		.split(' ')
		.map((word) => (word ? `%${word}%` : ''))
		.join(' ');
};
```

### Executing the Search ###
1. `services/items/search.ts`

```typescript
import { client } from '$services/redis';
import { deserialize } from './deserialize';
import { itemsIndexKey } from '$services/keys';

export const searchItems = async (term: string, size: number = 5) => {
	const cleaned = term
		.replaceAll(/[^a-zA-Z0-9\s]/g, '')
		.trim()
		.split(' ')
		.map((word) => (word ? `%${word}%` : ''))
		.join(' ');

	// Look at cleaned and make sure it is valid
	if (cleaned === '') {
		return [];
	}

	// Use the client to do an actual search
	const results = await client.ft.search(itemsIndexKey(), cleaned, {
		LIMIT: {
			from: 0,
			size
		}
	});

	// console.log('Search results:', results);

	// Deserialize and return the search results
	return results.documents.map(({ id, value }) => deserialize(id, value as any));
};
```

### Seeding Some Fake Data ###
1. `seeds/seed.js` - generates fake data and puts in db
	1. `npm run seed`
2. Fix: Circular dependency:
3. `client.ts`

```typescript
client.on('connect', async () => {
	try {
		await createIndexes(client);
	} catch (err) {
		console.error('Error creating indexes:', err);
	}
});
```

4. `create-indexes.ts`

```typescript
import { RedisClientType, SchemaFieldTypes } from 'redis'; // To designate the type of each field in the index
import { itemsIndexKey, itemsKey } from '$services/keys';

export const createIndexes = async (client: RedisClientType) => {
  // ...
};
```

### RediSearch and TF-IDF ###
1. Search term in the name instead of just description
2. Example:
	1. "Excellent fruit, good, fantastic, tasty fruit"
		1. Term Frequency = 2 / 6
		2. Inverse Document Frequency = log(1 + 2 / 2)
		3. Score = 2 / 6 x log(1 + 2 / 2) = 0.1
	2. "Good fruit"
		1. How does RediSearch decide which one is more relevant?
			1. TF-IDF algorithm
				1. Term frequency x Inverse Document Frequency = Score for each string (document)
					1. Term Frequency = (# times search term appears in a string) / (# total words in string)
					2. IDF = log(1 + (# strings / # strings containing the term))
		2. Score = 1 / 2 x log(1 + 2 / 2) = 0.15
			1. Higher score - appears before the other
3. RediSearch - calculation is slightly different
	1. Extra parameters
		1. Example: How many words occur in-between the searched words
4. Multiple words:
	1. Score calculation of each word
	2. Add them
		1. 0.1 + 0.05 = 0.15
		2. 0.15 + 0.15 = 0.30
5. We can give more weight to certain words
	1. Term: `[fruit, good x 2 weight]`
		1. score of `good` x 2 = 0.05 x 2 = 0.1

### Applying Weights to Fields ###
1. Weight a field (not term)
	1. Example: Item#1 - name has `chair`
	2. Example: Item#2 - description has `chair chair chair`
		1. This is ranked higher by default
			1. We want name to be ranked higher
2. Query: `@name:(chair) => { $weight: 5.0 } @description:(chair)`
	1. `chair` in a name is 5x more important than in a description
		1. The above is an `AND` query (both should contain it)
			1. Solution: `(@name:(chair) => { $weight: 5.0 }) | (@description:(chair))`
				1. Find names including chair and/or descriptions including chair
3. `search.ts`

```typescript
import { client } from '$services/redis';
import { deserialize } from './deserialize';
import { itemsIndexKey } from '$services/keys';

export const searchItems = async (term: string, size: number = 5) => {
	const cleaned = term
		.replaceAll(/[^a-zA-Z0-9\s]/g, '')
		.trim()
		.split(' ')
		.map((word) => (word ? `%${word}%` : ''))
		.join(' ');

	// Look at cleaned and make sure it is valid
	if (cleaned === '') {
		return [];
	}

	const query = `(@name:(${cleaned}) => { $weight: 5.0 }) | (@description:(${cleaned}))`;

	// Use the client to do an actual search
	const results = await client.ft.search(itemsIndexKey(), query, {
		LIMIT: {
			from: 0,
			size
		}
	});

	// console.log('Search results:', results);

	// Deserialize and return the search results
	return results.documents.map(({ id, value }) => deserialize(id, value as any));
};
```

### Understanding Queries with EXPLAIN ###
1. `FT.EXPLAINCLI` - Give a summary of how RediSearch interprets your query
	1. `idx:items` - Key youre index is stored at
	2. `'chair'` - Give a plan on how this query will be executed (query)
		1. It tells how it thinks it has to be executed
2. `rbook`

```
FT.EXPLAINCLI idx:items 'chair'
```

	1. Expanded - Opposite of stemming
		1. Comes up with variations: `chairs`, `chairing`, ...
	2. UNION: Union of search results with `chair` and `+chair(expanded)`
	
```
FT.EXPLAINCLI idx:items 'chair -desk'
```

	1. INTERSECT(UNION(chair, +chair(expanded)), NOT(desk))
	
```
FT.EXPLAINCLI idx:items '@name:(chair) | @description:(chair)'
```

	1. `description` got converted to `@NULL`
		1. Solution:
		
		```
		FT.EXPLAINCLI idx:items '(@name:(chair)) | (@description:(chair))'
		```
		
		```
		[
		  "UNION {",
		  "  @name:UNION {",
		  "    @name:chair",
		  "    @name:+chair(expanded)",
		  "  }",
		  "  @description:UNION {",
		  "    @description:chair",
		  "    @description:+chair(expanded)",
		  "  }",
		  "}",
		  ""
		]
		```

### Query Performance with PROFILE ###
1. `FT.PROFILE` - Give a performance profile of a query
	1. `idx:items`
	2. `SEARCH` - We want to profile a `search' operation
	3. `QUERY 'chairs'` - The query to profile
	4. `LIMIT 0 0` - Don't return any results of the query
2. rbook

```
FT.PROFILE idx:items SEARCH QUERY 'chairs' LIMIT 0 0
```

```
[
  [
    206
  ],
  [
    "Shards",
    [
      [
        "Shard ID",
        "5419",
        "Total profile time",
        "0.151389",
        "Parsing time",
        "0.036525",
        "Workers queue time",
        "0",
        "Pipeline creation time",
        "0.0033",
        "Warning",
        [
          "None"
        ],
        "Iterators profile",
        [
          "Type",
          "UNION",
          "Query type",
          "UNION",
          "Time",
          "0.04991",
          "Number of reading operations",
          206,
          "Child iterators",
          [
            [
              "Type",
              "TEXT",
              "Term",
              "chairs",
              "Time",
              "0.006171",
              "Number of reading operations",
              101,
              "Estimated number of matches",
              101
            ],
            [
              "Type",
              "TEXT",
              "Term",
              "+chair",
              "Time",
              "0.004447",
              "Number of reading operations",
              101,
              "Estimated number of matches",
              101
            ],
            [
              "Type",
              "TEXT",
              "Term",
              "chair",
              "Time",
              "0.008347",
              "Number of reading operations",
              176,
              "Estimated number of matches",
              176
            ]
          ]
        ],
        "Result processors profile",
        [
          [
            "Type",
            "Index",
            "Time",
            "0.093694",
            "Results processed",
            206
          ],
          [
            "Type",
            "Counter",
            "Time",
            "0.009469000000000005",
            "Results processed",
            1
          ]
        ]
      ]
    ],
    "Coordinator",
    []
  ]
]
```

```
FT.PROFILE idx:items SEARCH QUERY '%%chairs%%' LIMIT 0 0
FT.PROFILE idx:items SEARCH QUERY '%chairs%' LIMIT 0 0
```

### Sorting and Searching ###
1. `queries/items/by-user.ts`

```typescript

```

	1. We need to search and sort
2. Searching + Sorting
	1. RediSearch can sort search results
	2. Fields that you plan to sort by need to be marked as 'SORTABLE' when index is created
	3. Sorting can only be done by one field at a time
		1. Multiple sort criteria is not allowed
3. `name` and `description` are marked `NonSortable` by default
4. Other fields to be marked sortable
	1. `ownerId` - must be in index. It is not sortable
	2. `imageUrl` - not required in index
	3. `createdAt` - not required
	4. `endingAt` - sortable
	5. `views` - yes
	6. `likes` - yes
	7. `price` - yes
	8. `bids` - yes

### Updating an Existing Index ###
1. `redis/create-indexes.ts`

```typescript
import { RedisClientType, SchemaFieldTypes } from 'redis'; // To designate the type of each field in the index
import { itemsIndexKey, itemsKey } from '$services/keys';

export const createIndexes = async (client: RedisClientType) => {
	const indexes = await client.ft._list();

	const exists = indexes.find((index) => index === itemsIndexKey());

	if (exists) {
		return;
	}

	return client.ft.create(
		itemsIndexKey(),
		{
			name: {
				type: SchemaFieldTypes.TEXT,
				sortable: true
			},
			description: {
				type: SchemaFieldTypes.TEXT,
				sortable: false
			},
			ownerId: {
				type: SchemaFieldTypes.TAG,
				sortable: false
			},
			endingAt: {
				type: SchemaFieldTypes.NUMERIC,
				sortable: true
			},
			price: {
				type: SchemaFieldTypes.NUMERIC,
				sortable: true
			},
			bids: {
				type: SchemaFieldTypes.NUMERIC,
				sortable: true
			},
			views: {
				type: SchemaFieldTypes.NUMERIC,
				sortable: true
			},
			likes: {
				type: SchemaFieldTypes.NUMERIC,
				sortable: true
			}
		},
		{
			ON: 'HASH',
			PREFIX: itemsKey('') // This will match all keys that start with 'items#'
		}
	);
};
```

2. To change an index, we can only add fields to it
	1. We cannot remove existing fields
	2. We cannot change existing fields
		1. Solution: Manually delete index: `FT.DROPINDEX idx:items`
			1. Restart the server

### Executing the Search ###
1. `by-user.ts`

```typescript
import { client } from '$services/redis';
import { itemsIndexKey } from '$services/keys';
import { deserialize } from './deserialize';

interface QueryOpts {
	page: number;
	perPage: number;
	sortBy: string;
	direction: string;
}

export const itemsByUser = async (userId: string, opts: QueryOpts) => {
	const query = `@ownerId:{${userId}}`;

	const sortCriteria = opts.sortBy &&
		opts.direction && {
			BY: opts.sortBy,
			DIRECTION: opts.direction
		}; // if sortBy and direction are provided, use them for sorting

	const { total, documents } = await client.ft.search(itemsIndexKey(), query, {
		ON: 'HASH',
		SORTBY: sortCriteria,
		LIMIT: {
			from: opts.page * opts.perPage,
			size: opts.perPage
		}
	} as any);

	console.log(total, documents);

	return {
		totalPages: 0,
		items: []
	};
};
```

### Deserializing Search Results ###
1. `by-user.ts`

```typescript
import { client } from '$services/redis';
import { itemsIndexKey } from '$services/keys';
import { deserialize } from './deserialize';

interface QueryOpts {
	page: number;
	perPage: number;
	sortBy: string;
	direction: string;
}

export const itemsByUser = async (userId: string, opts: QueryOpts) => {
	const query = `@ownerId:{${userId}}`;

	const sortCriteria = opts.sortBy &&
		opts.direction && {
			BY: opts.sortBy,
			DIRECTION: opts.direction
		}; // if sortBy and direction are provided, use them for sorting

	const { total, documents } = await client.ft.search(itemsIndexKey(), query, {
		ON: 'HASH',
		SORTBY: sortCriteria,
		LIMIT: {
			from: opts.page * opts.perPage,
			size: opts.perPage
		}
	} as any);

	console.log(total, documents);

	return {
		totalPages: Math.ceil(total / opts.perPage),
		items: documents.map(({ id, value }) => deserialize(id.replace('items#', ''), value as any))
	};
};
```

## Section 21: Service Communication with Streams ##
### Streams ###
1. Streams:
	1. Kind of like a cross between a list and a sorted set
		1. Collection of records
	2. Used for communication between different servers
	3. Most useful with 'consumer groups'
	4. TONS and TONS of tiny details
		1. Syntax

### Use Case of Streams ###
1. Use-case
	1. Stream - a data structure to store some information
	2. Message producer (separate servers, apis, ...)
		1. Message is created - hash (normal redis hash)
			1. It is added into the stream
			2. It is assigned an id
				1. It is time in unix timestamp format (ms)
					1. 34343-0
						1. It points to the message
	3. Message consumer (separate servers, ...)
		1. Asks all recent messages added to the stream
		2. The messages stay until we delete them
2. Primary use-case
	1. Example: API - receives request to send email to somewhere
		1. It needs to make request to third-party API to send email
			1. The request is hanging until email is sent (in a pending state)
			2. After maybe several seconds, we can send response
		2. Solution: Streams
			1. Server (message producer)
				1. When it receives a request, it puts a message 
				2. After putting the message, it sends a response to the requester
			2. Worker (message consumer)
				1. Wait for an element to be added to the stream
				2. It sees the message, processes it and sends request to third-party to send an email
	2. Almost every application has a setup like this

### Adding Messages to a Stream ###
1. `XADD` - Add a new message to a stream (<timestamp>-0 - if multiple messages are added at the same millisecond, they are given different suffixes (-0, -1, -2, ...))
	1. `fruits` - Where the stream is stored (automatically created)
	2. `*` - Have Redis generate an ID for us (a unix timestamp)
	3. `name` (key) - Key to add to the hash for this message
	4. `strawberry` (value) - Value to add to the hash for this message
	5. `color` - Key
	6. `red` - value
2. rbook

```
XADD fruits * color red name strawberry
```

```
"1787156639095-0"
```

### Consuming Streams with XREAD ###
1. `XREAD`
	1. `STREAMS fruits` - The key of the stream we want to read from
	2. `0-0` - Read all messages from the beginning of time
		1. `1787156639095-0` - After and not including the given timestamp
2. rbook

```
XREAD STREAM fruits 0-0
```

```
[
  [
    "fruits",
    [
      [
        "1787156639095-0",
        [
          "color",
          "red",
          "name",
          "strawberry"
        ]
      ]
    ]
  ]
]
```

```
XREAD STREAM fruits 1787156639095-0
XREAD STREAM fruits 1787156639094-0
```

	1. The original message is not deleted
3. Limiting

```
XREAD COUNT 2 STREAMS fruits 0-0
```

	1. Read up to 2 messages
	
```
XADD fruits * color yellow name banana
XREAD COUNT 2 STREAMS fruits 0-0
```

### Blocking Reads ###
1. Variation: `XREAD`
	1. `BLOCK 3000` - If no messages are available, wait for 3000ms before returning
		1. Avoids sending too many `XREAD`s to check for data
	2. `STREAMS fruits`
	3. `999499-0`
2. rbook

```
XREAD BLOCK 3000 STREAMS fruits 0-0
```

```
XREAD BLOCK 3000 STREAMS fruits 1787158310473-0
```

```
XADD fruits * color orange name orange
```

3. If we use `COUNT 5`, it still returns even if one element is added

### An XREAD Shorcut ###
1. We want to watch from now
	1. `XREAD BLOCK 3000 STREAMS fruits $`
		1. Watch from right now

### A Little Gotcha Around Streams ###
1. Time series:
	1. Stream: Gets 3 messages (ids: 10, 11, 12)
	2. Consumer: `XREAD BLOCK 3000 ... $`
		1. It takes time to process the message
		2. Once we get the first message, it will resolve
		3. If we start the next `XREAD` from then onwards, we will miss the messages between when the last `XREAD` resolved and now
			1. Fix: For each follow up `XREAD`, we must use the id of the previous message (10)
	3. `$` is used only the first time

### Reading Streams with XRANGE ###
1. `XRANGE`
	1. `fruits`
	2. `12345-0` - Look for messages starting at (AND INCLUDING) this time
	3. `55555-0` - Look for messages up to (AND INCLUDING) this time
	4. `COUNT 5`
2. rbook

```
XRANGE fruits 1787156639095-0 1787156639096-0
```

3. `(124234-0` - Look for messages starting at or ending at (NOT INCLUDING) this time
4. `-` - Get the minimum ID
5. `+` - Get the maximum ID

```
XRANGE fruits - +
XRANGE fruits 1787156639095-0 +
XRANGE fruits - (1787156639095-0
```

```
[
  [
    "1787156639095-0",
    [
      "color",
      "red",
      "name",
      "strawberry"
    ]
  ]
]
```

6. It does not have blocking variant

### Issues with Standard Streams ###
1. Issues
	1. Standard streams deliver all messages to all consumers (if we have multiple workers)
		1. Duplicate messages
	2. Tough to handle a consumer crashing (after receiving a message)

### Consumer Groups ###
1. Consumer group
	1. Example, we have multiple workers (consumers) (separate processes)
	2. Coordination is required
		1. All consumers in a group get a unique name
			1. `emailer-1`
			2. `emailer-2`
			3. `emailer-3`
		2. Redis sends a message only to one consumer in the consumer group (no duplication)
	3. Redis keeps track of where it sent each message (a log)
		1. Stream log
			1. Also stores acknowledgement receipt of each worker
				1. emailer-1 sends a message to third-party and sends an ack
			2. Solves problem 2:
				1. If a worker crashes, it cannot send an ack
			3. It will be resent
			4. Tracks last delivered ID
				1. Benefit: When a worker asks for an undelivered message, it will get the new message

### Constructing and Inspecting Consumer Groups ###
1. `XGROUP CREATE` - Construct a new consumer group
	1. `fruits` - Key of the stream
	2. `fruits-group` - Name of the group
	3. `$` - If the stream already exists, only handle messages added from this point on
		1. Ignore messages that came in the past
		2. `0-0` - All messages
		3. `<timestam>-0` - from the timestamp
	4. `MKSTREAM` - Make the stream, if it does not already exist
2. rbook

```
DEL fruits
```

```
XGROUP CREATE fruits fruits-group $ MKSTREAM
```

3. `XGROUP CREATECONSUMER` - Construct a new consumer
	1. `fruits` - Key of stream
	2. `fruits-group` - Name of the group
	3. `fruits-1` - Name of the new consumer
		1. Consumer group is a data structure in Redis
4. rbook

```
XGROUP CREATECONSUMER fruits fruits-group worker-1
XGROUP CREATECONSUMER fruits fruits-group worker-2
```

5. `XINFO GROUPS` - Lists info of all consumer groups tied to the given stream
	1. `fruits`
6. `XINFO CONSUMERS` - Lists info about consumers in a group
	1. `fruits`
	2. `fruits-group`
7. rbook:

```
XINFO GROUPS fruits
```

```
[
  [
    "name",
    "fruits-group",
    "consumers",
    2,
    "pending",
    0,
    "last-delivered-id",
    "0-0",
    "entries-read",
    null,
    "lag",
    0
  ]
]
```

```
XINFO CONSUMERS fruits fruits-group
```

```
[
  [
    "name",
    "worker-1",
    "pending",
    0,
    "idle",
    174961,
    "inactive",
    -1
  ],
  [
    "name",
    "worker-2",
    "pending",
    0,
    "idle",
    174719,
    "inactive",
    -1
  ]
]
```

### Consumer Groups in Action ###
1. rbook

```
XADD fruits 10-0 name banana color yellow
XADD fruits 20-0 name apple color red
XADD fruits 30-0 name orange color orange
```

2. `XREADGROUP`
	1. `GROUP fruits-group`
	2. `worker-1` - Name of the worker we are reading as (pretending to be that worker)
	3. `COUNT 1` - Optional, read at most 1 entry
	4. `BLOCK 2000` - Optional, block for 2000ms
	5. `STREAMS fruits >` - Only messages that were not delivered to any other consumer in this group
		1. `>` - Give us any undelivered messages
3. rbook

```
XREADGROUP GROUP fruits-group worker-1 COUNT 1 STREAMS fruits >
```

```
[
  [
    "fruits",
    [
      [
        "10-0",
        [
          "name",
          "banana",
          "color",
          "yellow"
        ]
      ]
    ]
  ]
]
```

4. How does it work?
	1. Get one message that is not delivered to anyone
		1. Once Redis sends a message, it makes an entry in Stream log
			1. I sent 10-0 to worker-1. They have not ACK'd the message yet
			2. Last delivered ID: 10-0
	2. If we send another `XREADGROUP` message as `worker-2`
		1. Update stream log
			1. I sent 20-0 to worker-2. They have not ACK'd
			2. Last delivered ID: 20-0
	3. ...
5. rbook

```
XINFO CONSUMERS fruits fruits-group
```

```
[
  [
    "name",
    "worker-1",
    "pending",
    1,
    "idle",
    251292,
    "inactive",
    251292
  ],
  [
    "name",
    "worker-2",
    "pending",
    0,
    "idle",
    684031,
    "inactive",
    -1
  ]
]
```

```
XREADGROUP GROUP fruits-group worker-2 COUNT 1 STREAMS fruits >
```

```
XINFO CONSUMERS fruits fruits-group
```

```
[
  [
    "name",
    "worker-1",
    "pending",
    1,
    "idle",
    298730,
    "inactive",
    298730
  ],
  [
    "name",
    "worker-2",
    "pending",
    1,
    "idle",
    6814,
    "inactive",
    6814
  ]
]
```

### Claiming Expired Messages ###
1. Worker acknowledges a message
2. rbook

```
XACK fruits fruits-group 10-0
```

	1. `10-0` - id of the message we acknowledge
3. rbook

```
XINFO CONSUMERS fruits fruits-group
```

4. What if a worker crashes?
	1. `XAUTOCLAIM` - Claim messages that have been pending with other workers for too long
		1. `fruits`
		2. `fruits-group`
		3. `worker-2` - Assign these pending messages to worker-2
		4. `10000` - Claim any messages that have been pending longer than 10 seconds (filter)
		5. `0-0` - Look for any pending messages after this ID
5. rbook

```
XREADGROUP GROUP fruits-group worker-1 COUNT 1 STREAMS fruits >
```

```
XAUTOCLAIM fruits fruits-group worker-2 10000 0-0
```

```
XINFO CONSUMERS fruits fruits-group
```

```
[
  [
    "name",
    "worker-1",
    "pending",
    0,
    "idle",
    38921,
    "inactive",
    38921
  ],
  [
    "name",
    "worker-2",
    "pending",
    2,
    "idle",
    2721,
    "inactive",
    2721
  ]
]
```

## Section 22: Bonus! ##
### Bonus! ###
1. [NestJS: The Complete Developer's Guide](https://www.udemy.com/course/nestjs-the-complete-developers-guide/?couponCode=3E3B5E71C411F773E9DB)