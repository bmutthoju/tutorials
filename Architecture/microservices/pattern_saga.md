# Pattern: Saga #
## Context ##
1. After applying [Database per Service]() pattern, each service has its own database
2. Some business transactions span multiple services
	1. We need a mechanism to implement transactions that span services
	2. Example: e-commerce store with customers having credit limit
		1. New order must not ensure customer' credit limit
			1. Orders and Customers are in different databases (owned by different services)
				1. Simple ACID transactions cannot be used

## Problem ##
1. How to implement transactions that span services?

## Forces ##
1. 2PC is not an option

## Solution ##
1. Implement business transactions that span multiple services in a saga
	1. Saga: It is a sequence of local transactions
2. Each local transaction updates database and publishes a message or event to trigger next local transaction in the saga
	1. If a local transaction fails because it violates a business rule then
		1. saga executes a series of compensating transactions that undo changes that were made by preceding local transactions

	![from_2pc_to_saga](from_2pc_to_saga.png)
	
3. Two ways of coordinating sagas:
	1. Choreaography: each local transaction publishes domain events that trigger local transactions in other services
	2. Orchestration: an orchestrator (object) tells the participants what local transactions to execute

## Example: Choreography-based saga ##

	![choreography_saga_example](choreography_saga_example.png)
	
1. e-commerce application that uses the approach for creation of order could have the following steps:
	1. The **Order Service** receives the **POST /orders** requests and and **Order** is created in a **PENDING** state
	2. It then emits an **Order Created** event
	3. The **Customer Service**'s event handler attempts to reserve credit
	4. It then emits an event indicating the outcome
	5. The **Order Service**'s event handler either approves or rejects the **Order**

## Example: Orchestration-based saga ##

	![orchestration_saga_example](orchestration_saga_example.png)
	
1. e-commerce application that using the orchestration based saga for creation of order could have the following steps:
	1. The **Order Service** receives the **POST /orders** request and **Create Order** saga orchestrator is created
	2. The saga orchestrator instantiates and **Order** in the **PENDING** state
	3. It then sends a **Reserve Credit** command to the **Customer Service**
	4. The **Customer Service** attempts to reserve credit
	5. It then sends back a reply message indicating the outcome
	6. The saga orchestrator either approves or rejects the **Order**

## Resulting Context ##
1. Advantages
	1. Enables application to maintain data consistency across multiple services without using distributed transactions
2. Disadvantages
	1. Programming model is more complex
		1. Example: Developer must design compensating trnasactions that explicitly undo changes made earlier in a saga
3. Other issues to address
	1. To be reliable, service must automatically update it's database and publish a message / event.
		1. Traditional mechanism of distributed transaction that spans database and message broker cannot be used

## Related Patterns ##
## Learn More ##
## Example Code ##