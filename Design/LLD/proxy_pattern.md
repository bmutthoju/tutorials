# Proxy #
## Intent ##
1. Proxy is structural design pattern that lets us provide a substitute or placeholder for another object
2. Proxy controls access to original object
	1. We can perform something before or after the request gets through to the original object

## Problem ##
1. Why control access?
	1. Lazy loading

## Solution ##
1. Construct a proxy class with the **same interface** as an original service object
2. We can pass proxy object to all original object's client
3. Upon receiving request, proxy constructs real service object and delegates all the work to it
4. If we want to execute something before or after primary logic of the class, proxy lets us do it without changing the class
5. Since proxy implements the same interface as the original class, it can be passed to any client that expects a real service object

## Real-World Analogy ##
1. Debit card is proxy for a bank account
2. Bank account is proxy for cash
3. Both Debit card and Bank account implement the same interface

## Structure ##

		Client -> <<interface>> ServiceInterface
					+ operation()
				
				Proxy						Service
				- realService: Service <>->
				+ Proxy(s: Service)			+ operation()
				+ checkAccess()
				+ operation()


				if (checkAccess()) {
					realService.operation()
				}

## Pseudocode ##
## Applicability ##
1. Lazy initialization (virtual proxy)
	1. When we have a heavyweight service object that wastes system resources by being always up, even though we only need it sometimes
		1. We can delay the object's initialization to a time when its really needed
2. Access control (protection proxy)
	1. When we want only specific clients to be able to use service object
		1. When our objects are crucial parts of OS and clients are various launched applications (including malicious ones)
			1. Proxy can pass request to service object only if client's credentials match some criteria
3. Local execution of a remote service (remote proxy)
	1. When service object is located on remote server
		1. Proxy passes client request over network.
			1. It handles all the details of working with network
4. Logging requests (logging proxy)
	1. When we want to keep history of requests to service object
		1. Proxy can log each request before passing it to service
5. Caching request results (caching proxy)
	1. When we need to cache results of client requests and manage the life cycle of the cache
		1. Especially if results are too large
	2. Proxy can implement caching for recurring requests that yield same results
		1. Proxy may use parameters of requests as cache keys
6. Smart reference
	1. When we need to dismiss heavyweight object once there are no clients that use it
		1. Proxy can keep track of clietns that obtained a reference to service object of its results
			1. From time to time proxy may go over clients and check whether they are still alive
			2. If client list gets empty, proxy might dismiss service object and free underlying system resources
	2. Proxy can tract whether client had modified service object
		1. Unchanged objects may be reused by other clients

## How to Implement ##
## Pros and Cons ##
## Relations with Other Patterns ##
