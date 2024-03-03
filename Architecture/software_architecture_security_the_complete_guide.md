# Software Architecture Security - The Complete Guide #
## Section 1: Welcome ##
### Course Introduction ###
1. One of the most important aspects of software architecture (often overlooked)
2. Why security?
	1. Security breaches can cause a lot of damage
		1. The damage can come in many forms or shapes
3. Non-Secure System Will...
	1. Destroy your reputation
		1. No one likes a company that leaked sensitive data
	2. Kill the business
		1. It might lose all of it's paying clients
	3. May cause criminal charges
4. We need to ensure that our system is as secure as possible
5. What we will learn?
	1. Definition of security
	2. Secure Architecture Process
		1. How security is integrated into the architecture process
			1. Some of the steps must take security into account
		2. We need to talk about what are the security related actions for each step
	3. Role of the architect
		1. Where and when he or she needs to take action (security related)
	4. Very practical (case study, checklist)
		1. As an architect, we need to make our next system secure
		2. Case study: Real world system
			1. We will exercise the knowledge gained through the course
		3. Checklist
			1. Download at the end of the course
				1. Step by step guide to make sure we have done everything possible to make the architecture and system more secure
6. By the end of the course
	1. You'll know what you need to protect against
	2. You'll know how to integrate security into your systems
	3. You'll know what is your role, as an Architect, in the organization's overall security efforts
	4. You'll be able to help the org to define security policy
	5. You'll become a much better software architect
	6. At the end of the course - 
		1. Download the Secure Architect Checklist!
			1. The ultimate practical, step-by-step guide to ensure your architecture is secure
				1. Helps greatly when designing security in the system

### Join The Software Architects Community ###
1. We need a supporting community to succeed in every profession
	1. [Software Architects Discussion](https://www.facebook.com/groups/127639125043271/)
		1. Largest group in the world
	2. How to use it?
		1. Ask questions
		2. Bring up dilemmas
		3. Post interesting links
		4. Announce relevant events
		5. (everything of interest to those passionate about Software Architecture)
2. [Software Architecture Newsletter](https://memilavi.com/newsletters)
	1. Latest news
	2. Reports
	3. Articles
	4. Trends
	5. Recommendations for software architecture
	6. Past editions

### Who Is This Course For? ###
1. Architects
2. Development Background
	1. Developer
	2. Team Leader
	3. Dev Manager
3. Preferably with some experience
	1. With development
		1. There is no actual coding 
4. Preferably with Backend Development Experience
5. Anyone who wants to learn about software security

### What This Course is NOT ###
1. It is not a comprehensive hacking course
	1. Not ethical
2. It is not all-encompassing cyber security course
	1. There is some content found in the cyber security world
		1. Black hat
		2. White hat
	2. This is not for becoming a cyber security expert
3. It is not a guide for script kiddies
	1. This course is not for downloading and using hacking scripts
4. It is not a tour of the dark net
	1. Not for evil place

### An Update for Udemy Students ###
### Architects and Security ###
1. Security is a broad subject
	1. Not all are relevant to security architects
2. Three segments
	1. Security topics that software architects can completely ignore
		1. Example: Physical access to building
	2. Be aware of / recommend (but not directly responsible for)
		1. Examples: (opinion counts but not directly accountable for it)
			1. Type of OS
			2. Type of firewall in the network
			3. ...
	3. Decide and Design - security topics an architect is in-charge of
		1. Topics directly related to architectural security
3. We will cover all types
	1. Red square - outside influence but good to know about
	2. Orange square - somewhat relevant and we might be asked for contribution
	3. Green square - directly responsible for - to make most important decision about
		1. On which we are measured

### What We Will Talk About in This Course ###
1. Agenda
	1. Welcome
	2. Introduction to Software Security
		1. What is software security
		2. What do we want to protect against
	3. Secure Architecture Process
		1. 5 steps of architecture process
			1. What each step includes
	4. Threat Modeling - First step - what we are exactly afraid of in our system
	5. Secure Architecture - Second step - we are interested in this
	6. Application and Data Security - Topic of next section
	7. SDLC - Third Step
	8. Testing - Fourth Step
		1. Test types that are security related
	9. Production - Fifth Step
		1. There are security tasks even after the system has gone to production
	10. Case study
		1. We are going to run the whole process on a specific system to see what we end up with
	11. Conclusion
		1. What's next

## Section 2: Introduction to Software Security ##
### Introduction ###
1. It is huge
2. What are we talking about?
3. What is Actually Software Security?
	1. Examples:
		1. Someone logs into the system with fake identity
		2. The system is attacked using DDOS
		3. No! I didn't really perform this action! (identity stolen)
			1. They do not capture the essense of software security
				1. They are means but those are not what security is all about.

### What is Software Security? ###
1. What is it?
	1. The right question is:
		1. What do we want to protect using software security?
			1. Using software security, we protect against:
				1. **Data Loss**
				2. **Disruption of Service**
				3. **Data Leak**
				4. **Data Inconsistency**

#### Data Loss ####
1. It means: Sensitive data is lost due to security breach
	1. Due to a vulnerability in the system, someone hacked the system and made an important data disappear
		1. ie. An attacker gains access to the main DB and deletes records
			1. Example: VFEmail - formatted including backups

#### Disruption of Service ####
1. It is when the system activity is disrupted due to attacker's actions
	1. The attacker just wants the system to go down (they don't need any data)
		1. Reasons
			1. Ideological conflict
			2. Competition
			3. State origin hostility
	2. Examples:
		1. Attackers orchestrate denial-of-service attack, taing the service down
			1. Example: DDoS - Dyn was brought down (Twitter, Spotify, ...)

#### Data Leak ####
1. It occurs when sensitive data is stolen and made available to non-authorized recipients
	1. Attackers gain access to the DB and steal credit card info
		1. They can empty bank account
			1. Example: Marriott Hotel Brand

#### Data Inconsistency ####
1. Occurs when data is manipulated by non-authorized attackers and become inconsistent
	1. Example: Attackers impersonate as someone else and perform unauthorized actions
		1. Someone pretended to be someone else and performed an unauthorized operation
	2. These attacks are difficult to locate
		1. They are not reported to the press

### Software Security Terminology ###
1. Software Security includes new terminology (widely used)
	1. Used in a lot of security-related discussions
2. It is important to understand them before conducting said discussions
	1. As a Software Architect, I am going to participate in security related meetings and discussions
		1. Our opinion matters
3. Common terms:
	1. **Threat** - It is an event that, if happens, will lead to a security incident in the form discussed earlier (data loss, disruption of service, data lead, data inconsistency)
		1. Example:
			1. SQL Injection - Most common threat
				1. It allows attacker to gain access to confidential data stored in the database
					1. Solution: System code must be protected against such attacks
			2. DDOS Attack
				1. A lot of systems are susceptable to it
				2. They have hard time protecting against it
	2. **Attack** - An actual execution of Threat run by an attacker(s)
		1. Example: A malicious user enters SQL-Injection-bound input
			1. Causing SQL injection attack on the system
		2. Example: A group of attackers orchestrate DDOS attack
			1. Actual execution
		3. **DDOS Attack**:
			1. It is a special kind of attack used to overload sites and take them down
				1. Stands for: Distributed Denial of Service
					1. Distributed nature makes it dangerous
						1. Distributed - Geographical distribution of the origin of the attacks
						2. Bringing servers down - Denial of Service
	3. **Vulnerability** - It is a problem in the system that can be used by attacker to execute an attack on the system, and make it compromised
		1. When a threat is realized by an attacker, it is being carried out using non-vulnerability
			1. The more vulnerable the system, the more it is prone to security breaches
		2. Example: Misconfigured Firewall that exposes internal systems to the public web
			1. Systems were never designed to be exposed to the public web and they do not have the defense mechanisms expected from public facing system
				1. They are easy targets for hackers
		3. **Misconfiguration** - it is one of the most common types of vulnerabilities
			1. It must be thoroughly investigated to avoid breach
	4. **Authentication** - With it, we establish the identity of a user (human or not) based on reliable mechanism [designed to provide authentication]
		1. Example:
			1. Username/ Password authentication
			2. SMS for authenticating user using a phone
			3. Biometric identification - fingerprint, face identification, ...
	5. **Authorization** - It is used to establish what a given user is allowed to do in the system
		1. Example:
			1. A user X is allowed to instantiate a new service request
			2. A user X is NOT allowed to delete an existing service request
		2. It establishes, what the user can and cannot do
	6. There are a lot of other terms but the above are enough for our purposes

### Who is Responsible for the Security? ###
1. Typical organizational chart:

								CIO
		
		CISO		IT Services		Architect	Project Manager
		(Chief									Dev Manager
		Information									Developers
		Security									QA
		Officer)

	1. CIO - Responsible for all the IT aspects of the company
	2. CISO - New title embraced only recently
		1. Responsible for setting the security strategy in the company's IT
		2. He is not the sole owner of the security aspects of IT
			1. He however has an imprtant role
		3. Many companies do not have this role
			1. Solution: The others should fill in
	3. IT Services
		1. Responsible for servers, networks, databases, ... (lower level IT services the developers need to test and deploy their code)
	4. Architect
	5. Project Manager
	6. Development Manager
	7. Developers
	8. QA

#### CIO ####
1. Usually does not have an extensive knowledge of software security
	1. Makes sure everyone is aware of security
	2. Prioritizes
		1. Can make security awareness, high priority
			1. Required to ensure team takes care of security
	3. CIO's guidance is vital for software security of the organization

#### CISO ####
1. He sets security strategy of the organization
	1. He decides the threats we want to protect from
	2. He decides the ways to do that
	3. (any other strategical decision regarding software security)
2. Without this role, we don't know what should be done at the org level

#### Architect ####
1. **Designs secure architecture**
	1. If the architecture is not secure, nothing else will work
		1. Even if code adheres to all the security guidelines, it wont work if the architect neglected to integrate security into the architecture
	2. **Architect is vital to the security**

#### IT Services ####
1. They need to Implement Secure Operations
	1. Patch servers
	2. Setup Firewalls
	3. ...
2. The system is extremely vulnerable without their contribution

#### Project Manager ####
1. Ensures security awareness:
	1. Not a technical function is responsible to **raise awareness to the security aspect of the system** and ensure that the **aspects are part of the work plan** and are implemented

#### Dev Manager ####
1. Responsible to train developers
	1. He is the most senior developer around
		1. He should have a rich experience developing secure systems and provide guidance to junior developers that will write the code

#### Developers ####
1. Developers secure the code
	1. They must develop a secure code
		1. If not, the system is exploitable

#### QA ####
1. Responsible for performing security-related testing
	1. Without these tests, we wont know whether the system is actually secure or a pile of code and data, waiting to be hacked.

#### Everyone ####
1. When it comes to security, everyone is responsible

## Section 3: Secure Architecture Process ##
### Introduction ###
1. Process that will make the system secure
	1. We discuss the process that makes the system secure
		1. A methodological, and well-defined process
			1. Architect must follow this and insist on
2. Secure Architecture Process
	1. A well defined process for ensuring the system is as secure as possible
		1. The process cannot ensure 100% secure system
			1. It does not exist
				1. It, however, helps achieve a very secure system
	2. The process goes through all the system's phases
		1. The process begins at a very early phase in the system's lifecycle and never ends
	3. The process should be led by the project manager / dev manager
		1. Not led by the Architect because most of the tasks in the process are the architect's responsibility
			1. The architect is responsible for only one task in the process
				1. **Secure Architecture**
	4. Architect should be involved in all the stages in the process
		1. Reasons:
			1. Input is invaluable
				1. We will be able to contribute to steps that are not under my direct responsibility and our opinion should be heard 
			2. A great opportunity for me to learn more about the system by listening to the other stakeholders and hearing what they have to say about the system's security requirements
				1. We will be able to design the security architecture that best fits the needs
	5. The process has a total of 5 Stages:
		1. For each one we'll describe
			1. Goal - What we want to achieve in each stage
			2. Participants - Who are the stakeholders who take place in each stage
			3. Complete details about execution (of the stage)

#### Secure Architecture Process ####
1. Stages:
	1. Threat Modeling
	2. Secure Architecture
	3. SDLC
	4. Testing
	5. Production
2. Quick overview

### Threat Modeling ###
1. It is the process for identifying potential threats for the system
	1. It is used to try and define what we need protection from
2. We prioritize mitigation measures and decide what actions to be taken to defend the system
3. It has a great effect on the work plan
	1. The decisions made are going to affect what we are going to put emphasis on when designing and developing the system
4. The threat modeling involves almost everyone in the team
	1. Every input counts
5. It might utilize formal methods or tools we will review in the deep dive section
	1. Most orgs do not use these methods or tools

### Secure Architecture ###
1. It is the **most important step for the architect** (yay!)
2. It is based on the security perimeters paradigm
	1. What is it?
		1. Later
3. Goal of the phase: To integrate security defenses into the core architecture
	1. Not handle them afterwards
	2. Integrating the mechanisms from the beginning will make our architecture:
		1. More coherent
		2. Easier to understand
		3. More secure
4. Secure architecture touches all aspects of the system (most important phase)
	1. Example:
		1. Components
		2. Code
		3. Database
		4. Network
		5. ...

### SDLC ###
1. SDLC - Secure Development Life Cycle
	1. It refers to the actual development of the system
		1. In this phase, the developers write the actual code based on the secure architecture we designed and 
		2. **Implements code-level security measures**
			1. SQL Injection protection
			2. XSS (cross-site scripting)
			3. ...

### Testing ###
1. One of the most important phase
	1. It makes sure the system is actually secure and not an easily hackable pile of code
2. In this phase
	1. Testing team implements security-oriented testing
	2. Analyses the results
	3. The results are compared to the Threat Modeling items discussed earlier to make sure the specific threats we want to protect from are actually avoided in the system
	4. If the tests are successful, we move on to the next phase

### Production ###
1. The cycle doesn't end when the system is in production in the case of security
	1. Even when a system is in production, there is always what to do regarding security
2. Tasks in production
	1. Continous monitoring
		1. To ensure no attack is run against our system
	2. Get up-to-date
		1. Keeping the system upto date
			1. Example: If there are new security patches to the OS, they must be installed

## Section 4: Threat Modeling ##
### Introduction ###
1. Goal: Identify potential threats for the system and discuss ways to mitigate them
2. Participants:
	1. Progect Manager
		1. To manage and coordinate the threat modeling discussion
	2. Architect
		1. To give valuable input
	3. Dev Manager
		1. To convey the main point of the threat modeling to the developers
		2. To contribute based on experience
	4. System Analyst
		1. To provide any information relevant to system's functionality
	5. CISO
		1. To set the security policy of the IT organization and contribute to the discussion
	6. IT (OP)
		1. To learn about the process, the system, and security aspect
	7. Developers (OP)
		1. To learn about the process, the system, and security aspect
	8. QA (OP)
		1. To learn about the process, the system, and security aspect
3. It is a very important step in the process
	1. The other steps are pointless without this step
		1. We can't design protection against something we don't know
4. This phase belongs to the second category
	1. It is not led by the architect
		1. Not the main participant
	2. It is very important for architect to take part in this stage
	3. **Input from the architect will greatly help others**
	4. **It is a great opportunity for the architect to learn about the system and its intricate details**

### What is Threat Modeling ###
1. It is the process of identifying potential threats for the system
	1. It is done once, but might be repeated later
		1. Timing - later
2. For the threat modeling to be effective, it must be very methodical
	1. It is not a simple brainstorming
		1. It must be a well-defined process with known talking points & well defined results
3. For the threat modeling to be effective, we listen to everyone
	1. Everyone's input is welcome
		1. We can't really know with a scenario no one has thought about
			1. It is important to listen to everyone's opinion and suggestions
4. Questions to answer:
	1. How do we do threat modeling?
	2. How do we make sure it is as effective as possible?
5. A good threat modeling is based on 4 core questions:
	1. **What do we build?**
	2. **What can go wrong?**
	3. **How can we mitigate that?**
	4. **Did we succeed?**

#### What Do We Build? ####
1. We should describe the main functional and non-functional requirements of the system
2. If there are any known technical or architectural details - we need to specify them
	1. They will play important role later on
3. Example:
	1. We're designing an HR system to manage the employees' data, including salary, vacations, etc.
4. Think about what is the main threat we want to protect against

#### What Can Go Wrong ####
1. We need to describe what are the main threats the application might face, based on:
	1. Factors affecting the answer
		1. Sensitivity of the information the system stores
			1. If the system stores sensitive info such as:
				1. Credit cards
				2. Financial info
				3. ...
			2. We don't want the info to leak to un-authorized recipients
		2. Location of the system
			1. If a system is stored in a country known for high cyber-crime rate, we need to take that into account
		3. Competition
			1. When we face competition, our competitors might go into dark places, employing the hackers to take our system down or steal our precious data
		4. Any other factor that might be relevent...
2. Example:
	1. "Since we store sensitive data in the system, we want to make sure it won't leak"
		1. Employee's salary - most sensitive
			1. We don't want it leak to other organizations
3. A threat modeling never does with single threat (in real-life, we are going to have a lot of threats)
	1. However, for simplicity, we can discuss one threat

#### How Can We Mitigate That ####
1. Important questions:
	1. How can we avoid the threats?
	2. What steps can we take for that?
2. Steps:
	1. First we discuss mitigations to protect against the potential threats
		1. Research various mitigations methods if needed
			1. Ensure the mitigation selected is the optimal one
				1. Example: For encrypting data, there are many ways to do so
					1. The team should research various options and come up with a concrete implementation to ensure the best solution is applied
	2. Make sure to include the mitigations in the project's work plan
		1. The team might find that there is no time to implement security measures
		2. The system goes live without them
		3. It should be avoided at all costs
	3. If the dev team does not know how to implement it - we need to design a training plan for them
		1. A lot of developers are not well-versed with security related tasks and may not be familiar with implementing them
			1. Example: SQL injection defense
			2. Solution: **Schedule a training session and teach them**
				1. **The architect would often be asked to conduct the training as I am the most proficient with regards to security**
3. Example:
	1. "All the sensitive data is going to be encrypted. In addition, database access will be given on a least-privilege basis only"
		1. If someone, somehow steals the data, he wont be able to decrypt it and understand it
		2. We can design the access to the database so that only select people and software will have access to it
			1. Even those who have access will have the least privilege possible
				1. Instead of a comprehensive admin access
					1. Example: A software will be able to read tables from the database but will not be able to delete the tables, or chang the schema of the database

#### Did We Succeed ####
1. It is a different plan to implement the plan and make sure it actually works
2. Procedure:
	1. We need to design tests to validate the solution designed
		1. We must be able to ensure the solution actually works
	2. Usually, the test will be carried out in the testing phase
		1. But sometimes also during development
3. Example:
	1. "We're going to ask a security expert to extract and decrypt the encrypted data and see if she succeeds."
		1. We are going to ask a hacker to try and hack the sytem
			1. If it succeeded, we did a bad job
			2. If not, we are good to go
4. **Trying to simulate a hacker's behaviour and see if our system is exploitable is a great pattern for security testing**
5. Summary:
	1. Steps:
		1. **What do we build?**
			1. HR system to manage the employee's data, including salary, vacations, etc.
		2. **What can go wrong?**
			1. Since we store sensitive data in the system,we want to make sure it won't leak
		3. **How can we mitigate that?**
			1. All the sensitive data is going to be encrypted. In addition, database access will be given on a least-privilege basis only
		4. **Did we succeed?**
			1. We're going to ask a security expert to extract and decrypt the ecrypted data and see if she succeeds
6. Example:
	1. Steps:
		1. What do we build?
			1. Mobile game for kids, where they can learn English
				1. Different audience
				2. Different skils
		2. What can go wrong?
			1. Since it's a world-wide system, with a lot of competition, we're afraid of DDoS attacks
				1. HR system can go down sometimes but does not hurt anybody
				2. This system needs to be up all the time
					1. If it goes down, the kids will switch to one of the many other competitors and we will lose the business
						1. We must not allow the system to go down (and give advantage to our competitors)
		3. How can we mitigate that?
			1. Two-fold solution
				1. Using state-of-the-ark firewalls and app gateways
					1. They must have built-in DDoS protection
						1. The systems are built having DDoS attacks in mind and they are our first defense line
				2. Having DR sites for when the app is down
					1. DR - Disaster Recovery site
						1. Located in a different region that will go up if there is a major shut-down in our primary region
						2. If our server farm is attacked and goes down, we will use the second farm
			2. The two defense lines are quite common for DDoS attacks and can provide reasonable protection against such attacks
		4. Did we succeed?
			1. Simulate an attack under controlled and monitored condition
			2. We're going to conduct massive, geo-distributed load tests, simulating some previously-executed DDoS attacks, and see what happens
				1. By simulating the attacks under our on conditions while looking closely at all the components of the system, especially Firewalls and DR, we can see how the system behaves under extreme conditions
					1. If there is any problem, we will find out immediately
2. Result of Threat Modeling
	1. After going through all the questions and discussing all the answers, we need to have something to work with
		1. **Threat Modeling Document**
			1. It documents all the steps taken in the process
				1. It mainly documents the last 3 questions (emphasis)
					1. What can go wrong?
					2. How can we mitigate that?
					3. Did we succeed?
				2. The first question "What do we build?" is already documented in the system-analysis document
	2. Who prepares the document?
		1. Project manager decides who prepares the document
			1. **Usually not the Architect**
				1. It could be:
					1. **Development Manager**
					2. **One of the Developers**
					3. **Project Manager** - if he is technologically inclined
	3. Sometimes the team might prefer loading the threat modeling to a **dedicated tool** & not produce a document
		1. Such tools exists but not common

### Conducting Threat Modeling ###
1. How to conduct the threat modeling?
	1. We talked about the what...
	2. We need to talk about the When and How

#### When ####
1. What is the right time to conduct the threat modeling?
	1. Three answers
		1. At the beginning of the project
			1. When there are functional and non-functional requirements - best timing for threat modeling
				1. We know what the system should do
					1. We can analyse it and talk about potential threats
			2. If we have some basic architecture, it is an important addition to the discussion
		2. After major changes
			1. That might present new security risks
				1. It is a good practice to conduct threat modeling again
				2. We might find out that the new features contain vulnerabilities we hadn't thought about and we need to handle them before going to production
		3. Following security incident
			1. We need to conduct threat modeling to find out, what went wrong
				1. This is a living proof that our previous modeling wasn't good enough
					1. We need to have a better, tighter security
						1. Threat modeling is the basis for improving our security

#### How ####
1. Procedure:
	1. It is done in a meeting
		1. With a whiteboard
			1. We can write down our thoughts and insights
	2. It must have a designated supervisor
		1. The supervisor will manage the meeting and will make sure we are following the methodology
		2. The supervisor who is a project manager or a development manager must have a clear agenda
			1. Includes the 4 questions
			2. Includes any other items that supports the discussion
	3. It must have someone who summarizes the discussion
		1. The final threat model document is based on the comments prepared by this person

### Threat Modeling Methodology ###
1. It is usually done using free-form discussions
	1. The participants sit in a meeting room and discuss the threats, mitigations, and validations in the form of a brainstorming
		1. Usually works quite well
			1. But some methodologies exist that formalize the process
				1. Using the methodologies, the threat modeling is not done as a free-form discussion but is centered around a well defined talking points with clear input for each one of them
				2. Most organizations don't use the methodologies but stick to free-form discussion method
	2. We're going to have a quick look
		1. Not a comprehensive overview
2. Methodologies:
	1. STRIDE - most matured
		1. It was developed in 1999 and used by Microsoft
			1. Other cyber-security companies and other orgs
		2. Full form: (Each one represents a potential threat to the system)
			1. Spoofing
			2. Tampering
				1. Data Inconsistency
			3. Repudiation
			4. Information Disclosure
				1. Data Leak
			5. Denial of Service
				1. Disruption of Service
			6. Elevation of Privilege
		3. In the modeling process, the 6 threats are discussed against flow diagram of the system
			1. The diagram can be generated manually or by STRIDE supported tools (next)
		4. When a potential threat is found, a mitigation plan is formed
			1. Similar to the traditional threat modeling process
		5. The method is used by some groups in Microsoft and Cyber-Security companies
	2. Other Methodologies: (they are not widely used)
		1. PASTA
		2. DREAD
		3. Attack Tree
		4. CVSS
		5. ...

### Threat Modeling Tools ###
1. Threat Modeling usually utilizes:
	1. Whiteboard
	2. Word-processing tools
		1. Microsoft Word
		2. Google Docs
2. Some tools exist to help with the process
	1. None is widely used
3. We're going to take a quick look at two tools
	1. **Microsoft Threat Modeling Tool (TMT)**
		1. It is used for a complete Threat Modeling Process
		2. It contains vidual designer to build Data Flow Diagrams (DFD)
			1. The diagrams are often the basis for threat modeling analysis
		3. Looking at the diagram, it becomes easier to pinpoint potential vulnerabilities in the system
		4. It uses the STRIDE methodology
			1. For each element in the designer, a STRIDE threat can be attached, and a mitigation plan is designed for it 
		5. It was designed for developers
			1. They will feel extremely comfortable using it
				1. Non-technical users might have a harder time
		6. It is a stand-alone app
			1. Requires installation
	2. **Threat Dragon**
		1. New app
			1. Still in early stages
		2. Developed by OWASP
			1. Open Web-Application Security Project
				1. A leading community for security related information on the web
		3. Electron-based
			1. Can be installed locally or used as a web app
		4. It has a visual designer for DFDs
		5. It is based on the STRIDE methodology
		6. Diagram:
			1. We can select each element
			2. Click the frash icon
			3. Enter threat details in accordance with STRIDE methodology

### Summary ###
1. It is a process for identifying potential threats for the system
2. It should be conducted early in the project lifecycle
3. A good threat modeling is based on 4 core questions
	1. What do we build?
	2. What can go wrong?
	3. How can we mitigate that?
	4. Did we succeed?
4. Almost everyone in the team must be involved
5. We can utilize formal methodologies and tools
	1. Not a must

## Section 5: Secure Architecture ##
### Introduction to Secure Architecture ###
1. It is the second stage in the process
2. This stage is the most important stage for us, the Architects
	1. This is where our expertise as software architects and security experts manifests itself
	2. We will spend most time on this stage
	3. We are going to deep dive into topics relevant for it
3. Threat modeling and software architecture stage are closely related to each other
4. Goal of the stage:
	1. Design secure architecture based on the threats defined in the threat modeling stage
		1. We want to use the measures needed as analyzed in the threat modeling stage
			1. The system will be as secured as needed
			2. The system must not be bloated and too complicated due to unnecessary measures
5. Participants:
	1. Architect
		1. Only crucial person
			1. He is the one who is going to design the architecture
				1. There might be more functions useful in this stage (optional)
	2. Dev Manager (OP)
		1. Can provide valuable input into team's current capabilities
		2. Can provide experience from other projects that can be integrated into the architecture
	3. System Analyst (OP)
		1. A great source of info regarding system's requirements
			1. Knowing the system requirements is the key to an effective architecture
	4. CISO (OP)
		1. Good idea to involve CISO
			1. Reasons:
				1. He should be aware of what is going on in the company regarding security
				2. He might convey important info regarding security standards and procedures that we can use
					1. Will save time
	5. IT (OP)
		1. Can be consulted for all that is IT
			1. Supported OS versions
			2. Type of virtualization mechanism used in the org
			3. Network devices
				1. Firewalls
				2. ...
	6. Developers (OP)
		1. Be as open and as transparent as possible while designing the architecture
	7. QA (OP)
		1. They need to know what kind of testing is expected from them for testing the system
			1. We can tell them in the earliest stage
6. We as architect are responsible to decide and design everything in it
	1. We are responsible for the success and failure of the architecture
7. We need to pay close attention to what we are going to learn in the section
8. **The Architecture Process (standard)**
	1. **Understand the System's Requirements**
	2. **Understand the Non-Functional Requirements**
	3. **Map the Components**
	4. **Select the Technology Stack**
	5. **Design the Architecture**
	6. **Write Architecture Document**
	7. **Support the Team**
9. The security architecture should be fully integrated into the architecture process
	1. Where does the secure architecture fits it?
		1. Main Security Work is done in **Design the Architecture** phase
			1. **Most of the security architecture work of an Architect is at the component level**

#### Result of This Stage ####
1. Secure Architecture Document
	1. It contains all the information related to the security of the architecture
		1. It is not a standalone document
			1. It is a part of the overall Architecture Document prepared by an Architect as a means to document the whole system's architecture
	2. The document must take into account the threats defined in the Threat Modeling Phase
		1. The threats must be clearly documented when describing the security architecture
2. But First
	1. Let's have a review of Software Security
		1. We must have a good background of security before getting into secure architecture

### Security Perimeters ###
1. Software Security 101
	1. Software Security is done using the Security Perimeters paradigm
		1. Security Perimeters
			1. We look at our software as a collection of perimeters need protection
				1. Each one confined in the perimeter of the outer one
					1. If a hacker breaks through the first perimeter, he will find the next one posing new, and different challenges for him
						1. Somewhere along the road, the hacker will have enough and will stop to hack the system
		2. Perimeters
			1. Physical (outermost perimeter)
				1. For hackers that try to hack into the system will encounter this as the first perimeter
			2. Network
				1. A hacker next needs to gain access to the network through which he can reach the system
			3. Platform - The computer on which the system is installed
				1. The computer can also be protected from attacks
			4. Application (on the platform) - most important for Architect
				1. DDoS attacks - application is the target
			5. Data (innermost perimeter) - most important for Architect
				1. It is the most protected one
					1. All the other perimeters need to be hacked to reach it
		3. Some diagrams have 7 perimeters
			1. The 5 perimeters are simpler
2. To make the application and data security as reliable as possible, the architect must be familiar with other perimeters as well

### Physical Security ###
1. The only perimeter that an architect can ignore
	1. However, it is a good idea to know where the system physically lives
		1. It wont affect the architecture though
2. What is it?
	1. The perimeter that controls the access to the physical hardware or where the hardware is hosted
		1. Usually employed at the entrance to data-centers or server farms and in secure rooms inside building
	2. Usually implemented using physical elements
		1. Keycard
		2. Building control access
		3. Locks
		4. etc.
	3. Example:
		1. Microsoft's Azure's Datacenter
			1. Physical Security
				1. Two-factor authentication with biometrics
				2. One defined access point
				3. Perimeter fencing
				4. Background checks
				5. ...
			2. [Full Presentation](https://www.slideshare.net/karlots/azure-scurity-architecture-88395266)

#### Physical Security and the Architect ####
1. The architect usually not involved in physical security aspects of the software
	1. Usually it's given
		1. An architect works in an environment that won't change
	2. It's good to be aware of it, if nothing more
2. The architect should strive to be as familiar as possible with his environment even if he cannot influence it in any way

### Network Security ###
1. An architect must be aware of and actively participate in (most probably)
	1. It is not an area of responsibility
		1. An architect definitely needs to know
			1. What is going on with the network?
			2. How is the network protected?
			3. What segmentation is defined within it

#### Network Security ####
1. Two aspects
	1. **Access Control**: The ability to control the access to the organization's network
		1. Especially when defending against threats such as data leaks or data exposure
		2. The key to data-protection is to heavily guard access to the data
			1. This is what this aspect is responsible for
	2. **Reliability**: To make sure the network stays up and running and reliable even under heavy attacks (DDoS...)
2. Other aspects:
	1. Some more aspects we won't discuss here
		1. DNS Spoofing
		2. ...

#### Access Control ####
1. Usually performed by authentication engine
	1. Such as: Active Directory
		1. Such authentication engines provide robust, secure, and advanced authentication solution
		2. They can be used as org wide user-store
		3. They are extremely flexible for authentication requirements
		4. The authentication engines allow various types of authentication
			1. User/Password
			2. Biometrics
			3. Text
			4. MFA
				1. Multi-Factor Authentication
				2. It is widely used for accessing sensitive data and we are familiar with it
				3. It means more than one authentication proof
					1. Example: username/password + code received as text to the phone
						1. Bank account
						2. GMail
						3. ...
				4. Very effective weapon against access control violations

#### Reliability ####
1. How do we ensure that the network is reliable and can withstand DDoS attacks and other kinds of loads
2. Solution categories:
	1. **Firewall** - It protects network from unauthorized requests and is used as the first line of defense against DDoS attacks and other malicious activity
		1. It can come as a physical device installed in the network OR
			1. They are considered more robust and effective
				1. Large orgs will go for them
			2. Popular firewalls:
				1. Fortinet
				2. F5
				3. Cisco
		2. It can come as a software installed in a server
	2. **Segmentation** - A company network need not be a single monolith network allowing every device to access every other device
		1. We can have a collection of smaller networks, communicating with each other via well-defined tunnels
		2. We can define who can talk to who
			1. Example: Sensitive DB
				1. It is a good idea to put it in a dedicated segment (often called VNet or Subnet)
				2. Set up a specific guarded tunnel between it and other network
					1. Only authorized device can access it
		3. **It is quite a popular pattern**
		4. Used in large orgs using large network
	3. **IPS - Intrusion Prevention System**
		1. Devices or software sit behind the firewall and scan and analyze every communication that enter the network in search for anomalies
			1. Anomalies:
				1. Burst of communication from an un-known source
				2. A packet of bytes containing illogical content
				3. AI based algorithms that look for more anomalies (sophisticated)
			2. When such anomalies are detected
				1. The communication is blocked
				2. Notification is sent
				3. ...
		2. Popular implementations:
			1. From:
				1. **Paloalto**
				2. **Fireeye**

#### What is the Role of an Architect in a Network Security Aspect ####
	1. The architect should be aware of the network security in the org
		1. Reason: Some components, related to the network security, might affect the architecture
			1. Examples:
				1. Firewall that filters specific content that exists between two segments or VNets in the network and prevents specific content from passing between the segments
				2. Segmentation between two VNets that prevents certain components from communicating with each other
				3. Architectural decision
					1. We don't want to design an architecture that relies heavily on distributed cache to find out that the application servers cannot access the distributed cache's server since they are deployed in a segment they don't have access to
			2. The architect might recommend some network security aspects:
				1. Recommending adding firewall in front of the (newly designed) system
				2. Segmentation in the network to further protect the sensitive data
					1. The architect's role is pro-active
						1. Makes system more secure and I a better archtiect

### Platform Security ###
1. We must be aware of or recommend as an architect
	1. It is not under an architect's responsibility
	2. **There are things that we should definitely be aware of as an architect**
2. What is platform security?
	1. The security of computers, VMs, etc
		1. Security of the underlying infrastructure, our system is going to use
	2. This is a crucial security perimeter
		1. What if VM our system runs on is hacked?
			1. Attackers will get access to all the resources in the machine (especially the disk)
				1. The amount of damage is enormous
				2. There is a possibility of shutting off the machine altogether taking down our application
		2. Hence we want our compute resources to be definitely secure
	3. Sometimes, this paremeter is called **Operations security**
3. Done by:
	1. How do we ensure our platform is secure?
	2. There are some security measures we can apply that will help us with that
		1. **Use modern OSs** (no more Windows 2003/XP)
			1. The underlying OS must not be outdated and unsecure
				1. All OSs do not receive security patches
				2. All OSs do not protected against the modern methods of hacking
			2. Use modern OSs that are supported
		2. **Patch management**
			1. It is probably the best method to keep the OS upto date
			2. The most important kind of patches are:
				1. Security patches
				2. Example: Ubuntu security notices
					1. A new notice is released almost everyday
					2. The security patches are not released everyday but they mitigate security problems detected up unto the release date
					3. **If we miss a patch, we are going to have a lot of security holes in our OS**
						1. Solution: **Ensure IT have a well-defined patch management policy in place**
							1. One of the best techniques to keep the OS secure
		3. **Up-to-date Anti Virus**
			1. It is imperative to have one on the server
				1. An up-to-date one
			2. Similar to OS, anti-virus software also have patches with updates on recent viruses and malwares detected
				1. It is a good practice to patch them on time
		4. **DLP (Data Loss Prevention)**
			1. A special type of software installed on a server to monitor everything that is going out on the server
			2. It detects data that must not be leaving the server and blocks its transmission
			3. It also alerts the operators that a potential data leak attack has been detected
			4. It is less commonly used but it still has its use

#### Platform Security and the Architect ####
1. What does an Architect do with this perimeter?
	1. The Architect should be aware of the platform security
		1. Some measures might even affect the architecture
			1. Example: Anti-virus software that blocks legitimate files, uploaded to the system
		2. **The OS version is often part of the architecture**
			1. It is quite common for architect to dictate the exact version of the OS used
				1. The IT must make sure the version is supported
				2. The IT must make sure a patch management policy is in place for it
			2. **It is a good practice for an architect to make sure the unerlying OS is supported and protected (patched, anti-virus)**
				1. The IT can stand behind the OS

## Section 6: Application and Data Security ##
### Introduction ###
1. As architects we handle application and data security
2. We are at the second stage - Secure Architecture stage
3. We as architects are directly responsible for the two perimeters
	1. We are responsible for making the design as secure as possible
		1. If security problems are found in the network, the IT guys will try to understand why firewall did not block the attack or why there was no segmentation to make the attacker's life harder
		2. If system is not secure, the architect and team is the one the client will come to with questions
	2. We must make sure as much as possible is implemented in the system
4. With the Application and Data, we are going to decide & design the architecture
	1. We are going to consult with other professionals
		1. IT team
		2. DBA
		3. ...
	2. We are going to design the system and it is our responsibility
5. The Architect is responsible for both application and data
	1. The architect must set the guidelines for the team (DBA say) to follow
	2. This is where the main work happens
	3. Everything we have learnt is a great background to this perimeter and gives us the context we are working
6. In threat modeling, we have modeled a few threat types
	1. In this section, we can see how our architecture deals with all the types
7. **Security aspect of the architecture touches all the layers of the system**
	1. **APIs**
	2. **Code**
	3. **DB**
	4. **External mechanisms**
		1. Every layer has security concerns that we need to handle
		2. Security is a serious issue that needs to be handled seriously

#### How are We Going to Do That ####
1. We are going to discuss security topics
	1. Each topic covers a specific security aspect of the software
		1. Example: 
			1. Authentication
			2. Secure code
			3. ...	
		2. **For each topic we explain**
			1. **What it is**
			2. **What it's for**
				1. What threats the topic protects from
			3. **How to design / implement**
				1. What is it's inner architecture and how does it fit in the grand architecture of the system
			4. **Code examples**
				1. No actual coding

### Authentication ###
1. **What it is**
	1. It is an answer to the existencial question
		1. Who are you?
	2. It is a process of verifying the identity of a thing
		1. Thing
			1. Human
			2. Computer
			3. Software
			4. ...
		2. Example: IoT device communicating with server is who it says it is
	3. What it's for
		1. Why is it important when talking about security?
			1. When knowing who uses the system, we can:
				1. Find out what he's allowed to do
				2. Allow / deny certain actions
				3. Log all activities, the user performed for future research
				4. We can prevent data leak, data inconsistency
					1. If an unauthorized user cannot log into the system, it becomes hard for them to steal data or manipulate it
			2. It is usually the first line of defense in the application peremeter
				1. It is the defense the attacker will meet after breaking into the network

#### Authentication Design ####
1. Authentication mechanisms include at-least three components
	1. **User Store**
		1. A database storing information about users, allowed to log into the system
		2. At minimum the database holds user identification and some authentication data
			1. Username & password
	2. **Authentication Engine**
		1. The engine that does the actual authentication
			1. It is responsible for verifying if a user says he/she is X, then he/she is in-fact X
	3. **Software Component**
		1. It is not directly related to authentication mechanism
			1. It is enjoying the result of the authentication
		2. After authentication is done, the software component receives the details of the authenticated user and can know who the user is
			1. It uses the data for it's own needs
				1. Logging the user activity
2. How does it work?
	1. What is the authentication flow?
		1. There are at-least 2 authentication flows:

#### Authentication Design Flow #1 ####
1. steps:
	1. A user first enters authentication data (username/password)
	2. The authentication engine goes to the user store and verifies that the user with the given authentication details really exists in the database
	3. If such a user is found, the authentication engine approves the user and sends its details to the software component so that the component will know who it is working with
		1. Software component doesn't know anything about authentication mechanism
			1. What is the authentication engine
			2. Where is the user store
			3. What is the authentication process
		2. Software component only knows that the user is authenticated and it can trust the data received

#### Authentication Design Flow #2 ####
1. Steps:	
	1. User first goes to the software component (application) and enters his authentication details (username/password)
	2. Software component sends the authentication detials to the authentication engine
	3. The authentication engine goes to the user-store and verifies the user actually exists in the database
	4. If the user exists, the authentication engine sends the user's details to the software component
2. Differences:
	1. What is the starting point of the authentication process.
3. Historically, most softwares employed the second flow
	1. In recent times, the trend is to let the authentication engine to handle all aspects of the authentication and given a capable auth engine, the first flow is the preferred approach

#### More Flows ####
1. Component self-authenticates
	1. We don't want any external engine
	2. Not a recommended approach
		1. It could make sense for a small, standalone software, operating in an env where no authentication engine is available
2. Authentication Engine uses another engine
	1. If the user-store and authentication engine working with it, are located in another environment and we don't want to expose the user store to new more public environment
		1. Hybrid idenity mechanism
	2. Example:
		1. Active-Directory and AD-Connect
			1. It allows to connect to on-premises active directory
			2. User-store is located on premise
			3. Azure AD works with on-premise AD for the authentication
	3. This is not very common

#### Architectural Considerations ####
1. There are a few questions that we need to ask to design the authentication of our system
	1. **User store**
		1. **Where is it located?**
			1. Is it part of the Authentication engine?
			2. Is it a separate component? 
		2. **Who's responsible for maintaining the database?**
			1. Who adds new users?
			2. Who removes un-used ones?
				1. Is it the development team?
				2. Is it the team responsible for the authentication engine?
	2. **Authentication engine**
		1. **Which engine are we going to use?**
		2. **What is the authentication type we want to utilize for our system**
			1. Various types of authentication: later
	3. **Software Component**
		1. **How are user's details received?**
			1. At the end of the flow, the authentication engine sends user details to software component
				1. How is it done?
				2. In what form does the component receive this data?

#### User Store ####
1. Where is the user-store located
	1. Three locations:
		1. **Part of the Authentication Engine**
			1. Software itself has no access to it
			2. The authentication engine has all it needs to perform the authentication since it has user's data
		2. **Part of the Software Component**
			1. When Authentication Engine needs to check the user's authentication data, it goes to Software Component and asks it for data
		3. **Hybrid (preferred way to go)**
			1. Two user-stores
				1. One in the authentication engine
				2. One in the software component

#### Hybrid User Store ####
1. Instead of having a single user-store, we have two
	1. One is: Authentication User Store
		1. It is part of the Authentication Engine
	2. Second one: Component User Store
		1. It is part of the Software Component
2. Differences:
	1. Authentication User Store (It holds only the data required to perform the authentication only)
		1. It is used for authentication only
		2. It usually contains (data fragments that are part of identifing the user)
			1. User ID
			2. Password
			3. Organizational position
			4. Roles
			5. etc.
		3. It is maintained by the IT
			1. It manages all users in the organization
				1. Since authentication engine is organization wide mechanism
					1. Therefore, it is under the responsibility of the org's IT division
	2. Component User Store - It is used for component's needs (not authentication needs)
		1. Used for the component's needs
		2. Usually contains:
			1. Business data
				1. Financial
				2. Personal
				3. ...
					1. Example: If software component is an e-commerce website, it will store:
						1. User's order history
						2. User's shipments
						3. ...
		3. Maintained by the component's developers
			1. There is no point for the IT team to maintain it because it holds only business related data (not organization wide data)
3. Advantages:
	1. Clear separation of concerns
	2. Well-defined user-stores 
	3. Clear responsibility borders

#### Authentication Engine ####
1. What authentication engine should we use?
	1. Two potential options:
		1. Self developed (own)
			1. We should have a very good reason to develop an authentication engine from scratch
		2. 3rd party engine
			1. There are great out-of-th-box authentication engines and we must strive to use one of them
			2. This is the preferred way
2. 3rd Party Authentication Engine
	1. Why do we prefer them?
		1. They are **robust**
			1. They are designed to work with a huge amount of authentication (scale)
			2. They have built in authentication mechanism (design)
		2. They offer great **flexibility**
			1. **Multiple authentication types**
			2. **MFA**
			3. **Roles**
		3. They sometimes contain **built-in user store**
		4. They are **heaviliy monitored**
			1. If there is any problem, we are going to be alerted about it immediately
		5. They can be easily **managed**
			1. Using easy to use:
				1. Management console OR
				2. Convenient API
		6. They provide **SSO**
			1. Single-sign-on
				1. It gives the capability for the user to log into one system and preserve the identity for subsequent loging into other systems
					1. Eliminates logging into each and every system separately
		7. They are **standard based**
			1. They work with the authentication standards
			2. They can work with the latest authentication technologies out of the box
3. Which authentication engines should we look at?
	1. **Cloud Based**
		1. Azure Active Directory
		2. Okta offerings
		3. AWS IAM
		4. ...
	2. **On-Premise**
		1. Microsoft Active Directory
		2. Centrify
		3. RSA SecureID
		4. ...
	3. We can pick the one that fits our needs

#### Authentication Types ####
1. Authentication is divided to three factors:
	1. Something we know - (username/password, security question)
	2. Something we have - (phone, smart card)
	3. Something we are - (fingerprint, iris scan, other biometric data)
2. Selecting Authentication Type
	1. Some considerations
		1. **Feasibility** - (Not all computers / phones have fingerprint scanner)
			1. Can we actually implement this factor?
		2. **Ease of use** - (username / password is much quicker than text)
			1. Fingerprint and face-scan are easier as well
			2. If our intended audience is general population including elderly people or others that may have hard time figuring out complex auth mechanism,
				1. We go for easier method
		3. **Sensitivity** - (Biometric data is much more difficult to hack than username / password)
			1. The more sensitive the data, the safer auth mechanism we want to use
				1. **We need to think how sensitive the data is to choose the authentication type**
	2. Two Factor Authentication
		1. For extremely sensitive systems (banks, etc.)
		2. We pick two of the three factors and both are required for the authentication
			1. Something we know
			2. Something we have
			3. Something we are
		3. Examples:
			1. Something you know + Something you have (more common)
				1. username / password + code in Text)
				2. Two factors are employed
		4. Examples:
			1. Something you know + Something you are (more common)
				1. username / password + fingerprint
		5. Examples:
			1. Something you have + Something you are
				1. text to phone + fingerprint
		6. **Make sure the authentication engine supports two factor authentication**
			1. Multi-factor authentication
3. **We don't to find out in the future that if the authentication requirements change, we cannot follow them with the current auth engine**
4. The capabilities should come out of the box
	1. **We should not require any development to require any advanced authentication**
5. The decision to use two-factor or multi-factor authentication directly affects the end users
	1. **System analyst must be in the loop**

#### Software Component ####
1. It MUST know who it is working with
	1. Human
	2. Computer
	3. Other software
	4. ...
2. It MUST NEVER allow anonymous access
	1. Unless it is a software exposed to the general public
		1. Public website say
3. Third step in the auth flow: User passed to component
	1. How do these details get to the component?
		1. Is there any standard about it?
			1. Solution:
				1. User Token
					1. It contains the data generated from the Authentication Engine
					2. It must be secure
						1. If not, it is possible to hack and manipulate it using the man-in-the-middle attack
					3. Must be standard based (format)
						1. We can invent our own format but other auth engines will not be able to generate it
				2. Implementations:
					1. Authentication Protocols

#### Authentication Protocols ####
1. They define 3 things:
	1. Who are the participants in the authentication process
		1. There are more participants than the 3 (CA, etc.)
			1. Software architects don't have to get to that resolution
	2. Flow of the authentication
		1. The above flow & including all the low-level participants
	3. Format of the data passed
		1. **This is what interests us the most**
2. Authentication protocols in use today:
	1. NTLM
		1. Mature
		2. Targets enterprise on-premise systems
		3. Cons: Not suitable for modern web-based systems
	2. Kerberos
		1. Mature
		2. Targets enterprise on-premise systems
		3. Cons: Not suitable for modern web-based systems
	3. **OAuth2**

### OAuth2 Protocol ###
1. What is OAuth2?
	1. It is a standard protocol for authentication & authorization
	2. It is widely used, mainly in web apps
	3. It has many moving parts and is quite complicated to implement
	4. We'll discuss only high-level details
2. OAuth2 Components
	1. User - The end-user who wants to access protected resources in the API
		1. Human being
		2. Software
		3. ...
	2. Client App - The client application accessing the API
		1. To access API on the server
	3. Authorization Server - Specialized server that authorizes the user for the client application
		1. It identifies the user using an identification mechanism it supports and tells back the client app who the user is, and what is he allowed to do
	4. Resource Server - The API being accessed
3. OAuth2 Flow

		Client App --Redirects user to---> Authorization Server
		    |      <-Returns access token-     ^        |        
		Accesses API                           |        |
		anonymously                           Asks user to grant
		    |                                 permission
		    v
		Resource
		Server (API)

	1. Client App calls the API anonymously without passing any identification data
	2. The Resource Server (API) identifies that the call is anonymous and no user data is passed and tells the client app to re-direct to Authorization Server
	3. The Authorization Server asks user to grant permission (after identifying the user)
	4. The Authorization Server returns an access token to the Client App
		1. The access token contains the data that is needed by the resource server (API) to identify the user and to figure out what exactly the user is allowed to do
	5. The Client App sends access token to the resource server
		1. The resource server now knows who the user is and the client app can access the API
	6. Example:
		1. Feedly - It is the best RSS client in the web
			1. RSS clients are subscribed to blogs
				1. They are a great resource to learn about any field
			2. Home-page
				1. Login
				2. Server redirects the client app to authorization server
					1. It asks which authorization server do we want to use
						1. Facebook (say)
							1. Functions as an authorization server
				3. Give credentials and login
				4. Logged in
					1. Facebook told Fidly who I was
				5. Feedly didn't have to do anything related to identification
					1. Facebook identified and returned the info to Feedly
#### App Registration ####
1. Authorization Server should be familiar with the Resource Server (API) (Feedly)
	1. When Feedly redirected to Facebook, it said it is Feedly and it wants Facebook to identify the user and return the information to Feedly
		1. How?
			1. Facebook must be familiar with Feedly
				1. Solution: Resource Server must register itself with the Authorization Server
					1. It is called **app registration**
					2. It includes filling some data about Resource Server (name and URL address to which authorization server needs to return the user info)
		2. Demo:
			1. [Github](https://github.com/settings/applications/new)
				1. App registration page:
					1. Application name: Order Management
					2. Homepage URL: http://www.orgermng.com
					3. Application description
					4. Authorization callback URL: Most important part
						1. It is used by Authorization server to tell back who the user is, and what is he allowed to do
						2. Example: http://www.ordermng.com/callback
					5. Register application
					6. Keys: The two keys that must be passed to the Authorization Server when asking for authorization (for Auth server to know which application is requesting for authorization)
						1. Client ID
						2. Client Secret
	2. Access Token
		1. It is a token returned by the Authorization server
		2. The client sends the token to the Resource Server for the client to be identified
		3. What is it?
			1. **It is JWT** (with OAuth2)
				1. What is JWT?
					1. JSON Web Token
						1. It contains the data the server needs in order to authenticate the user
				2. The token is returned by the OAuth2 authorization server and it contains everything that Resource Server (API) needs
				3. Structure:
					1. Has three sections:
						1. **Header**
							1. Type of token (JWT)
							2. Signing algorithm
							3. Example: [https://jwt.io/introduction]()

									{
										"alg": "HS256",
										"typ": "JWT"
									}

						2. **Payload** - Actual data about the user that the server needs to make a decision whether the user can access the resource or not
							1. There is no standard format (we can put whatever we want)
							2. Example:

									{
										"sub": "1234567890",
										"name": "John Doe",
										"admin": true
									}

								1. Actual data about the user that API needs
						3. **Signature** - JWT is signed electronically so that it can't be tamperred with during the transfer from the Authorization Server to the API
					2. The three parts are:
						1. Base64 encoded
						2. Concatenated with `.`
					3. [jwt.io](jwt.io)
						1. Modify the payload
	3. REST API
		1. Client App sends the Access token to the Resource Server
			1. The Resource Server checks the signature
			2. The Resource Server reads the payload
		2. JWT & REST API
			1. JWT Should be sent to the API with `Authorization: bearer` header
			2. When accessing an API to make authorization decision
			3. Can be sent also in body or request parameter
				1. Not recommended
			4. API Call Example:

					GET /resource HTTP/1.1
					Host: server.example.com
					Authorization: Bearer mF_9.B5f-4.1JqM

### Authentication and the Architect ###
1. What is the role of the architect regarding authentication?
	1. Tasks regarding authentication
		1. **Decide on the Authentication Engine (with the IT)**
			1. It is our responsibility to recommend specific authentication engine that will meet all the authentication requirements
			2. Since authentication engine is cross organization asset, we need to talk to the IT team
				1. They are the one who will maintain it
				2. They must be on-board this decision
			3. Other factors to be taken into account
				1. Cost
				2. Existing Auth engine in the Org
				3. ...
		2. **Decide on the user store**
			1. Three possible locations - we need to decide which approach is the right one
				1. Authentication engine
				2. Software component
				3. Hybrid - almost always this is good
		3. **Design the user store**
			1. Design the table
			2. Design the JSON document that will hold the user data of the software
			3. This is not for auth related data
				1. Auth data is handled by the Auth engine
				2. This is for business data
		4. **Decide on Authentication Type**
			1. Auth engines offer many auth types
				1. We need to pick the correct one
			2. Work with the **system analyst** about it
				1. It directly affects the end-user
			3. Most of the time we end up with
				1. username / password or MFA (usually text message to the phone)
		5. **Decide on the Authentication protocol**
			1. Prefer modern protocols such as OAuth2 (whenever possible)
			2. If systems are fully Microsoft-based and run Windows, **kerberos** will be easier to implement
				1. Reason: There is great integration between Active Directory and IIS
				2. For other cases, look at OAuth2
		6. **Authentication is usually a cross-organization effort**
			1. Work closely with the IT and dev team to implement it
				1. We might find that our system is the first to implement Auth the way it should be
					1. It would shake a lot of people in the org
						1. Solution: Work closely with all relevant functions we must make sure they understand what is going to happen and we can bring them on board

### Authorization ###
1. What is it?
	1. Basically, another answer to another existential question:	
		1. **What can you do?**
			1. It is **assigning privileges to thing**
				1. **thing**
					1. Human
					2. Computer
					3. Software
					4. ...
			2. Example:
				1. Granting privileges to someone so that he can:
					1. Read data from the database
					2. Not delete data from the database
				2. Granting privileges to a software to:
					1. Run the `AddServiceRequest` method
					2. Not access the `api/v1/orders` URL
2. What is it for?
	1. Limits access to users so that they won't do unintended actions
		1. Example: We don't want a user, with access rights to the database, un-intentionally deleted the whole orders table when he simply needs to reads the data
			1. He runs `delete` command by mistake
	2. Another defense line: **Even if authentication was hacked - authorization will limit its impact**
		1. Impersonation attack will limit the impact due to privileges
			1. He cannot do whatever he wants in the system
				1. He can only do what he is authorized to do
	3. Authorization can be used to protect from:
		1. **Data leaks**
		2. **Data inconsistency**
3. Important principle for authorization:
	1. **Principle of Least Privilege (PoLP)**
		1. Authorization must be granted only for the intended tasks of the user, no more
			1. Example:
				1. Users that require only database read access - should not be granted database write access
					1. It is not so easy
						1. Dev env privileges (advanced user) may get carried to production
		2. **Deny by default, allow only what is needed**
			1. Any privilege granted must be minimum required

#### Two Types of Authorization ####
1. **Action Authorization**
	1. Defines: What actions are allowed or denied
	2. Examples:
		1. Allowed to add service request
		2. Allowed to update item inventory
		3. Denied from updating exam score
2. **Data Authorization**
	1. Defines: Which data is accessible (very important)
	2. Examples:
		1. Cannot see data from other teachers (Teachers)
		2. Cannot see data of other counties (Police Officer)
		3. Can see data of his own patients only (Doctor)

#### Role Based Access Control (RBAC) ####
1. What is it?
	1. In the past, authorization was defined per user or user group
	2. Examples:
		1. David is allowed to add items to the inventory
		2. John is not allowed to read data of other doctors
			1. This type of authorization is very granular and is extremely hard to maintain
		3. What if David leaves the company
			1. System has to go through all the authorizations of David and cancel them (can be dozens)
		4. What if we have category in the store and we need to allow all employees to add items to inventory
			1. We might need to go through all the users in the system and grant each one of them the right to work with the new category
				1. Hard to maintain
	3. Solution: RBAC
		1. Three elements to define authorization
			1. Users
			2. Roles
			3. Authorizations
		2. Example: Hotel system
			1. Users
				1. Jane
					1. Associated with: Hotel Owner (role)
				2. David
					1. Associated with: Front Desk
			2. Roles
				1. Hotel Owner
					1. Associated with:
						1. Set Price
						2. Check-In
						3. Check-Out
				2. Front Desk
					1. Associated with:
						1. Check-In
						2. Check-Out
			3. Privileges
				1. Set Price (one night stay)
				2. Check-In (guests)
				3. Check-Out
		3. Privileges of a role do not change frequently (almost constant)
		4. Association of users to role is one-to-one and it is simple
		5. Adding user:
			1. Rachel - Front Desk employee
				1. Add her to Front Desk role
					1. She will automatically be granted with all the privileges of a front-desk role
2. Implementation:
	1. Where are roles managed?
		1. Authorization process must be able to associate role to users after they are authenticated
			1. How?
				1. Options:
					1. In the Authentication Engine (ie. User Groups in Active Directory as roles representation - avoids maintaining separate roles mechanism)
						1. Legitimate choice - we can use it
						2. Caveat: Ensure that the user token passed to the software component contains the user groups the user is associated with
							1. Reason: The component can know what are the roles of the user
					2. Manage the roles in the component's user store
						1. Preferred option if the roles are highly specific
							1. The roles are not relevant to other systems the users are logged into
						2. Example:
							1. If org is an e-commerce website and it has a system to manage catering orders for employees, the roles in the system such as **orders manager** or **food quality supervisor** has nothing to do with e-commerce
								1. **There is no point defining these roles in an org wide authentication engine**
									1. Manage the roles internally in the component database
						3. The roles are retrieved after receiving the user's token from the Authentication Engine
							1. We need to ensure that the retrieval is happening first thing after receiving the user's token
	2. How to implement?
		1. **Action Authorization**
			1. Usually implemented using buit-in support in the development platform
				1. Most development platforms support RBAC out of the box
					1. They make it quite easy to implement it
					2. Example:

							[Authorize(Roles = "manager, Administrator")]
							public class DocumentsController : Controller {
								public ActionResult ViewDocument() {
									// Your code here
								}

								[Authorize(Roles = "Administrator")]
								public ActionResult DeleteAllDocuments() {
									// Your code here
								}
							}

						1. By default a Manager or Administrator can execute methods in the class
						2. The second method can only be executed by an Administrator
					3. Example: [https://blog.soshace.com/implementing-role-based-access-control-in-a-node-js-application](https://blog.soshace.com/implementing-role-based-access-control-in-a-node-js-application)


							// Add this to the top of the file
							const { roles } = require('../roles')

							exports.grantAccess = function (action, resource) {
								return async (req, res, next) => {
									try {
										const permission = roles.conn(req.user.role)[action](resource);
										if (!permission.granted) {
											return res.status(401).json({
												error: "You don't have enough permission to perform this action"
											});
										}
										next();
									} catch (error) {
										next(error)
									}
								}
							}

						1. Checking if a user with a specific role can perform a specific action and returning an error message if no permission
		2. **Data Authorization**
			1. How to implement?
				1. Using the database's **Row Level Security (RLS)** OR
					1. Pros: Can be found in popular databases
					2. Cons: Very complicated to implement it
						1. Not many orgs take advantage of it
				2. Self development of own data authorization
					1. Pros: Simpler
					2. Implementation:
						1. Add a condition to query statement
						2. Example:
							1. .NET Core

									public MedData GetMedicalData(doctorId doc) {
										using (var db = new MedContext()) {
											var medData = db.MedicalData
												.Where(d => d.ownerDocter == doc) // filters and returns own patients
												.Order(d => d.creationDate))
												.ToList();
										}
									}

								1. Drawback - Developer can forget and can cause data-breach
									1. Considering the alternative, this is a preferred approach

#### Authorization and the Architect ####
1. What should Architect do to design a robust authorization engine?
	1. **Decide on the roles management**
		1. Part of the Authentication Engine OR
		2. Part of the component
			1. If this option is chosen:
				1. Design:
					1. Roles table
					2. Data access mechanism to access the Roles table
	2. Design authrorization implementation
		1. **Recommend libraries for action authorization**
			1. Built in libraries
		2. **Decide and design data authorization**
			1. Two approaches
				1. DB's built in row level security
					1. Consult with DBA and bring him on-board (it is a delicate task)
				2. Self development
					1. We need to design the roles table and the data-access mechanism for it
		3. **Work closely with the dev team and system analyst to define the roles**
			1. It is part of system analysts job
				1. We must be in line with it

### Secure Communication ###
1. What is it?
	1. We want to make sure that the data in transit is secure
		1. Data in transit:
			1. Data that is transfered between two elements over a network
				1. Example: When we access a REST API that accesses the database that retrieves the data and returns it to the caller, the data is considered to be in transit the moment the data is returned from the API while it is on the network
					1. **We want to protect the data that is moving in the network**
		2. Data at rest:
			1. Addressing data that is physically stored and way to protect it
				1. Example: Data stored in database
2. What is the purpose?
	1. Ensures:
		1. Privacy
			1. Confidential data (example: credit card details) won't be evesdropped by un-authorized third party
		2. Data Consistency
			1. Insecure communication can cause data inconsistency
3. What is it for?
	1. Ensures that sensitive **data is not leaked** to unauthorized recipients
	2. Prevents Man-In-The-Middle attacks
	3. Secure communication protects agains:
		1. **Data leak**
		2. **Data inconsistency**

#### Privacy ####
1. Scenario to avoid
	1. Consider a regular user using a PC or phone and an e-commerce website the user wants to buy from
	2. User sends credit card details over the network to the website
	3. Somewhere in the middle, an attacker waits for it
		1. The attacker can listen to the network using simple sniffing tools and get everything that is sent over the network including the credit card details
			1. We want to prevent this
2. Senario to avoid: Man-In-The-Middle Attack (MITM)
	1. Consider a regular user using a PC or phone and a bank website the user wants to transfer money to his friend David
	2. The user sends an instruction to the bank website to transfer the amount
	3. A sophisticated attacker puts himself along the way and pretends to be the bank website
	4. The attacker modifies the instruction and sends the amount to John's account instead of David's
	5. The user doesn't know that something was wrong and he doesn't even know that the instruction was received by the attacker and not the bank account
	6. MITM - used to intercept the communication between them
3. How to mitigate them?
	1. Implemented using secure protocol
	2. There are maintly two secure protocols
		1. SSL
		2. TLS

#### SSL ####
1. SSL - Secure Socket Layer
	1. Developed by Netscape in 1995
2. It has 3 versions
3. All deprecated due to security flaws found in them
4. DO NOT USE!

#### TLS ####
1. TLS - Transport Layer Security
	1. First version released in 1999
	2. Latest version (1.3) released in 2018
	3. Versions 1.0 & 1.1 are deprecated
	4. DO NOT USE THEM!
2. The details of the inner workings of secure protocols are very intricate and will require extensive knowledge in the cryptography field
	1. Architect is not expected to be fluent in this field
		1. Not expected to know the intricacy that is part of the protocol specification
3. High level details of TLS:
	1. Uses symmetric cryptography to encrypt the data in transit
	2. Unique keys are generated for each connection
		1. Generated for each new connection between the parties
	3. Keys are generated using a shared secret that is negotiated between both the parties at the beginning of the session
	4. Additionally, parties are authenticated using public key cryptography
4. The authentication here is at the communication level and has nothing to do with actual users and actual authorization
5. The messages transmitted are verified by a message integrity check that is performed on both sides
	1. It prevents data tampering and ensures that no-one messed with the message on its way

#### Implementing Secure Protocol ####
1. It should be the IT responsibility
	1. It is not done by the development team and not something and architect can do
		1. There are a lot of moving parts:
			1. It requires Certificate Authority & Management and more
	2. **Architect's responsibility: Work closely with the IT guys to ensure that it's implemented and supported**

#### Secure Communication & The Architect ####
1. Secure Communication does not affect the architecture
	1. Nothing should be changed when using secure communication
		1. **It can be added later**
2. It might have a negligible effect on performance
	1. Much more is going on with secure protocol than sending messages in clear-text
	2. It is worth it as compared to un-secure communication
3. **Insist on having secure protocol in place**
	1. No excuses
4. Work closely with the IT on that
	1. Establishing secure communication environment is not an easy feat
	2. Talk to IT, explain the situation, and bring them on-board

### Secure Code ###
1. What is it?
	1. Making sure the application's code is secure
		1. As part of implementing secure code, **we need to educate developers on the importance of secure code**
			1. Explain why we do it
		2. **To adopt secure coding practices**
			1. By writing secure code, the Dev team and org in general will become familiar with threats the secure code will present and adopt the right practices for writing secure code
				1. We want developers to write secure code by instinct
					1. Possible if we do more and more
2. What it is for?
	1. Unsecure code can cause: (It is the most dangerous flow compared to other flows)
		1. Disruption of service
		2. Data leak
		3. Data inconsistency
		4. Data loss

#### Code Vulnerabilities ####
1. Often a result of mistake or lack of awareness
	1. It is rare that a developer leaves code vulnerable on purpose
		1. It is almost due to un-awareness
			1. **We must make sure the developers are aware of the risks of un-secure code**
2. There are identified, wide-spread code vulnerabilities that must be handled in all systems
	1. Vulnerabilities that were used by hackers for years (first to handle)
3. The basic premise:
	1. **Code is the last line of defense before the data, and must be well protected**

#### SQL Injection ####
1. One of the most common attacks
2. An attacker can exploit SQL databases by inserting malicious code into SQL statements
3. Example:
	1. users table
		1. user_id
			1. 1
			2. 2
			3. 3
		2. user_name
			1. davidg
			2. joank
			3. johnb
		3. password
			1. 66peos
			2. q48v5#
			3. 9qxnflx5
	2. Login Page
		1. Username
		2. Password
		3. Login
	3. SQL Statement:

			"Select user_name, password from users
			where user_name='" + txtUser + "' and
			password='" + txtPassword + "'"

	4. Use-case:
		1. username: rrr' or 1=1; --
		2. password: Hacked!
	5. SQL Statement:

			Select user_name, password from users
			where user_name='rrr' or 1=1; -- ' and
			password='Hacked'

		1. The statement returns all the users in the system and their passwords
	6. Use-case:
		1. username: rrr' or 1=1; DROP TABLE users; --
		2. password: Hacked!
	7. SQL Statement:

			Select user_name, password from users
			where user_name='rrr' or 1=1; DROP TABLE users; -- ' and
			password='Hacked'

		1. Returns all records (data leak)
		2. Drops the user's table (destroys) (data loss)
4. Protection:
	1. Always validate input (always true)
		1. Input from user must not contain suspicious characters
			1. `-`, `;`, `=`, ...
			2. Many websites allow only letters and numbers in a signup form
				1. To avoid potential SQL injection attacks
	2. Use parameterized query
		1. We send query to the database with parameters where the input should be and send actual values separately as params
			1. DB puts actual values in the query in a safe way and bypasses potential threats
		2. Example:

				String sql="Select user_name, password from users where user_name=@userID and password=@pwd"

				SqlCommand cmd = new SqlCommand(sql, con);
				cmd.Parameters.AddWithValue("@userId", txtUser);
				cmd.Parameters.AddWithValue("@pwd", txtPassword);

			1. `@` - placeholders
		3. It also comes with some performance improvement

#### Cross-Site Scripting (XSS) ####
1. It is one of the most common attacks
	1. What is it?
		1. It is one of the most common attacks
		2. An attacker injects malicious scripts to an unsuspecting user's browser

### Secure Data ###
### Logging and Monitoring ###

## Section 7: SDLC ##
### Introduction ###
### SDLC Process ###
### SDLC and the Architect ###

## Section 8: Testing ##
### Introduction ###
### Penetration Testing ###
### Load Testing ###
### Security Testing and the Architect ###

## Section 9: Production ##
### Introduction ###
### Security Review ###
### Penetration Testing ###
### Production and the Architect ###

## Section 10: Case Study ##
### Introduction ###
### Introducing Dunderly ###
### Threat Modeling ###
### Secure Architecture ###
### SDLC ###
### Testing ###
### Production ###
### Case Study Summary ###

## Section 11: Conclusion ##
### Download the Secure Architecture Checklist ###
### Conclusion ###
### BONUS: Next Steps ###