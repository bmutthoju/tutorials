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
		1. 