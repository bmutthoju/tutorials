# System Design Interview: A Step-By-Step Guide #
## Framework ##
1. Step 1: Understand the problem and establish design scope (5 minutes)
	1. System design questions are vague
		1. Solution: Focus our thoughts on what is important
			1. Ask as many questions as possible to understand the problem fully
				1. Don't: Jumping to solution without understand what we are building
	2. Questions to ask:
		1. **Clarify the requirements**
			1. **Why are we building the system?**
			2. **Who are the users?**
			3. **What features do we need?**
		2. Example:
			1. Chat apps are of different types used for different purposes (**They have different design challenges and constraints**)
				1. One-on-one to group chat-app: WhatsApp
				2. Office chat app: Slack
				3. Group chat app: Discord
		3. Goal:
			1. Build features in priority order (top few features)
				1. Ensure that the interviewer agrees to the feature list
		4. **Clarify the non-functional requirements** (more important if we are more senior)
			1. Focus on **scale**
			2. Focus on **performance**
			3. Other non-functional requirements:
				1. Security
				2. Consistency
				3. Freshness
				4. Accuracy
	3. To help us get a sense of scale and potential challenges, we do some rough back of the envelope calculations
		1. Math is rough estimate (for order of magnitude)
	4. End product:
		1. List of a few features
		2. List of a few non-functional requirements to satisfy
2. Step 2: Propose high-level design and get buy-in (20 minutes)
	1. Goal: Come up with a high level design and reach an agreement with the interviewer
	2. Top down approach steps:
		1. Step 1: Come up with APIs
			1. APIs establish contract between end users and back-end system
			2. **Translate the functional requirements into APIs**
				1. RESTful - if not specified otherwise
				2. Define input parameters and output responses carefully
				3. Verify that the APIs satisfy the functional requirements
			3. Don'ts: Introducing APIs that do not satisfy the functional requirements
			4. Pitfalls:
				1. For two way communication, we might need to use websocket
					1. Websocket is **stateful**
						1. Challenge: **stateful servers are challenging to operate at scale**
							1. **Be prepared to discuss websocket deployment in deep dive section**
		2. Step 2: Come up with high level design diagram
			1. It is blueprint that we can refer back to
			2. **Ensure that the design satisfies all the features identified end to end**
			3. Typical design:
				1. Load Balancer (API gateway say)
				2. Services to satisfy feature requirements
				3. Persistence
					1. Data storage layer (don't have to specify specific database technology at this stage)
						1. Reserve the discussion of specific database technologies to the deep dive section if necessary (**only after we have designed the schema**)
			4. Repeat step 3 for all features identified
			5. Pro tip:
				1. While developing the high level design, maintain a list of discussion points for later
					1. Don't dig into details too early before we have the full picture of the design
		3. Step 3: Come up with data model and schema
			1. Discuss data access patterns
				1. Consider how do users scale
				2. We can discuss databases to choose and indexing options
				3. Tip:
					1. If database is the key part of the modeling to satisfy the non-functional requirements, we can defer the discussion to deep-dive section
			2. Discuss read/write ratio
		4. Step 4: Review the design
			1. Ensure that each feature is complete end-to-end
3. Step 3: Design deep dive (15 minutes)
	1. Goal: Identify areas that could potentially be problematic and come up with solutions and discuss trade-offs
		1. **Work with interviewer closely to decide on what to discuss in depth**
		2. Stress on non-functional requirements
			1. Higher the level, the more important the section
	2. Tips: Watch for interviewer's body language
		1. Gives clues that they might be dissatisfied with certain aspects of design
			1. Pick up the clues and ensure that the issues are addressed
		2. Solution:
			1. As questions:
				1. Give reasons for choosing a particular solution and ask if they have any questions or concerns
	3. **Come up with multiple solutions and discuss trade-offs**
		1. Guidelines for discussions:
			1. Articulate the problem
				1. Example: 1M QPS is too high for a single database to handle
			2. Come up with at least two solutions
				1. Example: Reducing location update frequency per user or choose a nosql db that could handle the right rate
			3. Discuss the trade-offs of the solutions
				1. Use numbers to back-up our design
			4. Pick a solution and discuss it with the interviewer
			5. Repeat steps 1 to 4 for other problems
				1. Top 2 or 3 issues in the time given
4. Step 4: Wrap up (5 minutes)
	1. Summarise the design
		1. Focus on parts unique to the particular situation
		2. Keep it short and sweet
	2. Leave enough room to the interviewer to ask questions about the company

## Timeline ##
1. First 5 minutes: Introduction
2. Last 5 minutes: Q&A
3. 35 - 45 minutes: System design