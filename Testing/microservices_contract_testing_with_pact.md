# Microservices Contract Testing with Pact #
## Section 1: Introduction to MicroServices and Advantages of Them ##
### Course Goals - Objective (Must Watch) ###
1. What is contract testing?
	1. For microservices architecture
	2. It is for testing communication between systems
		1. Integration between
			1. Microservices
			2. FE and BE
	3. They help in integration testing
		1. It is integration testing done properly
	4. Test Pyramid
		1. Contract tests come in Unit Tests layer (bottom)
			1. The issues caused while communicating with external services will be caught in the unit-testing layer (even before committing the code)
				1. We know something is wrong early in the development lifecycle
2. Concepts:
	1. Microservices architecture vs Monolithic architecture
		1. To understand why we need contract tests
	2. Contract testing
	3. Pact contract testing tool
		4. Writing contract tests for microservices
	4. Deep dive
		1. States
		2. Interactions
		3. Server configs
		4. Pact flow (orchestrator)
3. Prerequisites
	1. Core Java
	2. Spring Boot

### Differences Between Monolithic and Microservices Architecture ###
1. Monolithic Architecture
	1. Service features
		1. User Profile
		2. Orders
		3. Products
		4. Payments
		5. Notifications
	2. Disadvantages:
		1. If a server goes down, we cannot access any feature
		2. On high load, some of the features may require more resources, and on replication, all the features will share the resources and the feature that needs more resources cannot get exclusive access
		3. If there is a problem in any feature, it can brind down the entire application
		4. If a problem in a feature is fixed, we need to redeploy the entire application including the features that were not touched
		5. Hard to understand because of massive codebase
		6. IDEs get overloaded with massive codebase
			1. IDEs might stall
		7. Hard to make changes due to massive codebase that is tightly coupled
		8. Hard to upgrade stack
			1. Especially for features that need the upgrade
2. Microservices Architecture
	1. Services:
		1. Orders
		2. Payments
		3. Notifications
		4. Products
	2. Business functionality can be split into a microservice
	3. Advantages:
		1. A portion of the website is not accessible
		2. We can have our own database for each service
		3. We can have our own code per service
		4. We can upgrade database or change its technology for each service independently
			1. Other DBs are not impacted
		5. We can host each function in separate server
			1. If any host goes down, the other functions still work
		6. Only the microservice that has changes can be re-deployed without affecting other services
		7. We can use different technologies and versions for each microservice
			1. They are independent
		8. Communication between services is done using HTTP requests which are language and technology agnostic

### How MicroServices Communicate with Each Other in the Distributed Systems ###
1. Monolithic
	1. Disadvantages:
		1. Each feature can interact with another feature by calling methods which are local to the service
2. Microservices
	1. Disadvantages:
		1. Need to make network calls for inter-service communication
			1. Network failures need to be handled gracefully
		2. Higher complexity due to many services
			1. Need to write integration tests with other services running
				1. Challenging to ensure all services are running
		3. More DevOps processes and set up

### Importance of Microservices Integration Testing in Agile World ###
1. Monolithic application:
	1. It is end-to-end testing due to one flow
2. Micorservices application
	1. Many integration points
3. Architecture or microservices testing
	1. Front End UI
		1. Interacts with Library Microservice (stores books)
			1. `/getProductPrices`
		2. Library Microservice interacts with Course Microservice (stores courses)
			1. `/allCourseDetails`
	2. Instead of spinning up a dependant microservice, we mock the dependent microservice and return mock data - Unit Test
	3. Integration testing:
		1. QA will deploy both microservices
			1. API test cases are written to test end-to-end
				1. Suppose the dependent microservice is changed
					1. The tests will fail
						1. Unit tests will also not mock the change so they will pass
							1. The error is thrown late in the lifecycle
								1. This can happen with many changes and with many microservices (due to contract change)
									1. Problem: Is there a way to realize this just before we deploy the code?
										1. The dependent microservice is not aware of what the clients are consuming (say ids only)
4. Solution: Pact
	1. The contract is shared with Pact
	2. Pact monitors for changes and stops from deploying if contract breaks

## Section 2: Importance of Contract Testing in MicroServices Agile World ##
### Why Contract Tests are Important to Have? And its Advantages ###
1. A way to define expectations on fields (Contract) we are using so that Provider unit test cases will start failing if they alter those values

### Setting up Microservices in Local Systems and Walk Through the Code ###

## Section 3: Setting up Pact Contract Testing Tool and Build Consumer Driven Tests ##
### How to Install and Configure Pact Library for Contract Testing ###
### Defining Pact Server Configuration and Related Iteractions with Response ###
### Understand How to Write Unit Tests on Pact Server to Generate Contract JSON File ###

## Section 4: Generate Contract File and Setup Provider Runner to Run on Contract Tests ##
### How to Configure Pact Library on Provider Side Microservice ###
### Setting up Pact Provider Side Tests Configuration with Context Object ###
### Define State Change Actions and Run the Tests on the Consumer Contract File ###
### Quiz 2: Section Quiz ###

## Section 5: How Contract Testing Catches Bugs if Changes Made on Provider Microservice ##
### How Contract Test Reports Failure on Change in API Response Contract ###
### How to Generate Contract Only on Required Fields of Consumer with Regex ###

## Section 6: End to End Contract Validations on Both Consumer and Provider Microservices ##
### Demonstration on Negative Scenario Real World Example on Contract Testing ###
### Build Consumer Side Unit Tests on Pact Mock Server to Generate Contract File ###
### Run Tests on the Provider Side Unit Tests by Updating State of Actions ###
### Building the Pact Server Configuration for Negative Scenarios of no Data Found ###
### Update the States on Provider Side to Update the Data as Per Contract Test ###

## Section 7: Pact Flow - Orchestrator to Manager Contract File Globally Between Microservices ##
### What is Pact Flow. How to Setup Pact Flow Account and Generate Tokens ###
### How to Publish the Contract from the Consumer Repo to Pact Flow ###
### Retrieving the Contract File from Pact Flow to Provider Repo with Config Changes ###
### Quiz 3: Section Quiz ###
### Article Reading ###

## Section 8: Article ##
### Bonus Lecture ###