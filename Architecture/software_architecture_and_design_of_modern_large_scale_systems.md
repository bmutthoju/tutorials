# Software Architecture & Design of Modern Large Scale Systems #
## Section 1: Introduction ##
### Introduction to Software Architecture ###
1. Topics:
	1. Software Architecture - Motivation
	2. Software Architecture Definition
	3. Software Architecture Definition - Explanation
	4. Software Development Cycle
2. Analogies from Outside of the Software World
	1. Everything we build has a structure
		1. Whether we consciously arrived at it or not
	2. The more we invest in building a product, the harder it is to change its structure (after the fact)
	3. The structure of our system describes: (What is the importance of a structure & why do we want to change it in the future?)
		1. The intent of our product
		2. The qualities of the product
3. Applications to Software
	1. Infinite ways to organize our code
	2. Different organizations will give us different properties
	3. The software architecture impacts:
		1. Performance and scale of the product
		2. Ease of adding new features
		3. Response to failure or security attack
	4. Cost of redesign will be significant in terms of **time and money** (especially for a large scale system)
4. Definition:
	1. Many ways to define software architecture
	2. The definition we're going to is:
		1. The software architecture of a system is a high-level description of the system's structure, its different components, and how those components communicate with each other to fulfill the systems' requirements and constraints.
4. Explanation:
	1. The software architecture of a system is a high-level description of the system's structure
		1. An abstraction that shows us the important components while hiding the implementation details (out of the view)
			1. Technologies or programming langauges are not a part of the software architecture but a part of the implementation
				1. Decisions about implementation should be delayed to the very end of the design
	2. its different components, and how those components communicate with each other
		1. The components here are "black box" elements defined by their behavior and APIs
		2. The components may themselves be complex systems with their own software architecture diagrams (the definition can be recursive when needed)
	3. to fulfill the systems' requirements and constraints
		1. Components come together to do what the system must do, which are our requirements
		2. The system does not do what it shouldn't do, which are the constraints
5. Levels of Abstraction
	1. Software architecture can have many different levels of abstraction:
		1. Classes/structs
			1. Organization and communication of objects inside a program
		2. Modules/packages/libraries
			1. And how they interact with each other
		3. Services (processes/groups of processes)
			1. Focus
			2. Each individual component is a separate service
			3. Advantages:
				1. This more distributed, multiple service approach allows us to architect systems that can:
					1. Handle large amounts of requests
					2. Process and store very large amounts of data
					3. Serve many users every day
	2. Examples:
		1. Ride-sharing
		2. Video-on-demand
		3. Social media
		4. Online video games
		5. Investment services
		6. Banks
		7. ...
	3. If we get the architecture right we can:
		1. Go from a small startup to a multi-billion dollar company
		2. Making a positive impact on millions of people
	4. Not doing a good job at the design phase can
		1. Waste months of engineering time
		2. Build a system that doesn't meet our requirements (no one wants to use)
	5. Restructuring a system that was not architected correctly is very hard and expensive
	6. So the stakes here are high
6. Software Development Cycle
	1. Phases:
		1. Design
		2. Implementation
		3. Testing
		4. Deployment (back to 1)
	2. The phases are repeated many times
	3. The first iteration is most critical
	4. Subsequent iterations make incremental changes to the existing system
	5. Software architecture:
		1. It is the output of the design phase and input of the implementation phase
		2. Design phase:
			1. A process of defining the software architecture of the system that an entire team or multiple teams of engineers later proceed to implement over a course of multiple weeks or months
7. Challenges of Software Architecture
	1. We cannot prove Software Architecture to be either:
		1. Correct
		2. Optimal
	2. What we can do to guarantee success is follow:
		1. Methodocial Design Process
		2. Arhictectural Patterns
		3. Best Practices
8. Summary:
	1. Got the intuition and motivation for Software Architecture
	2. Every software system has an architecture, which is critical for its success
	3. Definition: "A high-level description of the system's structure, its different components, and how those components communicate with each other to fulfill the systems' requirements and constraints"
	4. Software Architecture is the output of the design phase and the input to the implementation

### Download the Course Workbook ###
1. [https://www.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/34474542#content](https://www.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/34474542#content)
2. Workbook:
	1. Saves time
	2. Helps learn effectively

## Section 2: System Requirements & Architecture Drivers ##
### Introduction to System Design & Architecture Drivers ###
1. Topics:
	1. Requirements - Motivation
		1. Requirements - Formal description of what we need to build
		2. Large scale system requirements are different than the usual requirements we typically get for implementing
			1. Usual requirements are used to implement:
				1. A method
				2. An algorithm
				3. Class
		3. Big Scope and High Level of Abstraction
			1. Differences:
				1. Method/Function
					1. We know the inputs and outputs (precisely)
					2. We know the programming langauge
				2. As we go higher
					1. -> class -> module -> library -> application
						1. The range of ways to solve the problem becomes bigger and bigger (as we have more degrees of freedom)
						2. Scope of the problem becomes higher and hard to visualize
							1. We might get overhelmed and may not know where to begin
								1. Examples:
									1. File Storage System
									2. Video Streaming Solution
									3. Ride-Sharing Service
									4. ...
				3. High Level of Ambiguity
					1. System Design has high level of ambiguity
						1. Two reasons
							1. The person providing the requirements is often not an engineer and may even be not very technical
								1. A client or product manager might ask for something at a very high level and it is our responsibility to **transform those requests into precise technical requirements**
									1. The technical requirements will become our foundation for building the software architecture 
							2. Getting the requirements is part of the solution
								1. The client doesn't always know what they need
								2. The client generally knows only what probem they need solved
				4. Example: Hitchhiking Service
					1. High Level Requirement: "Allow people to join drivers on a route, who are willing to take passengers for a fee" (this may be the only requirement we might get from the client)
						1. We need to ask clarifying questions:
							1. Real time vs advance reservation
							2. User experience - Mobile? Desktop? Both?
							3. Payment through us or direct payment?
						2. Client may not know the answers right away until we ask those questions
						3. **Interviews test the ability to ask the clarifying questions ahead of time**
							1. The question narrow down what we need to build
		4. Importance of Gathering Requirements
			1. What happens if we don't get the requirements right?
				1. We can simply build something and then fix it (incrementally)
				2. Seemingly there's no cost of materials in software so changes should be cheap?
					1. Problem: Large scale systems are big projects that cannot be easily changed (cannot re-write code many times)
						1. Many engineers might be involved (cost of engineering time)
						2. Many months of engineering work (cost of engineering time)
						3. Hardware and Software costs (upfront)
						4. Contracts include financial obligations
						5. Reputation and brand (for not delivering projects on time)
	2. Requirements Classification
		1. Features of the System
			1. Functional requirements
		2. Quality Attributes
			1. Non-Functional requirements
		3. System Constraints
			1. Limitations and boundaries
2. Features/ Functional Requirements
	1. Describe the system behavior - what "the system must do"
	2. Easily tied to the objective of our system
	3. They describe the system as a black box function
		1. Inputs:
			1. User actions
			2. Events
		2. Outputs:
			1. Result/Outcome
	4. Functional requirements do not determine its architecture
	5. Generally, any architecture can achieve any feature
		1. It is hard for architects
	6. Example: "When a rider logs into the service mobile app, the system must display a map with nearby drivers within 5 miles radius"
		1. Input:
			1. User login action
		2. Output:
			1. View of map with nearby drivers
	7. Example: "When a ride is completed, the system will charge the rider's credit card and credit the driver, minus service fees"
		1. Input:
			1. Completion of ride (event)
		2. Output:
			1. Transfer of money
3. Quality Attributes/ Non-Functional Requirements
	1. System properties that "the system must have" (as opposed to what the system must do)
	2. Examples: (the list can change depending on the system)
		1. Scalability
		2. Availability
		3. Reliablility
		4. Security
		5. Performance
		6. ...
	3. **The quality attributes dictate the software architecture of our system**
		1. Software architecture defines the quality attributes
			1. Defferent architectures provide us with different quality attributes
4. System Constraints:
	1. Limitations and boundaries
		1. Time Constraints - Strict deadlines
		2. Financial Constraints - Limited budget
		3. Staffing Constraints - Small number of available engineers
	2. Constraints force us to make certain trade-offs and sacrifices
		1. Influence certain software architecture decisions
5. The above requirements are known as architectural drivers
	1. They drive our architectural decisions from an infinite set of possibilities towards one solution that satisfies our client's needs
6. Summary:
	1. Importance of system requirements in the design of large scale systems
	2. Challenges:
		1. High scope and abstraction
		2. Ambiguity
	3. Risks of not getting the requirements correctly up front
	4. Requirements classification/Architectural drivers:
		1. Features - Functional requirements
		2. Quality attributes - Non functional requirements
		3. Constraints - Limitations and boundaries

### Feature Requirements - Step by Step Process ###
1. Topics:
	1. Formal method of gathering functional requirements
	2. Example with a sequence diagram
2. User Journey - Motivation
	1. Gathering requirements
		1. Importance: Risks
		2. Challenges: Ambiguity & Scope
3. Requirements gathering - Native way
	1. Ask the client to describe everyting they need
		1. For complex systems - not a good approach
			1. Many features
			2. Multiple actors
	2. More powerful method of gathering requirements:
		1. Use Cases
			1. Situation/ Scenario in which our system is used
		2. User Flows
			1. A Step-by-step/ Graphical representation of each use case
	3. Requirements gathering steps:
		1. Identify all the **actors/users** in our system
		2. Capture and describe all the possible **use-cases/ scenarios**
		3. User Flow - Expand each use case through **flow of events**
			1. Each event contains
				1. Action
				2. Data (that flows with the action)
	4. Example:
		1. Hitchhiking Service - Actors
			1. "Allow people to join drivers on a route, who are willing to take passengers for a fee"
				1. Actors:
					1. Driver
					3. Rider
		2. Hitchhiking Service - Rider Use Cases
			1. Rider first time registration
			2. Driver registration
			3. Rider login
			4. Driver login
			5. **Successful match and ride**
			6. Unsuccessful ride
			7. ...
		3. Unified Modeling Language - Sequence Diagram
			1. Sequence Diagram - Diagram that represents interactions between actors and objects
			2. Part of the UML - Standard for visualizing system design
			3. In practice
				1. UML diagrams are used mostly for software design
				2. No real standard diagrams representing software architecture in the industry
				3. UML is not strictly followed in the industry
				4. Sequence diagrams are frequently used to represent interactions between entities
			4. Example:
				1. User flow for ride initialization:
					1. Driver: Read to Pick Up
					2. Rider: Look for Driver (+ origin, destination)
					3. System: Match Rider to a Driver
					4. System: Rider is Found (sent to Driver)
					5. System: Driver is Found (sent to Rider)
					6. Driver: Start Ride (sent to system)
					7. System: Ride started (sent to rider)
				2. User flow for ride completion
					1. Driver: Finish Ride (sent to system)
					2. System: Charge Rider
					3. System: Show Ride Receipt
					4. System: Take Service Fee
					5. System: Pay Driver
					6. System: Show Driver Earnings
		4. User flow can be used to identify the future API of the system (each interaction is an API call between our actor and the system)
			1. Data flowing between those actors are arguments in the API calls
4. Summary:
	1. Learned a formal way to capture the features and functional requirements
	2. The three steps in the process are:
		1. Identifying all the users and the actors
		2. Gathering all the use cases
		3. Expanding each use case with a flow of interactions between teh acto
	3. Sequence diagram - a visual way to document the interactions between actors and different components of our system

### System Quality Attributes Requirements ###
1. What we learn in this lecture
	1. Quality attributes motivation and definition
		1. These requirements have a direct effect on the software architecture
	2. Quality atttributes considerations
2. Quality Attributes - Motivation
	1. Systems are frequently redesigned NOT because of functional requirements
	2. But because the system as it stands:
		1. Isn't **fast** enough
		2. Doesn't **scale**
		3. Slow to **develop**
		4. Hard to **maintain**
		5. Not **secure** enough
3. System Quality Attributes - Definition
	1. Quality attributes are non functional requirements
	2. They describe
		1. The qualities of the functional requirements
		2. The overall properties of the system
			1. They do not say what the system does but:
				1. Provide a **quality measure** on how well our system performs on a **particular dimension**
					1. They have direct correlation with the architecture of our system
	3. Example: "When a user clicks on a search button after they typed in a particular search keywords, the user will be provided with a list of products that closely match the search keyword within at most a 100 milliseconds"
		1. Functional requirement: When a user clicks on a search button after they typed in a particular search keywords, the user will be provided with a list of products that closely match the search keyword
		2. Quality attribute: within at most a 100 milliseconds
			1. Performance
	4. Example: The online store must be available to the user at least 99.9% of the time
		1. Availability: 99.9%
	5. Example: Development team can deploy a new version of the online store at least twice a week
		1. **Quality attributes need to satisfy the requirements of all the stakeholders**
		2. Deployability: at least twice a week
4. Quality Attributes Considerations
	1. Important Considerations - Testability and Measurability
		1. Quality attributes need to be:
			1. Measurable
			2. Testable
		2. If we cannot prove that our system satisfied the required quality attribute we don't know if our system performs well or poorly
			1. Example: "When a user clicks on the buy button, the purchase confirmation must be displayed quickly to the user"
				1. Say within 200ms (does quickly requirement get satisfied?)
					1. We cannot measure quickly and we don't know if 200ms is good or bad
		3. No single software architecture can provide all the quality attributes
			1. If such an architecture existed, everyone would have used it for every system (Software architect is not required)
				1. Certain quality attributes conflict one another
				2. Some combinations of quality attributes are very hard/ impossible to achieve
			2. We (Software Architects) need to make the right tradeoff
				1. We need to prioritize some quality attributes over others in the design
					1. This gives the highest chance of success based on the requirements
			3. Examples:
				1. Login Page:
					1. Performance: Login Time < 1 second
					2. Security: Username, Password, SSL
						1. Typing & SSL makes login process slower
							1. Conflict with the first requirement
		4. Feasibility (of requirements)
			1. We need to make sure that the system is capable of delivering what the client is asking for
				1. System must be able to deliver what the client is asking for
			2. The client may ask for something that is either
				1. Technically impossible
				2. Prohibitively expensive to implement
			3. We need to call that out early on in the process
			4. Examples:
				1. Unrealistically low latency expecations
					1. If network latency between client in South America and Data Center in North East US is 100-150 ms => we cannot page loads to be < 100s
						1. HTTP also needs multiple roundtrips with multiple assets
				2. Our system can never fail
					1. We never have a chance to take our system down for
						1. Maintenance
						2. Upgrades
				3. Full protection against hackers
				4. High resolution video streaming in limited bandwidth areas
				5. Very high storage growth
				6. ...
			5. To overcome this, we might need to consult with people with domain expertise to make sure we can deliver what we promise
5. Summary:
	1. We got the motivation for quality attributes
	2. Quality attribute definition: "Quality measure on how well our system performs on a particular dimension"
	3. 3 important considerations:
		1. Testability and Measurability
		2. Trade offs (choose the right quality attributes over the others)
		3. Feasibility (ensure we can deliver what we promise)

### System Constraints in Software Architecture ###
1. Topics:
	1. System Constraints - Introduction
		1. Types of constraints
		2. Source of constraints
		3. Effects of the constraints on our software architecture
	2. System Constraints - Considerations
	3. Types of System Constraints
2. Introduction
	1. Once we define what our system must do (functional requirements), we have freedom on how to structure our system
	2. While defining the final architecture, we have to make a lot of decisions
		1. Since we have many ways to achieve the desired quality attributes with the desired functionality
	3. For quality attributes, we are expected to make trade-offs
3. System Constraints - Definition
	1. **A system constraint is essentially a decision that was already either fully or partially made for us, restricting our degrees of freedom**
		1. But this is not always a bad thing
4. System constraints
	1. Instead of looking at a constraint as a choice that was taken away, we look at it as **a decision that was already made** (makes our job easier)
	2. System Constraints are referred as pillars of software architecture because:
		1. They provide us with a solid starting point
		2. The rest of the system need to be designed around them
5. Types of System Constraints:
	1. There are three types of constraints
		1. Technical constraints
			1. We deal with everyday
			2. Examples:
				1. Being locked to a particular hardware/cloud vendor
					1. Due to existing contract or security reasons
				2. Having to use a particular programming langauge (because of existing frameworks we built in-house or may be due to difficulty in hiring engineers)
				3. Having to use a particular database or technology
				4. Having to support certain platforms, browsers, or OS
					1. Because of licenses, support costs or clients specifically asked for that
			3. Technical constraints may seem like they belong to implementation and not to software architecture
				1. In practice, they affect the decisions we make in the design phase and put restrictions on our architecture
				2. Example:
					1. If our company makes a decision to run on-premise data centers then (security or financial reasons):
						1. All the cloud architecture and paradigms will become unavailable to us (autoscaling, function as a service, ...)
							1. We would have to implement a lot of non-trivial infrastructure
				3. If we have to support some older browsers or low-end mobile devices (don't support certain communication protocols or do not handle much data) then:
					1. We have to adapt our architecture to support those platforms and their APIs
					2. While keep providing a different, more high-end experience for newer browsers or higher-end devices
		2. Business constraints
			1. As engineers, we make the right decisions and architectural choices from a technical perspective
				1. But we are unable to assess how the decisions align with the goals of the business
					1. This forces us to make sacrifices in:
						1. Architecture
						2. Implementation
			2. Example:
				1. Limited budget or a strict deadline will make us have very different choices than if we had an unlimited budget and unlimited time
			3. Different software architectural patterns are based on suitability between small startups or bigger organizations
				1. Small startups: Have to get to the market fast with a small team
				2. Biffer organizations: Many engineering teams with larger budget
			4. Usage of third-party services with their own APIs and architectural paradigms as part of our architecture
				1. Using third-party shipping/billing providers for an online store
				2. Integration of different banks/brokers/security/fraud detection services for an investing platform
					1. Focusing on a subset of vendors/partners
				3. Third-party providers have their own APIs and architectural paradigms that we have to work with to design our own system
		3. Regulatory/legal constraints
			1. Regulatory constraints may be:
				1. Global
				2. Specific to a region
					1. In the US, HIPAA (Health Insurance Portability and Accountability Act) places constraints on accessing patients' data
						1. Architecture and implementation needs to handle the constraints
							1. Security is required
					2. In the European Union, GDPR (General Data Protection Regulation) sets limitations on collecting, storing and sharing users' data
						1. On online services (about third parties)
							1. Also how long can the data be retained
					3. Depending on the region that we want to run our system, the regulations might affect the architecture
6. After identifying constraints, keep two considerations in mind:
	1. We shouldn't take any given constraint lightly
		1. There should be a distinction between
			1. Real constraints (we cannot do anything about it)
				1. External rules and regulations may not have room to negotiate
			2. Self-imposed constraints (can be negotiated and possibly removed)
				1. Internal constraints can be negotiated
					1. Examples: Budget constraint, time constraint
					2. Examples: If locked to using a particular
						1. Hardware
						2. Cloud vendor
						3. Technologies
					3. May be an opportunity to explore other options
						1. May benefit the business in the long-run
				2. Once we take on a set of constraints, it is very hard to back away
					1. Down the line if we find out that those constraints are not real constraints, our architecture may not make sense at the end
	2. Use loosely coupled architecture
		1. We need to leave enough room in our architecture to move away from those constraints in the future
			1. Example: If limited to a database/third-party service, we need to make sure our system **is not tightly coupled to that technology or APIs**
			2. Usage of different technology/service in the future should need minimal changes
		2. Different parts of the system can be decoupled to be easily replaced or updated independently
			1. Architectural building blocks (tools and techniques)
7. Summary:
	1. The 3rd type of architectural driver, the System Constraints
	2. "Decision that was already either fully or partially made for us, restricting our degrees of freedom"
	3. Three types:
		1. Technical constraints
		2. Business constraints
		3. Legal constraints
	4. Considerations
		1. Not taking constraints lightly
		2. Use loosely coupled architecture

## Section 3: Most Important Quality Attributes in Large Scale Systems ##
### Performance ###
1. List of Quality Attributes
	1. Performance
	2. Scalability
	3. Availability
	4. Testability
	5. Deployability
	6. Maintainability
	7. ...
	8. Portability
	9. Security
	10. Observability
	11. Consistency
	12. Efficiency
	13. Usability
	14. ...
2. Not all quality attributes are equally important for every system
3. Focus: (subset of QAs that are important in any large scale system regardless of the use-case)
	1. Performance
	2. Scalability
	3. Availability
4. Topics:
	1. Performance - Response Time
		1. We usually think about speed
		2. If a system responds fast to our actions, we associate the system with high performance
		3. Response time: Time between a client sending a request and receiving a response
			1. Response time = processing time + Waiting Time
				1. Processing time: Time spent in our system actively processing the request and building/sending the response
					1. Time spent in code, databases, and other parts of the system actively working on processing the request, applying business logic and building/sending a response
					2. End-to-end latency
				2. Waiting Time: Duration of time request/response spends inactively in our system
					1. Time spent in transit in network wires, switches and gateways
					2. Time spent in network / software queues waiting to be handled or sent to its destination
					3. Aka latency (means delay)
			2. Response time is an important metric when the request is in the critical path of a user interaction
				1. **Reason: Users have very little patience for long response times (they get frustrated)**
	2. Performance - Throughput
		1. Response time is not the only performance metric
		2. Throughput might be more important for some systems as compared to response time
			1. Example: Distributed logging system (aggregates and analyzes a constant stream of logs coming from hundreds or thousands of servers)
				1. **More data that we can injest per unit of time, the higher the performance of the system is**
		3. Throughput:
			1. Amount of work performed by our system per unit of time
				1. Measured in tasks/second
				2. Amount of data processed by our system per unit of time
					1. Measured in bits/second, bytes/second, megabytes/second
	3. Important Considerations
		1. Measuring Response Time Correctly
			1. Response Time = Processing Time + Waiting Time
				1. Not just Processing Time (consider waiting time as well)
		2. Response Time Distribution
			1. Consider 100s of servers running and we collect response times each minute
				1. We will get a distribution of response times
				2. What is the metric that we should:
					1. Set our goal around
					2. Measure
						1. Average?
						2. Median?
						3. Maximum?
				3. Solution: We need to organize and analyze the samples
					1. Sort the samples and bucket them into a histogram
						1. Frequencies of each response times
					2. Percentile - Definition:
						1. The "xth percentile" is the value below which x% of the values can be found
							1. Example: 20th percentile = 10 ms => 20% of response times are under 10 ms
							2. Exmaple: 50th percentile = median
					3. Tail latency: the x% of users that experiences the highest latency
						1. **The small percentage of response times from a system, that take the longest in comparison to the rest of the values**
							1. Shorter the tail => Better
						2. Response time consideration for tail latency
							1. **Define response time goals using percentiles**
							2. **Measure and compare to our goals using percentile distribution**
								1. Example: **30ms at 95th percentile of response time**
									1. We allow response times to exceed 30ms only for 5% of the requests
								2. Example: **30ms at 99th percentile of response time**
									1. More aggressive (some room for un-expected and transient gitter)
					4. Performance degradation
						1. **Identifying performance degradation point**
							1. A point when the performance of the application is getting significantly worse
							2. If the degradation is rapid, it implies that some of the resources are fully utilized
								1. High Resource Utilization:
									1. Potential overly-utilized resources:
										1. High CPU utilization
										2. High memory consumption (of one or more processes)
										3. Too many connections/ IO (in OS or Network)
										4. Message queue is at capacity (cannot keep up with the number of incoming messages)
						2. **Identifying how fast and how steep the degradation is**
5. Summary:
	1. Performance metrics:
		1. **Response Time** - Time between a client sending a request and receiving a response
		2. **Throughput** - Amount of work/data processed by our system per unit of time
	2. Important considerations:
		1. Proper measuring of response time
		2. Response time percentile distribution
		3. Performance degradation (in response to increasing load)

### Scalability ###
1. Topics:
	1. Scalability - Motivation & Definition
	2. Vertical Scalability
	3. Horizontal Scalability
	4. Team/Organization Scalability
2. Traffic Patterns
	1. The load/traffic on our system never stays the same
		1. It can follow different patterns
			1. Seasonal traffic pattern: (sine wave say)
				1. Example: Retail websites
				2. A lot of traffic during holidays or sales
			2. Spikes
				1. Example: Search engines
					1. A global event increases traffic (news say)
			3. Continuous spikes
				1. Example: News websites, tool at work
					1. Weekdays traffic is different from weekend traffic
		2. If the business is doing well, in general we must see more users using the system (a steady increase in traffic)
3. Response times:
	1. For the same budget and time, the degradation point must be to as much right as possible and the rate of degration must be as low as possible
4. Scalability Formal Definition:
	1. **The measure of a system's ability to handle a growing amount of work, in an easy and cost effective way, by adding resources to the system**
		1. Amount of Work vs Resources
			1. Ideal: Linear scalability
			2. Practically: It flattens as we increase the resources
				1. If performance degrades with increasing resources, it is undesirable
					1. It can happen due to the **overload in coordinating and managing the resources**
	2. We can scale our system in 3 orthogonal dimensions
		1. Scale Up/ Vertical Scalability:
		2. Scale Out/ Horizontal Scalability:
		3. Team/ Organization Scalability:
5. Vertical Scalability:
	1. Assume there is a server running on a single computer that is taking traffic from many users
		1. As the number of users grow, the system cannot take any more load and reaches the point of degradation
			1. Solution: Upgrade to a faster and newer machine (faster CPU, Memory, Network card (higher bandwidth))
				1. DB: Stronger hardware with more storage capacity
	2. It is called scaling up
	3. Vertical Scalability - Definition
		1. Adding resources or upgrading the existing resources on a single computer, to allow our system to handle higher traffic or load
6. Horizontal Scalability
	1. Add more units of the resources we already have
		1. Running service on multiple computers
			1. Advantages:
				1. We can spread the load keeping each machine far from it's degradation point
		2. DB: Run in multiple machines
			1. Advantages:
				1. Reduces performance pressure from any single computer
	2. Horizontal Scalability - Definition
		1. **Adding more resources in the form of new instances running on different machines, to allow our system to handle higher traffic or load**
7. Vertical Scalability - Pros & Cons
	1. Pros:
		1. Any application can benefit from it
			1. No code changes are required
				1. If CPU is high, increase the CPU (no code changes)
		2. The migration between different machines is very easy
			1. High traffic -> migrate to stronger machine
				1. Easy if we are renting hardware from cloud service provider
	2. Cons:
		1. The scope of upgrade is limited
			1. We can reach the limit very fast on internet scale
		2. We are locked to a centralized system which cannot provide
			1. High Availability
			2. Fault Tolerance
8. Horizontal Scalability - Pros & Cons
	1. Pros:
		1. No limit on scalability
		2. It's easy to add/remove machines
		3. If designed correctly we get (out of the box):
			1. High Availability
			2. Fault Tolerance
		4. **Smaller and cheaper hardware can be used for each instance**
	2. Cons:
		1. Initial code changes may be required
			1. If we make changes once, we can add or remove resources
		2. Increased complexity, coordination overhead
9. Team/Organization Scalability
	1. Scalability Definition - Developer's Perspective
		1. The measure of a systems ability to handle a growing amount of **work**, in an easy and cost effective way, by adding **resourcs** to the system
			1. Work (from developer's perspective)
				1. Adding features
				2. Testing
				3. Fixing bugs
				4. Do releases
			2. Resources (in this context)
				1. More engineers
	2. Assuming a single monolithic application: If we plot productivity as a function of engineers
		1. Upto certain point, the more engineers we add, the more work gets done (productivity increases)
		2. At some point, the more engineers we add, the less will the productivity be
		3. Reasons for poductivity degradation:
			1. Many crowded meetings - makes them less productive
			2. Code merge conflict - A lot of developers work on features simultaneously (overhead)
				1. Eventually, everyone might start stepping on each other's toes
			3. Business complexity - Longer ramp up time
				1. Each new developer has a lot more to learn before they become productive
			4. Testing is harder and slower
				1. No isolation
					1. Every minor change can potentially break something
						1. Any change to the code-base requires testing everything
			5. Releases become very risky
				1. Each release comes with lot of changes from many engineers
					1. Cause companies to make releases less frequently which makes it worse (each release has many changes)
	3. Team scalability:
		1. Software Architecture impacts engineering velocity (team productivity)
		2. Solution:
			1. Separate code into multiple modules/ abstract away into libraries
				1. Separate group of developers can work on each individual modules separately and not interfere with each other as-much
				2. The pieces are still part of the same service (still tightly coupled)
					1. Especially if we want to release new versions in production
			2. Separate code-base into separate services
				1. Each service has
					1. Own code-base
					2. Own stack
					3. Own release schedule
				2. Services communicate with each other through loosely coupled protocols over a network
				3. Advantages:
					1. Improves engineering productivity
					2. Helps scale organization
				4. Challenges:
					1. There are challenges and we need patterns
10. Scalability can be achieved in three orthogonal dimensions (we can scale in each direction independently)
	1. Scale Up/ Vertical Scalability
	2. Scale Out/ Horizontal Scalability
	3. Team/ Organization Scalability
11. Summary:
	1. We learned about a very important quality attribute - Scalability
	2. Motivation - traffic/load may increase:
		1. Over time
		2. On the seasonal pattern
		3. Sporadically
	3. Scalability definition: **Measure of a system's ability to handle a growing amount of work in an easy and cost effective way by adding resources to the system**
	4. We learned about three orthogonal ways to scale our system
		1. **Vertical Scalability** - Adding resources or upgrading the existing resources on a single computer
		2. **Horizontal Scalability** - Adding more resources in a form of new instances running on different machines
		3. **Team Scalability** - Increasing productivity while hiring more engineers into the team

### Availability - Introduction & Measurement ###
1. Topics:
	1. Importance and Risks
	2. What is high availability
	3. Availability definition and formulas
2. Introduction:
	1. Availability is an important attribute when designing a system
	2. It has the greatest impact on:
		1. Our users
		2. Our business
	3. Importance of Availability - Users
		1. Users try to purchase from online store but:
			1. The page doesn't load
			2. They get an error at checkout
		2. Users lose access to their email for considerable time
	4. Importance of Availability - Business (B2B)
		1. If we provide services to other companies, the impact of outage is compounded
			1. AWS simple storage service had an outage in February 2017
				1. Since many companies and websites used the service, it almost took down the entire internet
3. Importance of Availability - Mission Critical Services
	1. System downtime is not always just an inconvenience
	2. Our software can be used for mission-critical service like:
		1. Air trffic control in airports
		2. Healthcare in hospitals
	3. If it crashes/ becomes unavailable for prolonged periods, people's lives are on line
4. Impact of downtime on the business
	1. For a business, the consequences of our system going down are:
		1. If users cannot use our system, our profits become zero
		2. If users lose access constantly, they go to our competitors

### Fault Tolerance & High Availability ###
### SLA, SLO, SLI ###
### Real World SLA Examples from the Industry ###

## Section 4: API Design ##
### Introduction to API Design for Software Architects ###
### RPC ###
### Popular RPC Frameworks and Technologies ###
### REST API ###

## Section 5: Large Scale Systems Architectural Building Blocks ##
### DNS, Load Balancing & GSLB ###
### Load Balancing Solutions & Cloud Technologies ###
### Message Brokers ###
### Message Brokers Solutions & Cloud Technologies ###
### API Gateway ###
### API Gateway Solutions & Cloud Technologies ###
### Content Delivery Network - CDN ###
### CDN Solutions & Cloud Technologies ###

## Section 6: Data Storage at Global Scale ##
### Relational Database & ACID Transactions ###
### Non-Relational Databases ###
### Techniques to Improve Performance, Availability & Scalability of Databases ###
### Brewer's (CAP) Theorem ###
### Scalable Unstructured Data Storage ###
### Scalable Unstructured Data Storage - Cloud and Open Source Solutions ###

## Section 7: Software Architecture Patterns and Styles ##
### Introduction of Software Architecture Patterns & Styles ###
### Multi-Tier Architecture ###
### Microservices Architecture ###
### Event Driven Architecture ###

## Section 8: Big Data Architecture Patterns ##
### Introduction to Big Data ###
### Big Data Processing Strategies ###
### Lambda Architecture ###

## Section 9: Software Architecture & System Design Practice ##
### Design a Highly Scalable Discussion Forum 1 - Requirements & API ###
### Design a Highly Scalable Discussion Forum 2 - Functional Architecture Diagram ###
### Design a Hightly Scalable Discussion Forum 3 - Final Software Architecture ###
### Design an E-Commerce Marketplace Platform 1 - Requirements & Sequence Diagram ###
### Design an E-Commerce Merketplace Platform 2 - Functional Diagram ###
### Design an E-Commerce Merketplace Platform 3 - Final Software Architecture ###

## Bonus Section ##
### Bonus Lecture - Keep Learning ###