# Redis University #
## Overview ##
1. Topics:
	1. Overview
	2. Roadmap
	3. Tips
2. For Java programmers
	1. Basic Java
		1. Data structures
		2. Collections
		3. Maven
		4. JUnit
		5. REST APIs
		6. HTTP
	2. Redis:
		1. Basic data structures (RU101 - Introduction to Redis Data Structures)
			1. Strings
			2. Sets
			3. Sorted sets
			4. Hashes
3. Best way to learn: Write code
	1. Application: Solar power data ingestion and monitoring dashboard
		1. Rooftop solar utility
		2. Application to ingest and use the data
4. Complete the programming challenges

## About Redis, Inc ##
1. [Redis Enterprise](https://redis.com/redis-enterprise?utm_medium=referral&utm_source=redisUniversity&utm_campaign=ru102j)
2. [Redis Cloud](https://redis.com/redis-enterprise-cloud?utm_medium=referral&utm_source=redisUniversity&utm_campaign=ru102j)
3. [Redis Cloud Essentials](https://redis.com/redis-enterprise-cloud?utm_medium=referral&utm_source=redisUniversity&utm_campaign=ru102j)

## Course Outline ##
### Week 1 ###
1. Hello Redis
2. Redis Clients
3. Introducing the Jedis Library
4. Basic Operations with Jedis
5. Introducing Redis DAOs and Domain Objects
6. Implementing a DAO
7. Solving a Sample Challenge
8. Challenge #1
9. Homework
10. Chapter 1 Recap

### Week 2 ###
1. Data Model Overview: Meter Reading Ingestion
2. Metrics with Sorted Sets: Overview
3. Metrics with Sorted Sets: Implementation
4. Challenge #2
5. Site Stats
6. Pipelining with Jedis
7. Transactions with Jedis
8. Notes on Transactions with Redis
9. Lua with Jedis
10. Challenge #3
11. Homework
12. Chapter 2 Recap

### Week 3 ###
1. Site Capacity Leaderboards
2. Site Geo Queries
3. Challenge #4
4. Geo Queries with Criteria
5. Challenge #5
6. Streams for Feeds: Overview
7. Streams for Feeds: Implementation
8. Challenge #6
9. Notes on Streams with Redis
10. Homework
11. Chapter 3 Recap

### Week 4 ###
1. Building a Rate Limiter
2. Challenge #7
3. Implementing Metrics with RedisTimeSeries
4. Error Handling
5. Connection Management
6. Performance and Scaling
7. Debugging
8. Client Protocols
9. Homework
10. Chapter 4 Recap

### Week 5 ###
1. Final Exam
2. Course Recap

## Sample Applcation Overview ##
1. Project Overview
	1. Rooftop solar utility
	2. Solar panel installed on rooftops
	3. Each solar installation is called a site
	4. Each site has a power Meter
		1. Meter reports how much energy each solar installation is using and generating, minute by minute basis
		2. We are building an app that injests and displays the data
			1. map of solar installations
			2. Search bar to find installations closest to particular address
			3. For each site, we can view recent energy data
				1. Watt hours generated and used per minute
			4. We can see which sites have greatest and least capacity
	5. Frontend: Vue.js
	6. Backend: Java
		1. com.redislabs.university.ru102j
			1. api
			2. dao
			3. resources
		2. Dropwizard - REST framework
	7. Config and install:
		1. conf.yaml - points to local Redis instance
		2. `mvn package`
			1. Builds a fat jar `redisolar-1.0.jar`
		3. Running: `java -jar target/redisolar-1.0.jar load --flush true`
		4. Start server: `java -jar target/redisolar-1.0.jar server config.yml`
		5. Open: http://localhost:8081

## Application Setup Instructions ##
### Getting Started ###
1. Attempt programming challenges
2. Run example application
3. Examine source code
4. Pre-requisites:
	1. Redis stack instance
	2. Access to Github
	3. Choice of IDE
	4. JDK
5. [Discord](https://discord.gg/jucCB8h)
6. [Start](https://github.com/redislabs-training/ru102j)

## Running the Sample Application ##
### Important! ###
1. The below steps allows us to participate in the programming challenges that appear in the course

### Building the Project ###
1. Docker container:

		cd project
		mvn package
		
2. Local machine:

		cd ru102j
		mvn package
		
	1. Pre-configured to assume Redis is at port 6379 on localhost with no password
		1. To change host, port, or password, set values in:
			1. `config.yml` (for application)
			2. `src/test/java/com/redislabs/university/RU102J/HostPort.java` (for tests)
		2. Re-package the application:
		
				mvn package

### Running the Test Suite ###
1. Running tests:

		mvn test
		
2. Running individual test:

		mvn test -Dtest=HelloTest

### Loading the Sample Data ###
1. Application includes data loader
	1. Run it after completing each programming challenge
		1. It ensures that the data is up to date
2. Command:

		java -jar target/redisolar-1.0.jar load
		
	1. The data loader can flush Redis database before loading data (this will delete everything from Redis before loading)
	
			java -jar target/redisolar-1.0.jar load --flush true
			
	2. If using a different host, port, or password:
	
			java -jar target/redisolar-1.0.jar load --host myhost --port 6380 --password secret
			
		1. Use `--flush true` if we want to delete all data from Redis before loading the course data

### Running the Sample Application ###
1. Run the following to run the sample application:

		java -jar target/redisolar-1.0.jar server config.yml
		
2. Navigate to: `http://localhost:8001` to see the app

### Viewing the Programming Challenge Solutions ###
1. Docker container:
	1. `solutions` folder has source code
2. Local machine/ GitHub:
	1. `solutions` branch in GitHub repo contains a copy of source code with each programming challenge completed