# System Design Interview: A Step-By-Step Guide #
## Framework ##
### Steps ###
1. Steps:
	1. Step 1: Understand the Problem and Establish Design Scope
	2. Step 2: Propose High-Level Design and Get Buy-In
	3. Step 3: Design Deep Dive
	4. Step 4: Wrap Up
2. Time allocation: 45 minutes to 1 hour
	1. Introduction: 5 minutes
	2. System Design Interview: 35 minutes to 50 minutes
		1. Step 1: 5 minutes
		2. Step 2: 20 minutes
		3. Step 3: 15 minutes
		4. Step 4: 5 minutes
	3. Q & A: 5 minutes
3. System design questions are open-ended. There are deliberately vague
	1. **Tests our ability to focus on our thoughts and focus on what is important**

#### Step 1: Understand the Problem and Establish Design Scope ####
1. Ask as many questions as necessary to understand the problem fully
	1. Don't jump into a solution without any clarity on specifics
	2. Questions to ask: Goal - clarify requirements
		1. Why are we building the system?
		2. Who are the users?
		3. What features do we need to build?
			1. The apps have different **design challenges** and **constraints**
			2. Examples:
				1. Chat app types:
					1. One-on-one chat apps (WhatsApp)
					2. Small group chat apps (WhatsApp)
					3. Office chat apps (slack)
					4. Group chat apps (Discord)
			3. Focus on the top few features to build:
				1. Goal: Understand the features we are building in priority order
				2. Ensure that the interviewer agrees to the feature list
		4. What non-functional requirements are important?
			1. List of non-functional requirements in order of importance:
				1. Performance (focus on this)
					1. Latency
					2. Throughput
				2. Scale (focus on this)
				3. Consistency
				4. Accuracy
				5. Freshness
				6. Security
			2. The non-functional requirements make the design challenging:
				1. Designing Twitter for a few 100 users is easy
				2. Designing Twitter for 100s of millions of users with some popular accounts having millions of followers is interesting and challenging
			3. The more senior we are, the more important this sub-section is
		5. What is the scale of the system and what are the potential challenges and bottlenecks?
			1. Do rough back-of-the-envelope calculations
				1. Keep in mind that **we have yet to design anything**
					1. The math we do here is a rough estimate
					2. The goal is to get a general sense of the scale
						1. Get the order of magnitude right
							1. 10 QPS?
							2. 100 QPS?
							3. 1000 QPS?
							4. 10000 QPS?
							5. 100000 QPS?
							6. 1 million QPS?
		6. End-result:
			1. Feature list (small number)
			2. Non-functional requirements (scalability, capacity, availability, ...)

#### Step 2: Propose High-Level Design and Get Buy-In ####
1. Top-down-approach:
	1. Design APIs
		1. Establish a connection between end-users and the backend system
		2. Map requirements to APIs
			1. REST APIs (default)
			2. Exceptions:
				1. Two-way communication: Web-sockets
					1. It is stateful
					2. Challenging to operate at scale
						1. Prepare for how to manage web-socket deployment in the deep-dive section
		3. Define input parameters carefully
		4. Define output responses carefully
		5. Review APIs to ensure they satisfy the functional requirements
		6. Don't introduce APIs that do not match the functional requirements
	2. Lay out a high-level design diagram (blue-print of overall design we can refer back to)
		1. Ensure that the design satisfies all features end-to-end
			1. Steps (example):
				1. Start with a load balancer / API gateway
				2. Behind that are services that will satisfy the feature requirements
				3. Introduce a data-storage layer (if there is persistence)
		2. Do not specify database technology her
			1. Defer it to deep-dive-section if necessary
				1. Only after we have designed the data schema
					1. Example: Client sends frequent gps updates to the server
						1. We might need a location data store to write location data
		3. Repeat the steps above until the high-level design diagram is completed with all the major features
		4. While developing high-level design, maintain a list of discussion points for later
			1. Example:
				1. Database scaling
				2. High concurrency
				3. Failure scenarios
		5. Do not dig into details too early before we have the full picture of the design
	3. Hash out the data model and schema:
		1. Discuss data access patterns
		2. Discuss the read/write ratio
		3. If simple, discuss the databases to choose
		4. Discuss the indexing options
		5. If data modeling is the key part of the design to satisfy the non-functional requirements, defer the discussion to the deep-dive section
	4. Review the design and ensure that each feature is complete and end-to-end

#### Step 3: Design Deep Dive ####
1. We need to identify the areas that could potentially be problematic, come up with solutions, and discuss trade-offs
	1. Work with the interviewer closely to decide what to discuss in depth
	2. Look for the interviewer's body language to understand what aspects of the design they are dissatisfied with
	3. Pick up the clues, ask questions, address the issues
	4. List out reasons for choosing a particular solution
		1. Example:
			1. Cassandra:
				1. Open source
				2. Handles a high volume of writes
				3. Highly scalable
	5. Ask if the interviewer has any questions or concerns
	6. Once we decide on one or two important problems, come up with multiple solutions and discuss trade-offs for each option
		1. Guideline:
			1. Articulate the problem
				1. Example: 1 million QPS for a location database is too high for a single database to handle
			2. Come up with at least two solutions
				1. Example:
					1. Reduce the frequency of updates per user (dispatch in batch)
					2. Choose a NoSQL database that could handle the rate:
						1. Cassandra
						2. DynamoDB
			3. Discuss trade-offs of the solutions
				1. Use numbers to back the design
			4. Pick a solution and discuss it with the interviewer
			5. Repeat steps 1 to 4 for each of the next 1 or 2 problems

#### Step 4: Wrap Up ####
1. Spend a few minutes to summarize the design
	1. Focus on parts that are unique to the particular situation
	2. Keep it short and sweet
2. Leave enough room to ask interviewer questions about the company