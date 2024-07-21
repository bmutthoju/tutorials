# How to Prepare for Low Level Design Interview: A Guide #
## Blog ##
1. Goal: Transform high-level concepts into fine blueprints
2. LLD (Detailed design): visions -> viable solutions
	1. Goal: Craft **efficient**, **scalable**, and **maintainable code**

## What is the Purpose of LLD? ##
1. LLD is the core of software development
	1. It is a bridge between HLD and practicality of implementation
2. LLD is detailed design that brings system to life
	1. **It defines the logic and functionality of each module**
3. HLD defines the foundation & structure of the system
4. **LLD's focus: Component's**
	1. **Internal structure**
	2. **Algorithms**
	3. **Data structures**
5. It guides developers to bring system to life

## What can you Expect in an LLD Interview? ##
1. Interviewer might ask us to design different types of systems
2. What is tested?
	1. Ability to contruct software that is:
		1. Scalable
		2. Flexible
		3. Maintainable

### Class/Entity Design ###
1. We might be asked to design **classes** or **Entities** for specific objects
	1. Bird
	2. Pen
	3. Pizza
2. **Focus:**
	1. Creation of **appropriate class hierarchies**
	2. Defining **attributes and methods** (considering relationships between objects)

### Application Design ###
1. We might be asked to design **a complete application** or **system**
	1. Parking lot
	2. BookMyShow
2. **Focus:**
	1. Ask clarifying questions
	2. Design the architecture
	3. Design modules
	4. Design interactions between components

### Game Design ###
1. What is tested?
	1. Ability to contruct **logic and mechanics** for games
		1. Define:
			1. Rules
			2. Game states
		2. Design components
			1. Players
			2. Moves
			3. Game boards
	2. **Approach, problem-solving skills & understanding of design patterns**
2. **Focus:**
	1. Ask clarifying questions
	2. Communicate thoughts clearly
		1. Break down the problem into smaller components
		2. Construct a design that fulfills system's goals
	3. Practice
		1. With practice, we can contruct well-structured systems

## Foundations of LLD ##
1. Learning fundamentals will give the confidence to solve LLD problems
	1. **Understand the concepts thoroughly**

### Object-Oriented Programming ###
1. OOP is a programming paradigm
2. Focus:
	1. To organize software around objects (instances of classes) that encapsulate data and behaviour
3. The following are OOP principles.

#### DRY (Don't Repeat Yourself) ####
1. Avoid duplicating code
	1. How?
		1. By promoting code re-use through
			1. **Abstraction**
			2. **Inheritance**
			3. **Composition**

#### YAGNI (You Aren't Gonna Need It) ####
1. Only implement features and functionality **required at the moment**
2. Avoid unnecessary complexity based on speculative future needs

#### SOLID Design Principles ###
1. Five design principles which will help us construct maintainable and extensible software
2. Principles:
	1. **Single Responsibility Principle (SRP)**:
		1. A class should have only one reason to change
			1. It should have a single responsibility
	2. **Open-Closed Principle (OCP)**:
		1. Software entities (classes, modules, functions) should be open for extension, but closed for modification
	3. **Liskov Substitution Principle (LSP)**:
		1. Objects of a superclass should be replaceable with objects of their subclasses, without affecting the correctness of the program
	4. **Interface Segregation Principle (ISP)**:
		1. Should not depend on interfaces they do not use
		2. Interfaces should be focused and specific
	5. **Dependency Inversion Principle (DIP)**:
		1. High-level modules should not depend on low-level modules, but should depend on abstractions
3. [Star Interview Method](https://visit.preplaced.in/x1h)

#### Design Patterns ####
1. They are re-usable solutions to common design problems
2. They provide a structured approach to solving specific design challenges

##### Creational Patterns #####
1. The patterns deal with creation mechanisms
	1. Builder
	2. Factory
	3. Singleton
	4. **Abstract Factory**
	5. Prototype

##### Structural Patterns #####
1. The patterns focus on composition of classes and objects
	1. Composite
	2. Decorator
	3. Facade
	4. **Flyweight**
	5. Adapter
	6. **Bridge**
	7. **Proxy**

##### Behavioral Patterns #####
1. The patterns deal with communication between objects
	1. Chain of Responsibility
	2. **Command**
	3. Iterator
	4. Mediator
	5. **Memento**
	6. Observer
	7. **State**
	8. Strategy
	9. Template Method
	10. **Visitor**
	11. **Interpreter** 

#### UML Diagrams ####
1. A standard modeling language
2. It is used to visually represent software systems
3. 14 types of UML diagrams classified into two main categories

##### Structural Diagrams: Represent the static structure of a system #####
1. Class diagram
2. Object diagram
3. Deployment diagram
4. Package diagram
5. Composite structure diagram (?)
6. Component diagram
7. Profile diagram (?)

##### Behavioral Diagrams: Represent the dynamic structure of a system #####
1. Activity diagram
2. Use case diagram
3. Timing diagram
4. Communication diagram
5. State machine diagram
6. Interaction overview diagram (?)
7. Sequence diagram

#### Schema Design ####
1. **It is the process of designing the structure and organization of a database schema**
	1. **Focus:**
		1. Identifying entities
		2. Defining relationships among entities
		3. Specifying attributes
		4. Specifying constraints
2. Goal: Proper schema design ensures
	1. Efficient storage
	2. Efficient retrieval
	3. Efficient manipulation of data

## How to Prepare for an LLD Intervew? ##
1. Steps to follow to boost LLD interview preparation
	1. Focus: To build systems that exhibit
		1. Modularity
		2. Extensibility
		3. Maintainability
2. The following are the steps to follow:
	1. Clarifying and gatehering requirements
	2. Class daigram and use-case diagram
	3. Coding

### Clariying and Gatherig Requirements ###
1. Understand the problem at hand:
	1. **Engage with stakeholders, ask insightful questions, and gather detailed requirements**
	2. **Clarify any ambiguity**
2. Goals:
	1. Ensure clear understanding of
		1. Problem's scope
		2. Constraints
3. Grasping requirements is strong foundation for design

### Class Diagram and Use Case Diagram ###
1. Define:
	1. Construct a class diagram that depicts the structure of the system by defining:
		1. Classes
		2. Objects
		3. Relationships
	2. **Highlight essential entities and their associations**
	3. Develop a use-case diagram that captures the system's behaviour
		1. **Illustrate how different actors interact with it**
2. Visual representations serve as *blueprints for the system's design*
	1. They aid in conceptualizing its architecture

### Coding ###
1. Bring the system to life by coding after the design is established
	1. Implement system based on design decisions made in the previous steps
		1. **Apply object-oriented programming principles to come up with clean & modular code**
			1. Encapsulation
			2. Inheritance
			3. Polymorphism
		2. Adhere to SOLID principles
			1. Ensures that code is well-structured, maintainable, and extensible
		3. Leverage design patterns such as the following which will help us address specific design challenges and improve code organization
			1. **Builder**
			2. **Factory**
			3. **Singleton**
			4. **Observer**
2. Consider the following during coding phase:
	1. Breakdown the system into smaller modules or classes
		1. They lead to better manageability and reusability
	2. Write unit tests to verify the correctness of individual components
		1. It will ensure system functionality
	3. Refactor code when necessary to enhance readability
		1. Drop code smells
		2. Optimize performance
	4. Strive for a modular and extensible design
		1. **It must allow for future enhancements and changes**
3. Each step contributes to problem solving & enables us to construct high-quality software solutions

## Tips for LLD ##
### Know your ABCs ###
1. ABCs of LLD: (Secret sauce to impress interviewers)
	1. **Object Oriented Programming**
	2. **SOLID Principles**
	3. **Design Patterns**

### Practice problem-solving ###
1. Practice constructing elegant and scalable architectures
	1. Makes interviewer go "Wow!"

### Don't be a lone wolf ###
1. **Show the ability to work with a team**
	1. Be open to listen to different perspectives
		1. Great design is a collaborative symphony

### Keep it simple ###
1. Avoid overcomplicating design
	1. Simplicity is key to elegance and maintainability

### Think about extensibility and scalability ###
1. Consider how design can accommodate future growth
	1. Design components must be:
		1. Modular
		2. Loosely coupled
		3. Easily extendable

### Be a master of disaster (handling) ###
1. Show skills in error handling and exception management
	1. **Design a system that handles errors and provides helpful messages**

### Showcase your ability ###
1. **Discuss how to handle changing requirements**

### Keep calm and code on ###
1. Stay calm, confident, and collected throughout interview
	1. Interviewers are looking for **potential problem-solving abilities**

## LLD Interview Questions to Prepare For ##
### Design a Parking Lot ###
1. Consider various components
	1. Spots
	2. Vehicles
	3. Entry/Exit points
	4. Payment systems
2. **Focus:** Efficient and Scalabile Architecture
	1. To handle
		1. Parking spot allocation
		2. Vehicle management
		3. Payment processing

### Design a Social Media Feed ###
1. Backend architecture for a social media feed system
	1. Consider how to handle
		1. User feeds
		2. User relationships
		3. Post-ranking algorithms
	2. Show understanding of
		1. Efficient data retrieval
		2. Caching mechanisms
		3. Personalized content delivery

### Design a File Storage System ###
1. Consider how files are
	1. Organized
	2. Stored
	3. Accessed
2. Think about
	1. File hierarchy
	2. Metadata management
	3. Access control
3. **Focus:**
	1. Demonstrate understanding of
		1. Efficient data structures
		2. Indexing mechanisms
		3. Data integrity

### Design a Ride-Sharing Service ###
1. Design backend architecture for ride-sharing service like Uber or Lyft
2. Consider the following components:
	1. Users
	2. Drivers
	3. Rides
	4. Real-time tracking
	5. Pricing algorithms
3. **Focus:**
	1. **Location-based services**
	2. **Efficient matching algorithms**
	3. **Real-time data processing**

### Design a Hotel Reservation System ###
1. System that handles
	1. Room bookings
	2. Availability
	3. Pricing
	4. Guest management
2. Consider how we would
	1. Structure the database
	2. Handle booking conflicts
	3. Accommodate various types of rooms and pricing strategies
3. **Focus:**
	1. Data modeling
	2. Concurrency control
	3. Transaction management

## To Sum Up ##
1. Tips:
	1. Communicate thought process
	2. Justify design decisions
		1. Showcase understanding of trade-offs and best practices
	3. Remain calm, confident, receptive to feedback
	4. Feel free to reach out if you have further questions