# The Complete Microservices & Event-Driven Architecture #
## Introduction ##
### Introduction to Microservices and Event-Driven Architecture ###
1. What we will learn in the lecture?
	1. Motivation for Microservices Architecture
	2. Motivation for Event-Driven Architecture
	3. Problems with Monolithic Architecture
		1. Problems solved by the modern architecture styles
2. Motifivation for Microservices
	1. Microservices Architecture is the most:
		1. Modern
		2. Popular
	2. Architectural style in the industry
	3. Entire system is organized as a collection of independent services
		1. Each has its narrow scope of responsibility
		2. Each one is owned by a team of developers
	4. Microservices are the main topic in tech conferences
		1. Most of the successful tech companies
			1. Examples: Amazon, Google, Netflix, Meta, Etsy, Uber, AirBnb, Spotify, eBay, BBC
	5. When done correctly:
		1. Microservices architecture allows organizations to scale to thousands or 10s of thousands of Engineers
			1. Divided into small teams that operate independently
		2. It enables organizations to build systems that are highly scalable that reach billions of users
		3. All of it is done keeping the operational costs low
		4. Staying efficient and innovative
3. Challenges of Microservices
	1. Microservices are exciting
		1. But:
			1. Many organizations struggle / go back from their decision
	2. Microservices is NOT a silver bullet that solves all of our problems
	3. When applied correctly:
		1. It can be very beneficial
	4. When applied incorrectly (or if the company is not ready for the change):
		1. It can introduce unnecessary overhead (without bringing any benefits)
4. No worries:
	1. We will cover everything we need to know about Microservices architecture:
		1. Prerequisites for success
		2. Steps to migration
		3. Best practices
		4. Industry-proven patterns (for using Microservices correctly)
		5. Testing Microservices
		6. Deploying Microservices to production
		7. Troubleshooting (Observability)
5. By the end of the course:
	1. Intuition and skills to get the most benefit from Microservices
	2. Knowledge on how to avoid costly:
		1. Mistakes
		2. Pitfalls
		3. Anti-patterns
			1. Saves valueable time, money, and frustration
	3. Side Benefit:
		1. Helps is preparing for system design interviews
			1. Microservices concepts comes a lot especially when interviewing for a senior role
6. Motivation for Event-Driven Architecture:
	1. It is commonly used with Microservices Architecture
		1. Used to establish asynchronous, event-based communication between microservices, we can achieve greater decoupling and higher scalability for the company
	2. It allows us to implement very powerful design patterns for microservices architecture
7. Problems with Monolithic Architecture
	1. Typical Web-Based Application Architecture
	
			Front End <-> Web Application <-> Data
			
		1. Three logical and physical tiers
			1. Presentation Tier - Contains client-side, front-end code that runs on user's
				1. Mobile devices
				2. Tablets
				3. Web browsers
			2. Logic/Business/Application Tier - It runs business logic
				1. It handles all the interactions between the users and the system
			3. Data Tier - Stores all necessary info about our customers or business in persistence storage
				1. Database
				2. File System
		2. The architecture is called a monolithic architecture
			1. Because the business logic and backend development are concentrated inside a single code-base
			2. Because it is deployed at runtime as a single monolithic process
		3. The three tier architecture is the most commonly used architecture style
			1. Because it provides many great benefits out of the box
			2. Benefits:
				1. Easy to design
					1. The monolithic architecture fits any web-based system
						1. Regardless of the industry or the service it is providing
							1. Online News Magazine
							2. Stock Trading System
							3. Online Dating Service
							4. Online Bank
				2. Easy to implement
					1. A small team of full-stack developers and a few of-the-shelf web-frameworks and standard database technologies, we can easily have a fully functional system following the architecture
						1. The architecture is the best choice:
							1. If we have a small startup company and we to get our idea to the users quickly OR
							2. If we have a small development team
								1. The perfect size of a team should be small enough, that it can be fed with two Pizzas (key to efficiency and scalability)
									1. If the company fits this model, there is no reason to use anything else
							3. As the company becomes successful and the development team keeps growing, we start running into more and more issues (not satisfied with two pizzas)
								1. Issues:
									1. Low organizational scalability
										1. With too many engineers working on the same code-base, code merge conflicts become a serious problem
											1. Everyone stepping on every others' toes
												1. This makes completing even a trivial feature slower and harder
											2. To deal with these issues, we need a lot of coordination and planning
												1. So more meetings
													1. The more people we have in the meetings, the longer it takes and the less productive we become
									2. Complex Codebase
										1. As we add more features to our codebase becomes larger and more complex
											1. It makes it:
												1. Harder to reason about
												2. Takes longer to load in the IDE
												3. Slower to build / test
												4. Riskier to deploy
												5. Therefore, the release schedule becomes less frequent
													1. It makes things even worse
														1. Every release contains more features increasing the chances for bugs and outages
												6. Onboarding new developers takes longer
													1. It is much harder for them to get familiar with the large code-base
													2. With every addition of an engineer in the team, we see diminishing returns until we reach a point where adding more engineers to the team reduces everyone's productivity
									3. Low system scalability
										1. Technical problems
											1. Each application instance (which contains our entire business logic) requires a lot of CPU and memory
												1. Instead of using a commodity hardware, we need to run each instance on a high end expensive computer
											2. Legacy Application
												1. We are constrained by the technology choices we made many years ago
													1. We cannot take advantage of new and better technologies
													2. Refactoring the code-base from one library to another can be a huge effort
													3. It is challenging to consider new programming languages or frameworks
												2. Application becomes less stable
													1. A small memory leak, performance issue or bug can affect the entire system
														1. It may require a rollback
												3. Potential solution: Logically seperating the monolithic application into layers, modules, and libraries can help only so much
													1. The different modules are:
														1. Still tightly coupled together
														2. Still use the same technology and programming language
														3. are still deployed as a single deployment unit
														
8. Summary:
	1. Motivation for:
		1. Microservices Architecture
		2. Event-Driven Architecture
	2. Microservices:
		1. It is one of the biggest contributors to many companies' success (biggest and most successful companies)
		2. It is not a silver bullet
			1. We need to understand when to use it and how to use it correctly
	3. 3-Tier/Monolithic Architecture
		1. Perfect for:
			1. Startup companies 
			2. Companies with a small dev team (2 Pizza rule)
				1. With relatively small code-base
		2. Monolithic Architecture has issues with:
			1. Organizational scalability
			2. System scalability
		3. Solution:
			1. Microservices Architecture with Event-Driven Architecture
										
### Microservices Architecture-Benefits and Challenges ###
1. What we will learn in this lecture:
	1. Introduction to Microservices Architecture
	2. Benefits of Microservices Architecture
		1. How they solve the scalability issues of the monolithic architecture
	3. Challenges of Microservices Architecture
2. Introduction to Microservices Architecture:
	1. It organizes the business logic as a collection of **losely coupled** and **independently deployable** services
	2. Each service is **owned by a small team** and has a **narrow scope of responsibility**
3. Benefits of Microservices Architecture
	1. High Organizational Scalability
		1. Smaller Codebase
			1. Since each service contains a subset of overall functionality, each service's codebase is much smaller
				1. Allows each developer to load the codebase into an IDE much faster
				2. Building each microservice becomes much quicker
					1. Since the size of each binary is greatly reduced
				3. Testing & reasoning about each service in isolation becomes much easier
					1. Because, there is much less code and logic to understand and run and test
						1. The simplicity of code-base of each microservice also speeds up the onboarding process of new team members
							1. Company can grow quickly and stay efficient
			2. The advantages will increases the development velocity of each team
				1. Quicker and easier to:
					1. Design
					2. Develop
					3. Build
					4. Test
					5. Release
				2. So, we can deliver more features and gain an advantage over competitors
	2. High System Scalability
		1. Monolithic Application Instances
			1. Each instance had to run the entire code-base
				1. Requires very powerful and expensive hardware to run each instance
		2. Microservices
			1. We break the code-base into microservices so that each service is much smaller
				1. Each instance of a microservice consumes less memory and CPU
					1. Each instance can run on cheap and widely available commodity hardware
				2. Different Technologies for each Microservice
					1. Each team can make the best judgement as to what technologies would benefit their service
						1. They can also respond to technology changes much faster
							1. By refactoring the small codebase
							2. By re-writing the entire service if necessary
				3. Higher Stability
					1. Each microservice is deployed as a separate runtime unit
						1. Blast radius of a bug, performance leak, or memory issue is much smaller
							1. In most cases, a bug in the microservice will only impact that microservice
								1. Or just the ones that depend on it at some level
							2. The rest of the system can continue operating just fine
			2. Microservices break the scalability barrier we hit with the monolithic architecture
	3. Monolithic to Microservices
		1. Lower gier in a car is like the monolithic architecture
			1. It allows the company to quickly start moving from 0 and grow to a certain threshold
		2. To continue growing, we need to switch gears.
			1. Migrate to microservice architecture
5. Challenges of Microservices Architecture
	1. Technical challenges:
		1. Microservices is a highly distributed system
			1. We took a centralized system and broke it into a highly distributed system
				1. Method calls in monolithic application used to have:
					1. Predictable behavior
					2. Predictable success (success rate)
					3. Predictable performance
				2. Method calls have become network calls between services
					1. Requests are now traversing un-reliable network
						1. Packets can be lost or delayed
							1. They cause unpredictable latency issues and errors
								1. Predictability in behavior is worse
								2. Predictability of success rate f calls is worse
								3. Predictability of performance is worse
				3. Each component is inherently un-reliable
					1. If a request from one service instance hits a process that crashed either due to hardware or software failure or is restarted as part of a routine maintenance
			2. Testing Microservices
				1. Testing each microservice in isolation became faster and easier
				2. However, there is no guarantee that once all the services are deployed, they will work correctly together as a whole
				3. If we make a change in one service, there is much less confidence that once then new version of the service is deployed in production, it wont break another service
					1. This may lead to the creation of very complex and slow integration tests that can slow our productivity
						1. Since each service is owned by an independent team, it is very hard to decide who owns the integration tests
			3. Troubleshooting and debugging (performance issues and bugs)
				1. Consider a situation when a user request goes through a chain of microservices
					1. The user in the end got:
						1. The correct information
						2. An error
						3. The correct information with a delay
				2. How can we know which microservices is responsible for the bug or performance issue
			4. Organizational Scalability
				1. How to set the scope of responsibility between microservices
					1. If we set the boundaries incorrectly, we may have more organizational overhead than benefits
						1. If every change in the system requires careful coordination in the teams, we are better of with what we had in the monolithic architecture
					2. If every team uses a completely different technology stack, tools, best practices
						1. There might be a lot of duplicate efforts and confusion when looking at the code-base of a different team
		2. If we don't consider the above challenges, we might be in a much worse situation after migrating to microservices than staying a big monolithic application
			1. This situation is referred to
				1. Distributed monolith
				2. Big ball of mud
	2. Good news:
		1. Many companies have already gone through the "growing pains"
		2. Software Architects have been sharing:
			1. Knowledge
			2. Success stories
			3. Mistakes
		3. We can now have a set of (for successful microservices architecture):
			1. Principles
			2. Best practices
				1. If we follow the principles and best practices, the benefits we get far exceed the complexity
4. Summary:
	1. Learned about Microservices Architecture
	2. Benefits:
		1. Organizational scalability (due to smaller code-base of each microservice)
		2. System scalability (allows us to choose the best technology for each microservice and choose a cheaper hardware)
	3. Challenges:
		1. Complexity and unreliability of running a highly distributed system (with unreliable components talking to each other with an un-reliable network)
		2. Risk of decreased organizational scalability (if we incorrectly set the boundaries between microservices and the teams)

### Download Course Workbook ###
1. Interactive Workbook
	1. Notes
	2. Bullet-points
	3. Diagrams

## Migration to Microservices Architecture ###
### Microservices Boundaries - Core Principles ###
1. What we will learn in this lecture:
	1. System Introduction
	2. Attempt 1 - Splitting by Application Layers
	3. Attempt 2 - Splitting by Technology Boundaries
	4. Attempt 3 - Splitting for Minimum Size
2. Set of principles to arrive at the boundaries of microservices
	1. To arrive at the principles, we will go over those principles to split an existing monolithic application
		1. The case studies are not just thought experiments but real situations of companies that went through the migration and went through issues in the process
		2. Each case study helps us define a new core principle for successful migration to microservices architecture
3. System we are going to migrate
	1. Just breaking a large codebase into an arbitrary set of microservices (and handing each one to a separate team) won't give us any benefit
	2. Monolithic E-Commerce Application (Online store for 1000s of customers)
		1. Architecture:
			1. Tree Tier (monolithic web-application in the middle tier)
			
					Webpage
					Mobile App
						|
						v
					Online Store Web Application
						|				|
						v				v
					Database 			Payment Processing Company
					(transactions, 		(user credit card billing)
					products, 
					reviews, 
					inventory)
					
			2. Problems:
				1. Codebase is too large and complex
				2. Binary size is big - requires very expensive hardware
				3. Development team is too big (violation of 2 pizza rule)
			3. Solution:
				1. Microservices
					1. But how do we split the application into microservices?
4. Attempt 1 - Splitting by Application Layers
	1. Application Tier
	
			Store Front Layer (Split it into its own service)
			(handles:
			user requests,
			security,
			permission validation,
			serves HTML, CSS, JS to Web Browser
			- It is maintained by a separate team &
			- Physically deployed as a separate runtime unit)
			|
			v
			Business Logic Layer (split it)
			(handles:
			Product recommendations,
			Reviews,
			Checkout,
			Discounts,
			Accounts,
			Users,
			...)
			|
			v
			Data Persistence &
			Payment Processing Layer (separate service)
			
		1. It seems like a good idea!
			1. It takes advantages of existing logical layers within the application
			2. There is no major refactoring required
		2. This approach does not work very well (it doesn't give us much benefit)
			1. Reasons:
				1. Every new feature might require
					1. API change (in the Store Front Service)
					2. Business Logic Change (in the Business Logic Layer)
					3. Data Change (in the Data Persistence & Payment Processing Layer)
				2. All the microservices in the system will be involved in every feature
					1. This requires careful planning and release coordination between different teams
						1. No benefit in terms of organizational scalability
				3. Effectively, we have made 3-tier architecture into a 5-tier architecture
					1. It is still not microservices
						1. Breaking a monolith into more tiers might not work
	2. Microservices Boundaries - Core Principles:
		1. **Cohesion**: Each microservice needs to be cohesive
			1. Cohesion: Elements that are tightly related to each other and change together should stay together
		2. The logic that changes together stays within the boundaries of the same microservices
			1. Each team can truly operate independently
		3. Our migration failed because microservices were not cohesive enough (to improve organizational scalability)
5. Attempt 2 - Splitting by Technology Boundaries
	1. Observations:
		1. Rewriting a part of Store Front Layer in Node.js (with JS), they could reduce the number of lines of code by 50%
		2. Rewriting the other part of Store Front Layer in Java, they could improve the performance by 20%
		3. Rewriting a part of Product Recommendations engine that requires heavy computations into a C++ library 
		4. Rewriting the other part of Production Recommendations engine in Python enables us to some powerful machine learning libraries that can improve our performance even further
		5. Rewriting a part of Payment Processing Service that talks to external Payment service into GoLang improves performance and the number of lines of code in that module
		6. After splitting modules into those microservices, we saw a great performance improvment
	2. Results:
		1. Boundaries are purely technological
		2. Outside stakeholders (who are unfamiliar with the codebase like project managers requesting features or support engineers reporting bugs from users) don't know which subteam/service gets the task
			1. Example: If a project manager wants to update the recommendation engine, it is not clear whether they need to talk to C++ team or Python team or both
				1. Same is applicable for Store Front services
				2. It is unclear for a frontend developer, which code-base needs to change for a given feature
				3. Terminology of each API is also convoluted - we are mixing different contexts (User's ID, Bank Account ID, Product ID, Product Names, User Names)
					1. `GetById(...)`
					2. `ListNames(...)`
				4. The last microservice which still has most of the business logic has too much responsibility and is still too big
					1. It has the potential to become yet another monolithic application
	3. Microservices Boundaries - Core Principles:
		1. **Single Responsibility Principle (SRP)**
			1. Every Microservice should do only one thing and do it exceptionally well
				1. If each microservice follows this principle, there is no ambiguity about:
					1. Where new functionality needs to go
					2. Which team needs to own what
					3. It can be used to construct easy to follow API for each microservice
						1. All the terminology, entities, and identifiers are bound to a given context
						2. Example:
							1. To talk to user service - It is ID is user id, name is user's name (user's context)
							2. To talk to product service - It is product context (no ambiguity)
6. Attempt 3 - Splitting for Minimum Size
	1. Minimizing Microservices Size
		1. _Micro_services
			1. Assumption - Splitting into tiny services would give us the best benefits
				1. The smaller the better
					1. Hence we take a course grain approach and split every package and module into microservice
					2. If the application is written in an object oriented language, we could split every class into a microservice
						1. Bigger problems:
							1. Every request from user triggers a chain of communication between microservices
							2. Each microservice needs to talk to even more microservices to do its work
								1. Problems:
									1. Performance is really bad (due to network hops)
									2. Troubleshooting issues becomes almost impossible
								2. The microservices are tightly coupled with each other
									1. Operation requires a lot of communication between services
	2. Microservices Boundaries - Core Principles
		1. **Loose Coupling** - Loosely coupled microservices have very little/no interdependency
			1. Each microservice can perform its functionality with minimum communication with other microservices
			2. The size of a microservice is not important
				1. Common misconception - microservices have to be as small as possible
					1. Microservices name is somewhat misleading
7. As long as our microservices are the following, the size doesn't matter:
	1. **Cohesive**
	2. Follow the **Single Responsibility Principle**
	3. **Loosely Coupled**
8. Different microservices may have different sizes
9. The three principles are prerequisites for successful microservices architecture
	1. If we don't follow them, we are likely to encounter issues sooner or later
		1. However, the principles don't tell us exactly how to split a monolithic application into microservices that follow those principles
10. Summary:
	1. Core principles for Microservices Boundaries:
		1. Cohesion
			1. Elements that change together stay within the boundaries of one microservice
		2. SRP
		3. Loose Coupling
			1. From other microservices to minimize the runtime communication
	2. Size of the Microservices doesn't matter
		1. Sizes can be different depending on their functionality
 
### Decomposition of a Monolithic Application to Microservices ###
1. What we will learn in this lecture
	1. Decomposition by Business Capabilities
	2. Decomposition by Domain/Subdomain
	3. Decomposition by Business Capabilities vs Subdomain
2. Two methods to decompose microservices using the three principles
3. **Decomposition by Business Capabilities**
	1. We observe and analyse the system from a purely business perspective
		1. Business capability:
			1. It is any core capability that provides value to:
				1. Business
				2. Customers
			2. Examples:
				1. Revenue
				2. Marketing
				3. Customer experience
				4. ...
			3. Each Capability -transformed into-> Microservice
	2. Identifying Business Capabilities:
		1. Run a throught experiment
			1. Describe the system to a non-technical person
			2. Explain what the system does/ what value each capability provides
		2. Example:
			1. Online store
				1. **Browse** through products (using web-browser)
				2. Search/view for **products** (and details)
				3. Read the **reviews** (for each product left by customers)
				4. Place an **order**
				5. **Shipping** of the product
				6. Update/Maintain product **inventory** (from client's perspective, merchant's perspective)
			2. Mapping:
				1. Web App Service
				2. Products Service
				3. Reviews Service
				4. Orders Service
				5. Shipping Service
				6. Inventory Service
		3. How do we know that the services follow our three core principles?
			1. SRP - Design follows SRP because each service does only one thing
				1. Each service is responsible for an entire business capability
			2. Cohesive - Consider the changes that need to happen to our system to extend certain functionality
				1. Example:
					1. Adding new products (needs change only to the products service)
					2. Adding products to existing products (needs change only to the products service)
					3. Set policies for how users leave or filter reviews (only Reviews Service needs to be changed)
					4. Changing third party processing company or add a new accepted payment type (only Orders Service needs to change)
			3. Loosely Coupled - Verify that the services are not too interdependent by reviewing a few user journies or use-cases
				1. Example: User wants to load the online store
					1. Request can be fulfulled by the web-app service
					2. When a user wants to search for a product or view a product, the request can be fulfilled by the products service
					3. When user wants to review, only review service is invoked
					4. When orders for shipment of a product, the only services involved are: Orders Service, Shipping Service, Inventory Service
						1. Each takes care of one clearly defined part of the transaction
4. **Decomposition by Domain/Subdomain**
	1. Unlike the previous technique that looks only at the business side, we take the developer's point of view of the system
		1. Criteria for setting the boundaries of sub-domains is based on the Engineers understanding of the system (generally more intuitive)
	2. In this technique, we decompose the system into small sub-domains
		1. Sub-domain: Sphere of knowledge, influence or activity - Eric Evans
			1. Three types of sub-domains
				1. Core - Sub-domain that represets a core business capability
					1. It is the Key differentiator of our business from any other competitor in the field
					2. It cannot be bought of the shelve/outsourced
						1. In it we put our best effort and investment
					3. Without it, our business doesn't provide any value
				2. Supporting - Sub-domain that supports a business capability
					1. It is integral to our operation of our business
					2. It supports delivering the core capabilities
					3. But it is not (necessarily) different from our competitors
				3. Generic - Generic sub-domain
					1. Not specific to any business
					2. Can be bought/Use off-the-shelve
						1. Many companies use them
			2. This categorization of sub-domain helps:
				1. Prioritize the investment into each sub-domain
				2. Allocate engineers by experience
					1. Top and most experienced engineers
				3. Save costs/time using off-the-shelf solutions (where we can do that)
			3. Example: Online Store
				1. Core Subdomains
					1. Products Catalog
						1. If we go to any other online store, we do not see the same products or get the same experience
							1. Hence it is unique
				2. Supporting Subdomains (without them we cannot sell products but they may be similar in functionality to other online stores)
					1. Orders
					2. Inventory
					3. Shipping
				3. Generic Subdomains (still essential but very generic - many other business online/offline need and use them - we can use of-the-shelf implementations)
					1. Payments
					2. Reviews
					3. Search
					4. Images
					5. Image Compression
					6. Security
					7. Web UI
				4. Subdomains to Microservices:
					1. Products Catalog
					2. Orders
					3. Inventory
					4. Shipping
					5. Reviews
					6. Payments
					7. Search
					8. Images
					9. Image Compression
					10. Security
					11. UI
				5. We could have one microservices per subdomain
					1. However, we see that some subdomains are:
						1. Tightly coupled with the other
						2. They aren't cohesive enough
					1. We can group several subdomains into one microservice
						1. Images & Image Compression can be grouped into a single service if we find that they are inter-dependent
						2. If we figure out that the Payments service does not have enough logic to justify a separate service or if it is too tightly coupled with the Orders service, we can group them into one microservice
						3. If after a while, we realize that we need to separate them, we can do so (because of the small size of the microservices)
5. Other Methods
	1. Decomposition by Action
	2. Decomposition by Entities
6. Setting boundaries by business capabilities or sub-domains are the two most popular methods and easiest way to do so
7. Decomposition by Business Capabilities vs Subdomains
	1. Comparison
		1. By Business Capabilities
			1. Cohesion and Loose Coupling: Winner
			2. Size of Microservices: Course grained => larger microservices
			3. Stability of the Design: Stable
				1. Because core business is much more stable than Engineering and technology: Winner
			4. Intuitive for Engineers:
				1. Requires much better understanding of the business
					1. Less intuitive design for engineers
		2. By Subdomain
			1. Cohesion and Loose Coupling
			2. Size of Microservices: Fine grained => smaller microservices: Winner
			3. Stability of the Design
			4. Intuitive for Engineers: Winner 
8. Final Notes
	1. No "one right" way for decomposition into microservices
		1. What might work at the moment may not work well in the future
		2. Architecture keeps evolving as new features come in and new business capabilities are added
	2. No perfect decomposition
		1. Some friction or coupling is inevitable
			1. Goal of setting the boundaries correctly is to minimize the friction and not to eliminate it completely
	3. No technique is bulletproof
		1. They are just guidelines or tools to arrive at a good architecture
			1. It is not a substitute for good engineering judgement and intuition
9. Summary:
	1. Techniques for Decomposition to Microservices:
		1. By Business Capabilities
		2. By Subdomain
			1. Types:
				1. Core
				2. Supporting
				3. Generic
	2. The identified domains were guidelines for setting the boundaries of microservices
	3. Engineering judgement is necessary for the final design

### Migration to Microservices - Steps, Tips and Patterns ###
1. How to perform a migration from a large legacy monolithic application into microservices
2. What we will learn in this lecture
	1. Where to start the migration to microservices
	2. Preparing for the migration
	3. Execute the migration using the strangler fig pattern 
	4. Tip to ensure smooth migration (we don't run into issues while performing the migration)
3. Where to start the migration to microservices
	1. Big Bang Approach
		1. The plan:
			1. The team maps out microservices boundaries (for future microservices architecture)
			2. The team tries to get the management on board to stop any development of any features and fully focus on the migration
		2. On the surface:
			1. Seems to be a good idea
				1. If the entire team fully focuses on migration and doesn't get distracted by developing new features, they can finish it much faster
		3. In reality:
			1. Worst approach (in terms of productivity and impact on business)
			2. Problems:
				1. "Too many cooks in the kitchen"
					1. Having too many developers refactoring a monolith into microservices is a bad idea
						1. The goal was to migrate to microservices because our team already had productivity and communication issues
							1. Organizational scalability
						2. Having too many developers for such a large migration effort might cause a lot of friction
				2. Hard to estimate the effort for large and ambiguous projects
					1. Just as with big and ambiguous projects, we often encounter technical problems we didn't foresee
					2. If we promised management that we will be finished in 4 months and we are not done even 5 months later, the managers will get nervous
				3. High risk of abandonment
					1. To minimize the additional time loss
				4. Stopping development of new features for many months can be very detrimental to the business
					1. Product managers may get bored and might have no way to get promoted which in turn may cause them to leave the company
					2. Sales people have nothing to sell or pitch the new client
					3. Users (who don't care about our internal architecture) might think that our business is in trouble or the company is unwilling to improve its business
	2. Incremental and Continuous Approach:
		1. We identify the components that can benefit the most from the migration
			1. Best candidates: (ranked by the benefit we get from migrating them are the following):
				1. Areas with the most development/frequent changes
					1. Migrating code that no body ever touches doesn't give us any value
						1. It isn't the source of our problem
					2. Logic that is constantly evolving is the biggest source of merge conflicts
					3. It is the biggest contributor to our releases of our entire monolithic application
						1. If we separated into microservice, the changes will not require us to re-deploy the code that didn't change
						2. This dis-entangles the business logic from the rest of the application
							1. Much easier to reason about
							2. Less likely to introduce bugs
					4. Once we migrate that part of the application to a microservices, we identify the next candidate and continue until we reach a point when the original monolith is gone or nothing changes in the left over monolith
					5. Incremental and Continuous Approach - Benefits
						1. No hard deadlines necessary (to complete the migration)
							1. Even if it takes a long time to finish the migration, we are making a constant, visible and measurable progress
						2. Business is not disrupted
						3. Even if migration of one part of code exceeds the time estimates, it is not a problem
							1. It is going to be a few days or weeks & not months or years
				2. Components with high scalability requirements (that cannot be met as long as they are part of the big monolithic application)
				3. Components with the least technical debt (and good logical separation that fits the scope of a microservice)
4. Preparing for the Migration: (After identifying the components to migrate)
	1. Add/ensure code test coverage
		1. Critical
		2. With good code coverage, we have the confidence that we did not break any functionality during refactoring
			1. Or else, the entire migration might get delayed if things start breaking
	2. Define component API
		1. Define a clear and well thought out API for the component we want to migrate
	3. Isolate the component by removing interdependenices to the rest of the application
5. Execute the Migration using the Strangler Fig Pattern:
	1. Strangler Fig Pattern - By Martin Fowler
		1. Plant starts as a small wine growing on top of an existing old tree.
		2. Over time, it spreads and grows completely consuming the old tree, taking its place
	2. Steps:
		1. Introduce a Strangler Facade [in front of the monolithic legacy application]
			2. It allows requests to pass through
			3. It is usually implented with an API Gateway (of-the-shelf open-source or cloud based component that routes requests based on the API they indend for)
		2. Once the newly created microservice is throroughly tested and deployed, we divert the traffic for that API from monolithic application to the newly created microservice
			1. This change happens completely transparently to the users
			2. It minimizes the risk of issues during the migration
		3. After monitoring the performance and functionality of the new microservice for sometime, we can remove the old component with the same functionality in the monolithic application
		4. We repeat the above steps for each microservice until we are left with an empty old application or a legacy application to support old clients
6. Tip to Ensure Smooth Migration (bug free)
	1. Keep the code and technology stack unchanged as much as possible
		1. Every change we make is a potential source for a bug
			1. Migration itself is complex and risky enough
			2. We don't want to add any more risk factors to the process
		2. Once the migration is complete and the application is running and is stable, we can easily start refactoring them to use new technologies
7. Summary:
	1. We have learnt how to prepare and execute the migration to Microservices Architecture
	2. Best candidates:
		1. Components that change frequently
		2. Components that require higher scalability
		3. Components that have the least technical debt
	3. Migration process:
		1. Add/ensure "test coverage"
		2. Define the API
		3. Isolate the component
		4. Use Strangler Fig Pattern

## Microservices - Principles and Best Practices ##
### Databases in Microservices Architecture ###
1. The key principles and best practices for microservices architecture
	1. By following the principles, we will benefit the most from using microservices and minimize the chance of running into scalability or other issues
2. The principles and best practices comes from years of experience shared by software architects and technical leads running large scale systems using microservices
3. What we will learn in this lecture:
	1. Motivation for Database Per Microservice
	2. Benefits of Database Per Microservice Principle
	3. Downsides of Database Per Microservice
4. Motivation for Database Per Microservice:
	1. Example: Consider Monolithic architecture of an insurance company
		1. Three tier
		2. We migrated the application to a set of microservices with each team owning a microservice
			1. Policy Purchasing Service
			2. Claims Service
			3. Customers Service
			4. Reporting Service
		3. We expect the teams to operate with very little friction
			1. Allows microservices to share data
				1. Policies Table
				2. Claims Table
				3. Customers Table
			2. Reporting Service needs access to all 3 tables
				1. It is much more efficient for allowing Reporting Service to access the data from the database directly
					1. We don't have to pay the performance overhead of getting the data through the appropriate services
						1. Problems:
							1. Suppose the Policy Purchasing service gets a lot of traffic from potential policy buyers
								1. Team owning the service uses its autonomy to replace the slow, legacy relational database with a read optimized NoSQL database
									1. **However, the Reporting Service code is tightly coupled to the database technology where the policy purchasing data is stored, the changes must happen in both Policy Purchasing Service and Reporting Service simultaneously**
										1. Both services must be released simultaneously
							2. Suppose Claims Service team decided to change the schema of their Claims Table by renaming columns, removing old and unused columns, adding columns
								1. The two teams managing the Claims Service & Reporting Service respectively have to meet and discuss the schema that works for both of them
								2. Code changes need to be made to both the services and released simultaneously
							3. Suppose Customers Service team decided to add a lot of fine-grained security around what user data can be read or modified based on different organizational roles
								1. The security policies are outside the scope of Reporting Service team's domain
									1. The Customers Service team needs to communicate those changes including all the implementational details to the Reporting Service team
									2. Both teams must make code changes, write tests, and simultaneously release and monitor the changes
						2. Despite all the migration efforts, our teams are still tightly coupled and require a great deal of communication and coordination
							1. Negatively impacts organization's productivity and development velocity
5. Benefits of Database Per Microservice Principle
	1. Each microservice team fully owns it's data and does not expose it directly to any other service
		1. At the cost of additional latency
	2. Whenever a service requires data from another service, the request has to go through the target service API
	3. Each service needs to abstract the actual database technology at the API level
		1. If the team owning the microservice decides to change the database technology, or schema, the change is transparent to the consumers of the API
		2. If the changes requires changes to the API, we can offer different versions of the API for a few weeks or months
			1. Allows other teams to make their changes and update to the new API, without the need for any coordination
6. Downsides of Database Per Microservice
	1. Added latency (the following add latency as compared to a direct query against the database)
		1. Sending network request to another service
		2. Parsing the request
		3. Querying the database
		4. Sending the data back
		5. Parsing the response
			1. Solution: If performance overhead becomes an issue, it is okay to cache or store some data that belongs to another service in its own database
				1. It is important to ensure that the source of truth is the owning microservice
				2. If we cache data that belongs to another microservice, we lose strict consistency and have to settle for eventual consistency
					1. The local data might be stale until we get the new data from the source of truth
	2. No more "join" operation (from multiple tables)
		1. When all data belonged to a single database, we could easily perform join operations based on a common key or column
		2. When we split the data across different databases, some of which may not be relational databases, we can no longer perform join operations
			1. The only way to achieve the same functionality is to pull data from both the databases, transform the data so both objects are represented in the same format, and join the data programmatically
	3. No support for transactions
		1. With single database, we could modify rows in multiple tables as part of a single transaction and guarantee that the change to all those tables will be atomic
		2. Performing distributed transactions across multiple services is very hard
			1. It is theoretically possible, it is never used
		3. A few patterns that can solve the challenges very efficiently
7. Summary:
	1. Database per microservice principle
	2. Motivation:
		1. Sharing a database tightly couples:
			1. Codebases (coordination overhead)
			2. Teams (coordination overhead)
		2. Coordination overhead is eliminiated when each microservice owns its data
			1. Exposes it through an abstraction API
	3. Drawbacks of Database Per Microservices:
		1. Worse performance
		2. Complex join operations
		3. No transactions

### The DRY Principle in Microservices and Shared Libraries ###
1. DRY - Don't Repeat Yourself
2. What we will learn in this lecture
	1. Importance of DRY (Don't Repeat Yourself)
	2. Challenges of following the DRY and Shared Libraries
	3. Alternatives to Shared Libraries in Microservices Architecture
	4. Sharing / Duplicating data across Microservices
3. Importance of DRY (Don't Repeat Yourself)
	1. DRY - Don't Repeat Yourself
		1. If you repeat the same Logic or data (constant values) you should consolidate it as shared:
			1. Method
			2. Class
			3. Variable
		2. If we have a more complex logic used in multiple projects or applications, it is a common practice to package the logic into a shared libary that other applications can import and use
			1. If we want to change the logic, we can do it in only one place (no duplicate searching in multiple code-bases)
		3. Reduces duplicate effort
			1. Work of a single engineer can be reused (by others)
	2. DRY doesn't always apply to Microservices (particularly in regards to shared libraries)
4. Challenges of following the DRY and Shared Libraries
	1. Problems:
		1. Tight coupling: Violation of microservices core principle
			1. If two microservices share and depend on a library, any changes to the library becomes a source of tight coupling and friction between different microservices and owners of the library
			2. If there are API changes to the library, those changes need to be communicated to the other teams that own those microservices
				1. The teams need to make appropriate changes in their code-base so that they can continue using the library
		2. Every change (in the shared library) requires
			1. Rebuild
			2. Retest
			3. Redeploy
		3. Bug/vulnerability in a shared library impacts all microservices
			1. Defeats the purpose of isolating the microservices as separate runtime units in the first place
		4. Dependency Hell
			1. Microservice 1 uses shared library A (v5.0)
			2. Library A uses Library B (v1.0)
			3. Microservice 1 uses Library B (v1.0) in another part of its code base
			4. A new update has been made to Library A to v6.0
			5. Library A v6.0 depends on Library B v2.0
			6. In some cases, we cannot depend on two versions of the same library simultaneously (depending on the language and runtime we are using)
				1. If so, we are forced to make an unnecessary code change to use Library B v2.0 directly
			7. In other cases, where we can depend on two version of the same library, we are breaking the DRY principle
				1. 2 almost identical copies of library B
				2. Increases size of binary and time it takes to build and test it
5. Alternatives to Shared Libraries in Microservices Architecture
	1. Situation 1: Shared Business Logic
		1. Complex business logic is shared across multiple microservices
			1. May indicate that we incorrectly set the boundaries between the two microservices
				1. One of the core principles of microservices is SRP
					1. If we followed decomposition by business capability or by subdomain, we would rarely get into this situation
					2. If we do, we may have to consider re-evaulating the boundaries
			2. Solution:
				1. Option 1: Readjust the Boundaries
					1. Only one of the microservice contains the business logic
				2. Option 2: New Microservice
					1. If the business logic is complex enough, we can separate it into a separate microservice
	2. Situation 2: Common Data Models for Communication between two microservices
		1. Option 1: Have shared libraries or files
			1. Reasons:
				1. When it comes to communication between two microservices, we want the two teams and code bases to be co-dependent
				2. If the API or data model of one microservice changes to the point they cannot communicate:
					1. We want to break the tests asap
				3. If we don't share but duplicate code
					1. The tests of each microservice may pass successfully but not detect the change in the other microservice
						1. The two microservices may not be able to communicate at runtime and may find out about it only in production
		2. Option 2: Code Generation Tools
			1. Generate code based on data models or schema
			2. We have a shared schema representing the common data model for the communication of the two microservices
				1. Examples:
					1. Interfaces
					2. gRPC Definition
					3. GraphQL Schema
			3. Depending on the API language or technology, we can use the appropriate tool to generate data models and boilerplate code for communication between the microservices
			4. As long as the code is generated based on the shared interface definition and the generation is done as part of the following, it is a safe approach
				1. Build process 
				2. Test process
6. Code That is OK to Duplicate
	1. Utility methods that change frequently
		1. Duplicate it across different microservices instead of trying to reuse it in a shared library
			1. Reasons:
				1. Each microservice can have its own optimized implementation of the logic
				2. Makes it easier to migrate microservices to other programming languages
7. No Code Duplication Options
	1. Option 1: Sidecar Pattern
		1. We package and deploy the shared functionality as a separate process
			1. We run the process in the same host as the microservice instance
				1. This enables us to share the same functionality across multiple instances of the same microservice and across multiple instances of different microservices
		2. A microservice instance can communicate with its co-located sidecar process using its familiar and standard network protocols
			1. Microservice to sidecar communication overhead is:
				1. Smaller than with other services/hosts
				2. Higher than with code in a shared library inside the microservice process
	2. Option 2: Use shared libraries (if we have a very generic and stable code that rarely changes: logging, retrying, pattern matching if they don't lead us to dependency hell)
		1. The shared libraries have to be self contained/independendent of other libraries as much as possible
		2. Use it as a last resort
8. Final Note on DRY in Microservices
	1. Inside each individual microservices, we still follow DRY
	2. Code duplication (within a microservice) is unacceptable
		1. We extract common logic into method, class, or module
9. Data Duplication in Microservices
	1. Duplicating the same data across microservices and storing them into databases may seem like a waste of storage space
		1. It is sometimes necessary to improve performance
	2. **If we don't want to pay the price of sending a request to another service for data, we can store a cache of the data inside our microservice**
		1. In the microservices architecture, this approach is completely acceptable as long as we remember that:
			1. Only one owner/ source of truth
				1. Only one microservice gets write/update/delete
				2. Other microservices (containing a copy) only get read
		2. We can only guarantee eventual consistency
			1. If strict consistency is required, data duplication must be avoided
		3. Examples:
			1. Online store:
				1. We may store Ratings & Reviews of a product inside Products Service (cache)
					1. When a user wants to look at a product, we can quickly load the data from the Product Service (no communication is required with the Review Service)
						1. We may have only eventual consistency
							1. They may not be the most recent reviews
								1. The inacuary is not that important
				2. For up to date inventory information and account balance of a user, we need to guarantee strict consistency
					1. We must not duplicate the data in any other service (from Inventory Service and User Service)
10. Summary:
	1. Revisited the DRY Principle for shared libraries and data in Microservices architecture
	2. Benefits of DRY in general but not always in Microservices
	3. Challenges of shared libraries in Microservices:
		1. Tight coupling
		2. Rebuild, Retest, Redeploy (with every change in the library)
		3. Dependency hell
	4. Alternatives to shared libraries
		1. New microservices
		2. Sidecar pattern
		3. Code generation
		4. Code duplication
	5. Data duplication in Microservices
		1. Important for performance reasons
		2. Makes data eventually consistent
		3. Only one microservice needs to ramain the owner of each data
	
### Structured Autonomy for Development Teams ###
1. What we will learn in the lecture
	1. Problems with full team autonomy (giving too much freedom to each microservices team to decide its tech stack, tools, and processes)
	2. 3 Tiers of development team autonomy
	3. Factors in team autonomy boundaries
2. Problems with full team autonomy:
	1. Myth:
		1. Each team can choose their own:
			1. Technology stack
			2. Tools
			3. Databases
			4. APIs
			5. Frameworks
		2. Pitfalls of companies that migrate to microservices
		3. Reasons:
			1. Full Team Autonomy Problems:
				1. Upfront cost of infrastructure
					1. In a monolithic application, we put a lot of effort on how to structure our code, frameworks to use, how to organize classes, modules, packages, libraries
						1. We define guidelines on where to store our tests and how to run them
						2. We spend a lot of time on setting up and customizing build tools, scripts, and CI pipelines
						3. We also invest in monitoring and alerting tools (it is not a trivial effort)
						4. A lot of work went into designing database schema and configuring it for:
							1. Scalability
							2. Fault tolerence
							3. Highly available
					2. After migrating to microservices, each team may have to pay the same cost and duplicate the effort for their codebase and ecosystem
				2. Infrastructure maintenance cost
					1. Maintaining infrastructure is an ongoing effort
						1. If there are dedicated DevOps, QA, SRE teams
							1. They have to migrate the infrastructure of 100s of microservices where each one is entirely different
							2. The teams will eventually get overwhelmed and will need to hire more people **to keep up with the jungle of technologies**
							3. There is also cost associated with learning and becoming productive in all those tools
								1. Need to read documentation
								2. Memorize Infrastructure + best practices
								3. Get used to following them
				3. Steep Learning Curve:
					1. What if they need to make a small code change in another code-base?
					2. What if they just want to look at another codebase and find out how they setup integration tests, configuration?
					3. It doesn't scale in a large organization
				4. Non-Uniform API
					1. The microservices need to come together as one system
						1. They need to communicate with each other to accomplish a common goal in an easy and performant way
					2. What if each team could define their own API in their own style following their own best practices
						1. Problems:
							1. Front-end engineers who need to pull the data need to:
								1. learn the API of each team and integrate with it
								2. Use different naming conventions and using many different API styles and technologies
									1. Makes the front-end code a huge mess that is hard to read and maintain
							2. If a microservice needs to communicate with several different microservices, in different scenarios, we run into the same problem
								1. Engineer who needs to add or update an API call, may need to spend hours reading the other team's documentation to ensure it adheres to best practices
			2. We are making things worse by allowing teams full autonomy and introducing a lot of overhead
				1. Isn't the point of Microservices to allow team independence?
					1. Key to success with microservices is the balance between **autonomy** and **structure**
						1. **Structured autonomy** - each team is autonomous but only within certain boundaries
3. 3 Tiers of Development Team Autonomy
	1. Tier 1 - Fully Restrictive
		1. Describes the areas that should not be under each team's jurisdiction
			1. The areas should be uniform across the entire company
		2. Includes:
			1. Infrastructure (We can invest a lot of efforts upfront into adopting or building the infrastructure from scratch & effort is amortized across the entire organization - makes it cost effective)
				1. Monitoring and alerting
				2. CI/CD (technologies and scripts)
			2. API guidelines and best practices
				1. For defining public and internal APIs
					1. Because external clients don't care that they are sending requests that end up in different microservices inside our system
					2. Because, internally it makes integration and communication between microservices belonging to different teams very easy
			3. Security and data compliance
				1. Reasons:
					1. If any one microservice gets hacked, the entire system may become vulnerable
					2. If any any microservice violates local privacy or data retention policy, the entire Org can be held accountable
						1. No one cares externally that it was the fault of only one microservice
	2. Tier 2 - Freedom with Boundaries (each runtime and data storage solution is optimal for a different usecase, however, the set of approved programming languages and database technologies should be restricted - prevents a jungle of technologies (if team chooses the latest and most fashionable programming langauges for their microservice), it takes a lot of time for a company to develop expertise in managing, configuring and running each type of runtime and database in production)
		1. Choosing programming languages
			1. Most big tech companies use no more than a handful programming languages across 100s of microservices
		2. Choosing database technologies
	3. Tier 3 - Complete Autonomy (each team can work independently of other teams)
		1. Release process
		2. Release schedule and frequency
			1. Release features based on their workload, priorities, and requirements
		3. Develop their own tools and custom scripts for their local development and testing (to make it efficient)
		4. Documentation
			1. Each team owns its own documentation
		5. Onboarding process for new developers
			1. Each team owns its own onboarding process
4. Factors in team autonomy boundaries: (actual boundaries differ slightly in each company)
	1. Size / influence of DevOps / SRE team
		1. Companies with more dominant DevOps or SRE teams lean more towards common standards
			1. Makes their lives managing the system easier
	2. Seniority of Developers
		1. The more senior the developers are, the more freedom they prefer in setting up or building their own infrastructure
	3. Company's culture
		1. Some companies just stick to one programming language (C#, Java, Python, ...) and don't allow any freedom to choose any other programming languages
			1. Benefits
				1. They can hire developers once and move them between teams with very little overhead
5. Summary:
	1. Disadvantages of full freedom to each microservice team
		1. Upfront cost
		2. Ongoing maintenance costs
		3. Steep learning curve and overhead
		4. Non-uniform API
	2. Solution: "Structured Autonomy"
		1. Allows teams to still be independent but within a set of boundaries
	3. Factors that influence the boundaries of teams' autonomy:
		1. DevOps/ SRE team's influence
		2. Developers' seniority

### Micro-Frontends Architecture Pattern ###
1. What we will learn in this lecture:
	1. Problems of a Monolithic Frontend
	2. Micro-frontends architecture pattern
	3. Real-life example of Micro-frontends + Microservices 
	4. Benefits and best practices (for using the pattern)
2. What is a monolithic frontend?
	1. Example: Online learning platform
		1. Users can search for, enroll in, and take online courses
		2. Frontend includes the homepage
			1. Displays a search bar
				1. User can search for courses by key-words or categories
			2. Recommended for you
				1. Shows courses that the user may be interested in
			3. Learners Profile button
			4. When user searches for a course based on a keyword, a list of courses will be displayed
			5. When a user clicks on a course, it will bring them to the course landing page
			6. When they are interested in the course, then can click on the enroll button which brings them to the enrollment page
			7. On the enrollment page, they can provide payment info, name, and billing address and complete the enrollment
			8. On the homepage, when user clicks on Profile button, they will be presented with user profile and all the courses they are enrolled in
		3. Backend side:
			1. Architected the system using microservices architecture (following all the best practices of microservices decomposition)
			2. A separate team own each microservice
			3. Each microservice owns its own database
			4. The microservices communicate with each other will a well defined API that adheres to the company-wide standards
			5. The microservices share a common set of tools and infrastructure to test, deploy, and monitor the system in production
		4. Frontend Side:
			1. There is only one Frontend development team
				1. It maintains a single codebase responsible for all the user experiences
					1. The entire web-app code resides in one single code repository
					2. It is fetched from web-application service to the user's browser
				2. When Course Discovery Service wants to add a feature that allows users to search for courses using additional attributes (course length, language, rating, ...), we have a problem:
					1. Backend team makes the change in the microservice
					2. Backend team needs to ask the Frontend team to dedicate their time to add the feature to the frontend
				3. When Recommendations Service team wants to show the users more, or different data, they will have to coordinate and cooperate with the same frontend team to deliver it
				4. The above has resulted in dependency for all microservices teams on that one frontend team
					1. Bottleneck in a development organization
				5. When frontend team wants to improve user's profile page, the frontend developers will have to learn and integrate with Users Service team
				6. To optimize the enrollment and checkout process, the frontend team have to get very familiar with enrollment and payment services business domain and APIs
					1. **Frontend teams have to constantly develop expertise in domains that belong to other teams**
						1. This tightly couples backend teams and already constrained frontend teams
							1. We wanted to avoid this by moving to microservices
								1. Organizational problems
				7. Technical problems:
					1. As the business grows, so does the frontend
						1. Single codebase becomes very large to maintain and reason about
						2. It takes longer to test
						3. If we want to release a new UI feature, the entire frontend code needs to be rebuilt, re-tested, and redeployed
					2. The same problems we dealt with in the backend monolithic application
						1. Solution: Micro-Frontends architecture pattern
3. Micro-Frontends Architecture Pattern:
	1. We split the monolithic frontend application into multiple frontend modules or libraries that act as independent single-page applications
		1. This can be done by business capability or domain (just as we did with microservices)
	2. Each page in the webapp becomes a separate microfrontend
	3. We can have several microfrontends on the same page
	4. **Each microfrontend is completely decoupled from the other microfrontends**
	5. Each microfrontend needs to know how to load, mount, and unmount itself from the DOM in the browser
	6. Each microfrontend can be loaded in a web-browser as a standalone web-application for testing purposes
	7. Each microfrontend is owned by a separate frontend team with full-stack technical capabilities & domain knowledge to develop and maintain the microfrontend
	8. The micro-frontends are assembled together at runtime by a container web-application
		1. When user loads our site on their browser
	9. Role of the Container Application:
		1. To render common elements
			1. Page headers
			2. Page footers
		2. Take care of common functionality
			1. Authentication and shared libraries
		3. Tell each micro-frontend where/when to be rendered on the page
	10. Source of Confusion
		1. Micro-frontends is an architecture pattern - not a web-framework (or library)
			1. Many web-frameworks support this pattern
				1. We don't have to use any particular one to implement this pattern
		2. Micro-frontends are not reusable UI elements
			1. It is not a generic button, search bar, or other UI element that can be re-used in different places on the page
				1. It is a single-page web-application with very limited business functionality
			2. Different micro-frontends may re-use common UI elements (but the two concepts are un-related)
4. Real-Life Example of Micro-Frontends + Microservices:
	1. Online Learning Platform - With Micro-Frontends:
		1. When a user sends a request for Homepage, Web App Service sends back a container application to the user
		2. The container application handles the user authentication first and stores the Authentication token on the user's device
			1. User doesn't have to re-authenticate for every request or page reload
		3. After the authentication is complete, the container application renders the header and footer of learning platform
		4. Container application then calls the entry-points or the Course Discovery Micro-frontend and Course Recommendations Microfrontend
		5. The codes of each micro-frontend makes a request to the backend service to build the HTML with all the relevant data and renders itself on the page (or as container application told it to)
		6. When a user navigates to the User Profile page, it first triggers the unmounting of Course Discovery and Course Recommendation Frontends and the rendering of User Profile Microfrontend
			1. User Profile Microfrontend is maintained by the User profile team and is fetching data from its backend service
		7. Course enrollment page gets is Microfrontend from the enrollment service and is maintained by the enrollments team
		8. Every other part of the web-application follows the same pattern
5. Benefits:
	1. We replaced the complex monolithic codebase with a few small and manageable micro-frontends
		1. Each for a different micro-frontend
	2. Full-stack ownership of each micro-frontend
		1. Each team owns its domain and technical stack end-to-end
			1. If course enrollments team, course recommendations team, and course discovery team wants to deliver a new feature, they can do independently without waiting or depending on any other team
	3. Each micro-frontend is easier/faster to test in isolation
		1. Its scope is much smaller
	4. Each micro-frontend has its separate CI/CD pipeline
	5. Each micro-frontend team has its separate release schedule
6. Best-Practices
	1. Ensure that micro-frontends are loaded at runtime
		1. They are not expressed as compile or build time dependencies of the container application
			1. Or else, we have just separated the codebase logically but at runtime, we will have a monolithic frontend requiring complete redeployment for every new feature
		2. This best practice is very similar to the one we had on the backend where splitting a monolithic application into modules and libraries did not provide the same benefits as splitting into microservices
	2. Ensure that micro-frontends don't share state in the browser
		1. It is similar to different microservices sharing a database
			1. It is a bad approach
	3. Intercommunication through:
		1. Custom events
		2. Passing Callbacks
		3. Browser's address bar
7. Summary:
	1. Identified our system's technical and org bottlenecks: Monolithic frontend
	2. Learned about the Micro-frontends Architecture pattern
	3. Splits the web application into
		1. Independent single-page applications
		2. Maintained by separate teams
		3. micro-frontends are assembled by a container application at runtime (on the user's browser)
	4. Perfect for Microservices Architecture

### API Management for Microservices Architecture ###
1. What we will learn in the lecture:
	1. The problem (we are trying to solve) of managing APIs in Microservices Architecture
	2. The API Gateway Pattern (solution)
	3. Load Balancer vs API Gateway (common source of confusion)
2. The problem (we are trying to solve) of managing APIs in Microservices Architecture
	1. API Management Problem:
		1. Imagine we are a healthcare or fitness company providing digital services to clients in businesses like fitness centers, hospitals, and doctor's offices
		2. On the client side we have the following interacting with our platform:
			1. Smart watches
			2. Mobile phones 
			3. Other wearables
		3. Other company's servers, developers' computers, and healthcare professionals using our system
		4. Internally, we have dozens (or 100s) of microservices exposing different APIs specific to their functionality
			1. Microservices:
				1. Profiles Service (API1)
				2. Health Vitals Service (API2)
				3. Walking Tracker Service (API3)
				4. Subscription Service (API4)
				5. Notifications Service (API5)
				6. Health Risks Analyzer (API6)
		5. Problems:
			1. Tight coupling of API endpoints to client-side code:
				1. The different API endpoints exposed by microservices are hardcoded across many frontends and client SDKs
					1. Tightly couples the client side code with internal implementation of our system
				2. Example: 
					1. Suppose we break an existing microservice into two microservices (Health Vitals Service into Heart Rate Service and Blood Pressure Service)
						1. Each microservice exposes a new API with IDs and endpoints relevant to the microservice
							1. This will force us to refactor the client-side code in each type of device to use the new APIs
			2. Different types of API for different consumers (public/private/partner)
				1. Different microservices may expose their API to different customers
					1. We may expose public API endpoints externally to clients
					2. We expose private API endpoints to internal services
					3. We expose partner API endpoints only to partner businesses and developers
				2. Internally, we may do our best to follow specific API guidelines, it is not always possible to do it with external APIs (public APIs, partner APIs)
					1. In the same service, we may have to expose:
						1. One type of API for a partner company that only supports old API technology (SOAP + XML)
						2. Same type of API for other partner companies that support newer API technologies (REST + JSON, gRPC + ProtoBuf)
			3. Different API tiers based on subscription level
				1. We may have different versions of the same API for different tiers of clients with different capabilities based on their subscription level
					1. Free Trial Clients - Free Public API (limited and designed for free users)
					2. Premium Clients - Premium API (more capabilities)
					3. The jungle of APIs in microservices architecture can quickly become very hard to manage and reason about
			4. Traffic Control and Monitoring
				1. When loading a dashboard of daily workouts, particular users mobile app may have to make several API calls to different microservices
				2. Since calls are made directly to the microservices, monitoring and tracking them across the entire system is very hard
			5. Duplicated Effort Across Microservices:
				1. Authorization and rate limiting have to be implemented in each microservice
					1. Wastes a lot of time for each team that could instead focus on something else
3. The API Gateway Pattern
	1. To decouple client-side from internal architecture and make API management easier, we can use the API gateway pattern
	2. This pattern is useful for microservices architecture
		1. Used in many companies
	3. The pattern places a component called API Gateway Service at the entry to our system
		1. It is responsible for all the API management
		2. Scenario:
			1. API gateway routes requests for a given API endpoint to a relevant microservice that handles it
				1. In most cases, it can do much more than request routing
		3. Example:
			1. If we have three clients that need to interact with the same microservice to get some data
				1. The API technologies and data format for those clients are different
					1. Partner Company 1: SOAP + XML
					2. Partner Company 2: REST + JSON
					3. Partner Company 3: gRPC + ProtoBuf
				2. The API gateway transforms requests to one canonical API type and data formats that the microservice supports
				3. **Protocol Translation**: The API gateway can also make translation in reverse for the response back to the client
					1. Makes API definition and management much easier and cleaner for each microservice
						1. Each microservice can expose only GraphQL API
							1. One standard
							2. Utilize the same infrastructure
						2. They don't have to care about clients and their limitations
							1. They can all follow one standard and utilize the same infrastructure
				4. **Traffic management and Throttling**: The API gateway can perform traffic management and throttling
					1. Example: If we have a business partner who is trying to query data from our system at a very high rate, we can throttle it at the API gateway level, preventing it from putting too much load on the microservice that need to handle the requests
				5. **TLS Termination**: The microservices can delegate the authorization and TLS termination to the API gateway
					1. Microservices do not have to worry about it and can focus on the business logic implementation
				6. **Monitoring**: Since all the traffic from our frontends are going through the API gateway, we can easily monitor it
					1. It enables us to detect issues in particular APIs or analyze the behavior of clients in partner companies
				7. **Fanout**: Certain implementations of API gateway allow fanning out a given request to multiple services and aggregate the results before sending it back to the client
					1. Critical feature:
						1. Reasons:
							1. It **decouples the clients from our internal implementation**
								1. Example: Internally, we can refactor those services by either combining several microservices to one or splitting existing microservice into multiple microservices
									1. All those implementation details will remain transparent to the user
							2. **For Mobile devices and IoT**: Each network request on their end directly affects their battery life
4. Load Balancer vs API Gateway:
	1. Both route an incoming request from a client to a single destination
		1. The similaries end here
	2. Differences: Purpose
		1. Load Balancer:
			1. Balances traffic load on a group of servers
				1. The servers run identical copies of the same application
		2. API Gateway:
			1. With microservices, we typically have a load balancer in front of each microservice
				1. Each microservice is deployed as a group of identical copies of the microservices respectively
			2. API Gateway is a system's public facing interface
				1. It's role is used to route requests to services (not servers) based on different criteria
	3. Differences: Functionality
		1. Load Balancer:
			1. Features:
				1. It aims to be as simple as possible to reduce performance overhead
				2. Performs health checks on it's backend servers (to ensure it doesn't route requests to unresponsive servers)
				3. Offers different load balancing algorithms for different workloads
		2. API Gateway:
			1. Features:
				1. Throttling
				2. Monitoring
				3. API versioning & Management
				4. Protocol/Data format translation
5. Since the components have different purposes, they are usually used together in microservices architecture
6. Summary:
	1. Learned the problems of managing APIs in a Microservices Architecture
	2. API Gateway Pattern (Solution to those problems):
		1. We placed an API gateway service at the entry to our system which helps us route requests to microservices
		2. It provides us with many features:
			1. Throttling clients (that send us too many requests)
			2. Handling authorization and TLS termination
			3. Protocol and data translation
			4. Monitoring
			5. ...
	3. Load Balancer vs API Gateway:
		1. They serve different purposes and are used in microservices architecture

## Event-Driven Architecture ##
### Introduction to Event-Driven Architecture ###
1. What we will learn in this lecture:
	1. Motivation for Event-Driven Architecture (and why we need it)
	2. Fundamental concepts of Event-Driven Architecture
	3. Request-Response Model vs Event-Driven Model (to illustrate its benefits)
	4. Event-Driven Architecture - Real-life Example
2. Motivation for Event-Driven Architecture:
	1. Example: Video on Demand Subscription Service (designed using microservices architecture)
		1. After a user tried our service for free, they are ready to proceed to a paid subscription on our platform which gives them access to all our movies and many other advanced features
		2. Backend:
			1. Microservices participating in this transaction:
				1. Subscription Service
					1. Holds all the info about each subscriber
						1. Subscription level
						2. Expiration date
						3. ...
				2. Payment Service
					1. Given a credit card info, communicates with third party companies to bill a user
				3. Recommendations Service
					1. Constructs and maintains a unique profile for each paying customer
						1. To provide them with:
							1. Watch history
							2. Recommendations for future movies
								1. Based on:
									1. What they have watched in the past
									2. Their country
				4. For a user to be fully subscribed to our service, we must ensure that each one of those services receives and successfully processes the subscription request
	2. Ways to implement a user subscription:
		1. Approach 1:
			1. Steps:
				1. Send the request containing all the user's info to subscription service
				2. Subscription Service will update its own database and send a request to Payment Service (Payment Request)
				3. Payment Service will contact a third party credit card processing service
					1. Once it gets a confirmation, it will update its own database
				4. Payment Service then sends a request to Recommendation Service (Profile Creation Request)
				5. Once Recommendation Service successfully updates its database, it sends response to Payment Service
				6. Payment Service then sends response to Subscription Service
				7. Subscription Service will respond to the frontend (showing success to the user)
			2. Benefits:
				1. When a user receives a response, there is 100% guarantee that the subscription was successfull
					1. All three services have received and processed the request
			3. Downsides:
				1. Long chain of communication is holding the user for a very long time
					1. Poor user experience (even if everything goes smoothly)
						1. Worst case, the third party service the Payments Service talks to is facing performance issues, or if connection between payment service and recommendation service breaks and requires a retry, the entire transaction makes the user wait even longer
					2. We can also not cut corners and send confirmation to the user from Subscription Service before it gets response from the Payment Service
						1. If we do, and the payment service fails or never receives the request, the user will not be correctly billed
					3. If we make the Payment Service respond before the Recommendation Service Responds, we risk having an inconsistent state
						1. If Recommendation Service crashes right before or during the processing of the request
						2. User will not get any recommendations and personalization features as part of their subscription
					4. **The more microservices we have in the chain, the longer we have to hold the user to guarantee a consistent state**
						1. **The latency in many cases is too long to be acceptable**
			4. Solution: Orchestration Pattern
				1. Process:
					1. We add a single service orchestrating a complex business transaction involving multiple operations or services
						1. Orchestration may be combined with the API Gateway but we can assume a seprate service
					2. Steps:
						1. A request goes to the Orchestration Service
						2. The Orchestration Service broadcasts it in parallel to relevant services
							1. Parallel execution reduces the latency from: Sum of letencies of all services to latency of the slowest servcie in the transaction
							2. In some cases, the latency may be too high
								1. Consider a situation when the third party credit card processing service is having performance issues
									1. Other companies may be sending it too many concurrent requests
								2. Situation may not be in our control & can negatively impact our customers
							3. Orchestration service is now tightly coupled to the services that must be involved in the transaction
								1. If the API of one of the services changes or add another step to the subscription (another service), we need to update the Orchestration Service to call that service
							4. If we have a temporary issues with just one of the services in the transaction, all the subscription requests will have to denied losing us valuable customers
			5. Solution: Event-Driven Architecture
3. Fundamental Concepts of Event-Driven Architecture
	1. Main Concept in an Event-Driven Architecture: "Event"
		1. Event: Fact, Action, State Change (that happens in our system)
			1. It is always immutable
			2. It can be stored indefinitely
				1. Unlike a request which is ephemeral
			3. It can be consumed multiple times by different services
				1. Unline a request which can be consumed oned and by one server
	2. Three entities participate in the exchange of events in an event-driven architecture
		1. Producer: Produces events
		2. Message Broker: Stores and routes the events
		3. Consumer: Receives and processes those events
	3. Message Broker: Allows us to route a single event to as many consumers as we want
		1. It also adds a level of redundancy to our system
			1. If an event that is produced into the message broker it wont be lost
				1. We can always retrieve it from the message broker
4. Request-Response vs Event-Driven Model
	1. Synchronous vs Asynchronous
		1. Communication in the request-response model is synchronous
			1. When the sender sends a request, it must wait for response (even if it doesn't contain any useful information)
				1. If the response never arrives, this indicates a problem
		2. Communication in the event-driven model is asynchronous
			1. Publisher doesn't need to or expect to get any response from the consumer(s) of the events
			2. Delivery of the event to the consumer is outside of its control and responsibility
				1. Allows the producer to move on processing its next task instead of waiting for a response it doesn't need
	2. Inversion of Control
		1. In request/response model, when a sender sends a request to the receiver, the sender needs to be aware of the receiver & has to know exactly how to call its API
			1. If sender sends requests to multiple receivers, it needs to know about all of them and send requests to each one using their unique parameters
			2. Hense **sender depends on the receivers of the requests**
		2. In event-driven model, producer doesn't care and may not be aware of the consumers of the requests
			1. It **decouples the producer from the consumers**
	3. Loose Coupling
		1. It is one of the main qualities we desire in microservices architecture
			1. The reason why **event-driven architecture and microservices architecture go together with success**
5. Event-Driven Architecture - Real-Life Example
	1. Procedure:
		1. Place a message broker between each one of the microservices
			1. Subscription Service:
				1. Once Subscription Service receives a request from the user, it stores it in its own database
				2. Subscription Service emits an event to the message broker
				3. Subscription Service then sends a response to the user who doesn't need to wait for the rest of the transaction to complete
			2. Payments Service:
				1. Payments Service will consume the event, process the payment, and store the result in its own database and will emit a new event for the next service
					1. User is unaffacted even if this part took a very long time
			3. Recommendations Service:
				1. Recommendation service will consume the event, process it, and optionally produce another event to the notification service
				2. The notification service will consume its own event and send the user a confirmation email or a push notification to their mobile app
6. Summary:
	1. Motivation for Event-Driven Architecture
	2. Using the synchronous Request-Response model
		1. Our services may still be tightly coupled
		2. If a service is slow to respond (user is at risk)
	3. Fundamental concepts of event-driven architecture:	
		1. Event - representing a fact, action, or state-change
		2. Producer - emits events
		3. Message Broker - routes events to consumers
		4. Consumers - consume events
	4. Real-life example of using Event-Driven Architecture

### Use Cases and Patterns of Event-Driven Architecture ###
1. What we will learn in this lecture:
	1. Event-Drien Architecture Use Cases
		1. Event-driven architecture is not a silver bullet to solve every problem
	2. Request-Response Model Use-Cases
	3. Event Delivery Patterns
2. Event-Drien Architecture Use Cases
	1. Use-Case 1: **Fire and Forget**
		1. They are asynchronous by nature
		2. Sender does not expect any data in return immediately or not at all
		3. Example: When user sends a request to generate a report (that might take a few minutes of few hours to complete)
			1. Flow:
			
					User
					|
					Report Generation Request
					|
					v
					Web App Service
					|
					Generate Report
					|
					v
					Message Broker
					|
					Generate Report
					|
					v
					Report Service
					
			2. Flow 2:
				1. User leaving a review on a product they purchased
					1. User doesn't expect any data in response now or in the future
						1. They care about whether the review was accepted in the system or not
	2. Use-Case 2: **Reliable Delivery**
		1. Important in financial transactions where we cannot afford to lose messages in transit or need to guarantee certain delivery semantics
		2. Example: Ordering from an Online Store
		
				Customer
				|
				Product Order
				|
				v
				Web App Service
				|
				Product Order
				|
				v
				Message Broker
				|
				Product Order
				|
				v
				Payment Service
				Orders Service
				Delivery Service
				
			1. If we tell the user that they will receive the order, we must be absolutely keep our promise or send them an email explaining why that order was not fulfilled
				1. We must not lose the request in transit because some server crashed in the process
		3. Example 2: Money Transfer
			1. Customer -> Web App -> Message Broker -> Transfer Service -> Another Bank
				1. Action requires reliability
	3. Use Case 3: **Infinite Streams of Events**
		1. Location data from mobile devices or sensor data from IoT devices (vacuum cleaners, autonomous cars, ...)
			1. We have a continous and infinite stream of data coming into our system
				1. We need to analyze, aggregate, transform, and store the data in real-time
	4. Use Case 4: **Anomaly Detection/Pattern Recognition**
		1. Metrics from Servers:
			1. Each event can represent a fact
				1. Example: Current value of requests/second from each one of the servers
			2. Each data point in isolation is not that interesting or useful
				1. But when we put the events in a sequence, we gain insights
					1. If the requests/sec for a server increases, we need to scale our system out (add more servers), otherwise, our system will not be able to handle incoming traffic for much longer
					2. If requests/sec suddenly drops to zero, that indicates some hardware or software failure that we need to immediately investigate
	5. Use Case 5: **Broadcasting**
		1. When we have a service that has a state change wants to broadcast to other services interested in that event
			1. A perfect scenario for event-driven architecture
				1. Producer doesn't need to know about who is consuming the event and how it is used
				2. Example: User clicks on a digital Ad in a website
					1. Ad Service receives the request
					2. Ad Service emits the event to a message broker
					3. Message broker broadcasts the event to the following services:
						1. User Behavior Tracker
						2. Click Counter
						3. Advertiser Budget Limiter
					4. The producer and consumers are not unaware of who/who else is consuming respectively
	6. Use Case 7: Buffering
		1. Buffering messages to tolerate traffic spikes in our system
			1. We can tolerate a sudden spike of events from a service by placing a message broker and communicating asynchronously beteween services
				1. Example: Consider a situation where we have a social media company
					1. A global event has triggered a massive number of posts or comments on a particular event
						1. Solution: We can buffer those events in a message broker and deliver those events to the other services only as fast as the services can handle them
3. Request-Response Use Cases:
	1. Use Case 1: Immediate Response with Data Needed
		1. If a user requests a web-page containing all the products in a given category, we need to respond to this request synchronously and immediately
			1. Otherwise, the user will leave the online store
	2. Use Case 2: Simple Interaction
		1. We wont get any benefit if we use an event-driven model
			1. Configuring and running a distributed and cloud managed message broker comes with some complexity and cost
				1. It is not worth it for simple interactions
4. In Reality:
	1. A typical Microservices Architecture combines:
		1. Event-driven architecture
		2. Synchronous request-response model
	2. It's better to:
		1. Start with request-response model
		2. "Upgrade" the critical parts to the event-driven architecture when needed
5. Event Delivery Patterns:
	1. Pattern 1: Event Streaming:
		1. The message broker is used as a temporary or permanent storage for events
		2. The consumers have full access to the logs of those events even if they have been consumed by the same consumer or other consumers
		3. New consumers who join later also have access to those old events and can replay them from any point they want
		4. Use-Cases: 
			1. Use-Case 1: Reliable delivery
				1. The message-broker retains events either indefinitely or for a period of time which allows to recover those events and audit them if we need to
			2. Use-Case 2: Pattern/Anomaly Detection
				1. Consumer needs access to all events in a given window
	2. Pattern 2: Pub/Sub
		1. Consumers subscribe to a particular topic/queue/channel
		2. Consumers receive only new events after subscribing
			1. Subscribers don't have access to old events
			2. As soon as all the subscribers receives an event, the message broker will delete it from its queue (typically)
		3. If a new subscriber registers for events for a given topic, they will be notified only of new events
		4. Use-Cases:
			1. Use-Case 1: Message broker is a temporary storage/broadcasting mechanism
				1. After subscribers have consumed events, they are transformed and stored permanently in a database or passed to another service
			2. Use-Case 2: Fire and Forget
			3. Use-Case 3: Broadcasting
			4. Use-Case 4: Buffering
			5. Use-Case 5: Infinite Stream of Events
6. Summary:
	1. Common use cases for event-driven architecture:
		1. Fire and forget
		2. Reliable delivery
		3. Handling infinite stream of events
		4. Anomaly detection and pattern recognition
		5. Broadcasting
		6. Buffering
	2. Use cases that are not good fit for Event-Driven Architecture
		1. Need an immediate response containing data
		2. Simple interactions
			1. If it doesn't justify the cost and complexity of a message broker
	3. Event delivery patterns:
		1. Event Streaming
		2. Pub/Sub

### Message Delivery Semantics in Event-Driven Architecture ###
1. What we will learn in this lecture:
	1. Message delivery problem statement
	2. Event delivery problems in event-driven architecture
	3. At-most-once and at-least-once delivery semantics
	4. Exactly-once delivery semantics
		1. Misconceptions about it
		2. How we can achieve it in an event-driven and microservices architecture
2. Message delivery problem statement
	1. Example: Simple communication between two microservices
		1. Sending service sends a request to the receiving service
		2. Receiving service receives the request, processes it, and updates its database
		3. Receiving service sends a response to sending service
		4. In some cases, the sending service never receives a response
			1. May happen if
				1. Receiver never received a request in the first place
				2. Receiver crashed just before it successfully processed it
				3. Receiver crashed after it updated its database but response did not arrive at the sender
			2. From the sender's perspective, we are not sure which of the above cases actually happened
				1. What should we do?
					1. Should we send the request twice
						1. Receiver updates database twice
					2. Should we not resend the request and risk losing the data
3. Event Delivery Problems in Event-Driven Architecture
	1. Same problem with event delivery
		1. More complex than request-response model
			1. We have three entities
				1. Publisher
					1. May produce an event for the message broker
						1. The event might be lost in the network
						2. The message broker may receive the event and store it in its logs but acknowledgement to the producer is lost in the network
				2. Message Broker
					1. May send the message to the subscriber but subscriber may not receive it
					2. Subscriber received it but it crashed right before it processes it
					3. Subscriber could successfully process it but the acknowledgement is lost within the network
				3. Subscriber or Consumer
		2. Solution:
			1. Publisher, message broker, and subscriber need to agree on the delivery semantics of events ahead of time
	2. Delivery Semantics - Concepts:
		1. Universal
		2. Not specific to any message broker technology
		3. The specific configuraiton and guarantees vary between technologies
4. At-most-once and at-least-once delivery semantics
	1. At-most-once
		1. If we are okay to lose some data but want to avoid duplication of events
		2. We tell publisher, if it doesn't receive a response from the message broker, it should not resend the event
			1. Best case: If message broker received the event but acknowledgement got lost before the sender received it
				1. We wont lose any data
			2. Worst case: If the message broker did not receive the event or crashed before it stored the event
				1. We may lose the event entirely
		3. We also want the Subscriber to:
			1. Send acknowledgement first
			2. Process + Store in DB next
				1. If Consumer crashes and restarts after it processes the event, we are okay
					1. The event was already processed
				2. If Consumer crashes after the acknowledgement but before it processes the event, the subscriber will not receive the event again (effectively losing it)
		4. Use-Cases:
			1. If some data loss is "OK"
				1. We can extrapolate what we need from other events
					1. Example: We have a ride sharing service & each driver shares their location updates which we store as events in message broker, we can affort to lost some of their events
						1. If the location update is stored twice or processed twice, will not be a good use of our resources
			2. It provides us with least overhead/lowest latency
				1. For real-time processing of events such as logs or metrics from 100s of cloud servers, the delivery semantics will be the most cost effective
	2. At-Least-Once
		1. If a publisher doesn't receive an acknowledgement within a given period of time, it will resend the event to the message broker
			1. This guarantees that we will never lose the event
				1. But it may result in the same event being stored in the message broker more than once
		2. We configure the subscriber to:
			1. First Process + Store in DB
			2. Send Acknowledgemnt next
				1. If the subscriber receives the event but crashes before it processed and stored it, it will receive the same event again after it restarted
					1. If the subscriber received the event for the second time, it will process the event again and send the acknowledgement
					2. If the message broker receives an acknowledgement, it will no longer deliver it to the same subscriber
					3. If the subscriber processes the event but crashes before sending the acknowledgement, or if the acknowledgement is lost in the network, the message broker will redeliver the same event to the subscriber after it restarted.
						1. This may result in the subscriber processing the same event twice (more than once)
							1. But the event will never be lost
		3. Use-Cases:
			1. If data loss is unacceptable:
				1. Not delivering results is losing valuable data
			2. If data duplication is OK
				1. Acceptable
			3. Examples:
				1. Sending a push notification to a user to their mobile phone about their product being shipped
					1. If we push a notification twice in some cases, it is not a big deal
						1. However, we want to notify to the user at-least once
				2. When a user leaves a review for a product:
					1. If we already have logic in place that allows a user to leave a review for a product only once, that review will be overridden or ignored by our system
			4. Downside:
				1. Increased latency
					1. When a publisher sends an event to a message broker, it has to wait for a given period of time before it can resend the same event (milliseconds or seconds - depending on the configuration)
					2. The message broker has to wait and allow the subscriber some time to send back the acknowledgement before concluding that the subscriber crashed or acknowledgement was lost
					3. Due to this potential added latency, this delivery semantics is not a good choice for real-time or high throughput systems
	3. Exactly-Once
		1. Most desirable delivery semantics especially for use-cases that involve financial transactions
		2. Challenges:
			1. Most difficult to achieve
			2. Highest overhead / latency
		3. Not all message-broker technologies offer this semantics
			1. The once that do offer it, don't always offer what we'd expect
				1. Read the documentation carefully (especially if we are handling financially impacting data)
		4. We configure the publisher to:
			1. First Publisher needs to obtain an idempotency ID / a unique sequence number
				1. Some message-brokers can generate this for us internally while in other cases, we may have to use a separate service
			2. Idea:
				1. We need a unique ID that we can send to the broker along with the event
				2. If the publisher sends an event to the event-broker and never receives an acknowledgement, it follows the same procedure as the at-least once semantics
					1. It resends the event with the same ID
				3. The message broker is the one that provided this unique ID, it will check if an event with the same ID is already in the log
					1. If it is, the event will be ignored
					2. If it isn't, the event will be added to the log
						1. Hence, the exactly once delivery semantics is achieved on the producer side
							1. We never lose events
							2. We never end up with duplicate events
				4. On the subscriber side:
					1. Example: Finacial Event - Subscriber gets a billing event or money transfer
						1. When a subscriber receives it, it needs to process it first (may be do some validations and calculations)
							1. It then needs to put it in the database
								1. If event subscription includes a state update outside message broker
									1. Message-broker cannot guarantee anything more than at-least once delivery semantics (even if advertises that it supports exactly once delivery semantics)
										1. In this case, once the subscriber receives event event from message broker, it has to:
											1. Process + Store in DB first
											2. Send acknowledgement next
											3. Once Message broker receives an acknowledgement, it will not deliver the message again
										2. If subscriber crashes after processing the event but before it sends an acknowledgement, the message broker will continue waiting
											1. After the waiting period expires, it will assume that the event was not delivered
											2. The message broker will send the same event to the subscriber
												1. It will result in processing the same event twice
													1. Solution: Manually add an idempotency ID to the event record in the database
														1. If the same event is processed again, we can programmatically reject it if another event with the same idempotency id is already present in the database
															1. Message broker doesn't do this for us
															2. Solution: We can leverage the same idempotency ID that comes from the message broker

5. Summary:
	1. Unreliable event delivery problem
		1. What problems it will cause if we don't design our system upfront to handle it
	2. Event Delivery semantics for event-driven architecture
		1. At-Most-Once
			1. We might lose some data but data duplication can never happen
		2. At-Least-Once
			1. More complex
			2. More latency
			3. Guarantees that the event is not lost
			4. Processing the same event multiple times is possible
		3. Exactly-Once
			1. Most latency
			2. Most overhead (comparitively)
			3. Guarantees that each event is produced once to the message broker and is consumed and processed only once by the subscriber

### Message Broker Technologies - Delivery Guarantees ###
1. Apache Kafka:
	1. [Producer Delivery Semantics](https://docs.confluent.io/kafka/design/delivery-semantics.html#producer-delivery)
		1. At most once, At least once, Exactly once
	2. [Consumer Receipt Semantics](https://docs.confluent.io/kafka/design/delivery-semantics.html#consumer-receipt)
		1. At most once, At least once, Exactly once
	3. **Apache Kafka supports Exactly Once Delivery Semantics when transferring and processing data between Kafka topics**
2. Amazon SQS:
	1. [Amazon SQS Standard Queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/standard-queues.html) - At-least-once delivery
	2. [Exactly-once processing](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues-exactly-once-processing.html) - This applies only to publishing events into an SQS queue
3. Google Cloud Pub/Sub:
	1. [Exactly-once delivery](https://cloud.google.com/pubsub/docs/exactly-once-delivery)
4. Microsoft Azure:
	1. [Event Hubs output](https://learn.microsoft.com/en-us/azure/stream-analytics/event-hubs-output#exactly-once-delivery) - Exactly Once Delivery
	2. [Event Grid message delivery and retry](https://learn.microsoft.com/en-us/azure/event-grid/delivery-and-retry) - At Least Once Delivery

## Event-Driven Microservices - Design Patterns ##
### Saga Pattern ###
1. What we will learn in this lecture:
	1. Problem Statement
	2. Introdcution to the Saga Pattern
	3. Two ways to implement the Saga Pattern
		1. Using Microservices
		2. Event-Driven Architecture
2. Problem Statement
	1. Principle: Database Per Microservice
		1. Allowed us to decouple the following for all the microservices
			1. Teams
			2. Codebases
		2. The database is just an implementation detail of that microservices team
			1. It is not exposed externally to other microservices
				1. Allows each team to use the right database technology for its workload
				2. Iterate and make changes to it without having to communicate or coordinate those changes with anyone
		3. Everything in software architecture is a trade-off
			1. Decoupling introduces a new problem
				1. Monolithic Application with Single Database
					1. We had the ability to update multiple data sources atomically as part of a single transaction
						1. Transaction: To an external observer, a sequence of operations appears as a single operation
							1. The operations may involve:
								1. Multiple records in a table
								2. Multiple records within different tables
							2. ACID guarantees:
								1. Atomicity
								2. Consistency
								3. Isolation
								4. Durability
				2. Database Per Microservice:
					1. We no longer have one DB to perform ACID transactions
						1. Each operation in the workflow is performed by a separate microservice
							1. Each microservice is aware only about its part of the workflow
					2. Solution: Saga Pattern
						1. It helps us perform a distributed transaction that spans multiple microservices and databases
3. Introduction to the Saga Pattern
	1. Procedure:
		1. In this pattern, we perform the individual operations that are part of the whole transaction as a sequence of local transactions in each database
		2. Each successful operation triggers the next operation in the sequence
		3. If an operation fails, the SAGA pattern rolls back the previous operation(s) by applying compensating operations that have the opposite effect from the original operations
4. Two was to implement the Saga Pattern
	1. Workflow Orchestration
		1. Stateful management service that manages the entire transaction
		2. Functions:
			1. Orchestrate the workflow (transaction in the correct order)
			2. Apply compensating operations (in the opposite order if things go wrong)
		3. Example:
			1. Vacation Booking Service
				1. Offers a vacation package to customers
					1. Vacation package includes:
						1. A roundtrip flight to and from a vacation destination
						2. A hotel reservation
						3. A car rental for the given dates
				2. Transaction Steps:
					1. Payment received from the customer
					2. Flight to destination
					3. Flight from destination
					4. Hotel room reservation
					5. Car rental reservation
				3. We must have all the components of the vacation booked and paid for (it makes the transaction a success)
					1. If any of the parts fails, the entire transaction is considered a failure and is aborted
				4. Implementation of SAGA pattern:
					1. Microservices:
						1. Payments Service
						2. Flight Reservation Service
						3. Hotel Booking Service
						4. Car Rental Service
						5. Orders Service
						6. Workflow Orchestration Service
							1. Defining workflow order: (operations within the workflow are referred to as activities)
								1. Bill Customer (secure payment first)
								2. Reserve Flights (to and from the vacation destination given the seat preferences, the user provided us with)
								3. Book Hotel
								4. Reserve Car Rental (with car rental company for given dates)
								5. Insert Order (insert order entry with all the details about the booking)
							2. Add compensating operations for each activity in case we want to undo it
								1. Credit Customer (account/credit card)
								2. Cancel both flights
								3. Cancel hotel booking
								4. Cancel car reservation
								5. Update Order to "Cancelled"
									1. We need to define compensating operations to it in case we want to add more operations to this flow sometimes in the future (?)
							3. Calling the APIs of the corresponding microservices:
								1. Payments Service: Bill User
								2. Flights Reservation: Reserve Flights
								3. Hotel Booking: Reserver Room
								4. Car Rental: Reserver Car
								5. Orders Service: Insert Order
							4. Calling the APIs for compensating operations of the microservices
					2. Scenario: User wants to book a vacation with us
						1. User makes a request to web-app service
						2. Web-app shows the user the available options and prompt them to provide their preferred dates and other details
						3. When user submits the vacation booking request, the request will go through the API gateway to the workflow orchestration service
						4. The service will initiate the workflow step by step
						5. If everything goes smoothly, the:
							1. User gets billed
							2. Flights get booked
							3. Hotel room gets reserved
							4. Car rental at the vacation destination is arranged
							5. Order service gets updated
							6. Orchestration service returns a confirmation to the user
						6. If anything goes wrong, the entire transaction needs to be aborted and the user gets an error.
							1. Example: If Car rental service runs out of cars for the given date
								1. User already got billed, flights and hotel were already booked
								2. Workflow orchestration service will apply compensating operations calling the Hotel Booking service and Flights Reservation service to cancel the reservations
									1. It will also credit the user's credit card with the full amount
									2. It will send an error to the user explaining what went wrong
	2. Event-Driven Model
		1. We remove the Workflow Orchestration Service and deligate the management of the workflow to the microservices themselves
		2. The communication between the microservices is done asynchronously through events published to a message broker
		3. To compensate for the removal of the Workflow Orchestration Service, each microservice needs to know its role in the workflow
			1. It needs to know where to send an event when the operation is successful and where to send an event if it fails and it needs to trigger a compensating operation for the previous service in the sequence
		4. Example: Booking Service
			1. When a user places an order request for a vacation, the request will go straight to the payment service
			2. The payment service will respond to the user immediately (since it is asynchronous)
			3. The payment service will initiate the sequence by billing the user and sending a corresponding event to the message broker
			4. The Flight Reservation service will pick up the event and make a reservation
			5. Upon success, Flight Reservation service will emit another event to a topic to which the Hotel Booking service is subscribed
			6. Assuming all the operations are successful, the entire chain of events will eventually lead to Order Service getting the event that all the reservations are completed
			7. Order Service will update its database
		5. The response to the user needs to be asynchronous (because we used asynchronous event-driven architecture)
			1. Publish another event to another microservice called Notifications Service
				1. The Notification Service will notify the user about the outcome of the workflow through an email or push notification
		6. If an operation fails (we need to rollback the transaction)
			1. If Car Rental service could not make the booking
			2. Car Rental service will publish an event to another topic indicating a failure in the car reservation
			3. Hotel Booking service which is subscribed to the topic will pick up the event and it undoes the operation by cancelling the hotel reservation
			4. Hotel Booking service will publish an event to another topic to which the Flight Reservation service is subscribed to
			5. Flight Reservation service will cancel the flights and publish another event for the Payments Service to pick up
			6. Payments Service will credit the user and emit another event to a topic the notification service is subscribed
				1. The event indicates that the entire transaction is a failure
			7. Notification Service will pick up the event and notify to the user with all the details and the next steps that they need to take
5. Summary:
	1. Problem: Loss of ACID Transaction guarantees (when migrating a monolithic application from a single database to microservices architecture)
	2. Solution: Saga Pattern (breaks the transaction into a sequence of operations that each microservice will perform upon success and a sequence of compensating operations performed in reverse after a failure)
	3. Two ways to implement the Saga Pattern:
		1. Stateful Workflow Orchestration service to orchestrate the transaction
		2. Event-Driven Architecture where each microservice is respopnsible for triggering the next operation in the sequence or triggering a compensating operation in the previous microservice in case of a failure
						
### CQRS Pattern ###
1. What we will learn in this lecture
	1. Introduction to CQRS
	2. CQRS use cases or Microservices Architecture (benefits large scale systems designed using microservices architecture)
	3. CQRS real-life example
2. Introduction to CQRS
	1. CQRS: Command and Query Responsibility Segregation
		1. We can group the possible operations on the data into two types
			1. Command - It is an action we perform that results in data change in our system
				1. Actions:
					1. Insertion: New records
						1. Example: Adding a user
					2. Update: to existing records
						1. Example: Editing a review / Changing a user's phone number
					3. Deletion: of records
						1. Example: Deleting a user's comment (on a social media platform)
			2. Query - It only reads data from a database (but does not change it)
				1. System can return the data
					1. As-is
					2. Transformed
						1. Sorted
						2. Aggregated
				2. Data inside the database will never change due to the query
					1. Example: Show all products, filtered by category, sorted alphabetically
		2. When we use CQRS in microservices, we separate the code and storage of the command part of our system from the query part of our system
			1. Command (Inserts, Updates, Deletions) go to Command database through the Command Service
			2. Query (Read-Only operations) go to Query Database through the Query Service
				1. The query database contains a copy of the data that is in the command database
		3. To keep the command and query databases in sync, we use the event-driven architecture
			1. Add a message broker between the command-service and the query-service
				1. Everytime the command service receives a request that changes the data within its database, it publishes an event to the message broker that the query service can consume
				2. When the query service receives the event, it updates its own database with the new data
3. CQRS Use-Cases for Microservices Architecture:
	1. Use-Case 1: Separation of Concerns (between the command and query workloads in terms of business logic and performance)
		1. Separation of Concerns - Benefits
			1. Goes well with **Single Responsibility Principle (SRP)** for microservices
				1. Allows us to have the complexity in the Command service
					1. Managing permissions
					2. Input validation
					3. Other Business logic
				2. Keeps the Query service:
					1. Clean
					2. Simple
					3. Focused on the best way to present the data to the user
				3. Allows us to evolve them independently
					1. Using an optimal data model & programming language for the workload
				4. If only one part is updated (command side with new business or validation logic), the query side doesn't have to be retested or re-deployed (since it did not change)
			2. **High Performance**
				1. Since all command operations that involve changes go to the command database, we can use the most **optimal structure**, **schema**, and **database technology** for write operations
				2. Since all the queries go to the query database, we can organize the data to make the queries very efficient (for read operations)
					1. We can pick optimal datbase technology and configuration for read-intensive workloads
						1. Different from the ones used in write intensive workloads
				3. **We can optimize our system for both types of operations**
					1. Otherwise impossible to do if we have a single database for both command and query operations
			3. **Higher Scalability**
				1. We can adjust the number of instances for each microservice depending on the traffic
					1. Since we have distributed databases in this case, we can adjust the number of instances for each database depending on the rate of operations we get of each type
	2. Use-Case 2: Joining data from Different Sources (loss of the ability to join data from different sources)
		1. Single Database - We could perform join operations between multiple tables
		2. Multiple databases (database per microservice) - We cannot perform join operatations on multiple tables from different databases
			1. Solution 1: To join data
				1. We need to make APIs calls to each microservice
				2. Each microserive will get the relevant data from its own database and return it to the caller
				3. We parse and format the data from both the microservices
				4. Join both data programmatically into one view
					1. Problems: The programmatic join operation can be:
						1. Difficult
						2. Error prone
						3. Very slow
					2. The overhead is unacceptable if we are planning to show the data to the user
						1. In browser or mobile app
			2. Solution 2: CQRS pattern
				1. A new Query Service - with read optimized database
					1. The microservice will receive only query requests for the specific data we are tying to fetch to the user
					2. Inside the database, we will **store a joined view of all the data from all the required microservices formatted in a way that is optimal for reading or querying**
					3. For creation or updation of the view, we are going to add a message broker where the microservices can publish events whenever they change their data
						1. When data changes in a microservice, it will publish an event in the message broker
						2. The query service will pick up the event and update its joined view with the new data
					4. All the queries that need data from multiple microservices will go just to the Query Service
						1. The query servcie will return the data with very little formatting or filtering
							1. Performance gain for the user (or any other service that calls the API of the Query Service) can be substantial
				2. Caveat: We can only guarantee eventual consistency between the write and read operations
					1. In the time gap between data change in the command database and update in the query database, certain read operations will see the old data
4. CQRS Real-Life Example:
	1. Crowdsourced Business Reviews Service (like Yelp) (Restaurants, Bakeries, Car dealerships, Hair Salons, ...)
		1. A user who dines at a Sushi restaurant can use the app to leave a review and rating describing their experience at the business
		2. Based on the user's reviews, anyone can open our app and search for a Sushi restaurant in a given area
		3. System will return a list of restaurants sorted by the number of reviews, average rating, and relevance to the keywords the user typed in their search
		4. Assuming decomposition by domain we have the following microservices
			1. Users Service
			2. Restaurants Service
			3. Reviews Service
		5. Problems:
			1. Command side: Strict Business Rules as to who can add or update a business info
				1. We need to ensure that only verified owners of a business can update website, address, phone number, and other details
				2. When a user visits a business and wants to leave a review, we can have a lot of validation and business logic in the review service
					1. Authenticating user to ensure he is not a bot leaving a fake review
					2. Ensuring that the user has not left a review recently and if they did, we need to prompt them to update the existing review instead of leaving a new review
					3. Validating that the review text and star rating are valid inputs
				3. We have very infrequent updates to the business information (from a performance perspective)
				4. We have very frequent insert operations to the Reviews Service (daily)
					1. Review service needs database schema and technology optimized for write operations
			2. Query side: When a user searches for a business such as a sushi restaurant or a weekend bakery, we need to join data from both Restaurants (Business) Service and Reviews Service
				1. We will have to return all the businesses in the system that match the search query
				2. We need to request all the ratings for each business
					1. So that we can calculate and sort all those businesses accordingly
				3. The entire operation is extremely slow and inefficient
					1. Solution: CQRS pattern
				4. CQRS Solution:
					1. Introduce another service called Business Search Service
					2. Business Search Service will have an optional read-optimized database with a text-search engine specifically designed for text queries
					3. Any operation to add a new business or update an existing business in the business service will be published as an event to the business search service
					4. Business Search Service will index its name, description and metadata and place it inside its database
					5. Anytime a review is submitted and approved by the Review Service, it will be published as an event to a corresponding topic in the message broker
					6. Business Search Service will join the review with corresponding business and re-calculate its new average rating
						1. Any search request will go through the query part of our system to the Business Search Service
						2. The service is free from any authentication, validation, or any complex business logic
						3. It just parses, formats request, and pass it to the text database
						4. Once it gets the result, it will return a list of all businesses sorted by the relevance to the search query and rating (based on a predefined formula)
5. Summary:
	1. CQRS: Command and Query Responsibility Segregation
		1. It combines microservices and event-driven architecture
		2. Benefits:
			1. Sepration of Concerns
			2. Higher Performance for read and write operations
			3. Higher Scalability
			4. Solves the problem of joining data from multiple microservices
				1. Otherwise, it will be very hard to achieve in an efficient and performant way 
	2. Demonstrated the use of CQRS in a real-life example

### Event Sourcing Pattern ###
1. Problem Statement:
	1. Typical application data handling
		1. Generally, the data the application stores in the database reflects the current state of our business
		2. Any modification to the data reflects the new state which overrides the previous state
		3. To find its previous state after it is overridden, we can find its backup
		4. Unless something goes wrong, we don't care about previous state or states of our data
			1. We only care about what we have riht now
		5. The interactions we have with the data are usually CRUD operations
			1. Create
			2. Read
			3. Update
			4. Delete
				1. That is all we need for most use-cases
		6. Example:
			1. Online Store
				1. For each product, we store info such as name, description, price, links to images
				2. At some point, if the owner of the product updates the product's price or description, the user doesn't care
					1. User only cares about the current price and description
						1. History of the changes don't have any value
				3. In certain situations we need to know:
					1. The current state
					2. Every previous state
					3. Example: Online Bank
						1. We need to give a client their current balance and the transaction history
							1. If no data on withdrawals, deposits, fees or credits
								1. Not acceptable
						2. The reason is, the way the balance was calculated was important
							1. For auditing
							2. For potential corrections
					4. Example: Merchant Inventory
						1. Merchant that sells products in an online store
							1. If we just have at any given moment is the current state of our inventory of our products in the warehouse
								1. If we log into the system and see that there are 200 items in the inventory
								2. If we log into the system and see that we have only 100 items
									1. Did we made 100 items in sales?
									2. Did we sell all 200 items and get 100 returns?
										1. It is not that great
									3. Did we have one time bulk purchase of 100 items?
										1. It is not enough to have the current state
						2. Solution: Event-Sourcing Pattern
2. Event-Sourcing Pattern
	1. Instead of storing the current state, we only have events
	2. Each event describes the following about an entity in the system
		1. Change
		2. Fact
	3. Events are immutable (once we get an event into the system, we cannot change it)
		1. The only thing we can do is to append new events to the end of the log
	4. To find the current state on an entity, we simply apply or replay all events that happened to that entity
		1. It is version control for data
			1. Each event represents only the delta (change) from the previous state
	5. Example: Bank Account
		1. Instead of maintaining and updating current balance, we store only the transactions that move money in our out of the account
			1. Example list of events:
				1. Deposit: $100
				2. Debit: $10
				3. Credit: $5
		2. We replay the transactions from the day the account was opened, we can get to the most upto date current balance
	6. Benefits:
		1. We have the complete history of how we got to that balance
			1. We can report
			2. We can audit
		2. If we have duplicate transactions (may have happened by accident), we can recover from it
		3. We can detect suspicous patters that may indicate fordulant activity, the client was not aware of
		4. We can provide insights
			1. Better spending habbits
			2. Recommend another product such as
				1. Savings account
				2. Credit card
3. Event Sourcing - Where to Store Events
	1. Option 1: Store each event as a separate record in a database
		1. Example: Online Store
			1. Each order is stored in an orders table:
				1. Order ID: 10001
				2. State: PROCESSING
				3. Timestamp: Jan 14 12:08 PM
			2. Each time the order's status changes, we append a new row with the same order ID, new state and timestamp
				1. State 2:
					1. Order ID: 10001
					2. State: PAYMENT_COMPLETED
					3. Timestamp: Jan 14 12:10 PM
				2. State 3:
					1. Order ID: 10001
					2. State: SHIPPED
					3. Timestamp: Jan 15 8:03 AM
			3. We can see the entire history of each order transitioning from one state to another state over time
		2. Advantage:
			1. Ability to perform queries and analytics over an entire datasets
				1. We can track the progression of one order
				2. We can also track and analyse the progression of multiple orders at once and get certain insights
					1. Example: 
						1. We can find out that on a particular date we got a lot of new orders which may be correlated with a sale
						2. We can find out on a particular day that we had a lot of delivery problems
	2. Option 2: Store events in a message broker
		1. Instead of storing the events in a private database that belongs to a service, we can publish them for anyone to consume
			1. Message brokers are particularly:
				1. Optimized for handling a lot of events
				2. Make it easy to maintain the order between different events at the same entity
		2. Challenges:
			1. Performing complex qeuries on streams of events in a message broker is a bit harder and less intuitive
4. Another benefit:
	1. High Write Performance
		1. Without event-sourcing, if we have write intensive workload, we get high contention over the same entity in a database
			1. Results in poor performance
				1. Example: Online Store
					1. Inventory table that keeps track of inventory of a product
						1. If we have many updates to the same table (or worse to the same product), then all the updates will contend with each other and slow down each other as well as all readers of the table
						2. If we move to event-sourcing, then each purchase or return becomes an append only event
							1. It doesn't require any database locking and is a lot more efficient
								1. Race condition is okay because each append is an independent atomic operation
5. Efficient ways to use to read and reconstruct the most upto date state of an entity based on events
	1. Replaying all the transactions in someone's bank account everytime we want to show the client their balance is not very efficient
		1. **Optimization 1**: Strategies:
			1. Snapshots: At certain points of the events log
				1. Example: A snapshot of account balance for each user once a month
					1. We still have all the history for all the transactions since the beginning of time (if user wants to access it)
					2. A user can get the current account balance by only replaying the transactions from the last snapshot
						1. Instead of from the time the account was opened 
		2. **Optimization 2**: 
			1. CQRS Pattern
				1. We can separate the part that appends events to our system and stores them, from the query part that stores the current state in a read-optimized database
					1. Read-only database can be an in-memory database which makes reads even faster
				2. Everytime a new event comes in, if we store those events in a message broker, then the query service can subscribe to the same topic or channel and pull the data straight from it
					1. Command side doesn't need any database (we can remove the database)
		3. **The combination (Event Sourcing + CQRS) is very popular**
			1. Reasons: We get the best of both worlds
				1. We get **history** and **auditing**
				2. We get **fast** and **efficient** **writes**
				3. We get **fast** and **efficient** **reads**
		4. Drawbacks:
			1. We get only eventual consistency
				1. May or may not be good enough depending on the use-case
6. Summary:
	1. Learned Event Sourcing Architecture Pattern:
		1. Instead of storing/updating only current state,
		2. We store only changes/facts (about the entities) using events
	2. Two ways to store events (each approach comes with its advantages or disadvantages):
		1. Database
		2. Message Broker
	3. Side Benefits:
		1. Higher write performance (for write-intensive workloads)
	4. Powerful combination of Event Sourcing and CQRS which allows us to enjoy the benefits of:
		1. Auditing
		2. Performant writes
		3. Efficient reads

## Testing Microservices and Event-Driven Architecture ##
### Testing Pyramid for Microservices - Introduction and Challenges ###
1. Before deploying a system to production, and taking user traffic, we need to gain confidence through automated tests
2. What we will learn in the lecture:
	1. Recap of the testing pyramid for monolithic applications
	2. How to apply the testing pyramid to Microservices Architecture
	3. Challenges of testing Microservices and Event-Driven Architectre
3. Recap of the testing pyramid for monolithic applications
	1. When we setup tests for a single application, we could group those tests into three categories - The testing pyramid
		1. Unit Tests (bottom of the pyramid)
			1. Each unit test tests a small logical unit (class, module) in isolation
			2. They are cheapest to maintain because they are:
				1. Small
				2. Easy to write
				3. Fast to execute
			3. We have to write the maximum number of these tests (because they are cheap as compared to other tests)
			4. Problem: These tests give us the least confidence about our overall system
				1. They only test each unit in isolation
					1. Once we run the the application, we have no idea whether all those units will work together or not
		2. Integration Tests (middle slice of the pyramid)
			1. The tests verify the different units and systems we integrate with, such as a database or message broker actually work together
				1. These tests are bigger and slower
					1. Hence, we need to have fewer of them than unit tests
			2. Advantage:
				1. After running those tests, we have more confidence in our system
		3. Functional / End-to-End Tests (top of the pyramid)
			1. These tests run our entire system (UI, entire application, database)
			2. They verify that it works as intended from an end-user perspective
				1. Each test should test a particular user journey or business requirement and ensure that it matches the specification we set for our application
			3. Problems:
				1. Heaviest
				2. Most complex to setup
				3. Slowest to run
			4. We have the least number of them compared to the other tests
			5. These tests give us the highest degree of confidence that our system will work as intended in production
4. How to apply the testing pyramid to Microservices Architecture
	1. Microservices communicate with each other through a network or a message broker & each microservice has its own database
	2. Procedure:
		1. Each microservice team should follow the exact same testing pyramid (unit tests, integration tests, functional tests) for its own microservice and database
		2. We then treat each microservice as a small unit that is part of the larger system and we put it in the largest testing pyramid
			1. Since testing each microservice in isolation is essential but not enough
		3. Microservices Integration To increase the confidence that all the microservices can talk to each other at runtime, and work correctly together, we need to add another layer of integration tests
			1. The integration tests verify that every pair of microservices can talk to each other using the agreen upon API while mocking the rest of our system
		4. System-Level End-to-End Tests: The tests, in theory, should run all microservices, databases, message-brokers, frontends in test environment, and:
			1. Verify that all the individual components work together as expected
5. Challenges of testing Microservices and Event-Driven Architecture
	1. Challenge 1 - End-to-End Tests
		1. End-to-Tests provide us with the highest level of confidence, they are extremely hard to:
			1. Setup
			2. Maintain
		2. No clarity about ownership: It is not clear what team should own the environment
		3. One team may block everyone: If one of the microservices teams breaks the build even for a day, the entire test pipeline can be broken
			1. This can result in all the teams being blocked an unable to make any releases to production
		4. Low confidence (ignoring failed tests)
			1. Developers may ignore end-to-end tests and release the microservices anyway
				1. Makes the tests a liability with no benefit
		5. Very costly
			1. To run in a duplicate environment with the production environment
				1. Even if its scale is much smaller
		6. Companies either:
			1. Invest too much [effort in building and maintaining those few tests]
			2. Other companies don't invest at all
	2. Challenge 2: Integration Tests
		1. Challenges:
			1. Difficult to run
			2. Tightly couples teams to each other
				1. When a team that owns microservice A (API Consumer) that consumes the API of microservice B (API Producer) wants to run integration tests, it needs to build, configure and run both microservice
					1. Team A knows how to build and run Microservice A, it may not be clear to them how to setup microservice B
					2. It is much more difficult if microservice B has other dependencies like a database or another service that needs to be run or mocked
					3. Team that owns microservice B also has a problem
						1. It may have multiple microservices that consume its API
							1. To ensure that the changes they make in their API did not break the API consumers, they need to build, configure, and run all the consumers to execute their tests
				2. This will get quickly out of hand and slow down development (of the organization)
	3. Challenge 3: Event-Driven Microservices Integration Tests
		1. Microservices produce events to a message broker.
			1. It usually doesn't know, which other microservices consume those events
				1. The decoupling is a benefit that we wanted from an event-driven architecture
				2. Challenge: We cannot run integration tests with such microservices
		2. Microservices consume events produced by other microservices
			1. We need to run other microservices and a message broker just to test that: 
				1. Our microservice is able to consume those events
				2. The format of those events did not change without our knowledge
6. Summary:
	1. Revisited the testing pyramid in a monolithic architecture
	2. Apply the testing pyramid to microservices
	3. Challenges to testing microservices
		1. High _costs_ and _complexity_ of **end-to-end tests**
		2. _Tight_ _coupling_ [between teams] for running **integration tests**
		3. _Complexity_ and _overhead_ of testing **event-driven microservices**

### Contract Tests and Production Testing ###
1. Challenges of running end-to-end tests with microservices
	1. Forces companies to invest disproportionally high efforts into them or abandom those efforts all together
2. Challenges with microservices integration tests
	1. Complexity and tight coupling between teams
3. What we will learn in this lecture:
	1. Integration Tests using Lightweight Mocks
		1. Instead of running entire microservices
	2. Contract Tests for Synchronous Communication
	3. Contract Tests for Asynchronous Communication 
	4. Production Testing using Blue/Green Deployment and Canary Testing
4. Integration Tests using Mocks:
	1. Consider a team that owns microservice A that consumes the API of microservice B
		1. Normal procedure:
			1. The team wants to run integration tests that validates the triggering of functionalities with a set of parameters results in microservice A sending request to microservice B
			2. We need to build, configure, and run microservice B with all its dependencies (expensive and complex)
				1. Solution: 
					1. Mock the API layer of microservice B which we integrate with
						1. We set the mock to send hard-coded response if it receives the expected request
					2. Microservice B can run a set of mock consumers (which mock consumers of microservice B) instead of running real microservices
						1. We can write tests that make the mock consumers send us requests and test that our microservice returns the expected response
					3. Advantages:
						1. Reduces coupling between different teams
							1. If one team breaks its build, the other teams continue running its tests
						2. Reduces the overhead of running real instances of the other microservices
					4. Issues:
						1. The contract between the:
							1. API consumer
							2. API provider
								1. Can get out of sync without the teams ever detecting it
							3. Example: API provider team may update its API, update its mock consumers tests and all the tests will pass successfully
								1. The communication about the changes may be lost or misunderstood by microservice A which consumes the API
									1. They don't make any changes at all or they make incorrect changes
										1. Their tests also pass
								2. Once the two microservices are released to production, they won't be able to communicate with each other
									1. It will cause an outage
						2. Solution:
							1. Contract Tests
5. Contract Tests for Synchronous Communication
	1. Contract tests work by using a dedicated tool to keep the mock API provider and mock API consumer in sync through a shared contract
		1. When an API consumer team runs their tests, they are run against the mock API provider
			1. They test that their microservice sends the right requests and receives the right responses as expected
			2. Additionally, each request it sends to the mock API provider is recorded along with the expected response into a contract file
			3. The contract file is then shared with the team that owns the microservice B which provides the API
			4. Using the contract, the team that owns microservice B, replays all the recorded requests to their real microservice B, and verifies that the responses it gets are the same as recorded in the contract
			5. If microservice B has many consumers, it will take all their recorded contracts, construct their mock consumers and run each one against their actual API implementation
		2. Advantages:
			1. Each team runs their own integration tests [without dealing with the complexities of building, configuring, and running other microservices]
			2. Contract test tools keep the contract between microservices in sync: Guarantees that each team tests against the most upto date and correct contracts shared between microservices
6. Contract Tests for Asynchronous Communication
	1. For event-driven microservices
		1. Example: E-Commerce
			1. When a user sends a request to purchase a product, the request goes to the order service
			2. Order service publishes an event to the payment service, and responds to the user 
			3. Payment service consumes the event, bills the user, and passes it as another event to the shipping service
		2. Integration tests: Between payments service and shipping service
			1. Contract between services is the event format that contains info about the 
				1. User
				2. Product
				3. Quantity
				4. etc.
			2. Each team constructs a light-weight mock of the message broker
				1. When shipping service team tests its ownability to consume and parse the payment service event, the event is also recorded in a contract file
				2. The team then shares the contract file with the team that publishes the event
					1. Payment service
				3. When the team that owns the service that produces the event wants to run integration tests between their service and event consumer, they will trigger the function in their service that is supposed to produce that event
				4. Contract test will verify that the event format and content match the one that was recorded in the contract
					1. If it matches, the contract between the microservices is in sync
						1. We can confidently release them in production
	2. Advantages:
		1. Contract tests simplify running integration tests for microservices that communicate synchronously and asynchronously
		2. Contract tests give high confidence that when we deploy those microservices in production, they can communicate with each other as we would expect
7. Production Testing Using Blue/Green Deployment and Canary Testing
	1. Contract tests are not a substitute for end-to-end tests
	2. If setting up end-to-end tests is not feasible for our company, alternative is testing in production
		1. Solution: Blue-Green Deployment + Canary Testing
			1. Gradual release with blue-green deployment with canary testing
				1. Blue-green deployment - It is a safe way to release a new microservice version to production using two identical production environments without any downtime during the release
					1. Blue environment - Set of servers or containers that run our old version
					2. Green environment - Set of servers or containers that run our new version that we want to release
						1. Once we deploy the newer version to the green environment, no real user traffic is going to it
							1. An opportunity to run automated/manual tests against those servers without impacting real users
							2. Canary Testing:
								1. After running the tests successfully, we can shift a portion of production traffic to green environment
								2. Monitor the new version for performance and functional issues
								3. If there are issues, we redirect the traffic back from the green environment to the blue environment with minimal impact on users
								4. If no issues are detected, we direct all the production traffic from the blue environment to the green environment
								5. Gradually de-commission the blue environment (since it is no longer needed)
8. Alternative to Integration Tests: We have an alternative for integration tests for microservices that communicate directly with each other and through a message broker in the form of contract tests
9. Alternative to End-to-End Tests: Production Tests using blue-green deployment & canary testing
10. Caveat: The alternatives must be setup only if setting up real microservices in development stage for testing purposes is **too complex or expensive**
11. Summary:
	1. Address the complexity of running integration tests/end-to-end tests in microservices architecture
	2. Using mocks for integration tests
		1. Each team mocks the other microservices it depends on
		2. Advantages: Simplifies integration tests
		3. Disadvantages: Not enough to enforce API contracts between microservices
	3. Contract Tests:
		1. Solves the problem by keeping the contract between API consumers and API producers in sync
		2. We extended the concept of contract testing to event-driven microservices
			1. Microservices communicate with other through a message queue or message broker
	4. Alternative to end-to-end testing: Production Testing using:
		1. Blue-Green Deployment
		2. Canary Testing

### Contract Tests Solutions ###
1. Contract Testing Solutions:
	1. [Pact](https://docs.pact.io/) - Open-source contract testing tool that allows API consumers and API producers to define and verify their API contracts
		1. Pact supports for many programming langauges and frameworks
	2. [Spring Cloud Contract](https://spring.io/projects/spring-cloud-contract) - Open-source umbrella project for contract testing solutions
		1. Contains [Spring Cloud Contract Verifier](https://cloud.spring.io/spring-cloud-contract/2.1.x/multi/multi__spring_cloud_contract_verifier_introduction.html) - It enables Consumer Driven Contract (CDC) development of JVM-based applications using Groovy DSL or YAML
	3. [PactFlow](https://pactflow.io/) - A commercial offering that manages the lifecycle of contracts defined by contract testing tools (like Pact, Spring Contract, etc) & provides a workflow to manage them in CI/CD pipelines
		1. Supports all JVM langauges as well as:
			1. Ruby
			2. Golang
			3. NodeJS/ Javascript
			4. Python
			5. Objective-C/Swift
			6. .NET
			7. PHP
			8. C++
			9. Rust

## Observability in Microservices Architecture ##
### Introduction to the Three Pillars of Observability in Microservices ###
1. No matter how well we test our code, bugs, failures, and performance issues will always happen
	1. Such issues are hard to troubleshoot when we have a high-scale distributed system comprised of dozens or 100s of microservices
		1. Solution: Observability & Monitoring
2. What We will Learn in This Lecture:
	1. What is Observability
		1. How it is different from monitoring
	2. Importance of Observability
		1. Why for microservices architecture
	3. Three Pillars of Observability

#### What is Observability ####
1. Observability vs Monitoring
	1. Both provide tools to:
		1. Collect data
		2. Give insights into our system in production
		3. Detect issues when they happen
2. Monitoring
	1. Process of:
		1. Collecting
		2. Analyzing
		3. Displaying
			1. _Predefined_ set of metrics
	2. By attaching alerts to those predefined metrics, we can find out when something goes wrong
	3. Problem: Monitoring tools and dashboards on their own usually will only tell us when something is wrong
		1. Does NOT tell us:
			1. _What_ is wrong
			2. _How_ to remediate the problem
3. Observability:
	1. Enables us to
		1. Actively Debug
		2. Search for patterns 
		3. Follow inputs/outputs (of microservices)
		4. Get insights into the behavior of the system
	2. Allows us to follow the flow of individual
		1. Requests:
		2. Transactions
		3. Events
			1. Across the entire system
	3. Discover and isolate performance bottlenecks
	4. Point us to the source of the problem
		1. Not just telling us that the problem exists

#### Importance of Observability ####
1. While monitoring is important for any kind of system, observability is critical for microservices architecture
2. If we have an issue with a monolithic application, it is relatively straight forward to debug or profile it, since it happens within the boundaries of a single application
	1. We can SSH into the instance of our monolithic application and inspect its logs
	2. Instrument it and get an idea of what part of the code is causing the performance issues or is throwing the exception
3. In a micro-services architecture, a single user request may involve several microservices and databases
	1. Those can communicate with each other asynchronously through message broker
	2. If an issue happens at some point in a transaction, it becomes very difficult to find in which service it happened
	3. Additionally, all the services run as a group of instances on different computers
		1. The challenge is even more amplified
	4. Statistically, most issues in microservices architecture happen at the API boundaries of the microservices and not in the code
		1. Having insights into the flow and content of the data coming in and out of each microservice and tracing the path of requests across microservices is critical
	5. One type of signal is insufficient to debug a problem in microservices and event-driven architecture
		1. Solution: Three Pillars of Observability

#### Three Pillars of Observability ####
1. Three types of signals
2. Observability in Microservices:
	1. Distributed Logging
		1. Logs:
			1. Append only files
			2. They record individual events - happening in:
				1. Application process
				2. Container
				3. Database instance
				4. Server
			3. Events are represented as string of data (structured/semi-structured)
			4. Events are accompanied by metadata:
				1. Timestamp (of the event)
				2. Request (that triggered it)
				3. Method (where the event happened)
				4. Class (where the event happened)
				5. Application (where the event happened)
	2. Metrics
		1. Regularly sampled datapoints
		2. Numeric values
			1. Counters
			2. Distributions
			3. Guages
		3. Examples:
			1. Request/min
			2. Errors/hour
			3. Latency distribution
			4. Current CPU utilization
			5. Memory usage
			6. Cache hit rate
	3. Distributed Tracing
		1. Path of a given request through several microservices
		2. Time each microservice took to process it
		3. Traces may include:
			1. Request headers
			2. Response status codes
3. When we get an alert about an issue or manually detected using monitoring dashboards
	1. We can use the three forms of signals to further debug the issue
		1. Procedure: We can use the combination of signals to:
			1. We can trace individual requests
			2. Isolate the issue to a particular microservice or API
				1. Further narrow it down to an individual method or line of code that caused that bug or performance bottleneck
	2. Using the signals we can get enough insight into how to address the issue by:
		1. Issuing a rollback
		2. Making a hotfix
		3. Adding more instances
		4. Diverting traffic to another region/data center

### Distributed Logging ###
1. Using the three types of signals, we can get:
	1. Deep insights into our system
	2. Effectively debug
	3. Find source of the issue
	4. Find performance bottleneck
2. What We will Learn in This Lecture:
	1. What is Logging
	2. Distributed Logging - Best Practices
	
#### What is Logging ####
1. Logging: Simple way to provide insight into the application's state
	1. A logline can be an:
		1. Event - Receiving a new request
		2. Action - Perform a database query or starting a complex processing operation
		3. Exception - In a method
			1. With parameters that led to the issue
		4. Error - In a method
			1. With parameters that led to the issue
	2. The information can be invaluable to debug and fix the issue and add enough tests to prevent such bugs in the future

#### Distributed Logging - Best Practices ####
1. Centralized System
	1. In microservices architecture, we can have thousands of instances of different microservices
		1. Collectively producing thousands of log-lines per day
			1. When we have an issue, it is not practical to SSH and inspect the log files one by one
				1. Solution: **Collect the logs into a centralized, highly scalable, logging system**
					1. The system parses and indexes those logs so they can be easily searched by patterns or text and grouped or filtered by attributes like:
						1. Hosts
						2. Microservice
						3. Time-period
						4. Region
2. Predefined structure/schema - to make searching easy
	1. Follow same terminology across different events within a microservices and across separate microservices
	2. Predefined Structure:
		1. Loglines must be easy to read:
			1. By humans
			2. By machines
				1. For efficient:
					1. Parsing
					2. Grouping
					3. Analysis
				2. Important if we are facing time-sensitive issues affecting users and we need to get to the root of the problem quickly:
					1. Examples of log-structures:
						1. logfmt: key/value pairs
						
								time=2023-11-01T23:07:42+00:00 app=review level=INFO duration=432 message="example of a logfmt"
								
						2. JSON:
						
								{
									"timestamp": "2023-11-01T23:07:07:42+00:00",
									"level": "info",
									"message": "Server starting",
									"server_id": "baser3e",
									"start_time": "2023-11-01T23:07:42"
								}
								
						3. XML:
						
								<Event timeMillis="43234" thread="main" level="DEBUG" threadPriority="3">
									<Instant epochSecond="234323" nanoOfSecond="54322000"/>
									<Message>Sample debug message</Message>
								</Event>
								
3. Assigning Log Level/ Log Severity (for each logline)
	1. Depending on framework or system we use, there are different log-levels and different number of log-levels
		1. Typically:
			1. TRACE
			2. DEBUG
			3. INFO
			4. WARN
			5. ERROR
			6. FATAL
		2. Adds additional dimention to logs that we can slice and filter on which helps reduce noise and alert fatigue
			1. Example:
				1. Exceptions logged as ERROR
				2. User impacting errors logged as FATAL
			2. If we are an engineer on call and we get an alert in the middle of the night that something is going wrong, we can search the logs, and filter only by ERROR or FATAL to find out what has happened and take the right actions
			3. Automated tools can search and periodically group events on those levels of serverity (ERROR, FATAL)
				1. The tools can alert us or create a ticket and automatically assign it for somebody to work on
				2. Events that indicate potential problems such as:
					1. High processing time of outgoing requests
					2. Receiving requests containing unexpected values
						1. Must be logged on the WARN level
							1. Can be used to filter based on this log level (WARN) and prevent future issues by addressing those events
		3. If we are a developer digging into a very complex issue and we need to follow every event that happened on a particular instance, we can look info on all log levels
			1. Fine grained details get logged on DEBUG and TRACE levels
4. Using Correlation Id (for every user request or transaction)
	1. Adding the ID to each logline corresponding to an event or step in processing that request or transaction
		1. `request_id=432`
	2. Since each microservice instance is likely processing multiple user requests concurrently, this id helps to filter and search only events related to the request in question
		1. It also helps us to see the sequence of events for a given request across multiple microservices
5. Adding Contextual Information (to each log-line as possible)
	1. If we log ERROR or exception, **want to add a stacktrace to debug and understand how we got to that line of code**
		1. We also want to include the parameters that led to this error
			1. `processing_time=25s` (very long)
				1. Add the database query that took very long to complete:
				
						query="SELECT comment, rating FROM Reviews
							INNER JOIN Products
							ON Reviews.product_id = Products.id
							WHERE Reviews.rating > 3
							ORDER BY Reviews.rating ASC,
							
				2. Add the content of the request that triggered it
				
						request="GET HTTP/1.1\" 200 6394 /get_possitive_reviews"\"
						
			2. The above helps us understand what issues happened and what measures we can take to mitigate it 
	2. **Common Data Points to include in every logline**
		1. Service name (name of the service that emitted the log event)
		2. Hostname / IP Address (where the event happened)
		3. User ID (or other ID that adds context to who initiated the operation)
		4. Timestamp (when that event happened)
	3. Contextual Information - Considerations
		1. Log only **necessary** data
			1. Log only the info that is critical for debugging because on a large scale system, storage and processing can be very information
		2. Do NOT log:
			1. Sensitive data
				1. PII (Personally Identifiable Information)
					1. Usernames
					2. Passwords
					3. SSNs
					4. Emails
					5. Credit Card Numbers
					6. ...
				2. Having such data can be helpful in troubleshooting, this poses a huge legal risk for the company - in case of a breach
				3. Also adds a lot of complexity regarding security and data retention compliance
				4. It is also unethical
					1. Nobody wants a random engineer troubleshooting a random issue in production to have access to our personal information especially if they don't need that to fix the issue
6. Summary:
	1. We learned about Distributed Logging (first pillar of observability)
	2. Best practices:
		1. They can make a huge difference when there are production issues we need to debug
			1. Centralized Logging System
				1. Collect all the logs from every microservice instance to a centralized system that can store and index those logs
					1. Ensures that they can be easily searched or organized
			2. Log structure
				1. Common log structure in microservices
			3. Log Level / Log Severity (for each logline)
			4. Correlation Id (important)
			5. Adding Contextual Information (important)
				1. Critical to figure out what happened and how to fix it

### Metrics ###
1. What We will Learn in the Lecture:
	1. What are metrics?
	2. The problem of collecting too many metrics (that arn't necessary)
	3. The 5 "Golden Signals/Metrics"
		1. For maximum observability
		2. For minimum complexity
	
#### What are Metrics? ####
1. Definition: Measurable or countable signals of software that help us monitor the system's health and performance
2. Typically, metrics are regularly sampled so that we can see a continous progression that helps us monitor our system and help us detect anomalies when they occur
	1. They usually come in numeric values
		1. We can quantify them and set alerts based on their direct or derived values
	2. Since they are numbers, they are:
		1. Easy to collect
		2. Easy to visualize
		3. Easy to organize in a dashboard
			1. Which can show all the vital signals of a microservice
			2. It can compare a metric with its historical value from before the release or before a significant change in the system
			3. Production dashboard is a critical tool for us when a production issue needs our attention
			4. Instead of searching or reading through log-lines, we can read one/two dashboards and get a clue as to what's happening

#### The Problem of Collecting Too Many Metrics ####
1. Questions:
	1. What signals we should measure, collect, and monitor?
	2. Why wouldn't we collect all of them?
2. What metrics we can collect?
	1. Number of different signals we can collect is pretty large
	2. Resources level: (all may or may not be helpful)
		1. CPU:
			1. Sockets
			2. Cores
			3. Threads
			4. Interconnect
			5. Cache Performance
			6. User Time
			7. Kernel Time
			8. Idle Time
		2. Memory:
			1. Cached
			2. Used
			3. Inactive
			4. Errors
			5. Capacity
			6. Page Faults
		3. Disk IO:
			1. Utilization
			2. Errors
			3. Throughput
			4. Latency
			5. Write Speed
			6. Read Speed
		4. Network:
			1. Outgoing connections
			2. Incoming connections
			3. Request size
		5. Processes:
			1. Running
			2. Sleeping
			3. Blocked
			4. Stopped
		6. ...
	3. Application Instrumentation:
		1. Incoming Requests/min
		2. Database queries/min
		3. GC pauseTime
		4. Throughput
		5. Number of Threads
		6. Memory Usage
		7. Orders Received
		8. Queue Size
		9. Request/Response Parsing Time
		10. Configuration Reload Time
		11. Latency Distribution
		12. ...
	4. Collecting anything we can measure is a big anti-pattern
		1. Collecting and storing too many metrics can become
			1. Very expensive
				1. Especially when we are talking about large-scale system with dozens or hundreds of microservices
				2. Even if we can bare the cost or handle storage of all the metrics, we have nother problem:
					1. Information overload
	5. Information overload:
		1. We might get an alert because the page is not loading or is too slow for most of our users
			1. Which dashboard should we look at?
				1. Even if we know which dashboard to look at, the number of graphs on each dashboard won't fit on the screen
					1. It is really hard to find anomalies
						1. Even if we notice a change in some metric, it will be difficult to understand which one is the symptom and which one is the cause

#### The 5 "Golden Signals/Metrics" ####
1. This is based on decades of experience from companies that have been running large distributed systems and microservices in production
	1. 5 types of signals that will give the most amount of info and least amount of noise
2. The Five (Golden) Types of Signals:
	1. Sources:
		1. Google SRE Book - "The Four Golden Signals" (which focuses on user facing metrics)
		2. The USE Method by Brendan Gregg (focuses more on system resources)
	2. Combining those sources, we have 5 types of signals:
		1. Traffic
		2. Errors 
		3. Latency
		4. Saturation
		5. Utilization
3. Traffic:
	1. It is the amount of demand being placed on our system per unit of time
		1. Examples: 
			1. HTTP requests/sec (or min)
				1. For a microservice that receives HTTP traffic
			2. Queries/sec (for a database)
			3. Transactions/sec (for a database)
			4. Events received/sec (for a message broker)
			5. Events delivered/sec (for a message broker)
			6. Incoming requests + outgoing requests/sec
				1. If a single request to a microservice results in many outgoing requests
					1. Because, open connections to other resources consume resources and directly impact microservice performance
4. Errors
	1. Error Rate and Error Types
		1. Error Rate: Great signal to set an alert for
			1. If the error rate suddenly goes up, the users are most likely already impacted
			2. Examples:
				1. Number of application **exceptions**
					1. We may not be able to show the error type as the number value
						1. **We can defer this to the logging**
				2. HTTP response **status code** (4XX, 5XX)
					1. That is different from 2XX for the service we depend on can be used as a metric
				3. Response **exceeding latency** thresholds
					1. In latency sensitive systems, we can even count successful responses as errors if they exceed a latency threshold that we set ahead of time
				4. Failed **Events** (for event-driven microservice)
					1. Events a microservice fails to process and
					2. Reasons for failure (if it is possible to classify)
				5. Number of **Aborted Transactions**
				6. Number of **Disk Failures**
5. Latency
	1. The time it takes for a service to process a request
		1. Important considerations (to measure it correctly):
			1. Latency distribution vs average
				1. Consider full latency distribution (not just average latency)
				2. Example: Requests Processing Latency
					1. Microservice receives a 1000 requests/min
						1. 95% of the requests are processed within 50ms
						2. 5% of the requests take 5k ms to process
						3. Average latency /min = 300 ms
							1. Pretty good for a user facing system
								1. However, this hides the fact that 5% of users must wait for 5s for the website to load
									1. Suppose we have a million users/day visiting our website, 50k of them will have a terrible experience and will likely switch to competitors and never come back
				3. If we look at 95th percentile of latency / min
					1. Significant portion of requests take unreasonable time to complete
						1. Indicating a performance bottleneck in the system
			2. Separating the latency of successful operations from failed operations
				1. If we mix the successful with failed requests, we may get the wrong data
					1. If we fail fast when we cannot process a request, we may artificially make our total latency look better than it is
						1. If we take too long to respond with an error, we may not know about it if those errors happen rarely
						2. Successful requests take very fast to process
					2. Solution: If we collect and monitor both successful requests and failed requests separately, we can get a good view of what our clients experience in both the scenarios
6. Saturation:
	1. Measures how overloaded/full a service/resource is.
		1. Very important for any system that has a queue
			1. An external queue like a message broker
			2. Internal queue within microservice or CPU
	2. When we have too many things stored in a queue
		1. It can indicate that our system cannot keep up with the current demand
		2. Example: If the topic in a message broker that stores purchase orders from users keeps growing, that likely indicates that we have a scalability issue with one of the services that consumes those events
		3. Example: If network queue of requests keeps growing, it may indicate that our storage device is not fast enough
			1. We may need to upgrade our hardware
			2. If it is an in-memory database, we may have to shard and distribute the data across multiple database instances
		4. If some queue in a microservice instance keeps growing, it may indicate that some part of our logic is too slow and the microservice instance may soon crash with out of memory exception
	3. Having visibility into saturation can also explain why our users suddenly have longer latency and requests from other services are timing out
7. Utilization
	1. It is used to measure, how busy a resource is [0-100%] over a period of time
		1. This applies to resources with limited capacity
			1. CPU
			2. Memory
			3. Disk space
			4. ...
	2. In most cases, we see performance degradation before we reach 100% resource utilzation
		1. Solution: Set alerts before we reach that critical level
			1. Example: If we see that the CPU utilization in our microservice instances is growing and approaching 80%, we need to scale out and add more service instances, otherwise, as we cross the 80% CPU utilization, we may start experiencing higher latency, and other issues
	3. If we see that our database is running out of storage, we need to add more database instances to keep up with the growing amounts of data
	4. **We want to measure utilization with higher granularity and not just an average over several minutes**
		1. We will miss short periods of high utilization that might be attributed to bottlenecks or other inefficiencies in our processing
8. The 5 Golden Signals aren't the only ones we should collect:
	1. Depending on business logic and specifics of our system or microservice, we can collect additional metrics that can add more to our observability
		1. The 5 Golden Signals are:
			1. Most common (apply to any system)
			2. Give us the most value by tracking them
9. Summary:
	1. Learned the second pillar of observability - metrics
		1. For microservices and event-driven architecture
	2. Motifivation: Metrics are the:
		1. Easiest to collect and visualize
		2. Most valuable for debugging production issues
	3. The 5 (Golden) Signals (categories of signals we must measure and collect):
		1. Traffic
		2. Errors
		3. Latency
		4. Saturation
		5. Utilization

### Distributed Tracing ###
1. What We will Learn in This Lecture:
	1. Distributed Tracing - Motivation
		1. What it is and why we need it
	2. Terminology + How Distributed Tracing Works
		1. What it takes to enable distributed tracing for microservices
	3. Challenges of using Distributed Tracing in Event-Driven Architecture
	
#### Distributed Tracing - Motivation ####
1. Example: Order Transaction in an E-Commerce System with Microservices and Event-Driven Architecture
	1. Steps:
		1. When a user places a purchase order for one of our products, the request goes to API Gateway first
		2. API Gateway talks to Auth service and ensures that user is what they claim to be and authorizes to make the purchase
		3. API Gateway then sends the request to one of the Order Service instances through a load balancer
		4. The Order Service records the order in its database
		5. The Order Service then emits an event to a topic in a message broker
		6. The Order Service then responds to the user
		7. Then we have a long chain of events and requests that go through several microservices, third party services, and message broker topics
		8. When the entire transaction is complete, the notification service sends a push notification and email confirmation to the user
			1. Email contains
				1. Payment receipt
				2. Order confirmation number
				3. URL where they can track their order
	2. Problems:
		1. Suppose, some users start complaining that they never received email confirmation for their orders
		2. Some users may also complain that they get the email but after several hours or a day later
	3. Problem to solve:
		1. We have many microservices involved exchanging requests and async messages, the issue can be anywhere
			1. Where do we start the investigation?
				1. Do we start by looking at the metrics dashboards of every microservice in the process
				2. Do we start reading thousands of log entries of every microservice or message broker to find something that stands out
				3. It is more difficult if there are multiple instances of microservices running on different computers behind a load balancer or message broker
					1. Every message broker is distributed
					2. Every database is also distributed
					3. We call third party APIs that we don't have any visibility into
					4. We may have 100s of microservices
						1. Each microservice plays some part in processing a request flow or a transaction
						2. If a complex and constantly evolving architecture exists, it becomes humanly infeasible to remember what microservices are involved in processing a given type of request or in what order
			2. Solution: 
				1. Distributed tracing
2. Distributed Tracing:
	1. It is a method of tracking the entire requests as they flow through the entire system starting at the client's device all the way through our backend services and databases
	2. As the request is being traced, we collect critical performance information about the time, each part of the system is processing it
		1. Allows engineers to:
			1. Visualize the entire flow
			2. Understand all the components involved for processing the request
			3. Understand time it took for each component to do its work
		2. It is extremely valuable for troubleshooting bugs or errors that lead to:
			1. Wrong behavior or 
			2. Performance bottlenecks
	3. It is not enough on its own (to tell us exactly what is happening)
		1. It helps narrow down the:
			1. Faulty component
			2. Communication problem (between two components)
	4. Once we identify where the problem is happening:
		1. We can use logs and metrics to debug further

#### Terminology + How Distributed Tracing Works ####
1. How it works:
	1. When the initial request is made, we generate a unique **trace id** and place it into an object called a **trace context**
		1. The trace context object contains key data about the entire trace
	2. As the request flows through the services, context is propagated inside events
		1. Usually through:
			1. HTTP Headers
			2. Message Headers
	3. Just passing trace context from service to service is not enough
		1. For application instances to collect the data, we need to instrument them using a tracing instrumentation library or SDK
			1. The tracing libraries come in different programming languages
				1. Even if we have a polyglot system, we can still get a complete trace
	4. As soon as the service instance receives the service context, it collects the necessary data, and propagates the context to the next service
	5. At the end of the transaction, each service instance that was involved has its own measurements and data
		1. Which can be later aggregated by the trace id
2. To visualize all the parts of a transaction, and how long each part of the transaction took:
	1. The trace is broken into logical units of work
		1. Called spans
			1. The trace-spans can be coarse grained
				1. Processing of a request by a service or query by a database
				2. Manually instantiated by developers using instrumentation library
					1. Different units of work within a service can be visualized and measured separately
						1. If one logical part apears slower than usual, we can investigate it further as a potential performance bottleneck
							1. If an expected span is missing, we have a bug that we need to debug
					2. To increase granularity even further, we can connect related pieces of work together by organizing spans in a hierarchy
						1. With parent-child relationship
							1. Example: 
								1. After inspecting the trace, we notice that a particular service is slow to process a request
								2. We can then expand the span and see its children and their children spans
									1. We could see that one of the database queries was surprisingly slow
										1. We can now investigate by looking for particular log messages in that service
	2. How data gets collected from the services and aggregated into visual views
		1. Many solutions and vendors with different architectures and deployments
		2. General approach:
			1. Once the trace data is collected inside each service instance, it is pulled by an **agent**, which runs as a separate process within each service instance
			2. Agents send the trace data send to a central queue or topic in a message-broker
			3. The tracing data that comes from many services is analyzed, aggregated, indexed, and stored in a database by a big-data processor
			4. A developer can analyse and visualize the data using a tracing UI in a browser

#### Challenges in Event-Driven Architecture ####
1. Ditributed Tracing - Challengs
	1. Manual instrumentation of code (to collect data that can be used for distributed tracing)
		1. In most cases - not a big effort
			1. It requires us to:
				1. Depend on and load a library
				2. Sometimes, learn and manually add instrumentation code
			2. Otherwise:
				1. Spans may be too broad: If we don't do the manual work
					1. When we need to investigate the production issue, our spans may be too broad in granularity or important data
				2. Missing spans: In extreme cases, if we use the instrumentation library incorrectly, our traces may become broken
					1. Therefore, useless
	2. Cost
		1. We need to run an agent on each microservice host which consumes its own CPU and memory
		2. We then need to collect the data and must be sent over the network
			1. This needs additional bandwidth
		3. We need to run a big data pipeline with its own infrastructure to process those tracing logs that come from different services
		4. The big data pipeline comes with its own maintenance cost
		5. Cost of storing those traces in a database and retaining them for at-least a few weeks (most expensive relatively)
			1. Developers can find them if they need to debug an issue
			2. With a few million requests / day with each request flowing through a dozen microservices, the volume of data we need to store can be very high
				1. Solution: To keep the storage and network cost in check, most companies use sampling (1/1000 requests) on the client side
					1. 1 trace out of a 1000 or 10000 requests
					2. Advantage: Lowers storage cost
					3. Disadvantage: It makes it hard to find a trace that will reproduce a particular issue we are trying to debug
	3. Big Traces / Too Much Data
		1. Big Traces Problem:
			1. Microservices and Event-Driven Architecture usually involve many components that a single trace can be so big that it's hard for a human to look at
				1. Example: Some are so big that they can't be loaded in the UI
					1. Impossible to look at them
2. Distributed Tracing - Conclusion
	1. Very powerful and essential debugging tool [for microservices and event-driven architecture]
	2. Important for restoring confidence among developers that issues happen in prod, they have the tools to troubleshoot it and find the root cause

#### Summary ####
1. Learned about the 3rd pillar of observability: Distributed Tracing
2. Motivation: Issues in Microservices are very hard to debug
	1. Explored real-life scenario
		1. An issue in one of our microservices or communication between them becomes almost impossible to debug without tracing
3. Terminology:
	1. Trace ID
	2. Trace Context
	3. Spans
4. Challenges:
	1. Manual code instrumentation
	2. High cost
	3. Large amount of data (that we need to visualize and store)

### Distributed Tracing Solutions ###
1. Distributed Tracing Instrumentation Frameworks
	1. [OpenTelemetry](https://opentelemetry.io/) - OpenTelemetry is a collection of:
		1. APIs
		2. SDKs
		3. Tools for 
			1. Instrumenting
			2. Collecting
			3. Exporting
				1. Metrics
				2. Logs
				3. Traces
		4. It is open-source and is available in [many programming languages](https://opentelemetry.io/docs/instrumentation/#status-and-releases)
			1. [C++](https://opentelemetry.io/docs/instrumentation/cpp/)
			2. [#/.NET](https://opentelemetry.io/docs/instrumentation/net/)
			3. [Erlang/Elixir](https://opentelemetry.io/docs/instrumentation/erlang/)
			4. [Go](https://opentelemetry.io/docs/instrumentation/go/)
			5. [Java](https://opentelemetry.io/docs/instrumentation/java/)
			6. [Javascript](https://opentelemetry.io/docs/instrumentation/js/)
			7. [PHP](https://opentelemetry.io/docs/instrumentation/php/)
			8. [Python](https://opentelemetry.io/docs/instrumentation/python/)
			9. [Ruby](https://opentelemetry.io/docs/instrumentation/ruby/)
			10. [Rust](https://opentelemetry.io/docs/instrumentation/rust/)
			11. [Swift](https://opentelemetry.io/docs/instrumentation/swift/)
		5. [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-specification) - It is also a specification that describes the cross-language requirements and expectations for all OpenTelemetry implementations
2. Distributed Tracing Backends:
	1. [Jaeger](https://www.jaegertracing.io/)
		1. Open source, distributed tracing platform that is cloud-native, infinitely scalable, and 100% free
		2. It enables the monitoring of:
			1. Distributed worklows
			2. Tracking down root causes for performance bottlenecks
			3. Analyzing service dependencies
		3. Requires OpenTelementry for instrumentation
	2. [Zipkin](https://zipkin.io/)
		1. Another open-source distributed tracing system
		2. Data served to the UI is stored in memory or persistently within Apache Cassandra or Elasticsearch
		3. Originally developed at Twitter in 2010 and based on Google's Dapper papers
		4. Supports a variety of official and community-created [instrumentation frameworks](https://zipkin.io/pages/tracers_instrumentation)
	3. [Uptrace](https://uptrace.dev/)
		1. It is an OpenTelemetry-based observability platform that helps us monitor, understand, and optimize distributed systems
		2. It is a commercial, cloud-based solution
		3. It supports a variety of features:
			1. App performance monitoring
			2. Metrics collection
			3. Visualization
			4. Logs injection and analysis
			5. ...

## Deployment of Microservices and Event-Driven Architecture in Production ##
### Microservices Deployment - Cloud Virtual Machine, Dedicated Hosts and Instances ###
1. How to deploy and run microservices in production.
2. A few infrastructure choices for running microservices
	1. Primarily focusing on the cloud environment
2. What We will Learn in This Lecture
	1. Multi-Tenant Virtual Machine Deployment
	2. Dedicated Hosts and Instances

#### Multi-Tenant Virtual Machine Deployment ####
1. Virtual Machine
	1. It is an isolated environment running on top of a real-physical computer
	2. The VM acts like a virtual computer with its OS, and virtual resources (cpu, memory, networ interface, storage)
		1. Virtual resources are allocated, managed, and mapped to real resources on the physical hardware by another layer of software called the hypervisor
	3. Using VMs, a cloud provider can split each physical server into multiple VMs
		1. Amount of resources allocated to each VM depends on how we configured it and how much we pay for that VM
	4. **Multi-Tenancy**: Each VM can run a different instance of the same microservice or a separate instance of a different microservices or a different instance of microservice belonging to a different cloud provider customer
		1. By default, when we rent or reserve cloud VMs, we have no control over who else is running their VMs on the same host
			1. This allows the cloud providers to split their servers very efficiently fully utilizing their hardware
				1. Allows them to offer us compatitive prices which makes cloud VMs a very attractive option to run microservices
	5. Cloud VMs - Benefits
		1. Affordable, flexible pricing
			1. Typical pricing model: Pay-Per Use
				1. We pay only for the cloud VMs that we are renting for the duration we are renting them
				2. Rate depends on capabilities
					1. CPU
					2. Memory
					3. Network bandwidth capabilities
	6. Cloud VMs - Downsides
		1. Security risks - due to multi-tenancy
			1. Theoretically, when we run two VMs on the same serve, the two VMs are isolated from each other
				1. If the two VMs are running DB instances for example, each instance belongs to a completely different organization, a security breach in one VM should not pose a risk to the other VM
					1. Hypervisor is a software written by human beings
						1. All security and configs are managed and updated by human beings
							1. => It is possible for a hacker to gain access to a VM that was poorely secured by the engineers of another organizations
							2. Since cloud vendor allocated our VM to run on the same host, the hacker may manage to hack into our system and steal our data
				2. Solution: Cloud vendors and Hypervisor companies make great efforts to prevent this from ever hapening
					1. Probability of this ever happening is very small
						1. Exceptions: Due to compliance issues in certain industries, we may be unable to tolerate even such a small risk
							1. Examples of industries that cannot afford to run some parts of their services on cloud multi-tenant environment:
								1. Banking
								2. Healthcare
								3. Government
								4. National Security related services
		2. "Noisy Neighbor" - Potential lower performance due to this issue
			1. Theoretically, the hypervisor should be able to isolate and allocate hardware resources to each VM as configured ahead of time
				1. In practice, not all resources can be accurately allocated
					1. If a host has 16 CPU cores, the hypervisor could easily split 16 cores evenly so each VM can get dedicated 8 cores
					2. Problems:
						1. The network bandwidth of a network card or access to an internal bus that transfers data to and from a storage device cannot be easily rationed in an accurate way
						2. Many other physical resources inside the computer cannot be split (it is after all a one physical server)
						3. The hypervisor may consume some CPU, & memory for its own use
			2. Not a lot of data to suggest that running a very intensive workload on one VM can significantly impact the performance of the other VM
				1. In practice that impact is still there
					1. For very latency sensitive services such as the following services, multi-tenant deployments with cloud VMs is not the best option:
						1. High-frequency trading systems
						2. Gaming
						3. Video streaming
						
#### Dedicated Hosts and Instances ####
1. We can ask the cloud provider to run our VMs on servers that are dedicated to the account that belongs to our organization
	1. The only tenants that we are going to have on the hosts are instances of our microservice, other microservices, databases belonging to our organization only
		1. If we are in an industry that doesn't allow us to share infrastructure with other companies, this is great but slightly more expensive alternative
			1. The reason why the cloud vendors charge more for such deployments is that they cannot allocate their hardware as efficiently as the multi-tenant deployments
2. Some cloud providers allow us to rent or reserve an entire host just of our organizations
	1. It gives direct access to the host hardware resources which can completely eliminate the noisy neighbor effect and reduce the overhead of virtualization of the hypervisor
	2. Downside:
		1. Much more expensive than multi-tenant cloud VMs

#### Conclusion ####
1. Deployment Type
	1. Multi-Tenant Cloud VM
		1. Cost: Best pricing
		2. Security: Not most optimal
		3. Performance: Not most optimal
	2. Single-Tenant Cloud VM
		1. Cost: Bit more expensive
		2. Security: Better security
			1. VMs of on\ly our organization can run on the same physical hardware
		3. Performance: Higher performance
	3. Dedicated Host
		1. Cost: Most expensive
		2. Security: Most optimal
			1. Eliminates the possibility of a noisy neighbor
		3. Performance: Most optimal

### Cloud Virtual Machine, Dedicated Hosts and Instances - Solutions ###
#### Multi-Tenant Virtual Machine Cloud Service ####
1. [Amazon Elastic Compute Cloud (EC2) Instancees](https://docs.aws.amazon.com/ec2/) - Provides on-demand, scalable compute capacity using "virtual servers"
	1. Offers [different instance types](https://aws.amazon.com/ec2/instance-types/) optimized for different workloads such as:
		1. General purpose
		2. Memory
		3. Compute
		4. Storage
		5. ...
2. [GCP Compute Engine](https://cloud.google.com/compute?hl=en) - Offers secure and customizable VMs running on Google's infrastructure
	1. You can choose from a [variety of VMs](https://cloud.google.com/compute/docs/machine-resource) for different architectures (x86, ARM, etc.) and workloads such as:
		1. "Scale Out"
		2. General purpose
		3. ultra-high memory
		4. compute-intensive
		5. Accelerator-optimized machines
		6. ...
3. [Microsoft Azure VMs](https://azure.microsoft.com/en-us/products/virtual-machines)
	1. Allows creation of Linux and Windows VMs in seconds
	2. Includes [serveral series](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/series/) of VMs for:
		1. Testing/development
		2. Economical burstable VMs
		3. General-purpose computing
		4. Optimized for in-memory applications
		5. Compute-optimized VMs
		6. Memory and storage optimized VMs
		7. High-performance computing VMs
		8. Storage-optimized VMs
		9. GPU-enabled VMs
		10. ...
		
#### Dedicated Hosts and Single Tenant Virtual Machine Cloud Services ####
1. [AWS Dedicated EC2 Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html)
	1. Dedicated EC2 instances are regular EC2 instances that run on hardware that's dedicated to a single customer with an AWS account
	2. Dedicated EC2 instances that belong to different AWS accounts are physically isolated at a hardware level
	3. However, EC2 dedicated instances might share hardware with other instances from the same AWS account that are not dedicated instances
2. [Amazon EC2 Dedicated Hosts](https://aws.amazon.com/ec2/dedicated-hosts/)
	1. Amazon EC2 Dedicated Host is a physical server fully dedicated for our use so that we can help address corporate compliance requirements
	2. We can find the pricing of dedicated hosts [here](https://aws.amazon.com/ec2/dedicated-hosts/pricing/)
3. [GCP Sole-Tenant Node](https://cloud.google.com/compute/docs/nodes/sole-tenant-nodes)
	1. A sole-tenant node gives us exclusive access to a physical compute engine server that is dedicated to hosting only our project's VMs
	2. Within a sole-tenant node, we can provision multiple VMs on machine types
	3. Alternatively, we can meet **security or compliance requirements** with workloads that **require physical isolation from other workloads or VMs** by not sharing the node with any other project
4. [Microsoft Azure Dedicated Hosts](https://azure.microsoft.com/en-us/products/virtual-machines/dedicated-host)
	1. Azure dedicated host offers physical servers designed to host one or more Azure VMs
	2. The servers are exclusively dedicated to our organization and the workloads
		1. Ensures that the capacity is not shared with any other customers
	3. This level of isolation at host level serves to meet compliance requirements effectively

### Serverless Deployment for Microservices using Function as a Service ###
1. What We will Learn in This Lecture
	1. Motivation for Serverless Deployment using FaaS
		1. Problem it solves for us
	2. FaaS Deployment Benefits and Drawbacks
		1. So that we can use it in production correctly
		
#### Motivation for Serverless Deployment using FaaS ####
1. Use-Case: Video On Demand (VOD) Streaming Platform
	1. Users can rent or buy movies or shows
	2. Additional offering: They partner with performance venues to sell tickets for their live events
		1. There is a dedicated microservice to handle these events
	3. Microservices:
		1. Video Data Service
		2. Auth Service
		3. Payments Service
		4. Ticket Reservation Service
			1. For live events only
	4. The live events happen only occasionally
		1. Once a month at-most
		2. When we open the reservation, most requests come within 30 minutes to an hour
			1. During the time, 99% of the tickets are sold
		3. Then a few cheap tickets (Cheap/Not Good) and a few good tickets (Expensive/Premium) remain
			1. The tickets will be sold sometime between the initial launch and the event date
				1. The traffic will not be very significant
	5. Traffic pattern:
		1. We don't get traffic most of the time
		2. If we deploy it as a cloud VM, dedicated host, we will paying for renting the hardware during the downtime
		3. When we open the reservation for a new event, we get a very high traffic spike
			1. We need to configure and pay for a load balancer and maintain outer scaling policies for the microservice
				1. Add more infrastructure cost for running the service
2. Use-Case: Digital Advertisement Company
	1. Infrastructure Cost: One of the microservices allows customers to run a monthly or quarterly report that provides insights into their reach and return on investment for their advertising
		1. The report can be triggered directly by an admin working for the advertisement company or by a cronjob that runs once a month or quarter and triggers a report automatically
		2. Even with 1000 customers, we will get only 1000 requests/events per month/quarter
			1. Running the microservice all the time just for the events that happen rarely is not cost effective
	2. Development Costs (for maintaining it): 
		1. If we are team that owns such a microservice in addition to business logic,
			1. We need to handle HTTP/Event Handling boilerplate code (that triggers the logic)
			2. Scripts to build, package and deploy the microservice binary with all its dependencies to a cloud server
	3. We need to invest all that effort just to:
		1. **Handle very little traffic**
		2. **Events that happen rarely**
	4. Solution: FaaS - Function as a Service

#### FaaS Deployment Benefits and Drawbacks ####
1. FaaS
	1. It is a cloud offering that allows us to architect our system in a fully event-driven model
		1. From software perspective
		2. From infrastructure perspective
	2. As part of this offering, we need provide the cloud vendor:
		1. Type of request/event to handle
		2. Logic to execute
	3. Only when that event is triggered:
		1. The cloud provider will take our code
		2. Package our code
		3. Deploy it to a physical hardware
		4. Execute it in response to the request or event
	4. If our traffic has a seasonal pattern, where we may have a lot of requests coming in a very short period of time, the cloud provider will also horizontal scalability to allow us to handle traffic spike without the need to:
		1. Maintain autoscaling policies 
		2. Configuring a load balancer
2. FaaS - Pricing Model
	1. Based on:
		1. Number of requests/month (our microservice receives)
		2. Execution time
		3. Memory (required to handle each request by running our logic)
	2. If we don't get requests/events, the price is zero
3. FaaS - Benefits
	1. For events that happen rarely:
		1. Reduced **infrastructure costs**
	2. Reduced operational overhead for scalability:
		1. For seasonal workloads with rare but very high traffic spikes, the cloud provider also handles all the operational overhead for scaling that service
	3. Reduced development cost for building, packaging and deploying microservices
		1. Reduced cost and overhead
4. FaaS - Drawbacks
	1. If the traffic pattern changes, infrastructure costs may increase significantly
		1. Example: 
			1. If we start with a microservice that handles very seasonal or low traffic, but over time, we start getting more and more requests,
				1. Code will run more frequently
			2. As our business logic becomes complex, each time we receive a request or event handling it, we will require a lot more time and memory
				1. **It will become more expensive for us to use this offering than deploying on a cloud VM or dedicated host**
	2. Unpredictable performance
		1. Than deploying business logic as part of a microservice we fully control
			1. This is not the best option for latency sensitive workloads
	3. Multi-tenant deployment
		1. It is a less secure type of deployment
		2. Cloud vendor has our source code
5. Types of deployment for microservices
	1. Function as a Service
		1. Cost: Most cost efficient way to deploy our microservices
			1. If we use it incorrectly or not for the right workload, it can be the most expensive
		2. Security:
			1. Least optimal
		3. Performance
			1. Least optimal

### Serverless Deployment for Microservices using Function as a Service - Solution ###
#### Amazon Web Services (AWS) ####
1. [AWS Lambda](https://aws.amazon.com/lambda/)
	1. Serverless, event-driven compute service that enables us to execute code for nearly any kind of app or backend service without the need to set up or oversee servers
	2. We can execute our code in a lambda through more than 200 AWS services and SaaS applications

#### Google Cloud Platform (GCP) ####
1. [Cloud Functions](https://cloud.google.com/functions)
	1. Allows executing code in the cloud without the need to handle servers or containers
	2. By using GCP's scalable Functions as a Service (FaaS) offering
	3. We only pay for what we use
		1. Pay-as-you-go model

#### Microsoft Azure ####
1. [Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/)
	1. On-demand cloud service that provides the
		1. Latest infrastructure & resources
			1. Required to operate the application
	2. Allows us to fully focus on code while Azure Functions manages the remaining aspects

### Containers for Microservices in Dev, Testing, and Production ###
1. Containers for developing, testing, and deploying microservices to production
	1. This deployment type is the most popular and trending ways to package and deliver microservices in production
2. What We will Learn in This Lecture
	1. Problem Statement
	2. Benefits of Containers for Microservices over VMs
	3. Challenges of running microservices using Containers in Production
	
#### Problem Statement ####
1. Common problems:
	1. Lack of parity between the development environment and production environment
		1. Example: Suppose there is a developer on a team owning a microservice
			1. I setup all the development environment for the microservice locally, with a local standalone database version
			2. I also install all the dependencies of the microservice specific to the OS
			3. However:
				1. The production distributed database is configured differently than the local standalone database
				2. The OS in production is not the same as in the development laptop
					1. All the locations of the configuration files, and all the dependencies are entirely different
			4. When we developed and tested our feature locally, everything worked fine
			5. When we deploy it to production, things break and don't work as expected
	2. Possible Solution:
		1. Develop and test microservice in a production like VM in a development computer
			1. Solves the development vs production parity problem
				1. Introduces another problem:
					1. Host OS needs to run another software layer called hypervisor type 2
						1. Hyervisor runs like any other program on the host OS
						2. Hypervisor runs another OS with its own kernel
						3. The kernel manages:
							1. Processes
							2. File system
							3. Security
							4. Networking
							5. Memory
							6. ...
						4. The kernel also uses:
							1. Device drivers to interact with virtual hardware, which is emulated by the hypervisor
					2. So much unnecessary overhead just to run a single microservice instance
					3. To run and test the integration of a few microservices, we need to run multiple VMs
						1. Each with its own copy of the OS
							1. Too much overhead
								1. Everything will be extremely slow and inefficient
									1. Makes development and testing very hard

#### Benefits of Containers for Microservices over VMs ####
1. Containers solved this problem by:
	1. Isolating what we want to isolate
	2. Sharing everything else
2. When we package our microservices into containers, each container image includes the following in complete isolation from any other microservice:
	1. Microservice binary
	2. Command to run it
	3. Dependencies it requires
3. When we run one or multiple instances of the image, each container has its own:
	1. Isolated file system
	2. Isolated network interface
	3. Isolated runtime
4. The containers share the Kernel, drivers, etc (we don't need to isolate them)
	1. The overhead of running a few dozen of containers on our machine is minimal
		1. Perfect for developing and testing microservices
5. Benefits don't end in development and testing stage
	1. We can run the containers in a CI pipeline (which may run a completely different OS, and completely different hardware than development environment)
		1. **Container images are completely decoupled from the OS and hardware**
			1. They can be created once and run on any hardware and OS that supports containers and container runtime
6. Production Cloud Environment:
	1. Previously, each microservice instance was deployed in its own VM and scheduled by the cloud vendor to run in one of its servers
		1. The approach has many advantages
		2. It has big disadvantages
			1. Inefficient resource utilization:
				1. If two microservice instances run in a cloud server:
					1. Each VM runs in an entirely separate instance of the typically same OS
						1. Due to duplication, we lose valuable memory, cpu, and storage resources to the OS
				2. Deploying and starting each VM can take minutes until we are ready to accept traffic
			2. Cloud vendor lock-in (and lack of portability)
				1. When we construct an image for a microservice, the format of this image may be cloud vendor specific:
					1. AMI (Amazon Machine Image)
					2. VHD (Virtual Hard Disk)
					3. VMDK (VMWare Virtual Machine Disk)
				2. Configuration that describes the type of VM we want to rent, is also cloud vendor specific (m4.2xlarge, Dplsv5, c3-standard-44)
				3. Problem:
					1. If we get an attractive offer for another cloud vendor and we want to migrate completely, we need to do a lot of work constructing new images
				4. Multi-Cloud environment:
					1. When we run some services in one cloud provider and another part in another cloud provider
				5. Hybrid-Cloud
					1. One part may run on a public cloud vendor
					2. Another part runs in a private cloud environment
						1. For higher security or performance purposes
				6. Cloud VMs are hard to manage in the above types of environments
					1. Solution: Containers solves the above problems
						1. We need to build container images once and deploy them in generic cloud VMs or directly on dedicated hosts in any environment
							1. The only requirement is to install container runtime (software that runs the containers)
7. Containers in Production - Benefits
	1. Portability between environments
		1. We can build the microservices images once & use it in development, QA, staging, and production on any cloud provider, hardware, or OS
	2. Faster deployment / startup times
		1. Containers take only a few milliseconds to deploy and run
	3. Lower instrastructure cost
		1. Hardware utilization is much better when we use containers
8. Instead of renting multiple smaller VMs where we lose a part of CPU, and memory to OS, we can rent larger VMs or dedicated hosts
	1. When we deploy containers of different microservices on a single VM or host, we can better utilize the hardware because they share the same OS kernel
		1. => we can run more microservice instances for the same amount of hardware than when we use cloud VMs

#### Challenges of Containers in Production ####
1. Another problem to solve
	1. Connecting 2 layers of abstractions (that we need to glue together)
		1. Infrastructure Layer
			1. Cloud infra abstraction - includes cloud VMs or hosts
				1. We need to rent and autoscale based on traffic or load on our system
				2. Other cloud managed services
					1. Databases
					2. Message brokers
					3. Distributed logging
					4. ...
			2. Containers Layers
				1. There are dozens of container images representing different microservices
					1. Each microservice image needs to be deployed as a group of container instances on that infrastructure
				2. We need to discover and connect all the microservices to each other & the managed services through the network
				3. We also need to manage the scalability and availability of each group of the containers:
					1. So that we can add more instances if traffic goes up &
					2. Remove instances if traffic goes down
				4. We need to automatically replace containers that crash
				5. We need to update all the containers of a microservice when a new version of a microservice is released
					1. Problem: Doing all that manually for 100s or 1000s of instances, potentially running in different cloud regions or different cloud providers is an impossible task
					2. Solution:
						1. **Another layer called Containers Orchestration**

#### Summary ####
1. Problem of dev/prod and QA/prod parity
	1. May result in issues in production
	2. VMs don't solve this issue due to big overhead
		1. For each VM, we need to run an entire copy of OS with its own Kernel and hypervisor program
	3. Solution: Containers in:
		1. Development
		2. Testing (Continuous Integration)
		3. Production
			1. Increased portability
			2. Reduces start-up time for each microservice
			3. Cuts down on the cost of infrastructure
	4. **Deploying** and **Managing** containers in Production can be a challenge

### Container Orcherstration and Kubernetes for Microservices Architecture ###
1. Containers - Benefits
	1. Full parity between dev/QA and prod environment
	2. Portability between different cloud environments
	3. Faster development/startup
		1. Due to better hardware utilization
	4. Lower infrastructure cost
2. Challenge in the following with 100s or 1000s of microservices (even across different cloud providers):
	1. Deployment
	2. Configuration 
	3. Management
3. What we Will Learn in this Lecture:
	1. Introduction to Container Orchestration
		1. What it is
		2. In depth about a container orchestrator
	2. Container Orchestration Architecture - Kubernetes Example
	
#### Introduction to Container Orchestration ####
1. What is a container orchestrator
	1. It is a tool that manages the lifecycle of microservice containers
	2. It is like an OS but for microservices deployed as containers
2. Containers Orchestrator - Responsibilities
	1. Deployment Automation
		1. New microservices
		2. New versions
	2. Resource allocation
		1. To ensure each container gets the right amount of CPU, memory and storage to work properly
	3. Health monitoring
	4. Self-healing
		1. Allows automatic deployment of new containers to maintain a healthy number of instances of each microservice
	5. Bin-packing
		1. Scheduling containers in an efficient way for optimal utilization of existing hardware
	6. Load balancing
		1. Between containers of the same microservice
	7. Scaling services
		1. Out or in by adding or removing containers based on the traffic and resource utilization
	8. Container Discovery
	9. Network connectivity
		1. Among services, containers, and outside world

#### Container Orchestration Architecture - Kubernetes Example ####
1. Kubernetes - most popular but not the only one
2. Architecture:
	1. Control Plane - deployed on at-least one machine
		1. Controller node
			1. Runs all processes that orchestrate and manage our cluster
				1. API process - takes commands from us to:
					1. Add a microservice
					2. Update an existing microservice version
					3. Update an existing microservice configuration
					4. ...
				2. Key Value Store Database - Info about cluster config and current state is stored by another process
				3. Scheduler - To add another container
					1. It monitors worker node resources and decides where to schedule that new container
				4. Controller Manager - Monitors the health of worker nodes or state changes in those nodes
					1. If one of the nodes becomes unavailable, it will detect that and ensure that the scheduler process re-schedules those microservice containers to other worker nodes
				5. Cloud-Controller Manager - Process that manages all cloud provider specific logic
					1. Deleting un-responsive worker nodes by the cloud provider
					2. Adding cloud managed load balancers
					3. Routing load balancers to containers
					4. ...
	2. Worker Nodes - VMs and server that our microservices containers 
		1. Agents - To manage containers running only on that node
			1. Includes:
				1. Container runtime - software engine running the containers on each host
				2. Kubelet - Agent that monitors and starts the microservice containers when it receives command from control plane
		2. Kube-proxy - Proxy maintains a set of network rules to route network requests between containers of different microservices 
			1. Also balances the load on containers on the same microservices
	3. Sometimes we need to run each of our microservice with a sidecar process
		1. Sidecar process can be:
			1. Logging
			2. Monitoring agent
			3. In-memory cache
		2. Problem:
			1. Putting more than one process in a container is not a good practice
				1. Solution: k8s allows us to bundle several containers inside a logical unit called a pod
					1. Pod: Smallest runtime unit that k8s will manage for us (even if it contains a single microservice container)
	4. Description of all the microservices architecture, configuration, container images they use, how much cpu, memory, and storage they need is described in a declarative, human-readable way
		1. The configuration contains all the information about the services our microservices connect to outside container cluster
			1. Cloud functions
			2. Databases
			3. Object stores
			4. Message brokers
			5. ...
		2. The configuration is stored, maintained, and updated in a version control system (just like any other code)
			1. Once a change is made to the config, it will be sent to the control-plane's API server
				1. It triggers the relevant updates within the cluster
	5. In a typical microservices architecture, we will have 100s of such worker nodes running 1000s of containers belonging to different microservices
		1. For higher availability, keep up with everything going on in the cluster, we typically have replicas of the controller nodes (inside the control plane)
		2. For even higher availability, we can have multiple clusters with the same or different configs running:
			1. On different cloud regions
			2. On different cloud providers
	6. The traffic to different regions and cloud providers can be routed using a global load balancer
		1. The routing can be based on the criteria such as:
			1. Physical proximity to the user
			2. Load
			3. Health of each cluster
			4. ...
	7. The container orchestration architecture can be pretty complex to setup and manage
		1. It requires expertise from DevOps or SREs
		2. It also requires dedicated resources just for orchestration purposes
			1. Like the controller instances
3. Cost of Container Orchestration:
	1. The investment pays of
		1. Because it's amortized across all the teams / microservices we manage
			1. If our decision to migrate to microservices was correct, the benefits of running microservices as containers managed by the container orchestrator will outweigh its cost and complexity

#### Conclusion ####
1. We have all the skills to do the following for microservices and event-driven architecture:
	1. Migrate
	2. Develop
	3. Test
	4. Run

## Bonus Section ##
### Bonus Lecture - Let's Keep Learning ###
1. [https://www.udemy.com/course/the-complete-microservices-event-driven-architecture/learn/lecture/40200392#content](https://www.udemy.com/course/the-complete-microservices-event-driven-architecture/learn/lecture/40200392#content) 
	1. Courses
	2. E-Book
	3. LinkedIn
	4. Career Coaching