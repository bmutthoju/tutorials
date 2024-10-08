# How to Approach a System Design Interview Question #
1. System design interview is **open-ended conversation**
	1. **We are expected to lead it**
2. Work through the [System design interview questions with solutions](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#system-design-interview-questions-with-solutions) using the process

## Step 1: Outline Use Cases, Constraints, and Assumptions ##
1. Gather requirements and scope the problem
2. Ask questions to clarify use cases and constraints
3. Discuss assumptions
4. Questions:
	1. Who is going to use it?
	2. How are they going to use it?
	3. How many users are there?
	4. What does the system do?
	5. What are the inputs and outputs of the system?
	6. How much data do we expect to handle?
	7. How many requests per second do we expect?
	8. What is the expected read to write ratio?

## Step 2: Construct a High Level Design ##
1. Outline HLD with all important components
	1. Sketch the main components and connections
	2. Justify your ideas

## Step 3: Design Core Components ##
1. Dive into details of each core component
	1. Example: Design URL shortening service
		1. Generating and storing the hash of the full URL
			1. MD5 and Base62
			2. Hash collisions
			3. SQL or NoSQL
			4. Database schema
		2. Translating the hashed URL to the full url
			1. Database lookup
		3. API and object-oriented design

## Step 4: Scale the Design ##
1. Identify and address bottlenecks, given constraints
	1. Example: Do we need following to address scalability issues?
		1. Load balancer
		2. Horizontal scaling
		3. Caching
		4. Database sharding
2. Discuss potential solutions and trade-offs
	1. Everything is a trade-off
		1. Address bottlenecks using [principles of scalabile system design](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#index-of-system-design-topics)

## Back-of-the-envelope Calculations ##
1. [Use back of the envelope calculations](http://highscalability.com/blog/2011/1/26/google-pro-tip-use-back-of-the-envelope-calculations-to-choo.html)
2. Powers of two table
3. Latency numbers every programmer should know

## Source(s) and Further Reading ##
1. [How to ace a systems design interview](https://www.palantir.com/2011/10/how-to-rock-a-systems-design-interview/)
2. [The system design interview](http://www.hiredintech.com/system-design)
3. [Intro to Architecture and Systems Design Interview](https://www.youtube.com/watch?v=ZgdS0EUmn70)
4. [System design template](https://leetcode.com/discuss/career/229177/My-System-Design-Template)

## System Design Interview Questions with Solutions ##