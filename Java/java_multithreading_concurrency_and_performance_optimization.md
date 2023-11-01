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
4. What threads are - Introduction to OS
	1. OS - loaded from disk into memory
		1. It takes over and provides an abstraction layer for us and helps us interact with hardware and CPU (focus is shifted to developing apps instead of managing hardware resources)
		2. application stays on disk first
			1. OS takes program and an instance of the program is created in memory (the instance is called a process or context)
				1. Each process is completely isolated from other processes in the system
				2. A process consists of metadata
					1. PID
					2. Files opened for reading and writing
					3. Program instructions
					4. Heap
					5. Main thread
						1. Contains
							1. Stack
							2. Instruction pointer
		3. In a multithreaded application, each thread comes with its own stack and ip
			1. All rest of the components in the process are shared by all threads
			2. Stack - it is a region of memory, where local variables are stored, and passed into functions
			3. Instruction pointer - Address of the next instruction to execute
		4. Each thread is executing a different instruction in same or different function in any given moment
			1. Hence separate instruction pointer
			2. Hence separate call stack (for function local variables and return addresses)
5. Summary
	1. Motivation for multithreading
		1. Responsiveness achieved by concurrency
		2. Performnance achieved by parallelism
	2. Threads are and what they contain
		1. Stack
		2. Instruction pointer
	3. What threads share
		1. Files
		2. Heap
		3. Code

### Operating Systems Fundamentals - Part 2 ###
1. What we learn in this lecture
	1. Context switch
		1. Each process may have one or more threads
			1. The threads are competing to get executed on the CPU (there are way more threads than the cores)
				1. OS needs to run a thread, stop it, run another thread, stop it, ...
		2. Context switch: The process of
			1. Stop thread 1
			2. Schedule thread 1 out
			3. Scheudle thread 2 in
			4. Start thread 2
			5. ...
		3. Context switch cost
			1. Context switch is not cheap, and is the price of multitasking (concurrency)
			2. Same as we humans when we multitask - takes time to focus
				1. We are not productive during the time we are interrupted and we need to switch to another task
					1. Each thread consumes resources in the CPU and memory (kernel resources)
						1. Tasks to perform during context switch
							1. Store data for one thread
							2. Restore data for another thread
		4. Key takeaways
			1. Too many threads - Thrashing, spending more time in management than real productive work (running our tasks)
			2. Threads consume less resources than processes
				1. They share a lot of resources among themselves
					1. Context switches between threads from the same process is cheaper than context switches between different processes
	2. Thread scheduling
		1. Example: Doing homework in text editor, listening to music
			1. Music player - has two threads
				1. Music - loading and playing through speakers
				2. User Interface - responds to user input (mouse clicks, keyboard buttons)
			2. Text Editor - has two threads
				1. File Saver - saves file every two seconds
				2. User Interface
		2. Suppose there is one core and 4 threads we need to decide how to schedule on the core
			1. Who runs first?
				1. Say: FCFS (fair)
					1. File Saver, Text Editor UI, Music Player, Music Player UI
						1. Problem - Long thread can cause starvation (if long thread arrived first, it will cause starvation to other threads)
							1. May cause User Interface threads being unresponsive - Bad User experience (if the UI thread is starving)
				2. Observation - UI threads are typically shorter (they just respond to a user input and update screen)
					1. Shortest Job First
						1. Problem - If many user related tasks coming all the time, we will keep scheduling only them and longer tasks may not get executed
				3. OS looks for a tradeoff
					1. OS divides time into moderately sized pieces called epocs
						1. In each epoc - OS allocates different time-slice for each thread
							1. Not all threads complete in a given epoc
					2. How to allocate time slice?
						1. Dynamic priority is calculated
						
								Dynamic Priority = Static Priority + Bonus (bonus can be negative) # for each thread
								
							1. Static Priority is set by the developer programmatically
							2. **Bonus** is adjusted by the Operating System in every epoch, for each thread
								1. If certain threads need more immediate attension, they get higher **Bonus** value
								2. Or OS will give preference to threads that did not complete in the last epochs, or did not get enough time to run - preventing starvation
	3. Threads vs Processes
		1. Multiple threads
			1. Prefer if the tasks share a lot of data
			2. Threads are much faster to instantiate and destroy
			3. Switching between threads of the same process is faster (shorter context switches)
		2. Multi-Process Architecture
			1. Security and stability (?) are of higher importance
				1. They are completely isolated from each other
				2. Unlike multiple threads where a single faulty thread can bring down the entire application (a faulty process does not bring down the entire application with multiple processes)
			2. Tasks are unrelated to each other
2. Summary
	1. Context Switches, and their impact on performance (thrashing)
	2. How thread scheduling works in the Operating System
	3. When to prefer Multithreaded over Multi-Processes architecture

## Threading Fundamentals - Thread Creation ##
### Threads Creation - Part 1, Thread Capabilities & De	bugging ###
1. What we learn in this lecture
	1. Thread creation with `java.lang.Runnable`
	2. `Thread` class capabilities
	3. Thread Debugging
2. Simple java project
	1. All threads related properties and methods are encapsulated in `Thread` class by JDK

			Thread thread = new Thread(); // It is empty by default
			
			Thread thread = new Thread (new Runnable () {
				@Override
				public void run() {
					// Code that we will run in a new thread - it is scheduled by OS
					
				}
			}); // lambda can be used
			
			System.out.println("We are in thread: " + Thread.currentThread().getName() + " before starting a new thread");
			thread.start(); // instructs JVM to construct a new thread and pass it to the OS
			System.out.println("We are in thread: " + Thread.currentThread().getName() + " after starting a new thread");
			
			Thread.sleep(10000); // it does not spin in a loop. It only instructs OS to not schedule the thread until that time passes (doesn't consume any CPU)
			
		1. Main thread is `main`
		2. New thread takes time (for scheduling by OS)
3. `Thread` class capabilities
	1. Give a name to thread

			thread.setName("New Worker Thread");
			
	2. We can set static priority for a thread programmatically

			thread.setPriority(Thread.MAX_PRIORITY); 
			
		1. For large programs that need better response time, this will play a major role
4. Debugging
	1. Put breakpoints
		1. Threads tab
			1. stack traces
	2. **When we hit a breakpoint, all threads freeze** (to check each thread individually)
	3. Catching unchecked exception

				...
				throw new RuntimeException("Intentional Exception");
				...

			thread.setUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
				@Override
				public void uncaughtException(Thread t, Throwable b) {
					System.out.println("A critical error happened in thread " + t.getName() + " the error is " + e.getMessage());
				}
			});
			
		1. If an uncaught exception gets thrown in any of the threads spawned from main thread will be caught by the handler
		2. Purpose: To clean up some of the resources or log additional data to enable us troubleshoot any issues after the fact
	 
### Threads Creation - Part 2, Thread Inheritance ###
1. What we learn in this lecture:
	1. Thread creation with java.lang.Thread
	2. Case study - interactive mutithreaded application
2. Using `Runnable` is easier and faster to code
3. Extending `Thread` class (it implements `Runnable` interface)

		public static void main(String[] args) {
			Thread thread = new NewThread();
			thread.start();
		}

		private static class NewThread extends Thread {
		
			@Override
			public void run() {
				System.out.println("Hello from " + Thread.currentThread().getName());
			}
			
		}	
		
	1. We get access to methods that are directly related to the thread

			System.out.println("Hello from " + this.getName());
			
4. Case study
	1. Example: Consider a vault where money is stored and it is locked
		1. We want to know how long it might take to guess the code and take the money (for hackers)
			1. Hackers - Brute force (threads)
			2. Police (thread) - counts upto 10 seconds and if hackers were not able to break the vault, the police will arrest them
				1. Police shows us progress of it's arrival on screen
	2. Implementation: 

			public class Main {
				public static void main(String[] args) {
					Random random = new Random();
					
					Vault vault = new Vault(random.nextInt(MAX_PASSWORD));
					
					List<Thread> threads = new ArrayList<>();
					
					threads.add(new AscendingHackerThread(vault));
					threads.add(new DescendingHackerThread(vault));
					threads.add(new PoliceThread());
					
					for (Thread thread : threads) {
						thread.start();
					}
				}
				
				private static class Vault {
					private int password;
					public Vault(int password) {
						this.password = password;
					}
					
					public boolean isCorrectPassword(int guess) {
						try {
							Thread.sleep(5);
						} catch (InterruptedException e) {
						
						}
						return this.password == guess;
					}
				}
				
				private static abstract class HackerThread extends Thread {
					protected Vault vault;
					
					public HackerThread(Vault vault) {
						this.vault = vault;
						this.setName(this.getClass().getSimpleName());
						this.setPriority(Thread.MAX_PRIORITY);
					}
					
					@Override
					public void start() {
						System.out.println("Staring thread " + this.getName());
						super.start();
					}
				}
				
				private static class AscendingHackerThread extends HackerThread {
					public AsendingHackerThread(Vault vault) {
						super(vault);
					}
					
					@Override
					public void run() {
						for (int guess = 0; guess < MAX_PASSWORD; guess++) {
							if (vault.isCorrectPassword(guess)) {
								System.out.println(this.getName() + " guessed the password " + guess);
								System.exit(0);
							}
						}
					}	
				}
				
				private static class DescendingHanderThread extends HackerThread {
					public AsendingHackerThread(Vault vault) {
						super(vault);
					}
					
					@Override
					public void run() {
						for (int guess = MAX_PASSWORD; guess >= 0; guess--) {
							if (vault.isCorrectPassword(guess)) {
								System.out.println(this.getName() + " guessed the password " + guess);
								System.exit(0);
							}
						}
					}
				}
				
				private static class DescendingHanderThread extends HackerThread {
					public AsendingHackerThread(Vault vault) {
						super(vault);
					}
					
					@Override
					public void run() {
						for (int i = 10; i >= 0; i--) {
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
							
							}
							System.out.println(i);
						}
						
						System.out.println("Game over for you hackers");
						System.exit(0);
					}
				}
			}
			
		1. Diagram

			![multithreading_example.png](multithreading_example.png)
			
1. Summary:
	1. `Thread` class - Encapsulates all thread related functionality
	2. Two ways to run code on a new thread
		1. Implement `Runnable` interface, and pass to a new `Thread` object
		2. Extend `Thread` class, and construct an object of that class
	3. Both ways are equally correct (our preference)

### Coding Exercise 1: Thread Creation - MultiExecutor ###

		public MultiExecutor(List<Runnable> tasks) {
        	// Complete your code here
        	for (Runnable task : tasks)
          	new Thread(task).start();
    	}

### Thread Creation - MultiExecutor Solution ###

		import java.util.ArrayList;
		import java.util.List;
		 
		public class MultiExecutor {
		    
		    private final List<Runnable> tasks;
		 
		    /*
		     * @param tasks to executed concurrently
		     */
		    public MultiExecutor(List<Runnable> tasks) {
		        this.tasks = tasks;
		    }
		 
		    /**
		     * Executes all the tasks concurrently
		     */
		    public void executeAll() {
		        List<Thread> threads = new ArrayList<>(tasks.size());
		        
		        for (Runnable task : tasks) {
		            Thread thread = new Thread(task);
		            threads.add(thread);
		        }
		        
		        for(Thread thread : threads) {
		            thread.start();
		        }
		    }
		}

## Threading Fundamentals - Thread Coordination ##
### Thread Termination & Daeomon Threads ###
1. What we learn in this lecture
	1. Thread termination (from one thread to another thread)
	2. Thread.interrupt()
	3. Daemon threads
2. Why and When we want to terminate a thread?
	1. Threads consume resources (even when thread is not doing anything)
		1. Memory and kernel resources
		2. CPU cycles and cache memory
	2. If thread finished its work, but application is still running
		1. We want to clean up thread's resources (which are being consumed by finished thread)
	3. If a thread is misbehaving, we want to stop it
		1. It might be sending requests to servers (which is not responding)
	4. By default, application will not stop as long as at least one thread is still running
		1. Even if main thread stopped running
			1. We want the ability to stop all threads gracefully before closing the application
3. `Thread.interrupt()` - Each thread object has a method called interrupt
	1. Thread A - `threadB.interrupt()` -> Thread B
		1. Sending interrupt signal to Thread B in an attempt to interrupt thread B
4. When can we interrupt a thread?
	1. If thread is executing a method that throws an `InterruptedException`
	2. If thread's code is handling the interrupt signal explicitly
5. Example:

		package thread.interrupt;
		
		public class Main {
			public static void main(String[] args) {
				Thread thread = new Thread(new BlockingTask());
				
				thread.start();
				
				thread.interrupt(); // interrupted exception gets thrown
			}
			
			private static class Blocking implements Runnable {
				@Override
				public void run() {
					try {
						Thread.sleep(500000);
					} catch (InterruptedException e) {
						System.out.println("Exiting blocking thread");
					}
				}
			}
		}
		
6. Example:

		public class Main {
			public static void main(String[] args) {
				Thread thread = new Thread(new LongComputationTask(new BigInteger("200000"), new BigInteger("10000000000"));

				thread.start(); // calculation will take a very long time

				thread.interrupt(); // The thread does not have any logic to handle this interrupt
			}
			
			private static class LongComputationTask implements Runnable {
				private BigInteger base;
				private BigInteger power;
				
				public LongComputationTask(BigInteger base, BigInteger power) {
					this.base = base;
					this.power = power;
				}
				
				@Override
				public void run() {
					System.out.println(base + "^" + power + " = " + pow(base, power));
				}
				
				private BigInteger pow(BigInteger base, BigInteger power) {
					BigInteger result = BigInteger.ONE;
					
					for (BigInteger i = BitInteger.ZERO; i.compareTo(power) != 0; i = i.add(BigInteger.ONE)) {
						if (Thread.currentThread().isInterrupted()) {
							System.out.println("Prematurely interrupted computation");
							return BitInteger.ZERO;
						}
						result = result.multiply(base);
					}
					
					return result;
				}
			}
		}
		
	1. Find hotspot
		1. In each iteration, check if current thread has got interrupted from the outside world
7. Daemon Threads
	1. Background threads that do not prevent the application from existing if the main thread terminates
	2. Scenario 1:
		1. Background tasks (not the main focus of the application)
			1. That should not block our application from terminating
		2. Example: File saving thread in a Text Editor (every few minutes)
			1. We don't want to wait for this thread to finish
	3. Scenario 2:
		1. Code in a worker thread is not under our control, and we do not want it to block our application from terminating
		2. Example: Worker thread that uses an external library (that might not handle interrupt signal)

				
				thread.setDaemon(true);
				// ...

				for (BigInteger i = BitInteger.ZERO; i.compareTo(power) != 0; i = i.add(BigInteger.ONE)) {
					result = result.multiply(base);
				}
				
			1. Even if main thread ends, the entire app is allowed to terminate
8. Summary:
	1. Learned how to stop threads by calling `thread.interrupt()`
	2. If method does not respond to interrupt signal by throwing `InterruptedException`, we need to check for that signal and handle it ourselves
	3. To prevent thread from blocking our app from exiting
		1. We set thread to be a daemon thread

### Quiz 3: Thread Termination & Daemon Threads ###
### Joining Threads ###
1. What we learn in the lecture
	1. Threads coordination with `Thread.join()`
	2. Case study
2. How to guarantee that the thread upon which we depend completes its work by the time we expected
	1. For full control over tasks (to run in parallel)
		1. We also want to safely and correctly aggregate results
3. Different threads run independently (of each other by default)
4. Order of execution is out of our control
	1. Example: ThreadA finishes before Thread B or other way, they might run concurrently or in parallel
5. Thread coordination - Dependency
	1. What if one thread depends on another thread?
	
			Thread A
				| Output
				|
				| Input
				v
			Thread B
			
		1. How will Thread B know that Thread A has finished computing the output (and is not accessing an intermediate or partial result)?
			1. Naive solution:
				1. Thread B runs in a loop and keeps checking if Thread A' result is ready

						void waitForThreadA() {
							while (!threadA.isFinished()) {
								// burn CPU cycles
							}
						}
						
					1. Busy wait
						1. Inefficient and wasteful

								Thread B | Thread A  | Thread B | Thread A
								Check      doing work  Check      doing work
								  ^
								  |
								  waste
								  
						2. Better solution: Thread B checks and goes to sleep (get out of the way completely), Thread A finishes work, then Thread B will wake up using the results computed by Thread A
							1. Implementation: `Thread.join()`
								1. `public final void join()`
								2. `public final void join(long millis, int nanos)`
								3. `public final void join(long millis)`
6. Example: Factorial calculation (CPU intensive task)

		public static class FactorialThread extends Thread {
			private long inputNumber;
			private BigInteger result = BigInteger.ZERO;
			private boolean isFinished = false;
			
			public FactorialThread(long inputNumber) {
				this.inputNumber = inputNumber;
			}
			
			@Override
			public void run() {
				this.result = factorial(inputNumber);
				this.isFinished = true;
			}
			
			public BigInteger factorial(long n) {
				BigInteger tempResult = BigInteger.ONE;
				
				for (long i = n; i > 0; i--) {
					tempResult = tempResult.multiply(new BigInteger(Long.toString(i)));
				}
				return tempResult;
			}
			
			public boolean isFinished() {
				return isFinished;
			}
			
			public BigInteger getResult() {
				return result;
			}
		}
		
		public class Main {
			public static void main(String[] args) {
				List<Long> inputNumbers = Arrays.asList(0L, 3435L, 35435L, 2324L, 4656L, 23L, 5556L);
				
				List<FactorialThread> threads = new ArrayList<>();
				
				for (long inputNumber : inputNumbers) {
					threads.add(new FactorialThread(inputNumber));
				}
				
				for (Thread thread : threads) {
					thread.start(); // this and checking result have a race condition
				}
				
				for (int i = 0; i < inputNumbers.size(); i++) {
					FactorialThread factorialThread = threads.get(i);
					if (factorialThread.isFinished()) {
						System.out.println("Factorial of " + inputNumbers.get(i) + " is " + factorialThread.getResult());
					} else {
						System.out.println("The calculation for " + inputNumbers.get(i) + " is still in progress");
					}
				}
			}
		}
		
	1. Race condition: Two threads race towards their goals independently (no coordination)
		1. Solution: Forcing main to wait until all factorials are finished

				for (Thread thread : threads) {
					thread.join(); // returns only when the thread has terminated
				} // all factorial calculations are guaranteed to be finished
7. What if one of the numbers is large (from a file or user input) - edge case
	1. Other calculations are ready but cannot complete
		1. Solution: How long we are willing to wait for each of the worker threads

				thread.join(2000); // 2 seconds only
				
			1. Other thread is still running (can be solved to terminate elegantly) - convert it to daemon thread
8. Thread coordination: `Thread.join()`
	1. More control over independent threads
	2. Safely collect and aggregate results
	3. Gracefully handle runaway threads using `Thread.join(timeout)`
9. Summary
	1. Do not rely on the order of execution (of other threads)
	2. Always used thread coordination (to get reliable results)
	3. Design code for worst case scenario (defensive programming)
		1. Assume that: Threads may take unreasonably long time to finish
	4. Always use `Thread.join(...)` with time limit
		1. Stop the thread if it's not done in time

### Coding Exercise 2: Multithreaded Calculation ###
### Multithreaded Calculation - Solution ###

## Performance Optimization ##
### Introduction to Performance & Optimizing for Latency - Part 1 ###
1. What we learn in this lecture
	1. Performance criteria/ definition
	2. Performance in Multithreaded applications
	3. Latency
2. Performance (This can be measured differently for different use cases and different scenarios)
	1. Use cases:
		1. High Speed Trading System
		
				Buy Request	->	|     | -> Purchase
									| App |
				Sell Request	->	|     | -> Sale
										^
										|
									Latency
									
			1. Performance measured in latency
				1. The faster the transaction is, the performant the application is considered to be
				2. Latency measured in units of time
		2. Video Player
		
				App - Frames -> TV
				      [][][]
				      
			1. Delivering all frames as fast as possible would be terrible (1000 frames per second is too fast if the movie is 120 frames per second)
				1. Solution: We want to show movie at the correct frame rate (with minimum jitter)
					1. Performance metric: precision and accuracy of frame rate
		3. Machine Learning
		
				Large Data -Data-> Machine Learning -Prediction->
				
			1. Every 24 hours, prediction must be done
				1. The more data that the system can inject into the system, the better for us
					1. Performance metric: throughput (latency or lack or jitter is not important)
3. Performance in Multithreading (General case)
	1. Latency - The time to completion of a task. Measured in time units
	2. Throughput - The amount of tasks completed in a given period. Measured in tasks/time unit
4. Improving one may not have impact on the other or may even have adverse effect on the other
5. Latency:

		<----- Task ----->
				Latency = T
				
	1. We can break the task into multiple independent tasks

			Task1|task2| | | || | TaskN
			
		1. Schedule the sub-tasks to run in parallel to each other

				Latency = T/N
				
			1. N - number of sub-tasks
	2. Theoretical reduction of latency by N = Performance improvement by a factor of N
		1. N = ?
			1. How many subtasks/ Threads to break the original task?
		2. Does breaking original task and aggregating results coming for free?
		3. Can we break any task into subtasks?
6. N = ?
	1. On a general purpose computer: N = number of cores (as close as possible)
		1. Reduction of latency can be achieved by running the sub-tasks fully in parallel
			1. This is possible only if we run them in multiple cores
	2. OS tries it's best to schedule the tasks on available cores
		1. If no other tasks are running (utilizing hardware as best as it can to give the optimal performance)
			1. If we add a single additional thread (counter productive)
				1. Reduces performance and increases the latency
					1. The additional thread pushes the other thread back and forth resulting in context switches, bad cache performance, extra memory consumption:

							core 1 <- Thread 1
							core 2 <- Thread 2
							...
							core N <- Thread N
							Idle   <- Thread N + 1
							
						1. Thread N + 1 can push any of the Thread [1..N] out and cause context switch
						2. This can get repeated for any of the threads
		2. N = ? - Notes
			1. No of threads = No of cores
				1. It is optimal only if all threads are runnable and can run without interruption
					1. No IO/blocking calls/sleep
				2. In reality, the result will be rarely optimal but we can be close to that
			2. The assumption is that nothing else is running that consumes a lot of CPU
				1. Never the case
					1. Unless we have a dedicated server
						1. OS and other processes would have a negligible impact on application threads
			3. Hyperthreading - Virtual Cores vs Physical Cores
			
										|
								Physical Core
								[HW Unit 2]
										|
					[HW Unit 1]		|	[HW Unit 2]
										|
					Virutal Core 1	|	Virtual Core 2
					
				1. A physical core can run two threads at a time (we cannot get 100% parallelism)
					1. Certain HW units are duplicated (to run the threads in parallel)
					2. Certain HW units are shared
	3. Inherent Cost of Parallelization and Aggregation
		1. Cost of breaking tasks into many & aggregating the results
			
				Breaking task into multiple tasks (calculation cost) 
				+
				Thread creation, passing tasks to threads (cost)
				+
				Time between thread.start() to thread getting scheduled (by OS and run)
				+
				Time until last thread finishes and signals (aggregation - not all tasks take the same time)
				+
				Time until the aggregating thread runs (gets signal and runs again)
				+
				Aggregation of subresults into a single artifact
				
		2. Latency vs Original Task Latency
			1. Multithreaded solution has a constant penalty we have to pay for any size of tasks
				1. The longer the heavier the task is, it is worthwhile to run in parallel
					1. Point where we need to decide is at the intersection between multithreaded solution and single threaded solution
						1. Small and trivial tasks don't do well with parallel execution
		3. Can we break any task into subtasks?
			1. No
				1. Three types of tasks
					1. Tasks that are inherently parallelizable and can be broken into sub-tasks
					2. Tasks that cannot be parallelizable
						1. We are forced to run as single thread
					3. Tasks that can be partially broken into subtasks and partially needed to be run sequentially
7. Summary:
	1. Performance can be defined in many ways depending on the use case
	2. Multithreaded applications performance criteria
		1. Latency
		2. Throughput
	3. Latency reduction by breaking the task into multiple, and running in parallel
		1. Setting expectations as to what can and cannot be achieved by this approach

### Optimizing for Latency Part 2 - Image Processing ###
1. What we learn in the lecture
	1. Image processing - sequential
	2. Image processing - multi-threaded
	3. Performance/ latency measurement
2. Digital pictures:
	1. Pixels - single color points
		1. Each pixel is represented by 4 bytes
			1. ARGB
				1. A - Alpha (transparency)
				2. R - Red
				3. G - Green
				4. B - Blue
			2. We can combine RGB to get pretty much any color
				1. If all colors are the same, we get gray (from white to black)
3. Recoloring algorithm (modular):

		public class Main {
			public static final String SOURCE_FILE = "./resources/many-flowers.jpg";
			public static final String DESTINATION_FILE = "./out/main-flowers.jpg";
		
			public static void main(String[] args) {
				BufferedImage originalImage = ImageIO.read(new File(SOURCE_FILE)); // BufferedImage - specifies pixels, color space, dimentions, convenient methods to manipulate pixels of image
				BufferedImage resultImage = new BufferedImage(originaImage.getWidth(), originalImage.getHeight(), BufferedImage.TYPE_INT_RGB);
				
				recolorSingleThreaded(originalImage, resultImage);
				
				File.outputFile = new File(DESTINATION_FILE);
				ImageIO.write(resultImage, "jpg", outputFile);
			}
			
			public static void recolorSingleThreaded(BufferedImage originalImage, BufferedImage resultImage) {
				recolorImage(originalImage, resultImage, 0, 0, originalImage.getWidth(), originalImage.getHeight());
			}
			
			public static void recolorImage(BufferedImage originalImage, BufferedImage resultImage, int leftCorder, topCorner, int width, int height) {
				for (int x = leftCorner; x < leftCorder + width && x < originalImage.getWidth(); x++) {
					for (int y = topCorner; y < topCorner + height && originalImage.getHeight(); y++) {
						recolorPixel(originalImage, resultImage, x, y);
					}
				}
			}
			
			public static void recolorPixel(BufferedImage originalImage, BufferedImage resultImage, int x, int y) {
				int rgb = originalImage.getRGB(x, y);
				int red = getRed(rgb);
				int green = getGreen(rgb);
				int blue = getBlue(rgb);
				
				int newRed;
				int newGreen;
				int newBlue;
				
				if (isShadeOfGray(red, green, blue)) {
					newRed = Math.min(255, red + 10);
					newGreen = Math.max(0, green - 80);
					newBlue = Math.max(0, blue - 20);
				} else {
					newRed = red;
					newGreen = green;
					newBlue = blue;
				}
				
				int newRGB = constructeRGBFromColors(newRed, newGreen, newBlue);
				setRGB(resultImage, x, y, newRGB);
			}
			
			public static void setRGB(BufferedImage image, int x, int y, int rgb) {
				image.getRaster().setDataElements(x, y, image.getColorModel().getDataElements(rgb, null);
			}
			
			public static boolean isShadeOfGray(int red, int green, int blue) {
				return Math.abs(red - green) < 30 && Math.abs(red - blue) < 30 && Math.abs(green - blue) < 30; // found empirically
			}
			
			public static int constructRGBFromColors(int red, int green, int blue) {
				int rgb = 0;
				rgb |= (red << 16);
				rgb |= (green << 8);
				rgb |= blue;
				rgb |= 0xFF000000; // opaque
				return rgb;
			}
			
			public static int getRed(int rgb) {
				return ((rgb & 0x00FF0000) >> 16);
			}
			
			public static int getRed(int rgb) {
				return ((rgb & 0x0000FF00) >> 8);
			}
			
			public static int getBlue(int rgb) {
				return (rgb & 0x000000FF);
			}
		}
		
4. Multithreaded solution:
	1. Break the image into many pieces
		1. 2 threads - 2 pieces
		2. 4 threads - 4 pieces
	2. Solution:

			public static void main(String[] args) {
				// ...
				long startTime = System.currentTimeMillis();
			
				// recolorSingleThreaded(originalImage, resultImage);
				int numberOfThreads = 1; //2, 3, 4, 5, 6
				recolorMultiThreaded(originalImage, resultImage, numberOfThreads);
			
				long endTime = System.currentTimeMillis();
			
				long duration = endTime - startTime;
			
				// ...
			
				System.out.println(String.valueOf(duration));
			}

			public static void recolorMultithreaded(BufferedImage originalImage, BufferedImage resultImage, int numberOfThread) {
				List<Thread> threads = new ArrayList<>();
				int width = originalImage.getWidth();
				int height = originalImage.getHeight() / numberOfThreads;
				
				for (int i = 0; i < numberOfThreads; i++) {
					final int threadMultiplier = i;
					
					Thread thread = new Thread(() -> {
						int leftCorner = 0;
						int topCorner = height * threadMultiplier;
						
						recolorImage(originalImage, resultImage, leftCorner, topCorner, width, height);
					});
					
					threads.add(thread);
				}
				
				for (Thread thread : threads) {
					thread.start();
				}
				
				for (Thread thread : threads) {
					try {
						thread.join();
					} catch (InterruptedException e) {
						System.out.println("Interrupted!!!");
						return;
					}
				}
			}
			
		1. Between 4 (physical cores) - 8 (virtual cores), it is lowest for around 6 threads
			1. Reasons?
				1. Pairs of virtual cores share some resources among themselves
				2. Computer running the benchmark is not fully dedicated to our application
					1. Some CPU resources consumed by other OS processes and other background applications
			2. If number of threads is increased steadily, no benefit
		2. If we keep the number of threads fixed at 6 and compare for different resolutions
			1. If source resolution gets smaller (upto 759 x 1012 it is beneficial)
5. Summary
	1. We can get a speed up if we partition a problem into multiple sub-problems (performed by multiple threads)
	2. More threads than cores is counterproductive (for threads with only computation and no blocking calls)
	3. There is inherent cost for running an algorithm by multiple threads
	
### Additional Resource - Image Processing, Color Spaces, Extraction & Manipulation ###

### Optimizing for Throughput Part 1 ###
1. What we learn in this lecture
	1. Throughput definition
	2. 2 approaches to throughput improvement
	3. Thread pooling
2. Throughput - number of tasks completed in a given period
	1. Measured in tasks/time unit (typically in seconds)
3. When does it matter?

		- task1 -> |        |
		- task2 -> | System |
		- task3 -> |        |
		- task4 -> |        |

	1. If we have concurrent tasks and we want to perform as many of them as possible as fast as possible
		1. Increase throughput
4. 2 approaches to throughput improvement
	1. Approach 1: Breaking Tasks into Subtasks

			<------- original task ------->
						Latency = T
			
			Throughput = 1/T
			
		1. If we break task into sub-tasks

				Thread 1 -> Sub-task 1
				Thread 2 -> Sub-task 2
				Thread 3 -> Sub-task 3
				...
				Thread N -> Sub-task N
				            <--------->
				            Latency = T/N
				            
			1. Throughput = N/T (theoretical)
				1. T - Time to execute original task
				2. N - Number of subtasks or Number of Threads
			2. This is N times better than performing tasks sequentially
				1. Throughput < N/T - in practice
					1. Breaking and scheduling into multiple tasks and combining results has a cost
						1. It is unnecessary (for throughput)
	2. Approach 2: Running Tasks in Parallel

			<------ Task 1 ------>
			<------ Task 2 ------>
			<------ Task 3 ------>
			         ...
			<------ Task N ------>
			     Latency = T
			     
			Throughput = N/T
			
		1. In practice, we are much more likely to achieve this throughput than by breaking tasks into smaller sub-tasks (to reduce latency of each individual task)
			1. The tasks are un-related and independent from each other
				1. No breaking task into multiple subtasks (no pre-processing)
				2. No time until the last thread finishes and signals
				3. No time until the aggregating thread runs (no post-processing)
				4. No aggregation of subresults into single artifact (no post-processing)
				5. We can eliminate the following using advanced techniques (thread pooling, cache friendly non-blocking queues)
					1. Thread creation, passing tasks to threads
					2. Time between thread.start() to thread getting scheduled
5. Thread Pooling
	1. Threads are instantiated only once and re-used for future tasks (instead of instantating them for each task)
	2. The tasks are distributed to the threads from a queue
		1. Thread picks a task from the queue when it is available
			1. If all threads are busy, the tasks will just wait in the queue until any thread becomes available
	3. Technique:
		1. If we keep the threads as busy as possible by keep feeding tasks into the threads, we can get maximum throughput and maximum unitilization of our resources
	4. Thread pooling - implementation
		1. Implementing a thread pool is not trivial
			1. Implementing a low overhead and efficient queue may need en entire course
		2. JDK comes with a few implementations of thread pools
			1. Fixed thread pool executor (example)
				1. It constructs a thread pool with fixed number of threads in the pool (comes with built in queue)

						int numberOfThreads = 4;
						Executor executor = Executors.newFixedThreadPool(numberOfThreads);
						
						Runnable task = ...;
						executor.execute(task);
						
6. Summary
	1. By serving each task on a different thread, in parallel, we can improve throughput by N
		1. N = number of threads = number of cores
	2. Using a Fixed thread pool, we can maintain constant number of threads, and eliminate need for recreation of threads
	3. The above should give a significant performance improvement (xN)

### Optimizing for Throughput Part 2 - HTTP Server + JMeter ###
1. What we learn in this lecture
	1. HTTP server
	2. Measure throughput using Apache Jmeter
	3. Performance measurement and analysis
2. HTTP Server - Search and Count Word

		-HTTP Request-> |             |
		-HTTP Request-> |             |
		-HTTP Request-> | HTTP Server |
		-HTTP Request-> |             |
		-HTTP Request-> |             |
		
	1. HTTP Server will load a very large book from the disk
		1. War and Peace - Tolstoy (several megabytes)
	2. HTTP Request:
		1. http://127.0.0.1:8000/search?word=talk
			1. App will search for the word in the book and count the number of times the word appears in the book
	3. HTTP Response:
		1. status: 200, body: 3443
3. Code:

		public class ThroughputHttpServer {
			private static final String INPUT_FILE = "resrouces/throughput/war_and_peace.txt";
			private static final in NUMBER_OF_THREADS = 1;
			public static void main(String[] args) {
				String text = new String(Files.readAllBytes(Paths.get(INPUT_FILE)));
				startServer(text);
			}
			
			public static void startServer(String text) {
				HttpServer server = HttpServer.create(new InetSocketAddress(8000), 0); // backlog size - size of queue for the HTTP requests - 0: Because requests should end in thread pool queue
				server.createContext("/search", new WordCountHandler(text)); // assigns handler object to HTTP route
				Executor executor = Executors.newFixedTHreadPool(NUMBER_OF_THREADS);
				server.setExecutor(executor);
				server.start(); // app will start listening for requests on port 8000
			}
			
			private static class WordCountHandler implements HttpHandler {
				private String text;
				
				public WordCountHandler(String text) {
					this.text = text;
				}
				
				@Override
				public void handle(HttpExchange httpExchange) throws IOException {
					String query = httpExchange.getRequestURI().getQuery();
					String[] keyValue = query.split("=");
					String action = keyValue[0];
					String word = keyValue[1];
					if (!action.equals("word")) {
						httpExchange.sendResponseHeaders(400, 0);
						return;
					}
					
					long count = countWord(word);
					
					byte[] response = Long.toString(count).getBytes();
					httpEschange.sendResponseHeaders(200, response.length);
					OutputStream outputStream = httpExchange.getResponseBody();
					outputStream.write(response);
					ouptutStream.close(); // sends response to client
				}
				
				private long countWord(String word) {
					long count = 0;
					int index = 0;
					while (index >= 0) {
						index = text.indexOf(word, index);
						
						if (index >= 0) {
							count++;
							index++;
						}
					}
					return count;
				}
			}
		}
		
	1. http://localhost:8000/search?word=talk
4. Apache JMeter
	1. Java performance automation tool - automated tool that allows us to define an automated performance test plan
	2. Does not require writing any code
	3. Jmeter is out of scope for your course
	4. Test plan:

			Jmeter Performance Test -HTTP Request-> HTTP Server
				^		http://127.0.0.1:8000/search?word=word1
				|
			2600 unique words		
			
		1. For each word, we can send HTTP request and wait for response
			1. Tool will send as many requests as possible and as fast as possible
				1. It gives throughput
					1. requests / test duration (time to get responses)
	5. Open JMeter
		1. Name: Word Count
			1. Add: Thread Group (group of Jmeter threads that are going to send http requests to http server)
				1. Number of threads (users): 200 (to run concurrently)
				2. Log Controller > While Controller (to interate over words)
					1. Add > Config Element > CSV Data Set Config
						1. Browse > search_words.csv
							1. Each line contains a unique word
					2. Variable Names (comma-delimited): WORD
					3. Delimiter: \n (each word is on new line)
					4. Recycle on EOF? False (read the file only once)
					5. Stop thread on EOF? True
				3. Condition (function or variable):

						${__jexl3("${WORD} != "<EOF>")}
				4. Right click on While Controller > Add > Sampler > HTTP Request
					1. Path: /search?word=${WORD}
					2. Protocol: http
					3. IP: localhost
					4. Port Number: 8000
				5. Right click on While Controller > Add > Listener > Summary Report
					1. Gives throughput and other metrics
				6. Right click on While Controller > Add > Listener > View Results Tree
					1. To inspect each request (for meaningful response)
		2. Execution of test plan
			1. Save test plan
			2. Run (1 thread)
				1. 304.2 requests/ second
			3. View Results Tree
				1. All are green (200)
				2. Click on request
					1. Response data
		3. Increase threadpool size to 2
			1. Throughput: 505.9 / sec (almost twice)
		4. threadpool size to 4
			1. Throughput: 713.5 / sec (higher)
		5. Graph:
			1. Steap improvement upto 4 (upto no of physical cores)
			2. Moderate improvement upto 8 (upto no of virtual cores)
			3. No improvement after 8
			4. There is improvement upto 8 (unlike in the case of latency)
				1. We eliminated cost of breaking and combining
5. Summary
	1. Optimized throughput of an HTTP backend server
	2. Right number of threads (number of threads = number of cores)
	3. Choose best strategy - handling each request on a different thread
	4. Eliminated some of the cost of multithreading by using a thread pool

### Quiz 4: Performance Optimization ###

## Data Sharing Between Threads ##
### Stack & Heap Memory Regions ###
1. What we learn in this lecture
	1. Stack memory region
	2. Heap memory region
2. The topics are important
	1. To successfully write multithreaded applications that give consistent and correct results and high performance
	2. Will also complete picture about process architecture
3. Stack memory region
	1. Each stack region belongs to a thread
		1. What is the stack?
			1. Memory region where
				1. Methods are called
				2. Arguments are passed
				3. Local variables are stored
			2. stack + Instruction Pointer = State of each thread's execution
	2. Example:

			void main(String[] args) {
				int x = 1;
				int y = 2;
				int result = sum(x, y);
			}
			
			int sum(int a, int b) {
				int s = a + b;
				return s;
			}
			
		1. Stack
			1. As soon as a thread jumps into a method, it immediately allocates some space on top of stack (called stack frame)
			2. args to method are pushed onto the frame
			3. Each local variable is pushed onto the stack in the order of appearance
			4. If another method is called from the current method, another stack frame is allocated on the stack
				1. Args of the new method are also pushed onto the stack
					1. Each method has access only to variables in it's own frame
						1. The local variables and arguments are copies of the actual variables
			5. When a method is finished, the result is stored in a special register in the CPU
			6. IP then jumps to caller method
			7. The nested method's stack frame is invalidated
			8. The result is pushed back to stack
			9. When main method finishes, the stack frame is invalidated
			10. Why is it called stack?
				1. The frames are allocated and invalidated in LIFO order
4. Run the code in interractive debugger
	1. Frames window
		1. main frame
			1. variables
				1. x = 1
				2. y = 2
		2. sum frame
			1. variables (only this frame variables are accessible)
				1. a = 1
				2. b = 2
				3. s = 3
		3. When we return from sum method, it's stack frame disappears
		4. main frame
			1. x = 1
			2. y = 2
			3. result = 3
		5. When we return, it's stack frame is also invalidated
5. Stack's properties
	1. All variables belong to the thread executing on that stack
		1. Other threads have no access to them
	2. Stack is statically allocated when the thread is created
	3. The stack's size is fixed, and relatively small (platform specific) - cannot change at runtime
	4. If our calling hierarchy is too deep.
		1. We may get a StackOverflow Exception
			1. Risky with recursive calls
6. Heap
	1. It is a shared memory region that belongs to the process
		1. All threads share data that is located on the heap
		2. Any thread can access and allocate objects on a heap at any moment
	2. What is allocated on the heap?
		1. Objects (anything created with new operator)
			1. String
			2. Object
			3. Collection
			4. ...
		2. Members of classes (primitive or object)
		3. Static variables
			1. They are members of Class object associated with that class
	3. Heap Memory Management
		1. It is governed and managed by Garbage Collector
		2. Objects - stay as long as we have a reference to them (at-least one)
			1. They are garbage collected sometime after all the references to the objects are lost
		3. Members or classes
			1. Exist as long as their parent objects exist
				1. Same life cycle as their parents
		4. Static variables - stay forever (for the lifetime of the application)
7. Objects vs References
	1. References != Objects

			Object referenceVar1 = new Object();
			Object referenceVar2 = referenceVar1;
			
			// both point to same object
			
		1. References
			1. Can be allocated on the _stack_ (if they are local variables in a method)
			2. Can be allocated on the _heap_ if they are members of a class
		2. Objects
			1. Always allocated on the _heap_
8. Memory Regions - Summary
	1. Heap (shared)
		1. Objects
		2. Class members
		3. Static variables
	2. Stack (exlusive to a thread)
		1. Local primitive types
		2. Local references

### Quiz 5: Stack & Heap Memory Regions ###
### Resource Sharing & Introduction to Critical Sections ###
1. What we learn in this lecture
	1. Resource sharing between threads
	2. Atomic operations
2. What is a resource?
	1. It represents data (or a state)
		1. Variables (integers, Strings, ...)
		2. Data Structure (arrays, collections, maps)
		3. File or connection handles (or Databases)
		4. Message or work queues
		5. Any Objects ...
3. What resources can be shared within a process?
	1. Everything we store in the heap
	2. Everything outside the process is also shared (out of scope for this discussion)
4. Why do we want to share resources?
	1. Text Editor (example)
		1. UI thread - responds to keyboard and mouse events, represents doc's view on the screen
		2. Document saver - saves document to the disk
	2. Both threads have access to the same data structure (that represents document)
		1. The data structure is a shared resource
		2. Benefit:
			1. Document saver thread can save user from losing work
				1. If app crashes
				2. If we lose power
	3. Work Queue

										 	<- Worker Thread 1
			Work Dispatcher -> Queue	<- Worker Thread 2
										  	<- Worker Thread 3
										  	
		1. Dispatcher thread takes input (through HTTP Request or User) and distributes the work using a shared queue
		2. Worker threads wait for work to arrive on the queue and grab the task from it as soon as they finish the current task
		3. The queue is backed by a data structure and is stored on the heap (as shared resource)
			1. New thread is not required for every single task (high performance)
		4. Good CPU utilization & low latency
	4. Database microservice

			HTTP POST                       |
			----------> Request Thread 1 -> |
			HTTP PUT                        |
			----------> Request Thread 2 -> | DB
			HTTP GET                        |
			----------> Request Thread 3 -> |
			HTTP DELETE                     |
			----------> Request Thread 4 -> |
			
		1. Microservice acts as a software abstraction layer on top of a database
			1. Every request is handled by a different thread
				1. All requests become reads or writes from/to db
			2. Connections are represented by object
				1. The objects are shared by request threads
					1. We must have shared connections (since there is only one DB)
5. Problem:

		public static void main(String[] args) {
			InventoryCounter inventoryCounter = new InventoryCounter();
			IncrementingThread incrementingThread = new IncrementingThread(inventoryCounter);
			DecrementingThread decrementingThread = new DecrementingThread(inventoryCounter);
			
			incrementingThread.start();
			incrementingThread.join();
			
			decrementingThread.start();
			decrementingThread.join();
			
			System.out.println("We currently have " + inventoryCounter.getItems() + " items");
		}

		public static class IncrementingThread extends Thread {
			private InventoryCounter inventoryCounter;
		
			public IncrementingThread(InventoryCounter inventoryCounter) {
				this.inventoryCounter = inventoryCounter;
			}
			
			@Override
			public void run() {
				for (int i = 0; i < 10000; i++) {
					inventoryCounter.increment();
				}
			}
		}
		
		public static class DecrementingThread extends Thread {
			private InventoryCounter inventoryCounter;
		
			public IncrementingThread(InventoryCounter inventoryCounter) {
				this.inventoryCounter = inventoryCounter;
			}
			
			@Override
			public void run() {
				for (int i = 0; i < 10000; i++) {
					inventoryCounter.decrement();
				}
			}
		}

		private static class InventoryCounter {
			private int items = 0;
			
			public void increment() { // when we get new delivery
				items++;
			}
			
			public void decrement() { // when someone purchased an item
				items--;
			}
			
			public int getItems() {
				return items;
			}
		}
		
	1. Result is 0
	2. Modification:

			incrementingThread.start();	
			decrementingThread.start();
			
			incrementingThread.join();
			decrementingThread.join();
			
		1. Unexpected result(s)
			1. We get different results
6. The core problem:
	1. `InventoryCounter` is a shared object
		1. This makes `items` member shared between two threads
	2. `items++` and `items--`
		1. Are happening in the same time
		2. Both are not atomic operations
			1. Atomic operation
				1. An operation or a set of operations is considered atomic, if it appears to the rest of the system as if it occured at once
				2. Single step - "all or nothing"
				3. No intermediate states (we cannot interrupt and observe intermediate states)
				4. `item++` - not an atomic operation:
					1. Get current value of items
						1. `currentValue <- items` (`= 0`)
					2. Increment current value by 1
						1. `newValue <- currentValue + 1` (`= 1`)
					3. Store the result into items
						1. `items <- newValue` (`= 1`)
	3. `items++` and `items--` concurrently (order depends on how they are scheduled)

			IncrementingThread				DecrementingThread
			1. currentVal <- items = 0
			2. newVal <- currentVal + 1
												3. currentVal <- items = 0
												4. newVal <- currentVal - 1
												5. items <- newVal = -1
			6. items <- newVal = 1

	4. `items = 1` - which is wrong (decrementing thread's work is overridden)

			IncrementingThread				DecrementingThread
			1. currentVal <- items = 0
			2. newVal <- currentVal + 1
												3. currentVal <- items = 0
												4. newVal <- currentVal - 1
			5. items <- newVal = 1			
												6. items <- newVal = -1

	5. `items = -1` - which is wrong (incrementing thread's work is overridden)
7. Summary
	1. Benefits of sharing resources between threads
	2. Challenge of multithreaded programming
	3. Case study about a non atomic operation, performed concurrently by different threads

## The Concurrency Challenges & Solutions ##
### Critical Section & Synchronization ###
1. What we learn in this lecture
	1. Critical Sections
	2. Synchronized - Monitor/ Lock
2. Critical Sections
	1. Concurrency problem
		1. Two threads sharing `items` counter
		2. Both threads were reading and modifying the counter at the same time
		3. The operations were not atomic
	2. Critical Section

			void aggregateFunction() {
				operation1();
				operation2();
				operation3();
				...
			}
			
		1. The set of operations need to be performed in such a way that they will appear as single atomic operation
			1. No two threads will be performing the set of operations at the same time

					void aggregateFunction() {
						enter critical section
						operation1();
						operation2();
						operation3();
						exit critical section
						...
					}
					
				1. Entry point and exit point
					1. If no thread currently executing the critical section then a thread can enter the section and execute the operations
					2. If another thread comes and tries to enter a critical section while there is a thread in it, it will be denied access and will be suspended until the first thread exits the critical section
					3. If first thread crosses the exit point of critical section, the second thread can enter the critical section and perform the operations
				2. Hence we can achieve atomicity for any number of distinct operations without worrying about concurrency issues
3. JVM with support from OS and hardware provides multiple tools to guard critical section from multiple access from multiple threads
	1. The concepts are extensible to other languages
		1. The API might be slightly different
4. Solutions:
	1. `synchronized`
		1. It is a locking mechanism
		2. Used to restrict access to a critical section or entire method to a single thread at a time
	2. Two methods
		1. Synchronized - Monitor

				public class ClassWithCriticalSections {
					public synchronized method1() {
						...
					}
					
					public synchronized method2() {
						...
					}
				}
				
			1. If multiple threads try to call the methods on the same object of the class, only one thread will be able to access either of the methods
				1. If Thread A is executing method1
					1. Thread B is deprived from executing method1 and method2 both (or any other synchronized method of the object)
						1. `synchronized` is applied per object
							1. It is called a monitor
						2. Every `synchronized` method is a door to a room
							1. If we lock one door, every other door gets locked immediately
	3. Critical sections:

			void increment() {
				items++;
			}
			
			void decrement() {
				items--;
			}
			
	4. Solution:

			public synchronized void increment() {
				items++;
			}
			
			public synchronized void decrement() {
				items--;
			}
			
			public synchronized int getItems() {
				return items;
			}
			
		1. The operations are executed safely (one thread at a time)
2. Method 2: `synchronized` - lock

		public class ClassWithCriticalSections {
			Object lockingObject = new Object();
		
			public void method1() {
				synchronized(lockingObject) {
					// ...
					critical section ...
					// ...
				}
			}
		}
		
	1. `lockingObject` serves as a lock (can be any object)
	2. Only one thread is allowed to execute that block
	3. Monitor method is equivalent to:

			public void method1() {
				synchronized(this) {
					...
				}
			}
			
			public void method2() {
				synchronized(this) {
					...
				}
			}
			
		1. This method provides a lot of flexibility:

				public class ClassWithCriticalSections {
					Object lock1 = new Object();
					Object lock2 = new Object();
					
					public void method1() {
						synchronized(lock1) {
							...
						}
					}
					
					public void method2() {
						synchronized(lock2) {
							...
						}
					}
				}
				
			1. Thread A can access first critical section while Thread B is executing the second critical section
			2. But both threads cannot execute the same critical section
		2. Another benefit: We don't have to make the entire method synchronized

				Object lockingObject = new Object();
				public void method1() {
					... 
					... // concurrent execution is allowed
					synchronized(lockingObject) { // non-concurrent
						critical section
					}
					... // concurrent execution is allowed
					...
					...
				}
				
			1. Only a small portion of method can be critical
				1. We want to minimize the code in the critical section to bare minimum (as small as possible)
					1. This enables more code to be executed concurrently by different threads
						1. Less code requires synchronization (maximizes performance)
3. Example:

		private static class InventoryCounter {
			private int items = 0;
			
			Object lock = new Object();
			
			public void increment() {
				synchronized(lock) {
					items++;
				}
			}
			
			public void decrement() {
				synchronized(lock) {
					items--;
				}
			}
			
			public int getItems() {
				synchronized(lock) {
					return items;
				}
			}
		}
		
4. Synchronized block is Reentrant
	1. A thread cannot prevent itself from entering a critical section
		1. Thread can call synchronized method multiple times
		2. Thread can call other synchronized methods in the class
5. Summary:
	1. Formal definition of concurrency problem
	2. We now can identify the code that we need to execute atomically, by declaring that code as a critical section
	3. Use of synchronized keyword to protect the critical section in two ways
		1. Simple way (in front of a method)
		2. On an explicit object
			1. More flexible and granular
				1. But more verbose

### Quiz 6: Critical Section & Synchronization ###
### Atomic Operations, Volatile & Metrics Practical Example ###
1. What we learn in this lecture
	1. Atomic operations
	2. Volatile
	3. Metrics Use Case
2. How do we know what operations are atomic and what are not?
	1. Excessive synchronization
		1. Every method is marked as `synchronized`
			1. Minimizes code that can run in parallel
				1. Only one thread can run at a time
					1. Worse: We are paying the cost of context switching and memory overhead of maintaining multiple threads
	2. Better situation:
		1. Some contention for data but most of the time, the threads run in parallel (more work than single thread)
	3. Which operations are atomic?
		1. Unfortunately, most operations are NOT atomic
		2. Classification:
			1. All reference assignments are atomic
				1. We can get and set references to objects atomically

						Object a = new Object();
						Object b = new Object();
						a = b; // atomic
						
				2. Hence Getters and Setters (that set references to Strings arrays or objects) are all atomic
					1. We don't have to synchronize
			2. All assignments to primitive types are safe (except long and double)
				1. Reading from and writing to the following types is atomic
					1. `int`
					2. `short`
					3. `byte`
					4. `float`
					5. `char`
					6. `boolean`
				2. `long` and `double` are exceptions
					1. 64 bit long
						1. Java does not guarantee (even with 64 bit computer)

								x = y;
								
								x.lower_32_bits <- y.lower_32_bits
								x.upper_32_bits <- y.upper_32_bits
								
							1. Solution:
								1. Assignments to long and double if declared `volatile`

										volatile double x = 1.0;
										volatile double y = 9.0;
										
										x = y; // atomic
										
									1. Guaranteed to be performed as single hardware operation
	4. Classes in `java.util.concurrent.atomic`
	5. Those are more advanced operations
		1. Lock free atomic operations
			1. Multiple techniques are used
				1. Later
3. Metrics Use Case
	1. We want to measure how long the operations take
		1. They depend on input data, environment, hardware, OS, ...
		2. We want to capture duration of those operations (to identify performance issues and optimize)
	2. Code:

			public class Main {
				public static void main(String[] args) {
					Metrics metrics = new Metrics();
					
					BusinessLogic businessLogicThread1 = new BusinessLogic(metrics);
					BusinessLogic businessLogicThread2 = new BusinessLogic(metrics);
					
					MetricsPrinter metricsPrinter = new MetricsPrinter(metrics);
					
					businessLogicThread1.start();
					businessLogicThread2.start();
					
				}
			
				public static class MetricsPrinter extends Thread {
					private Metrics metrics;
					
					public MetricsPrinter(Metrics metrics) {
						this.metrics = metrics;
					}
					
					@Override
					public void run() {
						while (true) {
							try {
								Thread.sleep(100);
							} catch (InterruptedException e) {
							
							}
							
							double currentAverage = metrics.getAverage();
							
							System.out.println("Current Average is: " + currentAverage);
						}
					}
				}
			
				public static class BusinessLogic extends Thread {
					private Metrics metrics;
					private Random random = new Random();
				
					public BusinessLogic(Metrics metrics) {
						this.metrics = metrics;
					}
					
					@Override
					public void run() {
						while (true) {
							long start = System.currentTimeMillis();
							
							try {
								Thread.sleep(random.nextInt(10));
							} catch (InterruptedException e) {
								
							}
							
							long end = System.currentTimeMillis();
							
							metrics.addSample(end - start);
						}
					}
				}
			
				public static void main(String[] args) {
					private long count = 0;
					private volatile double average = 0.0; // atomic
					
					public synchronized void addSample(long sample) {
						double currentSum = average * count;
						count++;
						average = (currentSum + sample) / count;
					}
				}
				
				public double getAverage() {
					return average; // safe
				}
			}
			
		1. `count` and `average` are shared by multiple threads
		2. Expected averge - 5 ms + 1/2 ms (for thread to wakeup, capture timestamp)
4. Summary
	1. Atomic operations
		1. Assignments to primitive types (excluding double and long)
		2. Assignments to references
		3. Assignments to `double` and `long` using `volatile` keyword
	2. Metrics capturing Use Case
		1. Without interfering with application itself
	3. Knowledge about atomic operations is key to high performance

### Quiz 7: Atomic Operations, Volatile & Metrics Practical Example ###
### Coding Exercise 3: Min - Max Metrics ###
### Race Conditions & Data Races ###
1. What we learn in this lecture
	1. Race condition (formal definition)
	2. Data race (challenge & how to avoid)
2. Race Condition
	1. Condition when multiple threads are accessing a shared resource
	2. At least one thread is modifying the resource
	3. The timing of threads' scheduling may cause incorrect results
	4. The core of the problem is non atomic operations performed on the shared resource
3. Example: incrementing thread & decrementing thread
4. Solution:
	1. Identification of critical section where race condition is happening
	2. Protecting of critical section by `synchronized` block
5. **Data Race**:
	1. Example:

			public class SharedClass {
				int x = 0;
				int y = 0;
				
				public void increment() {
					x++;
					y++;
				}
				
				public void checkForDataRace() {
					if (y > x) {
						throw new DataRaceException("This should not be possible");
					}
				}
			}
			
		1. The methods are called by two different threads repeatedly
		2. Scenario

				checkForDataRace			increment
				1. y <- 0
				2. x <- 0
											3. x++
											4. y++

				x == y
				
				checkForDataRace			increment
				1. y <- 0
											2. x++
											3. y++
				4. x <- 1

				x > y
				
				checkForDataRace			increment
				1. y <- 0
											2. x++
											3. y++
											4. x++
											5. y++
											...
											100. x++
											101. y++
				102. x <- 50

				x > y
				
			1. Invariant: `x >= y` (y > x will never happen)
6. Example:

		public class Main {
			public static void main(String[] args) {
				SharedClass sharedClass = new SharedClass();
				thread thread1 = new Thread(() -> {
					for (int i = 0; i < Integer.MAX_VALUE; i++) {
						sharedClass.increment();
					}
				});
				
				Thread thread2 = new Thread(() -> {
					for (int i = 0; i < Integer.MAX_VALUE; i++) {
						sharedClass.checkForDataRace();
					}
				});
				
				thread1.start();
				thread2.start();
			}
			
			public static class SharedClass {
				private int x = 0;
				private int y = 0;
				
				public void increment() {
					x++;
					y++;
				}
				
				public void checkForDataRace() {
					if (y > x) {
						System.out.println("y > x - Data Race is detected");
					}
				}
			}
		}
		
	1. The invariant did not hold!!!
		1. Reason: Data Race
			1. Compiler and CPU may execute the instructions out of order to optimize performance and hardware utilization
			2. They will do so while maintaining the logical correctness of the code
			3. Out of order execution by the compiler and CPU are important features to speed up the code
				1. Or else the program might be much slower
		2. The compiler re-arranges instructions for better
			1. Branch prediction (optimized loops, "if" statements etc.)
			2. Vectorization - parallel instruction execution (SIMD)
			3. Prefetching instructions - better cache performance
				1. Cache lines
			4. ...
		3. CPU re-arranges instructions for better hardware units utilization
			1. If certain instructions need hardware unit that is currently unavailable
				1. But other instructions can be executed in a different hardware unit (instead of wasting CPU cycles)
					1. Done only if it is logically correct

							x = 1;
							y = x + 2;
							z = y + 10;
							
						1. These will not be executed out of order
							1. Each line depends on result of previous line (no data race)
						
									public void increment1() {
										x++;
										y++;
									}
									
									public void increment2() {
										y++;
										x++;
									}
									
								1. The instructions might get re-arranged (both methods are logically correct)
									1. Compiler and CPU core are unaware that different threads are accessing the variables
										1. May lead to unexpected, paradoxical and incorrect results!
				2. Example:

						checkForDataRace		increment
												1. y++
						2. y <- 1
						3. x <- 0
												4. x++
		
						x < y
						
7. Solutions:
	1. Establish a Happens - Before semantics by one of these methods:
		1. Synchronization of methods which modify shared variables
			1. Strict order is guaranteed
				1. Because if code inside the method is re-ordered, it will not matter (only one thread will have access to shared variables at any given moment)
		2. Declaration of shared variables with the volatile keyword
			1. Reduces overhead of locking & will guarantee order

					volatile int sharedVar;
					public void method() {
						...// all instructions will be executed before
						read/write(sharedVar);
						...// all instructions will be executed after
					}
					
				1. Code that comes before access to volatile variable will get executed before that instruction
				2. Code that comes after access to volatile variable will get executed after that instruction
	2. Example:

			private volatile int x = 0;
			private volatile int y = 0;
			// ...
8. Summary:
	1. Two problems with multithreaded applications
		1. Race Conditions
		2. Data Races
	2. Both involve
		1. Multiple threads
		2. At least one is modifying a shared variable
	3. Both problems may result in unexpected and incorrect results
	4. Synchronized - Solves both Race Condition and Data Race.
		1. But has performance penalty
			2. Solution: Volatile (but different meanings and implications)
				1. Solves Race Condition for read/write from/to long and double
				2. Solves all Data Races by guaranteeing order
	5. **Every shared variable (modified by at least one thread) should either be**
		1. **Guarded by a synchronized block (or any type of lock)**
		2. **OR**
		3. **Declared volatile**

### Quiz 8: Data Races ###
### Locking Strategies & Deadlocks ###
1. What we learn in this lecture
	1. Locking Strategy
	2. Deadlock
	3. Deadlock Conditions
	4. Solutions to Deadlock
2. Fine-grained locking vs Course-grained locking
	1. Course-grained locking - single lock on all resources
		1. Advantage: We have only single lock to worry about

				public class SharedClass {
					private DatabaseConnection dbConnection;
					private List<Task> tasksQueue;
					
					public synchronized Item getItemFromDB() {
						...
					}
					
					public synchronized void addTaskToQueue() {
						...
					}
				}
				
			1. Effectively, we have only one lock in this case
				1. If one thread is getting items from database & other thread tries to add task to queue, it will not be able to do so until the first thread gets item from database
					1. Simple to maintain
		2. Disadvantage: Overkill
			1. The operations are not interfering with each other
				1. We can allow them to execute concurrently
			2. Worst case scenario:
				1. Only one thread can make progress
					1. If the threads are only accessing the resources 100% of the time
						1. In reality there is some concurrency
	2. Fine-grained locking - multiple locks on resources (one per resource)
		1. Example:
	
				public class SharedClass {
					private DatabaseConnection dbConnection;
					private List<Task> tasksQueue;
					
					public Item getItemFromDB() {
						synchronized(dbConnection) {...}
					}
					
					public void addTaskToQueue() {
						synchronized(tasksQueue) {...}
					}
				}
				
			1. Advantages:
				1. More fine grained locking strategy
					1. Hence more parallelism & less contention
				2. Problems we may run into (with multiple locks)
					1. Deadlock
						1. Everyone is trying to make a progress but they cannot because they are waiting for other party to make a move
							1. Usually un-recoverable
					2. Scenarios:

							Thread 1			Thread 2
							lock(A)			lock(B)
							lock(B)			lock(A)
							delete(A, item)	delete(B, item)
							add(B, item)		add(A, item)
							unlock(B)			unlock(A)
							unlock(A)			unlock(B)
							
							Thread 1			Thread 2
							1. lock(A)		
												2. lock(B)
												3. lock(A) # cannot
							2. lock(B) # cannot

						1. Deadlock
3. Code example: Rail roads that cross

		public class Main {
			public static void main(String[] args) {
				Intersection intersection = new Intersection();
				Thread trainAThread = new Thread(new TrainA(intersection));
				Thread trainBThread = new Thread(new TrainB(intersection));
				
				trainAThread.start();
				trainBThread.start();
			}
		
			public static class TrainA implements Runnable {
				private Intersection intersection;
				private Random random = new Random();
				
				public TrainA(Intersection intersection) {
					this.intersection = intersection;
				}	
				
				@Override
				public void run() {
					while (true) {
						long sleepingTime = random.nextInt(5);
						try {
							Thread.sleep(sleepingTime);
						} catch (InterruptedException e) {
							
						}
						intersection.takeRoadA();
					}
				}
			}
			
			public static class TrainB implements Runnable {
				private Intersection intersection;
				private Random random = new Random();
				
				public TrainA(Intersection intersection) {
					this.intersection = intersection;
				}	
				
				@Override
				public void run() {
					while (true) {
						long sleepingTime = random.nextInt(5);
						try {
							Thread.sleep(sleepingTime);
						} catch (InterruptedException e) {
							
						}
						intersection.takeRoadB();
					}
				}
			}
		
			public static class Intersection {
				private Object roadA = new Object();
				private Object roadB = new Object();
				
				public void takeRoadA() {
					synchronized (roadA) {
						System.out.println("Road A is locked by thread " + Thread.currentThread().getName());
						synchronized (roadB) {
							System.out.println("Train is passing through road A");
							Thread.sleep(1);
						}
					}
				}
				
				public void takeRoadB() {
					synchronized (roadB) {
						System.out.println("Road B is locked by thread " + Thread.currentThread().getName());
						synchronized (roadA) {
							System.out.println("Train is passing through road B");
							Thread.sleep(1);
						}
					}
				}
			}
		}
		
	1. Deadlock
4. Conditions for Deadlock (if all the below conditions are met, then deadlock is possible)
	1. Mutual Exclusion - Only one thread can have exclusive access to a resource (at a given moment)
		1. Only one train could use a road at a time
	2. Hold and Wait - At least one thread is holding a resource and is waiting for another resource
		1. Two threads were holding a lock and waiting for another lock
	3. Non-preemptive allocation - A resource is released only after the thread is done using it
		1. No thread can take other thread's resource. It has to wait until the thread holding the resource releases it
	4. Circular wait - A chain of at least two threads each one is holding one resource and waiting for another resource
5. Solution:
	1. Ensure that at-least one of the above conditions is not met.
		1. Easiest solution: Avoid circular wait - Enforce a strict order in lock acquisition (same order everywhere)

				Thread 1			Thread 2
				1. lock(A)
				2. lock(B)
				3. // ...
				4. unlock(A)
				5. unlock(B)

									7. lock(A)
									8. lock(B)
									9. // ...
									10. unlock(A)
									11. unlock(B)

			1. Order of releasing the locks is not important here
	2. Change train solution:
		1. Acquire roadA and roadB in the same global order
6. Conclusion
	1. Enforcing a strict order on lock acquisition prevents deadlocks
	2. Easy to do with a small number of locks (is right approach)
		1. May be hard to accomplish if there are many locks in different places (maintaining the order can be difficult)
			1. Solution: Other techniques:
				1. Deadlock detection - Watchdog
					1. Microcontrollers - low level routine that checks the status of a register
						1. The register needs to be updated by every thread, every few instructions
							1. If watchdog detects that the register is no updated, it knows that threads are not responsive and will restart the threads
					2. Thread interruption (not possible with synchronized)
						1. Watchdog implemented as a different thread
							1. It will detect deadlock threads and try to interrupt them
					3. `tryLock` **(M)** (not possible with synchronized)
						1. Checks if a lock is acquired by another thread before trying to acquire a lock and getting suspended
							1. `synchronized` keyword does not allow suspended thread to be interrupted
						2. There are other kinds of locks that allow this
							1. Good if ordering on locking is not possible (to pre-determine)
7. Summary:
	1. Locking strategies
		1. Coarse-grained locking
			1. simple but not best strategy for performance
		2. Fine-grained locking
			1. Improves parallelism but may cause deadlocks
	2. Deadlock
		1. Solved by avoiding circular wait and hold
		2. Lock resources in the same order everywhere

### Quiz 9: Locking Strategies & Deadlocks ###

## Advanced Locking ##
### ReentrantLock Part 1 - tryLock and interruptible Lock ###
1. What we learn in this lecture
	1. `java.util.concurrent.locks.ReentrantLock`
	2. `ReentrantLock.lockInterruptibly()`
	3. `ReentrantLock.tryLock()`
2. ReentrantLock
	1. Works just like `synchronized` keyword applied on an object
	2. But requires explicit locking and unlocking

			Lock lockObject = new ReentrantLock(); // implements Lock interface
			Resource resource = new Resource();
			
			public void method() {
				lockObject.lock(); // explicit
				...
				use(resource);
				...
				lockObject.unlock(); // explicit
			}
			
		1. Disadvantage:
			1. We may forget to unlock
				1. Leaves lock object locked for ever (bugs and deadlocks possible)
			2. If we remember to unlock, we still have potential issues

					public void use() throws SomeException {
						lockObject.lock();
						throwExceptionMethod();
						lockObject.unlock(); // this is never reached
					}
					
		2. Solution:

				Lock lockObject = new ReentrantLock();
				
				public int use() throws SomeException {
					lockObject.lock();
					try { // critical section
						someOperations();
						return value;
					} finally {
						lockObject.unlock(); // will definitely be called
					}
				}
				
			1. For this complexity, we are rewarded with more:
				1. Control over the lock
				2. More lock operations
			2. Queue methods - For testing:
				1. `getQueuedThreads()` - Returns a list of threads waiting to acquire a lock
				2. `getOwner()` - Returns the thread that currently owns the lock
				3. `isHeldByCurrentThread()` - Queries if lock is held by current thread
				4. `isLocked()` - Queries if lock is held by any thread
3. Every production code needs to be thoroughly tested
	1. For that methods like `isLocked()`, `getQueuedThreads()` and others can be very handy
4. Another area where `ReentrantLock` shines is control over lock's fairness
	1. By default, `ReentrantLock` as well as `synchronized` do not guarantee any fairness
		1. If we have many threads wanting to acquire a lock
			1. Only one thread might acquire the lock most of the time while other threads starve
				1. Solution:
					1. `ReentrantLock(true)` - fair lock
						1. May reduce the throughput of the application (?)
							1. Lock acquisition might take longer
						2. Must be used only when needed
5. `ReentrantLock.lockInterruptibly()`
	1. In general, if a thread tries to acquire a lock object while another thread is holding the lock, the new thread is suspended and not wake up until lock is released
		1. `someThread.interrupt();` - does not do anything to a suspended thread (does not wake up)
	2. `lockInterruptibly()`

			@Override
			public void run() {
				while (true) {
					try {
						lockObject.lockInterruptibly();
						...
					} catch (InterruptedException e) {
						cleanUpAndExit();
					}
				}
			}
			
		1. This forces us to surround with `try` `catch` blocks
			1. To handle `InterruptedException` gracefully
	3. Use cases:
		1. Watchdog for deadlock detection and recovery (interrupt threads and recover from the deadlock)
		2. Waking up threads (suspended waiting for a lock) to do clean and close the application
6. What we learnt
	1. `java.util.concurrent.locks.ReentrantLock`
		1. Why?
	
				boolean tryLock()
				boolean tryLock(long timeout, TimeUnit unit);
				
			1. Returns true and acquires a lock if available
			2. Returns false and does not get suspended, if the lock is unavailable
	
	2. `ReentrantLock.tryLock()`
	3. `ReentrantLock.lockInterruptibly()`
7. `lock()` vs `tryLock()`

		lockObject.lock();
		try {
			useResource();
		} finally {
			lockObject.unlock();
		}
		// ...
		if (lockObject.tryLock()) {
			try {
				useResource();
			} finally {
				lockObject.unlock();
			}
		}
		
	1. If lock is available, it gets acquired and enters critical section (no other thread is allowed)
	2. If another thread reaches the lock() method, it would wait until lock is released
	3. When first thread reaches `unlock()` method, it allows other threads to access the resource
	4. `lockObject.tryLock()` - if lock is acquired, `true` is returned and indicates success in acquiring the lock
		1. If lock is not acquired, `false` is returned indicating failure in acquiring the lock
			1. It does not block the thread
				1. With regular lock, the thread is blocked until the owner releases it
			2. Thread can execute a different code & can come back
8. Note about `tryLock()`
	1. Does not block under any circumstances
	2. No matter what the state of the lock is, it always returns
	3. Use cases:
		1. Real time applications - where suspending thread with `lock()` is not acceptable
			1. Examples:
				1. Vieo/Image processing
				2. High speed/low latency trading systems
				3. User interface applications
9. Summary:
	1. Learned a new type of lock - ReentrantLock
		1. Same functionality and properties as `synchronized` lock
		2. Provides more control and advanced features
			1. Query methods for testing lock's internal state
			2. `lockInterruptably()` - allows thread suspended on a lock to be interrupted
			3. `tryLock()` - conditional locking

### ReentrantLock Part 2 - User Interface Application Example ###
1. What we learn in this lecture
	1. `ReentrantLock.tryLock()` use case in Real Time application (using JavaFX)
2. Financial Assets Dashboard
	1. Current prices of select number of investment assets
		1. Prices of stocks
		2. Prices of cryptocurrencies
		3. (anything we want to monitor in a real time)
	2. Implementation
		1. Two threads
			1. UI thread - shows animation in the background
				1. Responds to mouse events
				2. Shows current prices of assets
			2. Background thread - makes network calls to exchanges and gets up to date prices for all the assets periodically
		2. Shared resource
			1. Between UI thread and worker thread
				1. Worker thread can update prices
				2. UI thread can get the prices and display them
	3. Implementation:
		
			public static class PricesContainer {
				private Lock lock = new ReentrantLock();

				private double bitcoinPrice;
				private double etherPrice;
				private double litecoinPrice;
				private double bitcoinCachPrice;
				private double ripplePrice;

				// getters and setters
			}

			public static class PricesContainer {...}

			public static class PriceUpdater extends Thread {
				private PricesContainer pricesContainer;
				private Random random = new Random(); // to generate random prices
				
				public PriceUpdater(PricesContainer pricesContainer) {
					this.pricesContainer = pricesContainer;
				}

				@Override
				public void run() { // user must see all old prices or all new prices (not a combination)
					while (true) {
						pricesContainer.getLockObject().lock();

						try {
							try {
								Thread.sleep(1000); // simulates a network call
							} catch (InterruptedException e) {
							}

							pricesContainer.setBitcoinPrice(random.nextInt(20000));
							pricesContainer.setEitherPrice(random.nextInt(2000));
							pricesContainer.setLitecoinPrice(random.nextInt(500));
							pricesContainer.setBitcoinCashPrice(random.nextInt(5000));
							pricesContainer.setRipplePrice(random.nextDouble());
						} finally {
							pricesContainer.getLockObject().unlock();
						}

						try {
							Thread.sleep(2000); // simulates other scenarios
						} catch (InterruptedException e) {
						}
					}
				}
			}

			// JavaFX - Used to build cross platform UI applications with Java
			public class Main extends Application {
				public static void main(String[] args) {
					launch(args);
				}

				@Override
				public void start(Stage primaryStage) { // JavaFX thread enters this method - similar to `run()`
					primaryStage.setTitle("Cryptocurrency Prices");

					GridPane grid = createGrid(); // table like format
					Map<String, Label> cryptoLabels = createCryptoPriceLabels(); // placeholder to show text

					addLabelsToGrid(cryptoLabels, grid);

					double width = 300;
					double height = 250;

					StackPane root = new StackPane();

					Rectangle background = createBackGroundRectangleAnimation(width, height);

					root.getChildren().add(background);
					root.getChildren().add(grid);

					primaryStage.setScene(new Scene(root, width, height));
					primaryStage.show();
				}

				private Map<String, Label> craeteCryptoPriceLabel() { //maps from assets name to label object
					Label bitcoinPrice = new Label("0");
					bitcoinPrice.setId("BTC");

					Label etherPrice = new Label("0");
					etherPrice.setId("ETH");

					Label liteCoinPrice = new Label("0");
					liteCoinPrice.setId("LTC");

					Label bitcoinCashPrice = new Label("0");
					bitcoinCashPrice.setId("BCH");

					Label ripplePrice = new Label("0");
					ripplePrice.setId("XRP");

					Map<String, Label> cryptoLabelsMap = new HashMap<>();
					cryptoLabelsMap.put("BTC", bitcoinPrice);
					cryptoLabelsMap.put("ETH", etherPrice);
					cryptoLabelsMap.put("LTC", liteCoinPrice);
					cryptoLabelsMap.put("BTH", bitcoinCashPrice);
					cryptoLabelsMap.put("XRP", ripplePrice);

					return cryptoLabelsMap;
				}

				private GridPane createGrid() {
					GridPane grid = new GridPane();
					grid.setHgap(10);
					grid.setVgap(10);
					grid.setAlignment(Pos.CENTER);
					return grid;
				}

				private void addLabelsToGrid(Map<String, Label> labels, GridPane gird) {
					int row = 0;
					for (Map.Entry<String, Label> entry : labels.entrySet()) {
						String cryptoName = entry.getKey();
						Label nameLabel = new Label(cryptoName);
						nameLabel.setTextFill(Color.BLUE);
						nameLabel.setOnMousePressed(event -> nameLabel.setTextFill(Color.RED));
						nameLabel.setOnMOusePressed((EventHandler) event -> nameLabel.setTextFill(Color.BLUE));

						grid.add(nameLabel, 0, row);
						grid.add(entry.getValue(), 1, row);

						row++;
					}
				}

				private Rectangle createBackGroundRectanbleWithAnimation(double width, double height) {
					Rectangle background = new Rectangle(width, height);
					FillTransition fillTransition = new FillTransition(Duration.millis(1000), background, Color.LIGHTGREEN, Color.LIGHTBLUE);
					fillTransition.setCycleCount(Timeline.INDEFINITE);
					fillTransition.setAutoReverse(true);
					fillTransition.play();
					return background;
				}

				public static class PricesContainer {...}

				public static class PriceUpdater extends Thread {
					private PricesContainer pricesContainer;
					private Random random = new Random();

					public PriceUpdater(PricesContainer pricesContainer) {
						this.pricesContainer = pricesContainer;
					}

					@Override
					public void run() {
						while (true) {
							pricesContainer.getLockObject().lock();

							try {
								try {
									// ...
								}
							}
						}
					}
				}
			}

### Quiz 10 - ReentrantLock ###
### Reentrant Read Write Lock & Database Implementation ###
### Quiz 11 - Read-Write Locks ###
### Coding Exercise 4: Product Reviews Service ###
### Product Reviews Service - Solution ###

## Inter-Thread Communication ##
### Semaphore - Scalable Producer Consumer Implementation ###
1. What are we learning in this lecture?
	1. Semaphore - Introduction
	2. Binary Semaphores (particular case)
	3. Semaphores vs locks
	4. Producer Consumer using Semaphores
2. Semaphore:
	1. It is like a permission issuing authority
	2. **It can be used to restrict the number of "users" to a particular resource or a group of resources**
	3. Unlike the locks that allows only one "user" per resource
		1. The sephaore can restrict any given number of users to a resource
			1. Use-case:
				1. Parking lot - 8 parking spots so atmost 8 permits can be issued for 8 cars at any particular moment
					1. Any additional car that wants to park needs to wait for the permit
					2. If one or more cars leave the lot, parking permits can be acquired by other cars which can take their place or given back to semaphore until other cars arrive
	4. How to use:
	
			Semaphore semaphore = new Semaphore(NUMBER_OF_PERMITS);
			semaphore.acquire(); // NUMBER_OF_PERMITS - 1 now available, thread takes a permit and moves to the next instruction
			
			useResource();
			
			// Multiple permits at a time
			semaphore.acquire(5); // NUMBER_OF_PERMITS - 5 now available
			...
			semaphore.release(5); // NUMBER_OF_PERMITS now available
			
		1. We can acquire multiple permits and also release multiple permits
		2. If no permits left for the requesting thread, the thread gets blocked on `acquire()`
		
				semaphore.acquire(); // Thread is blocked because 0 permits are available until a semaphore is released by another thread
3. Semaphore vs Locks
	1. Lock is a particular case of a semaphore with only one permit to give
	
			int NUMBER_OF_PERMITS = 1;
			Semaphore semaphore = new Semaphore(NUMBER_OF_PERMITS);
			
			semaphore.acquire(); // lock
			
			useResource();
			
			semaphore.release(); // unlock
			
		1. Acquiring a permit is equivalent to locking the resource disallowing any other threads to acquire the semaphore until it is released
	2. Semaphore is not a good choice for a lock
		1. It is different in a few ways
			1. Semaphore doesn't have a notion of owner thread
				1. Many threads can acquire a permit
		2. The same thread can acquire the semaphore multiple times
			1. The binary semaphore (initialized with 1) is not reentrant
			
					Semaphore semaphore = new Semaphore(1);
					
					void function1 () {
						semaphore.acquire();
						semaphore.acquire(); // Thread is blocked
					}
					
				1. The thread needs to wait until it is released by another thread
		3. Semaphore can be released by any thread
			1. Even by a thread that hasn't actually acquired it
			
			2. Example:
			
					Semaphore sem = new Semaphore(1);
					
											sem.release();
											...
					sem.acquire();			sem.acquire();
					useSharedResource();	useSharedResource();
					sem.release();			sem.release();
					
				1. Suppose a second thread releases a semaphore first and then consequently allow two threads into the critical section that was supposed to allow only one thread inside it
					1. **Other locks allow only the locking thread to unlock it**
4. Semaphore - Producer Consumer

		Semaphore full = new Semaphore(0); // first thread that tries to acquire it will get blocked
		
		Semaphore empty = new Semaphore(1);
		Item item = null; // shared between producer and consumer, it doesn't contain any value yet
		
		Consumer:
		
		while (true) {
			full.acquire(); // waits here for producer to produce an item
			consume(item);
			empty.release();
		}
		
		Produder:
		
		while (true) {
			empty.acquire();
			item = produceNewItem();
			full.release(); // releases full semaphore which wakes up the consumer thread to consume the item
		}
		
	1. If producer proceeds before the consumer is done consuming the item, then it gets blocked at acquiring the `empty` semaphore.
	2. When the consumer the done consuming the item, it will release the `empty` semaphore which wakes up the producer to produce a new item
	3. If consumer is faster than the producer, it will spend most of the time in a suspended mode and will not consume any CPU
	4. If consumer is slower than the producer, it is guaranteed that the producer will not produce more items until the consumer is done consuming them
	5. The example works only with single producer and single consumer
	6. The example can be extended and generalized for many producers and many consumers
	
			...
			Semaphore full = new Semaphore(0);
			Semaphore empty = new Semaphore(CAPACITY); // queue's capacity
			Queue<Item> queue = new ArrayDeque();
			Lock lock = new ReentrantLock(); // protect from concurrent access to the queue by multiple producers and consumers at the same time
			...
			Producer:
			
			while (true) {
				Item item = producer();
				empty.acquire();
				lock.lock();
				queue.offer(item);
				lock.unlock();
				full.release();
			}
			
			Consumer:
			
			while (true) {
				full.acquire();
				lock.lock();
				Item item = queue.poll();
				lock.unlock();
				consume(item);
				empty.release();
			}
			
		1. Queue size ensures that the consumers can keep up with producers and the queue will not grow to infinity
			1. Which otherwise could cause an out of memory exception
		2. We can adjust the number of producers and consumers to maximize the CPU utilization if needed
	7. The producer-consumer pattern is common in modern multi-threaded applications
		1. **It is used to distribute work-tasks between threads and frameworks that use the actor model**
		2. **It is used in web-applications for socket-channels that consume TCP / UDP packets and pass them to handlers**
	8. Producer Consumer, Video
		1. Pretty much every inter-thread communication library or framework would use a version of the pattern
		
				Filter 2 --+------> Recorder
					^      |
					|      +------> Streamer
				Filter 1
					^
					|
				Video Capture
					^
					|
		
5. Summary:
	1. Learned a new Synchronization tool - the semaphore
	2. Semaphore can be used as a general case for a lock - permit issuing authority
		1. Can restrict the number of users per critical section/ resource
	3. Differences between locks and semaphores
		1. Any thread can release a semaphore (no ownership)
	4. Inter-thread communication for producer-consumer, using semaphore
		1. Allows consumers to apply back-pressure on producers if the producers produce faster than the consumers can consume

### Quiz 12: Semaphores - Barrier ###
### Condition Variables - All purpose, Inter-Thread Communication ###
1. What we will learn in this lecture:
	1. Review of inter-thread communication
	2. Semaphore as particular case of condition variable
	3. Condition variables - `java.util.concurrent.locks.Condition`
2. Inter-Thread - Thread.interrupt()

		Thread A			Thread B
			|					|
			|					|
			+------------------>|
			|					|-+
			|					| | Clean up and terminate
			|					|<+
			|					x
			
	1. The signal is used only one context
		1. To let Thread B know that we wanted interrupted
3. Inter-Thread - Thread.join()

		Thread A			Thread B
			|					|
			+-+					|
			| | threadB.join();	|
			|<+					|
			|<------------------x			
			|	Wake up Thread A
			|
			
	1. Thread A gives up its CPU and waits until Thread B was terminated
		1. `join()` is called on Thread B's `threadB` object
	2. When Thread B got terminated, it will send a signal to wake up Thread A
4. Inter-Thread - Semaphore

		Thread A				Thread B
			|						|
			|						|
			+-+						|
			| | semaphore.acquire() +-+
			|<+						| | semaphore.release()
			|<----------------------|<+
			|	Wake up Thread A	|
			|						|
			
	1. `acquire` causes Thread A to get suspended
	2. `release` sends a signal to Thread A to wake up
	3. A semaphore is a particular case of a condition variable
5. Inter-thread - Semaphore as Condition Variable
	1. Calling the `acquire()` on a Semaphore is equivalent to checking the condition "Is Number of Permits > 0?"
		1. Condition that thread A requires to move on to the next instruction
	2. If the condition is not met - thread A goes to sleep until another thread changes the semaphore's state
	3. When thread B calls the `release()` method, thread A wakes up
	4. Thread A checks the condition "Is Number of Permits > 0?"
		1. If it is, thread A continues to the next instruction
6. Condition variables - `java.util.concurrent.locks.Condition`
	1. It is a generic way of inter-thread communication
	2. It allows us to use any condition we want to stipulate the continuation of the execution of a thread
	
			Thread A				Thread B
				|						|
				|						|
				| Check condition		+-+
				| Condition is NOT met	| | Change state
				|	Signal Thread A		|<+
				|<----------------------|
				+-+						|
				| | Check condition		|
				|<+						|
				|						|
				
		1. Thread A checks for some condition
		2. If condition is not met, we can suspend Thread A
		3. Thread B changes some state
		4. Thread B signals Thread A to wake up
		5. Thread A checks if the condition is satisfied
		6. If the condition is satisfied, then it can move on and do its work
		7. If the condition is not satisfied, then it can choose to wait again until another thread wakes it up
7. Inter-Thread - Creation
	1. Condition variable is always associated with a lock
		1. The lock ensures atomic check and modification of the shared variables, involved in the condition
	2. Code:
	
			Lock lock = ReentrantLock();
			Condition condition = lock.newCondition();
			
8. Inter-Thread - Producer Consumer
	1. Thread 1: user-input thread
		1. Gets a pair of input variables (username, password)
	2. Thread 2: checks username and password in the database and checks if the user is authenticated
		1. This operation takes a long time
			1. We cannot do this in the UI Thread
				1. Solution: The information must be exchanged between user-interface thread and authentication thread 
				
						Lock lock = new ReentrantLock();
						Condition condition = lock.newCondition();
						String username = null, password = null;
						
						lock.lock();
						try {
							while (username == null || password == null) {
								condition.await(); // unlocks lock and puts thread to sleep
							}
						} finally {
							lock.unlock();
						}
						doStuff();
						
					1. `condition.await()` puts the thread to sleep until another thread signals the condition
						1. It unlocks the lock automically before sleep
							1. Required because UI thread needs to acquire the lock
			2. UI Thread code:
			
					lock.lock();
					try {
						username = userTextbox.getText();
						password = passwordTextbox.getText();
						condition.signal();
					} finally {
						lock.unlock();
					}
					
				1. If user didn't type either username or password, the corresponding fields will be null
				2. If user types username and password, they will be passed to the shared variables
				3. `signal` - wakes up the other thread
					1. `lock` needs to be released before the other thread can continue
				4. Once the other threads re-acquires the lock, it can continue
					1. If the condition is met, the auth thread will unlock the lock and then run `doStuff()` - checks if password matches against the database etc...
				5. If there is no match, the `condition.await()` is called again
9. Inter-thread - Condition.await()
	1. `void await()` - unlock lock, wait until signalled
		1. The method puts the thread to sleep completely giving up until another thread signals to it to wake up
		2. The method unlocks lock associated with the condition variable
	2. `long awaitNanos(long nanosTimeout)` - wait no longer than `nanosTimeout`
	3. `boolean await(long time, TimeUnit unit)` - wait no longer than time, in given time units
		1. `time` - upper bound on time to wait
	4. `boolean awaitUntil(Date deadline)` - wake up before the deadline date
10. Inter-thread - Condition.signal()
	1. `void signal()` - wakes up a single thread, waiting on the condition variable
		1. If there are more than one threads waiting on the condition variable, only one of those threads is going to be woken up
			1. Rest of the threads are going to stay asleep
	2. A thread that wakes up has to re-acquire the lock associated with the condition variable
	3. If currently no thread is waiting on the condition variable, the signal method doesn't do anything
		1. No thread is going to be signaled
			1. Difference between condition variable and semaphore
				1. The fact that the condition variable is signaled is not saved anywhere, the future thread that will call the `await()` method will not be affected.
	4. `void signalAll()` - Broadcast a signal to all threads currently waiting on the condition variable
		1. All the waiting threads will wake up
	5. **Doesn't need to know how many (if at all) threads are waiting on the condition variable**
	
									+-- condition.await()
									|
			condition.signalAll() --+-- condition.await()
									|
									+-- condition.await()
									
		1. Semaphore - If we want similar behavior, we need to release the semaphore as many times as the number of threads that are currently waiting for the semaphore
11. Summary:
	1. Reviewed some of the inter-thread communication techniques we had learned
	2. Semaphore as a particular case of condition variable
	3. Condition Variable
		1. `Condition.await()` - suspend the thread, and wait for a state change.
		2. `Condition.signal()`/ `signalAll()` - wake all waiting threads
	
### Objects as Condition Variables - wait(), notify(), and notifyAll() ###
1. What we learn in this lecture
	1. `wait()`, `notify()`, `notifyAll()` for inter-thread communication and signalling
	2. Backpressure practical example between a producer and consumer
2. wait(), notify(), and notifyAll()
	1. The Object class contains the following methods:
		1. `public final void wait() throws InterruptedException`
		2. `public final void notify()`
		3. `public final void notifyAll()`
	2. Every Java class inherits from the `Object` class
		1. We can call the methods on an object of any type
			1. Hence, we can use any object as a condition variable and a lock (using the synchronized keyword)
	3. `wait()` - Causes the current thread to wait until another thread wakes it up
		1. In the wait state, the thread is not consuming any CPU
		2. Two ways to wake up the waiting thread:
			1. `notify()` - Wakes up a single thread waiting on that object
				1. Method is called from another thread
				2. It will wake up a single thread that is waiting on that object
				3. If there are multiple threads waiting, one of them will be chosen arbitrarily
			2. `notifyAll()` - Wakes up all the threads waiting on that object
			3. To call `wait()`, `notify()`, or `notifyAll()`, we need to acquire the monitor of that object (use synchronized on that object)
				1. We need to synchronize on the object
3. Example:

		public class MySharedClass {
			private boolean isComplete = false;
			
			public void waitUntilComplete() {
				synchronized(this) {
					while (isComplete == false) {
						this.wait(); // thread will wait and completely give up its CPU
					}
				}
			}
			...
		}
		
		public void complete() {
			synchronized(this) {
				isComplete = true;
				this.notify(); // This will wake up the first thread
			}
		}
		
	1. The above are similar to condition variables:
	
			Object Signalling		Condition Variable
			synchronized(object) {	lock.lock()
			}						lock.unlock()
			object.wait()			condition.await()
			object.notify()			condition.signal()
			object.notifyAll()		condition.signalAll()
			
		1. The current object is used as both a condition variable and a lock
		2. If the current object is the lock, we can clean the code using `synchronized` keyword in the method declaration instead of inside the method
		
				public class MySharedClass {
					private boolean isComplete = false;
					
					public void synchronized waitUntilComplete() {
						while (isComplete == false) {
							wait();
						}
					}
					
					public void synchronized complete() {
						isComplete = true;
						notify();
					}
				}
				
4. Matrix Multiplication Pipeline

		Input Matrix 1 
						-> (M1) x (M2) -> Output Matrix 3
		Input Matrix 2
		
	1. Applications:
		1. Used in neural networks - Deep learning
			1. to train and define predictions as part of applications involving AI and deep learning
		2. Image processing:
			1. Represented as matrices of pixels in different effects such as edge detection and blur
			
					Edge Detection
					[-1  -1  -1]
					[-1   8  -1]
					[-1  -1  -1]
					
					Gaussian Blur
					1/16 [1  2  1]
					     [2  4  2]
						 [1  2  1]
						 
		3. Matrix Multiplication - Pipeline
			1. Matrices Reader Producer (thread)
				1. It will read a pairs of matrices from a file
			2. Matrices Multiplier Consumer:
				1. Multiplies the pair of matrices and saves the result into another file
			3. Between producer and consumer, we will build a thread safe Queue with back-pressure using the wait and notify methods
				1. Matrix multiplication: multiply row vector of matrix 1 and column vector of matrix 2 and add them to get a single value
				2. Formula:
				
						(AB)_rc = sigma^N - 1_k=0 A_rk B_kc
						
		4. MatricesGenerator
		
				public class MatricesGenerator {
					private static final String OUTPUT_FILE = "./out/matrices";
					private static final int N = 10;
					private static final int NUMBER_OF_MATRIX_PAIRS = 100000; // 100 thousand pairs of 10 x 10 matrices with random numbers
					
					public static void main(String[] args) throws IOException {
						File file = new File(OUTPUT_FILE);
						FileWriter fileWriter = new FileWriter(file);
						createMatrices(fileWriter);
						fileWriter.flush();
						fileWriter.close();
					}
					
					private static float [] createRow(Random random) {...}
					
					private static float [][] createMatrix(Random random) {...}
					
					private static void saveMatrixToFileWriter fileWriter, float [][] matrix) throws IOException {...}
					
					private static void createMatrices(FileWriter fileWriter) throws IOException {...}
				}
				
		5. Matrix Multiplication class
		
				public class MainApplication {
					public static void main(String[] args) {
						
					}
					
					private static class ThreadSafeQueue { // Simple queue without back-pressure
						private Queue<MatricesPair> queue = new LinkedList<>();
						private boolean isEmpty = true; // indicates whether our 
					}
					
					private static class MatricesPair { // pair of 2d arrays which will contain matrices
						public float[][] matrix1;
						public float[][] matrix2;
					}
				}

### Quiz 13: Condition Variables ###
### Coding Exercise 5: Simple CountDownLatch ###
### Simple CountDownLatch - Solution ###

## Lock-Free Algorithms, Data-Structures & Techniques ##
### Introduction to Non-Blocking, Lock Free Operations ###
1. What we will learn: (algorithms, techniques, and data-structures)
	1. Problems and limitations of locks
	2. Introduction to lock free programming
	3. Review of Atomic instruction
	4. Introduction to a new group of atomic operations
2. What's wrong with locks?
	1. Everything we've learned so far about locks is very valuable
	2. Majority of multi-threaded programming is still done with locks (synchronized, ReentrantLock, ReentrantReadWriteLock ...)
	3. Most of the concurrency problems are easier and safer to solve with locks
	4. Locks have great software and hardware support (they have been around for a very long time)
	5. Using locks we can solve all concurrency issues
		1. Race conditions
		2. Data races
3. Why learning lock free techniques?
	1. As engineers we are always faced with a trade off
		1. For most problems there's more than one solution
			1. The more tools we have, the better we can choose the right tool for the job
				1. Being able to choose the right tool for the job is what makes a good engineer
4. Issues with locks:
	1. Deadlocks:
		1. Deadlocks are generally unrecoverable (nastiest issue)
			1. Solution: We might need to implement deadlock detection and resolution logic
		2. It can bring the application to a complete halt
		3. **The more the locks in the application, the higher the chances of a deadlock**
	2. Slow critical section:
		1. If multiple threads are using the same lock, one thread can hold the lock for a very long time
			1. That thread will slow down all the other threads
				1. Hence all threds become as slow as the slowest thread
	3. Priority Inversion
		1. Happens when two threads sharing a lock
			1. Low priority thread (background document saver)
			2. Hight priority thread (UI)
				1. Must get scheduled first or more frequently
			2. What if low priority thread acquires the lock, and is preempted (scheduled out)
				1. High priority thread cannot progress (is stuck) because the low priority thread not scheduled to release the lock (it is holding the lock)
					1. Results in performance issues and unresponsiveness of the application
						1. Each OS solves this problem in their own way which have advantages and disadvantages
	4. Thread not releasing a lock (Kill tolerance)
		1. Thread dies, gets interrupted of forgets to release a lock
			1. It leaves all threads hanging forever
				1. It is unrecoverable, just like a deadlock
					1. To avoid, developers need to write more complex code (wrapping every critical section with a try and finally block, try locks with timeouts, ...)
	5. Performance
		1. Performance overhead in having contention over a lock
			1. If thread A acquires a lock
			2. And thread B tries to acquire a lock and gets blocked
			3. Implications:
				1. Thread B is scheduled out (context switch to another thread because it is not able to continue)
				2. Thread B is scheduled back (context switch which is an overhead)
			4. Additional overhead may not be noticable for most applications
				1. But for latency sensitive applications (say trading systems which operate in sub-millisecond latencies), the overhead can be significant
5. Lock Free Techniques:
	1. Why did we need locks?
		1. Multiple threads accessing shared resources
		2. At least one thread is modifying the shared resources
		3. Non-atomic operations
			1. Reasons:
				1. Non atomic operation on one shared resource
				2. A single Java operation turns into one or more hardware operations (at the lowest level of the abstract stack)
					1. Example: counter++ turns into 3 hardware instructions:
						
							Read count
							Calculate new value
							Store new value to count
							
						1. Another thread can modify the value of count in between the execution of the above 3 instructions
	2. Lock Free Solution - Breakdown
		1. Utilize operations which are guaranteed to be one hardware operation
			1. A single hardware opeartion is:
				1. Atomic by definition
				2. Thread safe
6. Review of all Atomic Instructions we Learned:
	1. Read/Assignment on all primitive types (except for long and double)
	2. Read/Assignment on all references
	3. Read/Assignment on volatile long and double
7. Avoiding Data Races:
	1. Read/Assignment on all volatile primitive types and references
		1. To avoid data races, we can make all shared variables that we want to read and write to without using a lock as **volatile**
8. Second group of atomic operations
	1. Comes from atomic classes that come from `java.util.concurrent.atomic` package
		1. Internally they use unsafe class which provide access to low level, native methods (discouraged to use directly)
			1. They utilize low level platform specific operations including atomic operations that the architecture provides
9. AtomicX Classes (available in Java 10)
	1. `AtomicBoolean`
	2. `AtomicInteger`
	3. `AtomicIntegerArray`
	4. `AtomicIntegerFieldUpdater<T>`
	5. `AtomicLong`
	6. `AtomicLongArray`
	7. `AtomicLongFieldUpdater<T>`
	8. `AtomicMarkableReference<V>`
	9. `AtomicReference<V>`
	10. `AtomicReferenceArray<E>`
	11. `AtomicReferenceFieldUpdater<T,V>`
	12. `AtomicStampedReference<V>`
	13. `DoubleAccumulator`
	14. `DoubleAdder`
	15. `LongAccumulator`
	16. `LongAdder`
10. **We can design very powerful lock-free data-structures and algorithms**

### Atomic Integers & Lock Free E-Commerce ###
1. What we will learn in the lecture
	1. AtomicInteger
	2. Lock-free E-Commerce Inventory Counter
2. AtomicInteger
	1. Provides atomic operations we can perform on integer values
	2. Syntax:
	
			int initialValue = 0;
			AtomicInteger atomicInteger = new AtomicInteger(initialValue);
			
			// atomically increment the integer by one
			atomicInteger.incrementAndGet(); // return new value after incrementing atomically
			atomicInteger.getAndIncrement(); // return previous value and increment atomically
			
			// atomically decrement the inteter by one
			atomicInteger.decrementAndGet(); // return new value
			atomicInteger.getAndDecrement(); // return previous value
			
			// atomically add any integer
			int delta = 5; // can be positive or negative
			atomicInteger.addAndGet(delta);
			atomicInteger.getAndAdd(delta);
			
		1. Pros:
			1. Simplicity
				1. No need for locks or synchronization
			2. No race conditions or data races
		2. Cons:
			1. Only the operations are atomic
				1. There's still race condition between 2 separate atomic operations (we cannot perform atomic operations tegether)
					1. Example:
					
							atomicInteger.incrementAndGet();
							atomicInteger.addAndGet(-5); // there is race condition here because they are two separate opearations
							
						1. If thread 1 executes both operations and then thread 2 executes both Operations
							1. value is: 0 -> 1 -> -4 -> -3 -> -8
						2. If thread 1 executes first and thread 2 executes second and thread 1 executes second?
							1. value is: 0 -> 1 -> 2 -> -2 -> -7
							
3. Inventory problem:
	1. We have a counter that keeps count of the inventory of a product
		1. Two threads increment and decrement counter concurrently (10000 times each)
		2. Inventory counter was shared between incrementing and decrementing threads
		3. We printed out the total number of items
			1. We expect the count to be 0 at the end
				1. To avoid race conditions, we locked access to items++ or items--
					1. Using synchronized key-word
	2. Implementation using Lock free techniques:
	
			public class Main {
				public static void main(String[] args) {
					InventoryCounter inventoryCounter = new InventoryCounter();
					IncrementingThread incrementingThread = new IncrementingThread(inventoryCounter);
					DecrementingThread decrementingThread = new DecrementingThread(inventoryCounter);
					
					incrementingThread.start();
					decrementingThread.start();
					
					incrementingThread.join();
					decrementingThread.join();
					
					System.out.println("We currently have " + inventoryCounter.getItems() + " items");
				}
			}
			
			public static class DecrementingThread extends Thread {
				private InventoryCounter inventoryCounter;
				
				public DecrementingThread(InventoryCounter inventoryCounter) {
					this.inventoryCounter = inventoryCounter;
				}
				
				@Override
				public void run() {
					for (int i = 0; i < 10000; i++) {
						inventoryCounter.decrement();
					}
				}
			}
			
			public static class IncrementingThread extends Thread {
				private InventoryCounter inventoryCounter;
				
				public IncrementingThread(InventoryCounter inventoryCounter) {
					this.inventoryCounter = inventoryCounter;
				}
				
				@Override
				public void run() {
					for (int i = 0; i < 10000; i++) {
						inventoryCounter.increment();
					}
				}
			}
	
			private static class InventoryCounter {
				private AtomicInteger items = new AtomicInteger(0);
				
				public void increment() {
					items.incrementAndGet();
				}
				
				public void decrement() {
					items.decrementAndGet();
				}
				
				public int getItems() {
					return items.get();
				}
			}
			
		1. When we run, we get the correct result without using any locks
4. Summary and Key Takeaways:
	1. AtomicInteger is a great tool for concurrent counting, aggregation of metrics, events, ... (anything that uses counting) without the complexiy of using a lock
	2. AtomicInteger should be used only when atomic operations are needed
	3. It's on par and sometimes more performant than a regular integer with a lock as protection
	4. If used only by a single thread, a regular integer is preferred (it is slower)
		1. Reason: Hardware and compiler optimizations become impossible to avoid a data race
	5. If long is required, we can use `AtomicLong` which provides the same capabilities as `AtomicInteger`
	6. Similarly `AtomicBoolean` provides atomic operations on boolean values

### Atomic References, Compare And Set, Lock-Free High Performance Data Structure ###
1. What we will learn in the lecture
	1. `AtomicReference<T>`
	2. CAS - CompareAndSet operation
	3. Build lock free data structure
	4. Compare performance with the blocking implementation of a data-structure
2. What is `AtomicReference<T>`
	1. `AtomicReference(V initialValue)`
		1. Wraps us a reference to an object of a class and gives the ability to perform atomic operations on that reference
			1. We can initialize by passing an object into the constructor or set the reference later
	2. `V get()` - Returns the current value
	3. `void set(V newValue)` - Sets the value to `newValue`
3. CAS - Most important methods
	1. `boolean compareAndSet(V expectedValue, V newValue)`
		1. Assigns new value if current value == expected value
		2. Ignores the new value if the current value != expected value
	2. Example:
	
			public class Main {
				public static void main(String[] args) {
					String oldName = "old name";
					String newName = "new name";
					AtomicReference<String> atomicReference = new AtomicReference<>(oldName);
					
					atomicReference.set("Unexpected name");
					if (atomicReference.compareAndSet(oldName, newName)) {
						System.out.println("New Value is " + atomicReference.get());
					} else {
						System.out.println("Nothing Changed");
					}
				}
			}
			
		1. The method protects against another thread that modifies the value without our knowledge
		2. CAS is available in all atomic classes
			1. It compiles into a single atomic hardware operation
			2. Many other atomic methods are internally implemented using CAS
4. Stack implementation:
	1. Java out of the box version is based on locks and uses the vector class
	2. Our implementation:
		1. Using linked list
			1. When a new item is pushed, it is added to the front of the LL and becomes the top
			2. When an item is popped, the head is returned and then the next item becomes the head
	3. Implementation:
	
			public static class StandardStack<T> {
				private StackNode<T> head;
				private int counter = 0; // used to count the number of operations
				
				public synchronized void push(T value) {
					StackNode<T> newHead = new StackNode<>(value);
					newHead.next = head;
					head = newHead; // race condition is possible between previous line and this line
					counter++;
				}
				
				public synchronized T pop() {
					if (head == null) {
						counter++;
						return null;
					}
					
					T value = head.value;
					head = head.next; // race condition is possible between previous line and this line
					counter++;
					return value;
				}
				
				public int getCounter() { return counter; }
			}
	
			private static class StackNode<T> {
				public T value;
				public StackNode<T> next;
				
				public StackNode(T value) {
					this.value = value;
					this.next = next;
				}
			}
			
		1. Read and write operations to the head variable can cause race conditions
			1. Heance, we can make head as the atomic reference instead of a direct reference to the first element in the linked list
		2. Lock Free Stack:
		
				public static class LockFreeStack<T> {
					private AtomicReference<StackNode<T>> head = new AtomicReference<>();
					private AtomicInteger counter = new AtomicInteger(0);
				
					public void push(T value) {
						StackNode<T> newHeadNode = new StackNode<>(value);
						while (true) {
							StackNode<T> currentHeadNode = head.get();
							newHeadNode.next = currentHeadNode;
							if (head.compareAndSet(currentHeadNode, newHeadNode)) {
								break;
							} else {
								LockSupport.parkNanos(); // 1 nano-second
							}
						}
						counter.incrementAndGet();
					}
					
					public T pop() {
						StackNode<T> currentHeadNode = head.get();
						StackNode<T> newHeadNode;
						
						while (currentHeadNode != null) {
							newHeadNode = currentHeadNode.next;
							if (head.compareAndSet(currentHeadNode, newHeadNode)) {
								break;
							} else {
								LockSupport.parkNanos();
								currentHeadNode = head.get();
							}
						}
						
						counter.incrementAndGet();
						return currentHeadNode != null ? currentHeadNode.value : null;
					}
					
					public int getCounter() {
						return counter.get();
					}
				}
				
5. Performance is not always better with atomic objects instead of using Locks
	1. Comparing the performances:
	
			public static void main(String[] args) {
				StandardStack<Integer> stack = new StandardStack<>();
				Random random = new Random();
				
				for (int i = 0; i < 100000; i++) {
					stack.push(random.nextInt());
				}
				
				List<Thread> threads = new ArrayList<>();
				
				int pushingThreads = 2;
				int poppingThreads = 2;
				
				for (int i = 0; i < pushingThreads; i++) {
					Thread thread = new Thread(() -> {
						while (true) {
							stack.push(random.nextInt());
						}
					});
					
					thread.setDaemon(true);
					threads.add(thread);
				}
				
				for (int i = 0; i < poppingThreads; i++) {
					Thread thread = new Thread(() -> {
						while (true) {
							stack.pop();
						}
					});
					
					thread.setDaeomon(true);
					threads.add(thread);
				}
				
				for (Thread thread : threads) {
					thread.start();
				}
				
				Thread.sleep(10000);
				
				System.out.println(String.format("%d operations were performed in 10 seconds", stack.getCounter());
			}
			
		1. Run: 156 million operations in 10 seconds
		2. Replace with LockFreeStack:
		
				LockFreeStack<Integer> stack = new LockFreeStack<>();
				
		3. Run: 509 million operations in 10 seconds
			1. Increased performance over 3 times (220% over blocking stack)
6. Summary:
	1. `AtomicReference<T>` - wraps a reference to an object, allows us to perform atomic operations on that reference, including the `compareAndSet(..)`
	2. `compareAndSet(..)` - Atomic operation available in all atomic classes
	3. Implemented a lock free data structure - stack, using the `AtomicReference<>` and `compareAndSet`
	4. Lock free Stack, outperformed the blocking stack implementation x3 (200 %)

### Quiz 14: Lock-Free Algorithms, Data-Structures & Techniques ###

## Threading Models for High Performance IO ##
### Introduction to Blocking IO ###
1. What we will learn in this lecture:
	1. Introduction to IO Operations
		1. IO bound applications
		2. Optimizing the performance of such applications by exploring through real life scenarios
	2. Consequences of Blocking IO on Performance
	3. Real-world Application Scenarios
	4. Important Observations
2. Negative Impact of Blocking on Locks
	1. Example:
	
			public synchronized accessSharedResource() {
				// ... enter critical section
				operation1();
				operation2();
				operation3();
				// ... exit critical section
			}
			
		1. When one thread enters the critical section, the second thread will be blocked and is forced to wait.
			1. The OS un-schedules the blocked thread and schedules it only when the lock is released.
				1. Under high load and lock contention, the performance impact can be very high
					1. Even if the time the thread is blocked is very short.
3. Alternative to Blocking on Locks
	1. Lock free:
		1. Algorithms
		2. Data Structures
		3. Atomic operations (hardware level)
	2. **Blocking IO (Input/Output)**
		1. What is an IO operation?
			1. A general purpose computer abstraction has CPU and Memory
			2. Other devices such as Keyboard, mouse, monitor, hard-drive, network card, ... are considered as external devices
				1. Reason? CPU can access memory directly at any time
					1. **Program can read from or write to memory without the involvement of an OS**
					2. CPU doesn't have direct access to external devices
						1. CPU can communicate with controllers of devices to send data or receive data
						2. When device is doing its work or when it is idle, the CPU has nothing to do.
							1. If user has not typed any key on the keyboard
							2. The result of an external request to the network has not yet arrived, **the CPU can continue running other tasks**
							3. **When the operation of the device is complete and is ready, the CPU gets an interrupt, then and only then, the CPU will get involved in reading the operation result from the device using special OS routine or driver**
							4. **To minimize the involvement of the CPU to read or write large chunks of data (from a disk or network card ...) most computers have additional hardware unit called DMA (Direct Memory Access)
								1. DMA is used to give permission to the device to read the relevant data from the memory or write results to the memory without CPU's involvement
									1. When the operation is complete, the CPU gets notified about the operation's completion
							5. **The CPU is not involved while the external devices are doing their work**
								1. **CPU is free to run other processes or threads**
									1. CPU is involved only when:
										1. Initiating a data transfer
										2. When it gets the interrupt that the operation is complete
		2. Thread pooling:
			1. To optimize the throughput of an application, the best approach is to allocate a pool of threads and send every incoming task to be executed by the next available thread in that pool.
				1. Logic behind a fixed size thread pool
					1. We can reuse the same threads for the entire duration of the application
					2. Elimiates the following overhead for each task:
						1. creation
						2. starting
						3. Shutting down
					3. Optimal size: #threads = #Cores
						1. Allows OS to schedule each thread on a separate core
							1. Complete parallelism
			2. Assumptions for fixed size thread pool:
				1. Tasks involve only CPU operations
				2. No blocking calls
					1. Scenario 1: Online Store Web Application:
						1. Web application listens for incoming HTTP requests from different users interested in different categories of products
							1. Anytime it gets a request, it
								1. Reads client's request
								2. Connects to a database
								3. Read all the currently available products, their reviews and prices
								4. When it receives all the data from the database, it simply sends back all that data in the form of a web-page back to the user
						2. Assume the web-application is running on a single core computer
							1. Size of thread pool will be 1
						3. Example code:
						
								public void handleRequest(HttpExchange exchange) {
									Request request = parseUserRequest(exchange);
									Data data = readFromDatabase(request);
									sendPageToUser(data, exchange);
								}
								
							1. `parseUserRequest` - Quick CPU operation
							2. `readFromDatabase`
								1. Database might be running on a different Computer
								2. Waiting for this complete is a long operation
								3. It is a blocking I/O operation
									1. The thread is blocked
										1. The CPU is idle
							3. The above is an IO bound application
								1. **Most of its time is spent on doing IO** (as opposed to using the CPU)
							4. If another request arrives, we have the CPU capacity to handle it (despite the fact that we have only one core)
								1. Since application has only one thread and it is blocked on the long IO operation, the new request will stay in the network card's queue until the first request is complete
		3. IO-Bound applications - Use cases:
			1. They are very common use cases in the industry
				1. web-applications that power most web-sites are IO bound applications
					1. The applications spent most time waiting for
						1. User request to arrive
						2. Response from a remote service to arrive
						3. Response from a database to arrive
						4. Loading a web-page like HTML, CSS, or JavaScript from it's local disk
				2. Big Data processing and [ML] transformation applications
					1. The applications prepare and sanitize input data for storage in a database or for machine learning purposes
						1. The applications spend most of their time doing IO
							1. Reading a very large files from the disk
							2. Sending the results to another transformation application
							3. Storing in another location
		4. Scenario 2 - Multithreaded Web Application
			1. IO bound applications are not the only types of applications we need to worry about when it comes to blocking io
			2. Let us assume that blocking IO happens occasionally
				1. Let the web application cache some of the data in Memory and occasionally makes calls to DB when it doesn't have the necessary data
				2. Let us assume that we are running a 4 core computer (4 threads)
			3. Let us say we have 4 requests from 4 different users
				1. 3 of them found the required data in memory so they were completed in a very little time
				2. 1 request required the application to make a request to the database which takes a long time
				3. Suppose we have 4 more requests
					1. But we have only 3 threads available (first thread is still blocked on the IO)
				4. Let us assume that 3 requests completed without making requests to external database but 4th request needed data from database
					1. 2 threads are blocked on io
				5. Subsequently we will run out of threads
					1. However all the 4 CPU cores are not doing anything
					2. Only 1/4 of the requests needed DB
			4. Observations:
				1. When a task involves blocking calls, "# threads = # cores"
					1. Doesn't gives us the best Performance
					2. Doesn't give us the best CPU utilization
				2. Even if just have a few long blocking calls, they impact the performance of the entire application for all the tasks (not just the blocking calls)
4. Next:
	1. A few techniques that will allow us to better utilize the CPU and improve the throughput of our application even if there are IO Operations
5. Summary:
	1. How IO operations work
	2. The CPU is not involved in long IO operations
		1. It is free to perform other tasks, if they exist
	3. Explored a scenario of an IO-based web application
		1. Discovered that with tasks involving blocking calls
			1. # threads = # cores (doesn't work)
				1. Doesn't give optimal performance or hardware utilization
		2. Blocking calls impact the performance of the entire application
			1. Even if most of the logic doesn't involve any IO

### Thread Per Task / Thread Per Request Model ###
1. What we will learn in the lecture:
	1. Introduction to Thread-per-task Threading model
	2. Practical Example of an IO-Bound application
	3. Performance analysis and conclusions
2. Thread-per-core and blocking IO
	1. Doesn't give us the optimal performance
		1. While the application was blocked on IO, CPU was not doing anything
	2. An obvious solution:
		1. Add more threads, one for each incoming network request or task
			1. Even on a single core computer, multiple threads can be used to service multiple requests concurrently
			2. If we have multiple cores, some of the tasks can be performed in parallel to each other while others run concurrently with each other
	3. Thread-per-task model:
		1. Let us assume that N requests are being processed at any time
		2. At some point in the application lifecycle, it ends up performing N Blocking IO operations at the same time.
			1. The N operations can be:
				1. Reading N files form the disk
				2. Sending N different network requests to the services
				3. Sending N queries to a remote database
		3. While application waits for the results of the N IO operations, it doesn't do anything
		4. If each task task takes say, 1 second, then executing each task on a separate thread, we must be able to complete all the N operations concurrently in around 1 second all together
		5. Example:
		
				public class IoBoundApplication {
				
					private static final int NUMBER_OF_TASKS = 1000;
					
					public static void main(String[] args) {
						Scanner s = new Scanner(System.io);
						System.out.println("Press enter to start");
						s.nextLine();
						System.out.println("Running %d tasks\n", NUMBER_OF_TASKS);
						
						long start = System.currentTimeMillis();
						performTasks();
						System.out.println("Tasks took %dms to complete\n", System.currentTimeMillis() - start);
					}
					
					private static void performTasks() {
						try (ExecutorService executorService = Executors.newCachedThreadPool();) { // will grow to as many threads as we need and cache the threads to be used later, we usually don't know how many tasks we need to perform and how many threads need to be pre-allocated
						
							for (int i = 0; i < NUMBER_OF_TASKS; i++) {
								executorService.submit(() -> blockingIoOperation()); // every task is expected to be executed by a new thread in the pool
							}
						}
					}
					
					// Simulates a long blocking IO
					private static void blockingIoOperation() {
						System.out.println("Executing a blocking task from thread: " + Thread.currentThread());
						try {
							Thread.sleep(1000); // simulates an IO operation and is a blocking operation
						} catch (InterruptedException e) {
							throw new RuntimeException(e);
						}
					}
				}
			
			1. Run:
				1. Thread pool grew to a 1000 threads
					1. Time: 1000 ms
						1. 1000 operations / second
				2. Increase the number of tasks to 10_000
					1. Application crashes:
						1. OS refused to allocate a new thread
							1. JVM ran out of memory or
							2. OS reached the cap on the number of threads it can allow
								1. **The cap is different on different OSs and configurations**
				3. **Allocating too many threads is extremely expensive and dangerous**
					1. It is better to limit the threads in the pool to 1000
					
							try (ExecutorService executorService = Executors.newFixedThreadPool(1000)) {
								for (...) {
									// ...
								}
							}
							
						1. At the rate of only 1000 operations / second, 10_000 operations would take around 10 s
							1. **We had to cap at 1000 ops / sec even though CPU is idle and is not running anything**
				4. Next change the blocking time to only 10 ms and execute 100 blocking operations instead of 1:
				
						public void run() {
							for (int j = 0; j < 100; j++) {
								blockingIoOperation();
							}
						}
						...
						Thread.sleep(10);
						...
						
					1. Run the application:
						1. It took around 22 k ms (double)
							1. **Reason: every task consists of 100 blocking operations with 99 context switches in between**
								1. Context switches: un-scheduling and re-scheduling the thread back.
								2. blocks again
								3. Context switching adds up time to blocking operations time
3. Thread-per-task model - analysis:
	1. Benefits:
		1. Improvement for:
			1. throughput
			2. Hardware utilization
		2. Processed tasks concurrently and completed them faster than in the thread-per-core model
	2. Issues:
		1. Threads are expensive
			1. Number of threds we can instantiate is limited (depending on the OS and the configuration)
			2. Threads consume stack memory and other resources
				1. CPU for context switching as well
			3. Too many threads - application will crash
			4. Too few threads - lower throughput and CPU utilization
				1. Throughput is directly proportional to the number of threads in the pool
		2. Price of context switches:
			1. OS is trying hard to fully utilize the CPU as efficiently as possible
				1. As soon as there's a blocking call, the OS unschedules that thread and find another one to make progress
			2. If we have too many threads and frequent blocking calls, it will lead to CPU being busy running the OS code
				1. OS code just moves threads in and out of CPU
			3. **Thrashing:**
				1. A situation where most of the CPU is spent on the OS managing the system
					1. Application code is not doing any useful work (we want to avoid this)
4. Thread-per-task model - conclusion:
	1. Thread-per-task has been the standard for many decades
	2. It will not give us the optimal
		1. Performance
		2. CPU utilization
5. Next: Other alternative approaches to handle tasks that involve blocking calls and IO blocking calls in particular
6. Summary:
	1. Made first attempt to improve the performance of tasks that involve blocking calls
	2. Used the thread-per-task / thread-per-request threading model (running each task on a separate tread)
		1. Allows processing thousands of tasks concurrently (improving CPU utilization)
		2. Issues:
			1. Can instantiate only a limited number of threads
			2. Too many threads - application crashes
			3. Too few threads - poor performance
				1. Throughput will be limited by the number of threads in the pool
			4. Potential thrashing
				1. If we have many frequent blocking calls

### Asynchronous, Non-Blocking IO with Thread Per Core Model ###
1. What we will learn in this lecture:
	1. Additional issues of thread-per-task model
		1. for long io Operations
	2. Introduction to non-blocking IO
		1. solves issues and give us much better performance
	3. Non-blocking IO vs thread-per-task model
		1. Comparison
2. Thread-per-task threading model - issues
	1. Does not give us optimal performance
		1. When a thread is blocked on long IO operation, it cannot be used for any other operation until blocking call returns
		2. Requires us to allocate more threads
			1. Consumes more resources
			2. Adding context-switching overhead
	2. Blocking calls can pose a bigger problem than just poor performance
		1. Example: Web-application that takes requests from external users
			1. There are two code paths
			
					public void handleRequest(...) {
						...
						if (needsDatabase()) {
							data = readFromDB();
						} else {
							data = readFromExternalService();
						}
					}
					
				1. The application can read a database which is internal to the company or send request to an external service that belongs to another company (runs on a different computer)
			2. Assume that we have a allocated a fixed pool of 100 threads (to ensure that the application doesn't crash due to too many threads)
			3. Let 50% of the requests make call to a db while other 50% make call to an external service.
			4. Assume that the external application becomes extremely slow (due to high load, garbage collection, or a performance bug)
				1. Our application can quickly run out of threads to handle incoming requests
					1. All those threads get blocked waiting for responses from the external service
			5. It affects 100% of our application even though only 50% needed data from the external service
				1. Inversion of control
					1. Instead of we controlling the external application, the external application controls us when it has issues
	3. Stability issues due to inversion of control
3. Solution: Introduction to Non-Blocking IO
	1. OSs and JVM added another way to interact with external devices called non-blocking IO
	
			public void someMethod() {
				nonBlockingIO(); // Does not block
				...              // CPU operation
			}
			
		1. Thread that calls the method returns immediately and can continue performing the next instruction
			1. Usually the code that comes after the IO operation is the one that uses the results from the IO operation
				1. To still execute the code that depends on the result of the non-blocking IO operation is in a callback
				
						nonBlockingIO(resultData -> {
							...
							useData(resultData);  // CPU operation
							...
						});
						
					1. The callback is executed sometime in the future when the result is ready with the result of the operation as the argument
			2. Example: Simple online store web-application that runs on a single core computer
			
					public void handleRequest(HttpExchange exchange) {
						Request request = parseUserRequest(exchange);
						readFromDatabaseAsync(request, (data) -> {
							sendPageToUser(data, exchange);
						});
					}
					
				1. When the first request arrives
					1. CPU performs `parseUserRequest` operation
					2. CPU then calls the `readFromDatabaseAsync` (non-blocking io operation) and returns to handle the next request
				2. When the next request arrives, CPU will start serving the request immediately in a similar way
				3. The CPU will continue serving more and more requests until the result of the first operation arrives at the OS 
				4. The OS will in-turn notify the application that the result of the first IO operation is ready
				5. The application thread then executes the callback `sendPageToUser` and send the result back to the user
				6. The above process will continue until the callbacks of all the operations are executed.
			3. Our request handling threads are not blocked and the CPU is fully utilized, we don't have to instantiate more threads than cores 
				1. CPU is fully utilized
				2. There is no overhead of context switches (**there are no context switches**)
			4. **The only reason for the creation of more threads is if we have more cores to execute requests in parallel**
	2. By using non-blocking IO with a thread per core model, we make our app immune to any issues due to external devices
		1. Example: Previous example with external application and a database
			1. If the external service becomes extremely slow or crashes, the users who need data from the database will not be affected
			2. Worst that can happen is that the callbacks that need to be called when we get the response from the external service will not execute at all or will execute with a long delay
4. Thread-Per-Core with Non-Blocking IO:
	1. Benefits:
		1. Thread-Per-Core + Non Blocking IO provides optimal performance
			1. This model can be used for any time of application
				1. CPU bound
				2. IO bound
		2. Stability and Security against issues or crashes of other systems that we communicate with
	2. Issues:
		1. Readability of blocking IO operations
		
			1. Synchronous code
		
					public void someMethod() {
						Result result1 = blockingOperation1();
						Result result2 = blockingOperation2(result1);
						Result result3 = blockingOperation2(result2);
						Result result4 = blockingOperation2(result3);
						Result result5 = blockingOperation2(result4);
						Result result6 = blockingOperation2(result5);
						...
					}
					
			2. Non-Blocking IO operations
			
					public void someMethod() {
						blockingOperation1(() -> {
							blockingOperation2(result1, (result2) -> {
								blockingOperation3(result2, (result3) -> {
									...
								});
							});
						});
					}
					
				1. Results in deep nesting
					1. It is called a callback hell
						1. It is hard to write, read, test or debug if something goes wrong
		2. Very Hard APIs
			1. Non-Blocking IO OS methods are very hard to work with
			2. JDK provides only a think layer of abstraction on top of the low-level APIs and are extremely hard to work with directly
			3. Most projects use third party libraries and frameworks to make it happen like:
				1. netty
				2. vert.x
				3. webflux
				4. ...
			4. The libraries increase the complexity of our code and size of our application and our dependency on external tools outside of our company
5. Threading Models Comparison:
	1. Blocking IO + Thread-Per-Task
		1. Performance
			1. High Memory & Context Switches
		2. Safety/ Stability
			1. Inversion of Control
		3. Code Writing
			1. Easy
		4. Code Reading
			1. Easy
		5. Testing
			1. Easy
		6. Debugging
			1. Easy
	2. Non Blocking IO + Thread-Per-Core
		1. Performance
			1. Optimal
		2. Safety/ Stability
			1. No issues
		3. Code Writing
			1. Hard
		4. Code Reading
			1. Hard
		5. Testing
			1. Hard
		6. Debugging
			1. Hard
	3. Engineers had to make a trade-off and decide whether performance is important and sacrifice the other aspects of software development or not
		1. Can we not enjoy the best of both worlds?
			1. Next
6. Summary:
	1. Learned about Non-Blocking IO as an alternative model for applications involving long io operations
		1. It can be used with thread-per-core model
			1. Improves performance
			2. Minimizes context switches and memory overhead
			3. Makes our system more stable and safe
	2. Non-Blocing IO has many drawbacks:
		1. Hard to write, read, test and debug
		2. Increases our dependencies on external framework and libraries
			1. JDK on its own doesn't provide easy ways to write code using non-blocking io

### Quiz 15: Threading Models for High Performance IO - Quiz ###

## Virtual Threads and High-Performance IO ##
### Introduction to Virtual Threads - Project Loom ###
1. What we will learn in this lecture
	1. Quick review of Java Thread and OS threads
	2. Introduction to Virtual Threads
	3. Demo of Virtual Threads (code example)
2. Quick review of Java Thread and OS threads
	1. Java Thread Objects and OS threads - Review

			JVM		run() {...}, start() -> Thread Object
												|
												start()
												|
												v
			OS								OS Thread
			
		1. When we run `start()` method, we ask the OS for creation and starting of an OS Thread belonging to application's Process
		2. We ask JVM to allocate a fixed size stack-space to store the thread's local variables
		3. From this point, OS is responsible for scheduling and running the thread on the CPU (like any thread it manages)
		4. Hence, Thread object in JVM is a thin wrapper around an OS Thread
			1. We call this a platform Thread
				1. Platform threads:
					1. They are expensive and heavy
						1. Each platform thread maps one-to-one with an OS thread and it is a limited resource
						2. They are also tied to static stack space of the JVM
3. Introduction to Virtual Thread
	1. New type of thread, developed as part of "Project Loom"
		1. Scheduled to be released as part of JDK 21
			1. Target release date - September 19, 2023
			2. Will "revolutionize" concurrent programming in Java
	2. You are as a Java Multithreading expert, need to be ready, you can:
		1. Use it correctly
		2. Optimize the performance of the application
	3. Architecture:
	
			JVM		run() {...}, start() -> Virtual Thread
												|
												start()
												(managed 
												by 
												JVM)
												|
												x
												|
												v
			OS								Not managed
			
		1. Virtual threads are managed by JVM and not by OS
		2. Virtual threads do not come with a fixed size stacks
			1. Virtual Thread is like any other Java object and is allocated in the Heap space
				1. It can be reclaimed by GC when it is no longer needed
		3. Virtual threads are very cheap and fast to create in large quantities
			1. How do they run on the CPU?
				1. JVM instantiates a small pool of platform threads
					1. When the JVM wants to run a Virtual Thread, it mounts it on a platform thread within its pool
						1. The platform thread that is used to mount a virtual thread is called a **carrier thread**
					2. When virtual thread finishes its execution, the JVM will unmount the thread from its carrier and makes the platform thread available for other objects
					3. The virtual thread object is garbage which is cleaned by GC
					4. If a virtual thread is unable to make any progress, the JVM will unmount it and save its state on the heap
						1. State:
							1. Instruction pointer
							2. Snapshot of carrier thread stack
						2. At that point, JVM can use the platform thread to mount another virtual thread on it
						3. When previous thread is able to continue and if another platform thread is available, then virtual thread is mounted on it
							1. If no platform threads are available, the virtual thread needs to wait
								1. If a virtual thread mounted on a carrier thread is unable to proceed, it is unmounted and the waiting virtual thread is mounted on the platform thread.
								2. IP is set to that of the virtual thread that is mounted
								3. The snapshot of the virtual thread is copied from the heap back to the carrier thread's stack memory
				2. The developers have very little control over the carrier threads and scheduling of virtual threads on them
					1. JVM manages it for us
4. Demo:

		public class VirtualThreadDemo {
			public static void main(String[] args) throws InterruptedException {
				Runnable runnable = () -> System.out.println("Inside thread: " + Thread.currentThread());
				
				// Thread platformThread = new Thread(runnable);
				Thread platformThread = Thread.ofPlatform().unstarted(runnable);
				
				platformThread.start();
				platformThread.join();
			}
		}
		
		public class VirtualThreadDemo {
			public static void main(String[] args) throws InterruptedException {
				Runnable runnable = () -> System.out.println("Inside thread: " + Thread.currentThread());
				
				Thread virtualThread = Thread.ofVirtual().unstarted(runnable);
				
				virtualThread.start();
				virtualThread.join();
			}
		}
		
	1. **ForkJoinPool-1-worker-1**
		1. To schedule virtual thread, JVM instantiated a thread pool of platform threads called ForkJoinPool-1
		2. JVM then mounted the virtual thread on one of the platform threads in ForkJoinPool-1 called worker-1
	2. New worker thread:
	
			private static final int NUMBER_OF_VIRTUAL_THREADS = 2;
			public static void main(String[] args) throws InterruptedException {
				Runnable runnable = () -> System.out.println("Inside thread: " + Thread.currentThread());
				
				List<Thread> virtualThreads = new ArrayList<>();
				
				for (int i = 0; i < NUMBER_OF_VIRTUAL_THREADS; i++) {
					Thread virtualThread = Thread.ofVirtual().unstarted(runnable);
					virtualThreads.add(virtualThread);
				}
				
				for (Thread virtualThread : virtualThread) {
					virtualThread.start();
				}
				
				for (Thread virtualThread : virtualThread) {
					virtualThread.join();
				}
			}
			
		1. The threads are mounted on different worker threads
		2. Increse the number of virtual threads to 20
			1. JVM dynamically decided to instantiate 6 platform threads
			2. The 20 virtual threads were scheduled to run on small pool of 6 platform threads
		3. Increase the number of virtual threads to 100
			1. Only 7 platform carrier threads exist
		4. Increase the number of virtual threads to 1000
			1. Only 8 platform carrier threads to 1000 (max number of cores)
5. Demo of mounting and unmounting of threads
	1. Example:
	
			List<Thread> virtualThreads = new ArrayList<>();
			
			...
				Thread virtualThread = Thread.ofVirtual().unstarted(new BlockingTask());
			...
	
			private static class BlockingTask implements Runnable {
				@Override
				public void run() {
					System.out.println("Inside thread: " + Thread.currentThread() + " before blocking call");
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						throw new RuntimeException(e);
					}
					System.out.println("Inside thread: " Thread.currentThread() + " after blocking call");
				}
			}
			
		1. Output:
			1. Changes workers sometimes
6. Run 100 virtual threads:
	1. Inspite of blocking, the JVM runs all the 100 threads on a small pool of 8 platform threads
		1. As soon as a virtual thread goes to sleep, the JVM unmounts it from platform thread making it available to run another virtual thread
7. Summary:
	1. Introduction to Virtual Threads
	2. Reviewed the "Platform Threads"
		1. Platform threads are expensive
			1. Each one contains a fixed size stack
			2. Each one maps 1-to-1 to OS threads which are limited in number
	3. Virtual threads
		1. They are just like any other Java objects allocated on the heap
		2. Mounting / Unmounting allows scheduling of many virtual threads on a limited number of carrier threads
8. Next:
	1. Why do we need virtual threads?
	2. How they can help us with Performance?

### Try Early Version of Virtual Threads ###
1. To experiment with VTs:
	1. Option 1: Download the early version of JDK 21
		1. Downlod from [link](https://jdk.java.net/21/)
		2. Unpack it
		3. In intellij:
			1. File > Project Structure
			2. Under Project Settings, click Project
			3. Add the new SDK
			4. Select path to unpacked directory of JDK 21
			5. Project
				1. SDK: 21
				2. Language level: SDK default
			6. Modules:
				1. Language level: Project default
	2. Option 2: Use Preview API of JDK 20
		1. https://www.udemy.com/course/java-multithreading-concurrency-performance-optimization/learn/lecture/38165428#overview

### High Performance IO with Virtual Threads ###
1. What we will learn in the lecture:
	1. Performance/ Throughput Gain with Virtual Threads for Blocking Operations
	2. Practical Example
2. Performance benefits of Virtual Threads:
	1. If VTs represent only CPU Operations:
		1. No performance benefit
			1. It is just an abstraction for scheduling tasks on a pool of (platform) threads in the order of their arrival (FIFO)
	2. If VTs represent operations that require the thread to wait (blocking operations, IO etc)
		1. Very usueful for performance/ **throughput**
			1. How?
				1. Example: Online store web application
				
						public void handleRequest(HttpExchange exchange) {
							Request request = parseUserRequest(exchange);
							Data data = readFromDatabase(request);
							sendPageToUser(data, exchange);
						}
						
					1. When the first request arrives from a user, we instantiate a virtual thread to handle it
					2. JVM will mount the VT on a platform thread to execute the code in the VT
					3. When Data `data = readFromDatabase(...)` is called, it first checks if thread is a platform thread or a virtual thread
						1. If it is a virtual thread, instead of blocking, it simply unmounts the virtual thread
							1. JVM internally uses a non-blocking version of the network operation
								1. Hides the complexity from us
									1. **We can use the blocking API**
					4. When another request arrives, a new VT is created to handle it (it is cheap)
						1. New OS thread or stack frame is not required
							1. JVM will mount the VT to the platform thread to be its carrier and run its code until it encounters a long blocking operation
							2. JVM will use non-blocking io implementation and unmount the VT from platform thread
					5. The above steps are repeated for each VT
					6. Once a response is received from blocking call, the JVM will mount the corresponding VT back to a platform thread and continue to execute the thread from the point where it was paused.
					7. When the handling of request is completed, the VT is no longer needed so it can be thrown away and later be GCd.
					8. The process is repeated for all VTs and the VTs are disposed off when they are no longer needed
				2. Advantages:
					1. No context switches when we use VTs since OS is not involved in scheduling
						1. Only the JVM stops the execution of one piece of code and starts or continues the execution of another piece of code belonging to another VT
							1. Unmounting + Mounting has ome overhead (but it is smaller than context switch involving the OS)
					2. Size of Carrier Threads
						1. Depends on the number of Cores
							1. If singe core, 1 platform thread
							2. If multiple cores, multiple platform threads
								1. JVM automatically handles the creation of platform threads not exceeding the number of cores
3. Threading models comparison:
	1. Blocking IO + Thread-per-Task
		1. Performance: High memory & context switches
		2. Safety / stability: Inversion of control
		3. Code writing: Easy
		4. Code reading: Easy
		5. Testing: Easy
		6. Debugging: Easy
	2. Non blocking IO + Thread-per-Core
		1. Performance: Optimal
		2. Safety / stability: No Issues
		3. Code writing: Hard
		4. Code reading: Hard
		5. Testing: Hard
		6. Debugging: Hard
	3. Virtual Threads
		1. Performance: Optimal
		2. Safety / stability: No Issues
			1. Non-blocking IO Internally
		3. Code writing: Easy
		4. Code reading: Easy
		5. Testing: Easy
		6. Debugging: Easy
4. More on benefits of Virtual Threads
	1. Many blocking operations were refactored to support virtual threads (in Java)
		1. Some of those operations:
			1. Sleep - `Thread.sleep()`
			2. Locks - `ReentrantLock.lock()`
			3. Semaphores - `Semaphore.acquire()`
			4. Networking API - Socket / Datagram (TCP/UDP)
			5. ...
5. Practical Example:
	1. Thread-per-task with virtual threads - example:
		1. N requests to a web application (concurrently)
		2. N blocking IO calls
			1. Read Files
			2. Request to database
			3. Request to external application
	2. Code:
	
			public class IoBoundApplication {
				private static final int NUMBER_OF_TASKS = 10_000;
				
				public static void main(String[] args) {
					System.out.printf("Running %d tasks\n", NUMBER_OF_TASKS);
					
					long start = System.currentTimeMillis();
					performTasks();
					System.out.println("Tasks took %dms to complete\n", System.currentTimeMillis() - start);
				}
				
				private static void performTasks() {
					// try (ExecutorService executorService = Executors.newCachedThreadPool()) {
					try (ExecutorService executorService = Executors.newVirtualThreadPerTaskExecutor()) {
						for (int i = 0; i < NUMBER_OF_TASKS; i++) {
							executorService.submit(() -> blockingIoOperation());
						}
					}
				}
				
				private static void blockingIoOperation() {
					System.out.println("Executing a blocking task from thread: " + Thread.currentThread());
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						throw new RuntimeException();
					}
				}
			}
			
		1. Crashes if we try 10_000 platform threads (OS doesn't allow)
		2. With VTs, executes all 10_000 tasks within around 1.5 seconds
			1. There were only 8 platform threads (matching with the number of cores)
		3. Next reduce the sleep duration to 10 ms
			1. Run blocking operation is a loop a 100 times:
			
					for (int i = 0; i < NUMBER_OF_TASKS; i++) {
						executerService.submit(new Runnable() {
							@Override
							public void run() {
								for (int j = 0; j < 100; j++) {
									blockingIoOperation();
								}
							}
						});
					}
				
				1. If we use `newFixedThreadPool` of 1000 threads, execution took 21k milli-seconds (twice as long)
					1. Due to very high overhead of context switching among very large number of platform threads (thrashing)
				2. If we use `newVirtualThreadPerTaskExecutor` of 1_000 threads
					1. It took only 8k milli-seconds
						1. Degradation - Due to higher overhead of context switching due to short io wait
6. Summary:
	1. Performance benefits of virtual threads for long blocking calls
	2. Virtual threads are a perfect choice for IO bound applications
	3. Using virtual threads:
		1. We get similar performance as thread-per-core + Non-blocking IO
		2. We get the ease of programming, testing and debugging of thread-per-task + blocking API
	4. Virtual threads' mounting + unmounting
		1. Has a bit of overhead
		2. Not as much as a context switch

### Virtual Threads Best Practices ###
1. What we will learn in the lecture:
	1. Virtual Threads and Thread Safety
	2. Virtual Threads and Performance
	3. Virtual Threads - Best Practices & Additional Details
	4. Observability and Debugging
2. Virtual Threads and Thread Safety
	1. Everything we learned about
		1. Thread-Safety applies 100% to virtual threads
			1. Race Conditions
			2. Deadlocks
			3. Data Races
		2. Inter-thread communication tools are the same
		3. Lock-free algorithms are the same
	2. VTs are just abstractions over platform threads that can run concurrently and in-parallel with each other
	3. Measures for correct execution
		1. Stay the same
	4. Intuition about thread safety stay exactly the same for virtual threads
3. Performance:
	1. Tasks involving only CPU
		1. Virtual threads provide no benefit
			1. Just another level of indirection on top of platform Threads
				1. At best, will not impact the performance
		2. Solution: If we are sure that there are no blocking calls in the code, we can stick to the platform threads
	2. Virtual Threads and Latency
		1. Virtual Threads provide no benefit
			1. If T is the total time to execute a task which includes long IO in between, it will still take T time to execute with virtual threads
		2. The only performance benefit to VTs is throughput
			1. While the computer is waiting for response from IO during which time the CPU can become idle, we can run other tasks using VTs
		3. Short and Frequent Blocking calls
			1. Short and frequent blocking calls are very inefficient
				1. VTs are better than using Platform Threads directly
					1. Thread-per-task with platform threads introduce context switches
					2. Thread-per-task with virtual threads have only **mounting/unmounting overhead**
						1. Much smaller than a context switch
							1. It is still not zero
								1. Solution: **Batch short IO operations into less frequent, long IO operations whenever possible**
4. Virtual Thread - Best Practice
	1. Never cosntruct fixed-size pools of virtual threads
		1. JVM already constructs an internal pool of platform threads for us
		2. We can use the simple and intuitive, thread-per-task model for each request or task
	2. Preferred way to use Virtual Threads is using `Executors.newVirtualThreadPerTaskExecutor()`
		1. Takes care of the creation of VTs for each task submitted to the executor service
	3. VTs are always daemon threads
		1. `virtualThread.setDaemon(...)` - Throws an exception
			1. It never prevents our application from terminating (they can run in background even if our main application terminates)
	4. VTs always have default priority
		1. `virtualThread.setPriority(...)` - Doesn't do anything
5. Observability and Debugging:
	1. Carrier threads are "hidden" from us
	2. But setting breakpoints/inspecting the thread state is the same as of platform threads
		1. Standard troubleshooting tools are also updated to treat VTs as any other threads (there is nothing special to do)
	3. Important note:
		1. We may have thousands/ millions of VTs (it becomes harder to debug)
		2. We need to follow all the thread safety guidelines/best practices as usual

### Quiz 16: Virtual Threads and High-Performance IO ###

## Beyond Multithreading - Final Lecture ##
### Distributed Systems, Big Data & Performance ###
1. Directions to explore further:
	1. From Multithreading to Distributed Systems
		1. Multithreading on much bigger scale
			1. When the volume of data or network traffic is too large for a single machine, run multiple instances on a cluster of many machines
			2. The multiple machines communicate with each other over the network using RPCs, HTTP, TCP, UDP, ...
		2. The machines are not sharing heap so they must store their shared data on external distributed Databases
			1. Non-atomic operations on shared data has challenges such as:
				1. Distributed locking
				2. Race conditions
				3. ...
			2. Other challenges:
				1. Network failures
				2. Network partitions
				3. Hardware & software failures
					1. As the number of machines grow
	2. To deal with challenges of distributed systems we need to use distributed algorithms:
		1. Leader election - to agree on a single machine to coordinate the work
		2. Failure Detection - To uninimously agree that a host is not reachable anymore and another node may be needs to take its place
		3. Recovery - after nodes come back to life after their failure was resolved
		4. Replication & Redundancy - to ensure that no data is lost if a particular machine dies
		5. ... (any other algorithm to ensure that the distributed task is performed correctly in a timely manner and without losing any data along the way)
	3. Scalability:
		1. Our system should be able to scale further to handle larger tasks and larger amounts of data
	4. Motivation:
		1. Decades of research on fault-tolerant, scalable, and high performance distributed systems brought us:
			1. Instant search
			2. Social networks
			3. Cloud computing
			4. E-Commerce
			5. Video on Demand
			6. Ride Sharing
			7. Autonomous vehicles
			8. ...
		2. **There are many engineering challenges that need to be solved**
	5. Big Data:
		1. Very interesting field (it is a subset of distributed systems) that deals with a very large flow of data
			1. The data to be processed is so big that we need to bring computation to the data instead of loading the data from database into the computing nodes
				1. Special file-system is used called HDFS (optimized for big files)
		2. Popular technologies:
			1. Apache Hadoop (Java)
			2. Apache Spark (Scala)
		3. Dominant factors:
			1. Large scale of work and data
				1. Multithreaded on a higher level of parallelism
		4. Motivation:
			1. Machine Learning - advances in big-data has allowed machines learning to handle large amounts of input data to find patterns or predict future products (that we might like)
				1. Diagnose medical conditions
				2. Detect fraudulant activities (malware) and filter spam emails
	6. Performance:
		1. Speed / Responsiveness
			1. Expectation from user is that they get response for their search or action instantaneously
				1. **Efficiency is of a very high priority for small and large companies alike**
		2. Key Topics:
			1. To master performance engineering we need to master:
				1. Computer architecture
					1. CPU instructions execution (how it is done)
					2. Caches (how is caching done)
					3. Branch prediction
						1. Need to learn how the different components work together to maximize performance
				2. Operating System
					1. How it coordinates between applications and hardware
				3. Compiler and runtime (JVM)
					1. How do they take our code and transform it into instructions that run on the CPU
				4. Memory management
					1. And organization
				5. GC tuning
					1. How to do that for our needs
				6. Optimal Algorithms, data structures, and threading models
					1. How to use them for the task
				7. Systematic performance measurement
					1. The ability to do that correctly and systematically
	7. There are many other fields that are directly or indirectly related to concurrency and performance

### Bonus Material - Courses Links and Coupons ###
1. [Other courses](https://topdeveloperacademy.com/courses)
2. Other topics to learn:
	1. Software architecture
	2. Cloud computing
	3. Advanced Java
	4. Performance
	5. Concurrency
	6. Interview preparation
	7. ...
3. [LinkedIn](https://www.linkedin.com/comm/mynetwork/discovery-see-all?usecase=PEOPLE_FOLLOWS&followMember=michaelpog)
4. [Free newsletter](https://subscribe.topdeveloperacademy.com/)
	1. For senior engineers, tech leads, software architects
5. [1-on-1 Technical Career Coaching](https://topdeveloperacademy.com/technical-career-coaching) - for personal help, advice, or guidance on achieving goals