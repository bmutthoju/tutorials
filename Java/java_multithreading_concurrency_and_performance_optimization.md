# Java Multithreading, Concurrency & Performance Optimization #
## Introduction ##
### Motivation & Operating Systems Fundamentals - Part 1 ###
1. Motivation - Concurrency and Parellelism
2. What threads are - Introuction to OS
3. Why we need Threads?
	1. Responsiveness
		1. Example: Waiting for customer support
			1. Late response from a person
			2. No feedback from an application
		2. We want to avoid this frustration to users
		3. Example: Online store web application
			1. Suppose a user has made a request to the application and database operation is taking a long time
			2. Second user tries to send request to the application but the application is busy and the request will not be served (might wait or fail)
		4. Solution: Multiple requests can be served simultaneously by serving each request in a separate thread
		5. Responsiveness is particularly critical in applications with a User Interface
			1. Move player - showing images, playing movie, moving mouse gives instant feedback
				1. Can be achieved by using multiple threads, with a separate thread for each task
					1. Otherwise generally very hard to achieve
			2. Achieved by multi-tasking between threads
				1. Done quickly by the OS - to give illusion that all the tasks are executing simultaneously
		6. **Concurrency = Multitasking**
			1. Note: We don't need multiple cores to achieve concurrency
				1. Can also be achieved with single core
	2. Performance - parallelism
		1. With single core: An illusion of multiple tasks executing in parallel can be created using just a single core
		2. With multiple cores we can truly run tasks completely in parallel
		3. Impact: Completing a complex task much faster
		4. Finish more work in the same period of time
		5. For high scale service -
			1. Fewer machines
			2. Less money spent on hardware
			3. More money in your pocket
	3. Caveat
		1. Multithreaded programming is fundamentally different from single threaded programming
			1. Intuition that we have with single thread might break when using multiple threads
				1. Solution: The course will lay the groundwork, and learn all the tools to become a successful multithreaded programming developer
					1. We can write highly performant and responsive applications
3. 

### Operating Systems Fundamentals - Part 2 ###
### Quiz 1: Threading and Operating Systems Fundamentals Quiz ###

## Threading Fundamentals - Thread Creation ##
### Tips About Coding Lectures and Debugging Instructions ###
### Threads Creation - Part 1, Thread Capabilities & Debugging ###
### Threads Creation - Part 2, Thread Inheritance ###
### Quiz 2: Thread Creation ###
### Coding Exercise 1: Thread Creation - MultExecutor ###
### Thread Creation - MultiExecutor Solution ###

## Threading Fundamentals - Thread Coordination ##
### Thread Termination & Daeomon Threads ###
### Quiz 3: Thread Termination & Daemon Threads ###
### Joining Threads ###
### Coding Exercise 2: Multithreaded Calculation ###
### Multithreaded Calculation - Solution ###

## Performance Optimization ##
### Introduction to Performance & Optimizing for Latency - Part 1 ###
### Optimizing for Latency Part 2 - Image Processing ###
### Optimizing for Throughput Part 1 ###
### Optimizing for Throughput Part 2 - HTTP Server + JMeter ###
### Quiz 4: Performance Optimization ###

## Data Sharing Between Threads ##
### Stack & Heap Memory Regions ###
### Quiz 5: Stack & Heap Memory Regions ###
### Resource Sharing & Introduction to Critical Sections ###

## The Concurrency Challenges & Solutions ##
### Critical Section & Synchronization ###
### Quiz 6: Critical Section & Synchronization ###
### Atomic Operations, Volatile & Metrics Practical Example ###
### Quiz 7: Atomic Operations, Volatile & Metrics Practical Example ###
### Coding Exercise 3: Min - Max Metrics ###
### Race Conditions & Data Races ###
### Quiz 8: Data Races ###
### Locking Strategies & Deadlocks ###
### Quiz 9: Locking Strategies & Deadlocks ###

## Advanced Locking ##
### ReentrantLock Part 1 - tryLock and interruptible Lock ###
### ReentrantLock Part 2 - User Interface Application Example ###
### Quiz 10 - ReentrantLock ###
### Reentrant Read Write Lock & Database Implementation ###
### Quiz 11 - Read-Write Locks ###
### Coding Exercise 4: Product Reviews Service ###
### Product Reviews Service - Solution ###

## Inter-Thread Communication ##
### Semaphore - Scalable Producer Consumer Implementation ###
### Quiz 12: Semaphores - Barrier ###
### Condition Variables - All purpose, Inter-Thread Communication ###
### Objects as Condition Variables - wait(), notify(), and notifyAll() ###
### Quiz 13: Condition Variables ###

## Lock-Free Algorithms, Data-Structures & Techniques ##
### Introduction to Non-Blocking, Lock Free Operations ###
### Atomic Integers & Lock Free E-Commerce ###
### Quiz 14: Lock-Free Algorithms, Data-Structures & Techniques ###
### Atomic References, Compare And Set, Lock-Free High Performance Data Structure ###

## Beyond Multithreading - Final Lecture ##
### Distributed Systems, Big Data & Performance ###
### Bonus Material - Courses Links and Coupons ###