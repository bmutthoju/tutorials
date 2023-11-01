# How to Crack Any System Design Interview #
1. Purpose of system design interview: 
	1. **Assess the ability of the candidate to translate an ambiguous problem statement into concrete technical requirements**
		1. Features
		2. Non-functional requirements
		3. APIs
	2. Craft an architecture design that satisfies those requirements
	3. Articulate and **defend the design decisions** throughout the discussion
2. Example systems to design:
	1. Instagram feed
	2. Uber ride sharing
	3. Twitter timeline
	4. Google search infrastructure
3. Tips:
	1. Demonstrate technical expertise
	2. Demonstrate my approach to problem solving
	3. Demonstrate my skills to communicate effectively
	
## Preparation approach ##
### Practice, practice, and practice ###
1. Get hands on with designing apps and services we use regularly
	1. Instagram
	2. Uber
	3. Gmail
	4. ...
2. Take out a pen and paper and draw
	1. Push to sketch out the core components and how they interact with one another
3. Breakdown:
	1. Think through the key parts that front-end users may interact with
		1. Application servers that process millions of requests
		2. The caching mechanism to speed up response times
		3. The dedicated databases used to store posts, comments, and feeds
		4. The distributed object storage for hosting billions of photos and videos
	2. Sketch out how the main flows work
		1. How would an end-user's image gets uploaded and stored
		2. How would algorithms determine the order of posts in a user's feed
		3. How would system leverage cached data
		4. When would system make database calls

### Understand Common Design Patterns ###
1. Common patterns:
	1. Load Balancing
	2. Database Sharding
	3. CDN
	4. Cache
	5. ...
2. Know the pros and cons of different approaches so that we can intelligently weigh the trade-offs in the design
3. While studying the patterns, anticipate the types of questions the interviewer might ask and practice responding confidently
	1. redis vs memcached
		1. Be ready to dive into technical details and justify the choice
			1. Redis superior data structures
			2. Redis persistence options

### Tooling ###
1. Get comfortable using whiteboards, diagramming apps, and other visual tools
	1. Diagramming tools:
		1. draw.io
		2. OmniGraffle
		3. Whimsical
	2. Tools must become second nature to focus on communicating effectively and not struggling with the interface
		
### Mock Interviews ###
1. Do regular mock interviews to practice end-to-end
	1. Experience the settings and pressures of an actual interview beforehand
	2. Get feedback on the 
		1. Technical design
		2. Communication skills
		3. Ability to think on my feet
		4. How efficiently I manage the allotted time. (pace myself appropriately and keep moving forward)
			1. Introduction
			2. Clarifying questions
			3. Diagramming
			4. Minor interruptions
	3. Identify areas of strength and those needing improvement
	4. Ask targetted questions to deeply understand the following before starting the design: 
		1. Use-cases
		2. Scalability requirements
		3. Technical constraints
		4. Other key parameters
	5. Think out loud and verbally walk through the thought process
		1. Explain (don't make interviewer guess what is going on in my head)
			1. Rationale
			2. Trade-offs
			3. Decisions
			4. Take quick pauses for interviewers
			5. Vocalise assumptions
	6. Document key aspects on the whiteboard as we go through the design
		1. Helps interviewer follow my thought process
		2. Break the system down into logical components
		3. Highlight the main data flows and dependencies between them
		4. Focus on high-level design and broader trade-offs and avoid low-level details
	7. If I get stuck, take a breadth and don't panick
		1. Ask clarifying questions to resolve uncertainities
		2. Think through issues incrementally and systematically to get unblocked
			1. Overcoming obstacles and making progress with incomplete information is part of the challenge