# Advanced Java Topics: Java Reflection - Master Class #
## Section 1: Introduction to Reflection ##
### Introduction to Java Reflection ###
1. What we learn in this lecture
	1. What is Java Reflection
	2. Reflection Use Cases - Examples
	3. Java Reflection - Challenges
2. What is Java Reflection
	1. Language and JVM feature that gives us Runtime access to information about our application's classes and objects
	2. Those features are available to us through the Reflection API (set of classes and methods)
3. What can we do with Java Reflection?
	1. Using Reflection API we can write flexible code that
		1. Links different software components together at runtime
		2. Constructs new program flow without any source code modifications
	2. Reflection allows writing general purpose algorithms that dynamically adapt and change their behavior based on the type of objects or classes they are working on
4. Program without reflection
	
```
Data -input-> Program without Reflection -output-> Output data
```

5. Program with reflection

```
                    (app code)
               +----input----+
               |             v
Data -input-> Program with Reflection -output-> Output data
```

6. More on Reflection
	1. With the ability to analyze application's objects and classes at Runtime
	2. We can construct very powerful
		1. Libraries
		2. Frameworks
		3. Software Designs
			1. That would otherwise be impossible
7. Reflection Use Cases - Examples
	1. Popular Java Reflection Use Cases
		1. JUnit - Framework for Unit Testing of Java Applications
			1. JUnit - without JUnit
			
			```java
			public class CarTest {
				public void setUp() {...}
				public void testDrive() {...}
				public void testBrake() {...}
				...
				public static void main(String[] args) {
					CarTest carTest = new CarTest();
					carTest.setUp();
					carTest.testDrive();
					carTest.setUp();
					carTest.testBrake();
				}
			}
			```
			
			2. JUnit - Unit Testing Framework for Java
			
			```java
			public class CarTest {
				@Before
				public void setUp() {...}
				
				@Test
				public void testDrive() {...}
				
				@Test
				public void testBrake() {...}
				...
			}
			```
			
				1. JUnit will
					1. Start test program
					2. Construct CarTest object
					3. Find setup and test method
					4. Run tests (in the correct order)
					5. Test report
		2. Dependency Injection
			1. Spring/ Spring Boot
			2. Google Guice
			3. Reflection Use Cases - Dependency Injection
			
			```
			public class Car {
				...
				public Car() {
					this.engine = new Engine(); // may have their own dependencies
					this.driver = createDriver(); // may have their own dependencies
				}
				...
				public void drive() {...}
			}
			```
			
				1. Tightly couples `Car` class to details of the creation of all of its dependencies
				
			4. Reflection Use Cases - Spring
			
			```
			public class Car {
				...
				@Autowired
				public Car(Engine engine, Driver driver) {
					this.engine = engine;
					this.driver = driver;
				}
				
				...
				public void drive() {...}
			}
			```
			
				1. Spring uses reflection
				
			5. Configuration
			
			```java
			@Configuration
			public class Config {
				@Bean
				public Engine constructEngine() {...}
				
				@Bean
				public Driver constructDriver() {...}
			}
			```
		
		3. JSON Serialization / Deserialization
			1. Jackson
			2. Gson
				1. JSOn Parsing
					1. Looking at a JSON string, library can use reflection to inspect the class, analyze its fields, and populate its values (based on field names)
			3. Code:
			
			```
			String json = "{\"name\":\"John\",\"age\":25,\"pets\":[\"dog\","\cat\"]}";
			
			Person person = objectMapper.readValue(json, Person.class);
			```
			
			4. Jackson Parsing
			
			```java
			Person person = new Person("John", 25, ["dog", "cat"]);
			
			String json = objectMapper.writeValueAsString(person);
			```
			
		4. Other popular use cases include:
			1. Logging frameworks
			2. ORM (Object-Relational Mapping) tools
			3. Web Frameworks
			4. Developer tools
			5. Many more...
		5. We can use Reflection to architect our applications and libraries and augment them with unique functionality and features
8. Java Reflection - Challenges
	1. Can do very powerful things and get access to internal and hidden structures
		1. If use incorrectly or not for the right purpose we risk:
			1. Making the code harder to maintain
			2. Slower to run
			3. Dangerous to execute (can crash unrecoverably)
		2. "With Great Power, Comes Great Responsibility"
		3. Reflection is often reserved for skilled developers (who has strong grasp on the Java language)
9. Roadmap for Overcoming Those Challenges
	1. Throughout the course we will learn how to use Reflection
		1. Correctly
		2. Safely
	2. Practice our knowledge on real life use cases
	3. So that by the end of the course we will have
		1. Confidence in our skills
		2. Intuition on when to use reflection
10. Summary:
	1. Java Reflection is a language and JVM feature
	2. Allows to write Java code gets special information and access to our application's classes and objects
	3. We talked about many use cases for Java Reflection
		1. Popular external libraries and frameworks
		2. Our own applications
	4. Challenges of Java Reflection which require extra care

### Reflection API Gateway & Wildcards ###
1. What we learn in this lecture
	1. Introduction to Reflection's Entry Point (Class)
	2. Ways to obtain an object of type `Class<?>`
	3. Java Wildcards
2. Introduction to Reflection's Entry Point (`Class`)
	1. `Class<?>` is an entry point for us to reflect on our application's code
	2. An object of `Class<?>` contains all the information on
		1. A given object's runtime type
		2. A particular class in our application
	3. That information includes
		1. What methods and fields it contains
		2. What classes it extends
		3. What interfaces it implements
		4. ...
3. Ways to obtain an object of type `Class<?>`
	1. Three ways:
		1. `Object.getClass()`
		
		```java
		String stringObject = "some-string";
		
		Car car = new Car();
		Map<String, Integer> map = new HashMap<>();
		
		Class<String> stringClass = stringObject.getClass();
		Class<Car> carClass = car.getClass();
		Class<?> mapClass = map.getClass(); // returns HashMap class (not `Map` interface class) - it is the runtime type of the variable
		```
		
			1. No Object.getClass(); for primitive types
			
			```java
			boolean condition = true;
			
			int value = 55;
			
			double price = 1.5;
			```
			
		2. ".class" suffix to a type name (when we don't have an instance)
		
		```java
		Class<String> stringClass = String.class;
		Class<Car> carClass = Car.class;
		Class<?> mapClass = HashMap.class;
		```
		
		```java
		// .class - primitive types
		// Useful if we want to obtain full type information if we inspect method parameters or class members
		
		Class booleanType = boolean.class;
		
		Class intType = int.class;
		
		Class doubleType = double.class;
		```
		
		3. `Class.forName(...)` - We can dynamically look up a class in a class path using the fully qualified name
		
		```java
		Class<?> stringType = Class.forName("java.lang.String"); // built-in classes
		Class<?> carType = Class.forName("vehicles.Car");
		Class<?> engineType = Class.forName("vehicles.Car$Engine"); // inner class
		
		package vehicles;
		class Car {
			...
			static class Engine {
				...
			}
		}
		```
		
			1. No `Class.forName()` for Primitive Types:
			
			```java
			boolean condition = true;
			
			int value = 55;
			
			double price = 1.5;
			
			Class booleanClass = Class.forName("boolean"); // Runtime error (instead of a compilation error)
			```
			
			2. Notes on `Class.forName()`
				1. Much more likely to mistype the class name and get the `ClassNotFoundException` (at runtime)
				2. The class we pass into the `Class.forName(...)` may not even exist
				3. `Class.forName(...)` is the least safest way to get a `Class<?>` object
				4. There are use cases where `Class.forName(...)` is our only option
					1. When to use `Class.forName()` - Use Cases
						1. When the type we want to inspect or instantiate is passed from a user-defined config file
						
						```
						<servlet>
							<servlet-name>image-servlet</servlet-name>
							<servlet-class>servlets.ImageServlet</servlet-class>
						</servlet>
						```
						
						```
						<appender name="fileAppender" class="org.apache.log4j.RollingFileAppender">
							<layout class="org.apache.log4j.PatternLayout">
						</appender>
						```
						
						```
						<bean id="vehicle" class="vehicles.Car">
							<property name="numberOfWheels" value="4" />
						</bean>
						```
						
						```
						<bean id="vehicle" class="vehicles.Motorcycle"> <!-- Users can modify the application's behavior just by changing the text-file -->
							<!-- No need to change or re-compile the source-code -->
							<property name="numberOfWheels" value="4" />
						</bean>					
						```
						
						```java
						Class<?> vehicle = Class.forName(value);
						```
					
						2. When the class we want to reflect on is not part of our project and does not exist when we compile the code
							1. The class is added to the application class-path at runtime
							2. Use-cases:
								1. When we are building a library separate from the application that will import and use it
4. Generics - Java Wildcards

```
Number (abstract class)
 ^
/_\
 |
extends
 |
Integer (class)

CharSequence (interface)
 ^
/_\
 |
implements
 |
String (class)
```

```
List<Number>
 ^
/_\
 |
x extends
 |
List<Integer>
```

```
List<?>
 ^
/_\
 |
extends
 |
List<Number> / List<Integer> / List<CharSequence> / List<String>
```

```
List<?>
 ^
/_\
 |
extends
 |
List<T> // For any generic parameter T
```

	1. Using `Class<?>` we can describe a Class object of any parameter type
	2. `Class<?>` is a super type of `Class<T>` of any type `T`
		1. Example: `Class<?> carClass = Class.forName("vehicles.Car");`
			2. Useful when the compiler doesn't know the generic type at compile time. In the above case, type is provided as a string
		2. Example:
		
		```java
		Map<String, Integer> genericMap = new HashMap<>();
		Class<?> hashMapClass = genericMap.getClass(); // generic parameter of a class is generic type
		```
		
	3. Used to put restrictions on types of classes passed as method parameter type to those that extend or implement a particular class or interface
	
	```java
	public List<String> findAllMethods(Class<? extends Collection> clazz) {
		...
	}
	```
	
5. Summary:
	1. `Class<?>` - The gateway to use reflection
	2. Learned 3 ways to obtain the Class object for any type
		1. `getClass()` method on an existing object
		2. Append ".class" to any class or primitive type
		3. `Class.forName(...)` - to look up a class using its fully qualified name
	3. Java Wildcards

### Reflection API Gateway in Practice ###
1. What we learn in this lecture
	1. Analyze custom and JDK built in classes and data types
	2. Practice obtaining the `Class<?>` object using different methods
2. Example:

```
package exercises;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

public class Main {

  public static void main(String[] args) throws ClassNotFoundException {
    Class<String> stringClass = String.class;
    
    Map<String, Integer> map = new HashMap<>();
    Class<?> hashMapClass = map.getClass();

    Class<?> squareClass = Class.forName("exercises.Main$Square");

    // printClassInfo(stringClass, hashMapClass, squareClass);

		var circleObject = new Drawable() {
			@Override
			public int getNumberOfCorners() {
				return 0;
			}
		};

    printClassInfo(Collection.class, boolean.class, int [][].class, Color.class, circleObject.getClass());
  }

	private static void printClassInfo(Class<?> ... classes) {
		for (Class<?> clazz : classes) {
			System.out.println(String.format("class name: %s, class package name : %s", clazz.getSimpleName(), clazz.getPackageName()));
			
			Class<?>[] implementedInterfaces = clazz.getInterfaces();
			
			for (Class<?> implementedInterface : implementedInterfaces) {
				System.out.println(String.format("class %s implements : %s", clazz.getSimpleName(), implementedInterface.getSimpleName()));
			}

      System.out.println("Is array: " + clazz.isArray());
      System.out.println("Is primitive: " + clazz.isPrimitive());
      System.out.println("Is enum: " + clazz.isEnum());
      System.out.println("Is interface: " + clazz.isInterface());
      System.out.println("Is anonymous class: " + clazz.isAnonymousClass());
			
			System.out.println();
			System.out.println();
		}
	}

	private static class Square implements Drawable {
		@Override
		public int getNumberOfCorners() {
			return 4;
		}
	}

	private static interface Drawable {
		int getNumberOfCorners();
	}
	
	private enum Color {
		BLUE,
		RED,
		GREEN
	}
}
```

3. Summary:
	1. We learned how to get the basic data about a given class that represents a Java type
	2. We analyzed a variety of types. From a simple String to 2D arrays and anonymous classes
	3. We practiced getting the `Class<?>` object from 
		1. An existing instance of an Object
		2. Appending ".class" to known type name
		3. `Class.forName("package.ClassName")`

### Coding Exercise 1: IDE Information Plugin - Class Analysis ###
### Coding Exercise 2: Reflection, Interfaces and Basic Recursion ###
### Solution - Reflection, Interfaces and Recursion ###

## Section 2: Object Creation and Constructors ##
### Constructor Discovery & Object Creation ###
1. What we learn in this lecture
	1. Introduction to `Constructor<?>` and ways to obtain it
	2. Constructor parameters inspection using Reflection
	3. Dynamic object creation using Reflection
2. `java.lang.reflect.Constructor<?>`
	1. A constructor of a Java class is represented by an instance of `Constructor<?>` class
	2. The Constructor object contains all the information about the class's constructor including:
		1. Number of parameters
		2. Types of the parameters
	3. A class may have multiple constructors
3. Methods to get `Constructor<?>` objects
	1. `Class.getDeclaredConstructors()` **(M)**
		1. Returns all declared constructors within the class
		2. Includes all the public and non-public constructors
	2. `Class.getConstructors()` **(M)**
		1. Returns only public constructors
	3. If you know the particular constructor parameter types we call:
		1. `Class.getConstructor(Class<?> ... parameterTypes)` or `Class.getDeclaredConstructor(Class<?> ... parameterTypes)`
			1. Returns a particular constructor based on the parameter types
			2. Throws `NoSuchMethodException` if no matching constructor is found
4. Getting the default constructor:
	1. `Constructor<?>[] constructors = Person.class.getConstructors();`
		1. Single element array containing the default constructor
	2. `Constructor<?> defaultConstructor = Person.class.getDeclaredConstructor();`
5. Constructor parameters inspection using Reflection
	1. Example:
	
	```java
	package in.co.benesyslabs.training.java.reflection_poc;

	import java.lang.reflect.Constructor;
	import java.util.Arrays;
	import java.util.List;
	import java.util.stream.Collectors;

	public class Main {
	  public static void main(String[] args) {
		printConstructorData(Person.class);
		printConstructorData(Address.class);
	  }

	  public static void printConstructorData(Class<?> clazz) {
		Constructor<?>[] constructors = clazz.getDeclaredConstructors();

		System.out.println(String.format("Class %s has %d declared constructors", clazz.getSimpleName(), constructors.length));

		for (int i = 0; i < constructors.length; i++) {
		  Class<?>[] parameterTypes = constructors[i].getParameterTypes();

		  List<String> parameterTypeNames = Arrays.stream(parameterTypes).map(type -> type.getSimpleName()).collect(Collectors.toList());

		  System.out.println(parameterTypeNames);
		}
	  } 

	  public static class Person {
		private final Address address;
		private final String name;
		private final int age;

		public Person() {
		  this.name = "anonymous";
		  this.age = 0;
		  this.address = null;
		}

		public Person(String name) {
		  this.name = name;
		  this.age = 0;
		  this.address = null;
		}

		public Person(String name, int age) {
		  this.name = name;
		  this.age = age;
		  this.address = null;
		}

		public Person(Address address, String name, int age) {
		  this.address = address;
		  this.name = name;
		  this.age = age;
		}
	  }

	  public static class Address {
		private String street;
		private int number;

		public Address(String street, int number) {
		  this.street = street;
		  this.number = number;
		}
	  }
	}
	```
	
6. Goal and Motification - Object Constructor
	1. Implment a single "factory" method that can construct an object of any class
	2. Depending on the arguments passed to our method, it will find the right constructor
	3. Construct the given class object by calling the right constructor
	4. Without reflection it is impossible
7. Without reflection, we have to write a switch-case statement with one case for each type (not generic)
8. Object Creation with Java Reflection
	1. `Constructor.newInstance(Object ...arguments)` **(M)**
		1. Takes a variable number of constructor arguments in the type and order of the constructor parameters declared in the constructor
	2. Upon success
		1. Calls the appropriate constructor
		2. Returns an object of the given class
	3. Upon failure
		1. Throws an appropriate exception, describing the reason of the failure
9. Example:

```java
package in.co.benesyslabs.training.java.reflection_poc;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
  public static void main(String[] args) throws IllegalAccessException, InvocationTargetException, InstantiationException {
    printConstructorData(Person.class);
    printConstructorData(Address.class);

    Person person = createInstanceWithArguments(Person.class);
    System.out.println(person);

    Person person2 = createInstanceWithArguments(Person.class, "John", 20);
    System.out.println(person2);

    Address address = createInstanceWithArguments(Address.class, "First Street", 10);
    Person person3 = createInstanceWithArguments(Person.class, address, "John", 10);
    System.out.println(person3);
  }

  @SuppressWarnings({ "uncheched", "unchecked" })
  public static <T> T createInstanceWithArguments(Class<T> clazz, Object ...args) throws IllegalAccessException, InvocationTargetException, InstantiationException {
    for (Constructor<?> constructor : clazz.getDeclaredConstructors()) {
      if (constructor.getParameterTypes().length == args.length) {
        return (T) constructor.newInstance(args);
      }
    }
    System.out.println("An appropriate constructor was not found");
    return null;
  }

  public static void printConstructorData(Class<?> clazz) {
    Constructor<?>[] constructors = clazz.getDeclaredConstructors();

    System.out.println(String.format("Class %s has %d declared constructors", clazz.getSimpleName(), constructors.length));

    for (int i = 0; i < constructors.length; i++) {
      Class<?>[] parameterTypes = constructors[i].getParameterTypes();

      List<String> parameterTypeNames = Arrays.stream(parameterTypes).map(type -> type.getSimpleName()).collect(Collectors.toList());

      System.out.println(parameterTypeNames);
    }
  } 

  public static class Person {
    private final Address address;
    private final String name;
    private final int age;

    public Person() {
      this.name = "anonymous";
      this.age = 0;
      this.address = null;
    }

    public Person(String name) {
      this.name = name;
      this.age = 0;
      this.address = null;
    }

    public Person(String name, int age) {
      this.name = name;
      this.age = age;
      this.address = null;
    }

    public Person(Address address, String name, int age) {
      this.address = address;
      this.name = name;
      this.age = age;
    }

    @Override
    public String toString() {
      return "Person [address=" + address + ", name=" + name + ", age=" + age + "]";
    }
  }

  public static class Address {
    private String street;
    private int number;

    public Address(String street, int number) {
      this.street = street;
      this.number = number;
    }

    @Override
    public String toString() {
      return "Address [street=" + street + ", number=" + number + "]";
    }
  }
}
```

10. Summary:
	1. We learned a few ways to get the information about declared public and non constructors of any Java class
	2. We learned to get the list of parameter types of a constructor
	3. Implemented a powerful, generic method that can construct an object of any class
	4. The factory method can take any number of arguments and find just the right constructor
	5. We realized that implementing such a factory method without reflection is impossible
	6. With reflection we achieved it just with a few lines of code
	7. At the heart of that method was the `Constructor.newInstance(Object ...args)` method

### Restricted Constructor Access ###
1. What we will learn in this lecture
	1. Non-public constructor invocation
	2. Server configuration using reflection
2. Non-public constructor invocation
	1. Calling private constructors
		1. Cannot be called from outside the class
	2. Private constructors with reflection
		1. Using reflection we have full access to all
			1. public
			2. protected
			3. package-private
			4. private
		2. Using `Constructor.newInstance()` we can construct objects of a class using the restricted constructors
		3. Exception: A class belonging to a Java module that does not allow access to a given class
		4. Use-case:
			1. Creation of an immutable object of a class that can be accessible to everyone but can only be created by library or framework (uses reflection)
				1. System configurations
		5. Calling private constructors with reflection
		
		```java
		Constructor<?> constructor = getDeclaredConstructor();
		
		constructor.setAssessible(true); // make constructor accessible
		
		constructor.newInstance(arg1, arg2);
		```
		
3. Server configuration using reflection:

```java
package in.co.benesyslabs.training.java.reflection_poc;

import java.io.IOException;
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

import in.co.benesyslabs.training.java.reflection_poc.web.WebServer;

public class Main2 {
  public static void main(String[] args) throws InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException, NoSuchMethodException, IOException {
    initConfiguration();
    WebServer webServer = new WebServer();
    webServer.startServer();
  }

  public static void initConfiguration() throws InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException, NoSuchMethodException {
    Constructor<ServerConfiguration> constructor = ServerConfiguration.class.getDeclaredConstructor(int.class, String.class);

    constructor.setAccessible(true);
    constructor.newInstance(8080, "Good Day!");
  }
}
```

```java
package in.co.benesyslabs.training.java.reflection_poc.web;

import in.co.benesyslabs.training.java.reflection_poc.ServerConfiguration;

import java.io.IOException;
import java.io.OutputStream;
import com.sun.net.httpserver.*;

public class WebServer {
  public void startServer() throws IOException {
    HttpServer httpServer = HttpServer.create(ServerConfiguration.getInstance().getServerAddress(), 0);

    httpServer.createContext("/greeting").setHandler(exchange -> {
      String responseMessage = ServerConfiguration.getInstance().getGreetingMessage();

      exchange.sendResponseHeaders(200, responseMessage.length());

      OutputStream responseBody = exchange.getResponseBody();
      responseBody.write(responseMessage.getBytes());
      responseBody.flush();
      responseBody.close();
    });

    System.out.println(String.format("Starting server on address %s:%s", ServerConfiguration.getInstance().getServerAddress().getHostName(), ServerConfiguration.getInstance().getServerAddress().getPort()));

    httpServer.start();
  }
}
```

4. Summary:
	1. We learned an advanced feature of Java Reflection - Ability to construct objects using otherwise inaccassible constructors.
	2. We demonstrated the feature in a use cases where we wanted to instantiate an object of a class that would be accessible to use, but impossible to construct accidentally.
	3. All we need to do to use the feature is to call `Constructor.setAccessible(true)` before calling `Constructor.newInstance(...)`
5. Important Notes:
	1. The advanced feature should be reserved to specific use cases
	2. It should not be abused to invoke internal or deliberately restricted constructors on classes that do not belong to us
	3. With reflection, we gain a lot of power, but also a lot of responsibility
	4. We need to be careful about where we break the access-modifiers rules (only when it makes sense and adds value)

### Restricted Classes Instantiation - Automatic Dependency Injection Implementation ###
1. What we will learn in the lecture
	1. Package-private classes instantiation using constructor class
	2. External package - private classes access use cases
	3. Dependency injection implementation
2. Package-private classes instantiation using constructor class
	1. Package-private classes
		1. There are cases where we need to allow access to package-private classes from outside the package for:
			1. Reading
			2. Initializing
		2. Typically when we want to use an external library to help us initialize those classes
		3. The code in the external libraries is outside of our package
	2. We need to set its constructor's `accessible` property to true
3. Examples:
	1. Parsing to/from Java Objects
		1. `BestPriceApi.java`
			1. It is a gateway to the package for users who want to get the best price for a product
			2. It uses the following package private classes and an external library to communicate with external service 
		2. `HttpClient.java`
		3. `Request.java`
		4. `Response.java`
	2. Code:
	
	```java
	package bestprice;
	import com.fasterxml.jackson.databind.ObjectMapper;
	
	class HttpClient {
	  private final ObjectMapper objectMapper;
	  
	  public float getPriceFromService() {
	    Request request = buildRequest(); // It is an object of a package-private class
		byte[] requestData = objectMapper.writeValueAsBytes(request); // external library has no access
		byte[] responseData = sendHttpRequest(requestData);
		Response response = objectMapper.readValue(requestData, Response.class); // package-private class
		response.getPrice();
	  }
	}
	```
	
4. Dependency Injection
	1. Instantiation of Package-Private classes from another package
	2. Auto creation of objects at application setup
		1. Assume classes are internal and are restricted from external users
		2. Assume each class depends on the existence of other classes (they can be passed into its constructor)
		3. DPInjector.java - needs access
	3. OOAD implementation of tic-tac-toe
		1. Classes:
			1. BoardDimensions
				1. Board
				2. BoardPrinter
			2. KeyboardInputProvider
				1. HumanPlayer
			3. ComputerInputProvider
				1. ComputerPlayer
			4. TickTacToeGame
	4. We are going to construct by implementing an automatic dependency injection engine using reflection
	5. We performed the exact same task on each of the classes we visited
		1. A recursive algorithm (function that calls intsef) is a great fit for the implementation
			1. For each dependency we visit
				1. We keep going deep into the graph
				2. Until we find a class with no dependencies that we can instantiate
				3. Once the entire graph is covered: We are done
5. Code:

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package init;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.ArrayList;
import java.util.List;

import game.Game;
import game.internal.TicTacToeGame;

/**
 * Tic Tac Toe
 * https://www.udemy.com/course/java-reflection-master-class
 */

public class Main {

    public static void main(String[] args) throws InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException {
       Game game = constructObjectRecursively(TicTacToeGame.class);
       game.startGame();
    }

    @SuppressWarnings("unchecked")
    public static <T> T constructObjectRecursively(Class<T> clazz) throws InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException {
        Constructor<?> constructor = getFirstConstructor(clazz);

        List<Object> constructorArguments = new ArrayList<>();

        for (Class<?> argumentType : constructor.getParameterTypes()) {
            Object argumentValue = constructObjectRecursively(argumentType);
            constructorArguments.add(argumentValue);
        }

        constructor.setAccessible(true);
        return (T) constructor.newInstance(constructorArguments.toArray());
    }

    private static Constructor<?> getFirstConstructor(Class<?> clazz) {
        Constructor<?>[] constructors = clazz.getDeclaredConstructors();
        if (constructors.length == 0) {
            throw new IllegalStateException(String.format("No constructor has been found for class %s", clazz.getName()));
        }
        return constructors[0];
    }
}
```

6. Summary:
	1. We talked about another powerful capability of Java Reflection:
		1. Inspection and instantiation of package-private classes
	2. We discussed a few scenarios where breaking the private-package access modifier restriction is desirable
	3. Implemented a basic but powerful version of dependency injection
	4. Tested on an object-oriented implementation of the Tic-Tack-Toe game

## Section 3: Inspection of Fields & Arrays ##
### Introduction to Fields ###
1. What we will learn in this lecture
	1. Introduction to the Field class
	2. Ways to obtain Field class objects
	3. Synthetic class Fields
	4. Getting class Field values
2. Introduction to the Field class
	1. Field - A variable declared within the direct boundaries of a class or an interface
		1. Class variables - static 
		2. Object variables
	2. Properties:
		1. Name
		2. Typee
3. Ways to obtain Field class objects
	1. Obtain field objects of a class
		1. `Class.getDeclaredFields()` **(M)** - get all declared fields of a class
			1. Includes all fields regardless of their access modifiers
				1. Excludes inherited fields
		2. `Class.getFields()` **(M)** - get all the public fields of a class
	2. If we know the field's name:
		1. `Class.getDeclaredField(fieldName)` **(M)** - get the `Field` object corresponding to the declared field with the given name
		2. `Class.getField(fieldName)` **(M)** - get the `Field` object corresponding to the public field with the given name
	3. If the field with the given `fieldName` does not exists a `NoSuchFieldException` is thrown
4. Example:

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package init;

import java.lang.reflect.Field;

/**
 * Introduction to Fields
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {

    public static void main(String[] args) {
        printDeclaredFieldsInfo(Movie.class);
    }

    public static void printDeclaredFieldsInfo(Class<?> clazz) {
        for (Field field : clazz.getDeclaredFields()) {
            System.out.println(String.format("Field name : %s type : %s", field.getName(), field.getType().getName()));
            System.out.println();
        }
    }

    public enum Category {
        ADVENTURE,
        ACTION,
        COMEDY
    }

    public static class Movie extends Product {
        public static final double MINIMUM_PRICE = 10.99;

        private boolean isReleased;
        private Category category;
        private double actualPrice;

        public Movie(String name, int year, double price, boolean isReleased, Category category) {
            super(name, year);
            this.isReleased = isReleased;
            this.category = category;
            this.actualPrice = Math.max(price, MINIMUM_PRICE);
        }

        // Nested class
        public class MovieStats {
            private double timesWatched;

            public MovieStats(double timesWatched) {
                this.timesWatched = timesWatched;
            }

            public double getRevenue() {
                return timesWatched * actualPrice;
            }
        }
    }

    // Superclass
    public static class Product {
        protected String name;
        protected int year;
        protected double actualPrice;

        public Product(String name, int year) {
            this.name = name;
            this.year = year;
        }
    }
}
```

5. Synthetic Fields
	1. Java compiler generates artificial fields for internal usage
	2. We don't see those fields unless we use reflection to discover them at runtime
	3. Synthetic fields and their names are compiler specific
	4. In most cases we don't want to touch/modify/rely on them
	5. To find out if a `Field` is synthetic, we check the `Field.isSynthetic()` **(M)**
6. Getting class Field values

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package init;

import java.lang.reflect.Field;

/**
 * Introduction to Fields
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {

    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException, NoSuchFieldException {
        Movie movie = new Movie("Inception", 2010, 8.99, true, Category.ADVENTURE);
        printDeclaredFieldsInfo(Movie.class, movie);

        Field minPriceStaticField = Movie.class.getDeclaredField("MINIMUM_PRICE");
        System.out.println(String.format("Static MINIMUM_PRICE value : %f", minPriceStaticField.get(null))); // Accessing static field value with null instance
    }

    public static <T> void printDeclaredFieldsInfo(Class<T> clazz, T instance) throws IllegalArgumentException, IllegalAccessException {
        for (Field field : clazz.getDeclaredFields()) {
            System.out.println(String.format("Field name : %s type : %s", field.getName(), field.getType().getName()));

            System.out.println(String.format("Is synthetic field : %s", field.isSynthetic()));
            System.out.println(String.format("Field value is : %s", field.get(instance)));

            System.out.println();
        }
    }

    public enum Category {
        ADVENTURE,
        ACTION,
        COMEDY
    }

    public static class Movie extends Product {
        public static final double MINIMUM_PRICE = 10.99;

        private boolean isReleased;
        private Category category;
        private double actualPrice;

        public Movie(String name, int year, double price, boolean isReleased, Category category) {
            super(name, year);
            this.isReleased = isReleased;
            this.category = category;
            this.actualPrice = Math.max(price, MINIMUM_PRICE);
        }

        // Nested class
        public static class MovieStats {
            private double timesWatched;

            public MovieStats(double timesWatched) {
                this.timesWatched = timesWatched;
            }

            public double getRevenue() {
                return timesWatched; // has access to parent's field
            }
        }
    }

    // Superclass
    public static class Product {
        protected String name;
        protected int year;
        protected double actualPrice;

        public Product(String name, int year) {
            this.name = name;
            this.year = year;
        }
    }
}
```

7. Java Reflection - Fields
	1. Using the FIeld class, we can use Java Reflection to get information about a class's or object's fields, dynamically at runtime
	2. We can write generic algorithms and libraries that operate on objects
		1. Whose types are unknown
		2. Don't even exist until the program is executed
8. Summary:
	1. We learned a few ways to obtain the object's and class's Fields using Reflection
	2. We learned how to get some basic information about fields such as its
		1. Name
		2. Type
		3. Runtime value
	3. We learned about synthetic fields, which are compiler generated and should not be relied on or modified

### Reading Fields - JSON Serializer ###
1. What we will learn in this lecture 
	1. Java Reflection - Fields use cases
	2. Practical example of an Object to Json Serializer
2. Fields continued and use cases
	1. Using the `Field` class we were able to get a class's field
		1. Type
		2. Name
	2. Read the field value of an object
	3. This ability really shines when we are working on Objects that represent data
	4. The types of those objects and fields may not be known to us at compile time or when we write our program
	5. The object types are typically not even available to our library
	6. The types may be defined in the application that uses our library
3. Practical example of an Object to Json Serializer
	1. JSON - popular format for
		1. Storing objects in a database
		2. Sending data between services over the network
	2. It supports a small set of types (simple protocol)
	3. It is human readable
4. JSON Example:

```json
{
  "name": "John",
  "employed": true,
  "age": 29,
  "salary": 100.50,
  "address": {
    "street": "Main Street",
	"apartment": 20
  },
  "friends": ["Michael", "Jessie"]
}
```

5. JSON Serializer Implementation
	1. We are going to implement a method that takes any object and serialize it into a JSON object
	2. We have no prior knowledge about the data objects we are going to serialize
		1. This is a perfect task for Java Reflection
6. Restricted Field Handling
	1. We have already been in a similar situation before
		1. Solution:
			1. `Field.setAccessible(true)`
			2. Grants Java Reflection access to restricted fields
	2. Exception: Classes that belong to a different Java Module that does not allow access to those classes
7. JSON - Example:

```json
{
  "name": "John",
  "employed": true,
  "age": 29,
  "salary": 100.50,
  "address": {
    "street": "Main Street",
	"apartment": 20
  },
  "friends": ["Michael", "Jessie"]
}
```

8. Code:

```json
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package jsonwriter;

import data.Address;
import data.Company;
import data.Person;

import java.lang.reflect.Field;


/**
 * Json Writer
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {
    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException {
        Address address = new Address("123 Main St", (short) 25);
        Company company = new Company("Google", "Seattle", address);
        Person person = new Person("John", true, 30, 100.555, address, company);
        String json = objectToJson(address, 0);
        System.out.println(json);
        json = objectToJson(person, 0);
        System.out.println(json);
    }

    public static String objectToJson(Object instance, int indentSize) throws IllegalArgumentException, IllegalAccessException {
        Field[] fields = instance.getClass().getDeclaredFields();
        StringBuilder jsonBuilder = new StringBuilder();

        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("{");
        jsonBuilder.append("\n");
        for (int i = 0; i < fields.length; i++) {
            Field field = fields[i];
            field.setAccessible(true);
            if (field.isSynthetic()) {
                continue;
            }
            jsonBuilder.append(indent(indentSize + 1));
            jsonBuilder.append(formatStringValue(field.getName()));
            jsonBuilder.append(":");
            if (field.getType().isPrimitive()) {
                jsonBuilder.append(formatPrimitiveValue(field, instance));
            } else if (field.getType().equals(String.class)) {
                jsonBuilder.append(formatStringValue(field.get(instance).toString()));
            } else {
                jsonBuilder.append("\n");
                jsonBuilder.append(objectToJson(field.get(instance), indentSize + 1));
            }

            if (i != fields.length - 1) {
                jsonBuilder.append(","); 
            }
            jsonBuilder.append("\n");
        }
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("}");
        return jsonBuilder.toString();
    }

    private static String indent(int indentSize) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < indentSize; i++) {
            stringBuilder.append("\t");
        }
        return stringBuilder.toString();
    }

    private static String formatPrimitiveValue(Field field, Object parentInstance) throws IllegalArgumentException, IllegalAccessException {
        if (field.getType().equals(boolean.class)
        || field.getType().equals(int.class)
        || field.getType().equals(long.class)
        || field.getType().equals(short.class)
        ) {
            return field.get(parentInstance).toString();
        } else if (field.getType().equals(double.class) || field.getType().equals(float.class)) {
            return String.format("%.02f", field.get(parentInstance));
        }

        throw new RuntimeException(String.format("Unsupported primitive type: %s", field.getType().getName()));
    }

    private static String formatStringValue(String value) {
        return String.format("\"%s\"", value);
    }
}
```

9. Summary:
	1. Implement an algorithm that converts a Java object into a Json string
	2. Thanks to Java Reflection, our implementation works on any object without knowing anything about its type ahead of time
	3. Using Java Reflection runtime type inspection feature, we were able to format fields based on their type
	4. Using recursion we ended up with an elegant solution that added support for objects that contain other objects

### Solution - Object Size Calculator ###

```java
import java.lang.reflect.*;

public class ObjectSizeCalculator {
    private static final long HEADER_SIZE = 12;
    private static final long REFERENCE_SIZE = 4;
    
    public long sizeOfObject(Object input) throws IllegalAccessException {
        /**
         * Complete your code here
         */
        long objectSize = HEADER_SIZE + REFERENCE_SIZE;
        Field[] fields = input.getClass().getDeclaredFields();
        for (int i = 0; i < fields.length; i++) {
            Field field = fields[i];
            field.setAccessible(true);
            if (field.isSynthetic()) {
                continue;
            }
            if (field.getType().isPrimitive()) {
                objectSize += sizeOfPrimitiveType(field.getType());
            } else if (field.getType().equals(String.class)) {
                objectSize += sizeOfString(field.get(input).toString());
            }
        }
        return objectSize;
    }
    
    
/*************** Helper methods ********************************/    
    private long sizeOfPrimitiveType(Class<?> primitiveType) {
        if (primitiveType.equals(int.class)) {
            return 4;
        } else if (primitiveType.equals(long.class)) {
            return 8;
        } else if (primitiveType.equals(float.class)) {
            return 4;
        } else if (primitiveType.equals(double.class)) {
            return 8;
        } else if (primitiveType.equals(byte.class)) {
            return 1;
        } else if (primitiveType.equals(short.class)) {
            return 2;
        }
        throw new IllegalArgumentException(String.format("Type: %s is not supported", primitiveType));
    }
    
    private long sizeOfString(String inputString) {
        int stringBytesSize = inputString.getBytes().length;
        return HEADER_SIZE + REFERENCE_SIZE + stringBytesSize;
    }
}
```

### Introduction to Arrays ###
1. What we will learn in this lecture
	1. Array inspection using Java Reflection API
	2. Reading values from arrays using Java Reflection
2. Identifying Arrays and Element Types
	1. Arrays are special classes
	2. We can get basic information about arrays using the `Class<?>` API (of any dimension)
	3. We can confirm that the object is an array using `Class.isArray()` **(M)** property
	4. We can use the `Class.getComponentType()` **(M)** to get the type of the array elements
	5. `Class.getComponentType()` returns null on non array Class objects
3. Example:

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package arrays;

import java.lang.reflect.Array;

/**
 * Introduction to Arrays
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {

    public static void inspectArrayObject(Object arrayObject) {
        Class<?> clazz = arrayObject.getClass();

        System.out.println("Is array: " + clazz.isArray());

        Class<?> arrayComponentType = clazz.getComponentType();

        System.out.println("Array component type: " + arrayComponentType);
    }

    public static void main(String[] args) {
        int[] oneDimensionalArray = {1, 2};
        double[][] twoDimensionalArray = {{1.0, 2.0}, {3.0, 4.0}};
        inspectArrayObject(oneDimensionalArray);
        inspectArrayObject(twoDimensionalArray);
    }
}
```

3. Reading values from arrays using Java Reflection
	1. `java.lang.reflect.Array` class
		1. Given an array object, we can use the Reflection to access the array object's runtime properties and data
		2. `Array` class contains static methods that help us get that data from an array object.
		3. Examples:
			1. `Array.getLength(Object arrayObject)` - get array's length
			2. `Array.get(Object arrayObject, int index)` - get element by index
4. Example:

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package arrays;

import java.lang.reflect.Array;

/**
 * Introduction to Arrays
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {

    public static void inspectArrayObject(Object arrayObject) {
        Class<?> clazz = arrayObject.getClass();

        System.out.println("Is array: " + clazz.isArray());

        Class<?> arrayComponentType = clazz.getComponentType();

        System.out.println("Array component type: " + arrayComponentType);
    }

    public static void inspectArrayValues(Object arrayObject) {
        int arrayLength = Array.getLength(arrayObject);
        System.out.print("[");
        for (int i = 0; i < arrayLength; i++) {
            Object arrayElement = Array.get(arrayObject, i);

            if (arrayElement.getClass().isArray()) {
                inspectArrayValues(arrayElement);
            } else {
                System.out.print(arrayElement);
            }
            
            if (i != arrayLength - 1) {
                System.out.print(", ");
            }
        }
        System.out.print("]");
    }

    public static void main(String[] args) {
        int[] oneDimensionalArray = {1, 2};
        double[][] twoDimensionalArray = {{1.0, 2.0}, {3.0, 4.0}};
        String[][][] threeDimensionalArray = {{{"a", "b"}, {"c", "d"}}, {{"e", "f"}, {"g", "h"}}};
        inspectArrayObject(oneDimensionalArray);
        inspectArrayObject(twoDimensionalArray);
        inspectArrayObject(threeDimensionalArray);

        inspectArrayValues(oneDimensionalArray);
        inspectArrayValues(twoDimensionalArray);
        inspectArrayValues(threeDimensionalArray);
    }
}
```

5. Summary:
	1. How to inspect array classes with Java Reflection
	2. How to get the element types of an array class of any dimension or type
	3. Array helper class which has many methods that allow us to get the runtime information about an array object using Java Reflection
	4. Using the Array class we were able to
		1. Get the array's length
		2. Read the individual elements of an array of any dimension

### Reading Arrays - JSON Serializer ###
1. What we will learn in this lecture
	1. Convert objects with arrays of primitive and String elements to JSON
	2. Convert objects with arrays of any type to JSON
2. Convert objects with arrays of primitive and String elements to JSON

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package jsonwriter;

import data.Actor;
import data.Address;
import data.Company;
import data.Movie;
import data.Person;

import java.lang.reflect.Array;
import java.lang.reflect.Field;


/**
 * Json Writer
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {
    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException {
        Address address = new Address("123 Main St", (short) 25);
        Company company = new Company("Google", "Seattle", address);
        Person person = new Person("John", true, 30, 100.555, address, company);
        String json = objectToJson(address, 0);
        System.out.println(json);
        json = objectToJson(person, 0);
        System.out.println(json);

        System.out.println("-----------------------");
        Actor actor = new Actor("Brad Pitt", new String[] {"Fight Club", "Seven"});
        json = objectToJson(actor, 0);
        System.out.println(json);

        System.out.println("-----------------------");
        Movie movie = new Movie("Fight Club", 8.8f, new String[] {"Action", "Thriller"});
        json = objectToJson(movie, 0);
        System.out.println(json);
    }

    public static String objectToJson(Object instance, int indentSize) throws IllegalArgumentException, IllegalAccessException {
        Field[] fields = instance.getClass().getDeclaredFields();
        StringBuilder jsonBuilder = new StringBuilder();

        jsonBuilder.append("{");
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("\n");
        for (int i = 0; i < fields.length; i++) {
            Field field = fields[i];
            field.setAccessible(true);
            if (field.isSynthetic()) {
                continue;
            }
            jsonBuilder.append(indent(indentSize + 1));
            jsonBuilder.append(formatStringValue(field.getName()));
            jsonBuilder.append(": ");
            if (field.getType().isPrimitive()) {
                jsonBuilder.append(formatPrimitiveValue(field.get(instance), field.getType()));
            } else if (field.getType().equals(String.class)) {
                jsonBuilder.append(formatStringValue(field.get(instance).toString()));
            } else if (field.getType().isArray()) {
                jsonBuilder.append(arrayToJson(field.get(instance), indentSize + 1));
            } else {
                jsonBuilder.append(objectToJson(field.get(instance), indentSize + 1));
            }

            if (i != fields.length - 1) {
                jsonBuilder.append(","); 
            }
            jsonBuilder.append("\n");
        }
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("}");
        return jsonBuilder.toString();
    }

    private static String arrayToJson(Object arrayInstance, int indentSize) throws IllegalArgumentException, IllegalAccessException {
        StringBuilder jsonBuilder = new StringBuilder();
        int arrayLength = Array.getLength(arrayInstance);
        Class<?> componentType = arrayInstance.getClass().getComponentType();
        jsonBuilder.append("[");
        jsonBuilder.append("\n");
        for (int i = 0; i < arrayLength; i++) {
            Object element = Array.get(arrayInstance, i);

            if (componentType.isPrimitive()) {
                jsonBuilder.append(indent(indentSize + 1));
                jsonBuilder.append(formatPrimitiveValue(element, componentType));
            } else if (componentType.equals(String.class)) {
                jsonBuilder.append(indent(indentSize + 1));
                jsonBuilder.append(formatStringValue(element.toString()));
            }
            if (i != arrayLength - 1) {
                jsonBuilder.append(",");
            }
            jsonBuilder.append("\n");
        }
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("]");
        return jsonBuilder.toString();
    }

    private static String indent(int indentSize) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < indentSize; i++) {
            stringBuilder.append("\t");
        }
        return stringBuilder.toString();
    }

    private static String formatPrimitiveValue(Object instance, Class<?> type) throws IllegalArgumentException, IllegalAccessException {
        if (type.equals(boolean.class)
        || type.equals(int.class)
        || type.equals(long.class)
        || type.equals(short.class)
        ) {
            return instance.toString();
        } else if (type.equals(double.class) || type.equals(float.class)) {
            return String.format("%.02f", instance);
        }

        throw new RuntimeException(String.format("Unsupported primitive type: %s", type.getName()));
    }

    private static String formatStringValue(String value) {
        return String.format("\"%s\"", value);
    }
}
```

3. Convert objects with arrays of any type to JSON

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package jsonwriter;

import data.Actor;
import data.Address;
import data.Company;
import data.Movie;
import data.Person;

import java.lang.reflect.Array;
import java.lang.reflect.Field;


/**
 * Json Writer
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {
    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException {
        Address address = new Address("123 Main St", (short) 25);
        Company company = new Company("Google", "Seattle", address);
        Person person = new Person("John", true, 30, 100.555, address, company);
        String json = objectToJson(address, 0);
        System.out.println(json);
        json = objectToJson(person, 0);
        System.out.println(json);

        System.out.println("-----------------------");
        Actor actor = new Actor("Brad Pitt", new String[] {"Fight Club", "Seven"});
        json = objectToJson(actor, 0);
        System.out.println(json);

        System.out.println("-----------------------");
        Actor actor1 = new Actor("Brad Pitt", new String[] {"Fight Club", "Seven"});
        Actor actor2 = new Actor("Edward Norton", new String[] {"Fight Club", "American History X"});
        Movie movie = new Movie("Fight Club", 8.8f, new String[] {"Action", "Thriller"}, new Actor[] {actor1, actor2});
        json = objectToJson(movie, 0);
        System.out.println(json);
    }

    public static String objectToJson(Object instance, int indentSize) throws IllegalArgumentException, IllegalAccessException {
        Field[] fields = instance.getClass().getDeclaredFields();
        StringBuilder jsonBuilder = new StringBuilder();

        jsonBuilder.append("{");
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("\n");
        for (int i = 0; i < fields.length; i++) {
            Field field = fields[i];
            field.setAccessible(true);
            if (field.isSynthetic()) {
                continue;
            }
            jsonBuilder.append(indent(indentSize + 1));
            jsonBuilder.append(formatStringValue(field.getName()));
            jsonBuilder.append(": ");
            if (field.getType().isPrimitive()) {
                jsonBuilder.append(formatPrimitiveValue(field.get(instance), field.getType()));
            } else if (field.getType().equals(String.class)) {
                jsonBuilder.append(formatStringValue(field.get(instance).toString()));
            } else if (field.getType().isArray()) {
                jsonBuilder.append(arrayToJson(field.get(instance), indentSize + 1));
            } else {
                jsonBuilder.append(objectToJson(field.get(instance), indentSize + 1));
            }

            if (i != fields.length - 1) {
                jsonBuilder.append(","); 
            }
            jsonBuilder.append("\n");
        }
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("}");
        return jsonBuilder.toString();
    }

    private static String arrayToJson(Object arrayInstance, int indentSize) throws IllegalArgumentException, IllegalAccessException {
        StringBuilder jsonBuilder = new StringBuilder();
        int arrayLength = Array.getLength(arrayInstance);
        Class<?> componentType = arrayInstance.getClass().getComponentType();
        jsonBuilder.append("[");
        jsonBuilder.append("\n");
        for (int i = 0; i < arrayLength; i++) {
            Object element = Array.get(arrayInstance, i);

            if (componentType.isPrimitive()) {
                jsonBuilder.append(indent(indentSize + 1));
                jsonBuilder.append(formatPrimitiveValue(element, componentType));
            } else if (componentType.equals(String.class)) {
                jsonBuilder.append(indent(indentSize + 1));
                jsonBuilder.append(formatStringValue(element.toString()));
            } else {
                jsonBuilder.append(objectToJson(element, indentSize + 1));
            }
            if (i != arrayLength - 1) {
                jsonBuilder.append(",");
            }
            jsonBuilder.append("\n");
        }
        jsonBuilder.append(indent(indentSize));
        jsonBuilder.append("]");
        return jsonBuilder.toString();
    }

    private static String indent(int indentSize) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < indentSize; i++) {
            stringBuilder.append("\t");
        }
        return stringBuilder.toString();
    }

    private static String formatPrimitiveValue(Object instance, Class<?> type) throws IllegalArgumentException, IllegalAccessException {
        if (type.equals(boolean.class)
        || type.equals(int.class)
        || type.equals(long.class)
        || type.equals(short.class)
        ) {
            return instance.toString();
        } else if (type.equals(double.class) || type.equals(float.class)) {
            return String.format("%.02f", instance);
        }

        throw new RuntimeException(String.format("Unsupported primitive type: %s", type.getName()));
    }

    private static String formatStringValue(String value) {
        return String.format("\"%s\"", value);
    }
}

```

```json
{
        "name": "Fight Club",
        "rating": 8.80,
        "categories": [
                "Action",
                "Thriller"
        ],
        "actors": [
{
                        "name": "Brad Pitt",
                        "knownForMovies": [
                                "Fight Club",
                                "Seven"
                        ]
                },
{
                        "name": "Edward Norton",
                        "knownForMovies": [
                                "Fight Club",
                                "American History X"
                        ]
                }
        ]
}
```

4. Summary:
	1. We applied our newly acquired knowledge of inspecting/reding array elements using Reflection in practice
	2. We implemented a practical real life algorithm, converting data objects to JSON strings
	3. Using recursion (method that calls itself), we traversed fields that contain objects or arrays of objects
	4. Without Java Reflection we wouldn't have been able to construct such a generic solution, which is perfect to be packaged as a library

### Coding Exercise 4: Reading Arrays ###

```java
import java.lang.reflect.*;
public class ArrayReader {
    
    public Object getArrayElement(Object array, int index) {
       if (index >= 0) {
           return Array.get(array, index);
       } else {
           return Array.get(array, Array.getLength(array) + index);
       }
    }
}
```

### Solution - Reading Arrays ###

## Section 4: Field Modification & Arrays Creation ##
### Setting Field Values - Generic Configuration File Parser ###
1. What we will learn in this lecture:
	1. Setting Field values
	2. Use cases for setting field values with Reflection
	3. Configuration File Parser
2. Setting Field values
	1. Code:
	
	```java
	public <T> void setFieldValue(T instance) {
	  Class<T> clazz = instance.getClass();
	  Field field = clazz.getDeclaredField("fieldName");
	  field.setAccessible(true); // if field is private
	  field.set(instance, value); // value must be of the right type
	}
	```
	
3. Use cases for setting field values with Reflection
	1. Field type is unknown ahead of time
	
	```
	public <T> void setFieldValue(T instance, String fieldName) {
	  // ...
	}
	```
	
		1. Works on ANY type T
	2. Object Deserializers
		1. Take data in a predefined protocol and translate into a Java Object representation (Plain Old Java Object)
		2. Example:
			1. Network Protocol Deserializers
				1. They read json objects coming from the network, persistence storage and convert them back into Java objects
			2. Object Relational Mapping Software
				1. Abstraction to read data from DBs without writing complicated queries.
					1. Converting rows of tables to objects
			3. Application Configuration File Parsers
				1. Text into objects
			4. There are more use cases for setting fields using Reflection
4. Configuration File Parser

```java
/*
 *  MIT License
 *
 *  Copyright (c) 2020 Michael Pogrebinsky - Java Reflection - Master Class
 *
 *  Permission is hereby granted, free of charge, to any person obtaining a copy
 *  of this software and associated documentation files (the "Software"), to deal
 *  in the Software without restriction, including without limitation the rights
 *  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 *  copies of the Software, and to permit persons to whom the Software is
 *  furnished to do so, subject to the following conditions:
 *
 *  The above copyright notice and this permission notice shall be included in all
 *  copies or substantial portions of the Software.
 *
 *  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 *  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 *  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 *  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 *  SOFTWARE.
 */

package configloader;

import java.io.IOException;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.nio.file.Path;
import java.util.Scanner;

import data.GameConfig;
import data.UserInterfaceConfig;

/**
 * Config Parser
 * https://www.udemy.com/course/java-reflection-master-class
 */
public class Main {

    private static final Path GAME_CONFIG_PATH = Path.of("resources/game-properties.cfg");
    private static final Path UI_CONFIG_PATH = Path.of("resources/user-interface.cfg");

    public static void main(String[] args) throws IllegalArgumentException, IllegalAccessException, InstantiationException, InvocationTargetException, NoSuchMethodException, IOException {
        GameConfig gameConfig = constructConfigObject(GameConfig.class, GAME_CONFIG_PATH);
        System.out.println(gameConfig);

        UserInterfaceConfig userInterfaceConfig = constructConfigObject(UserInterfaceConfig.class, UI_CONFIG_PATH);
        System.out.println(userInterfaceConfig);
    }

    @SuppressWarnings("resource")
    public static <T> T constructConfigObject(Class<T> clazz, Path filePath) throws IllegalArgumentException, IllegalAccessException, IOException, InstantiationException, InvocationTargetException, NoSuchMethodException {
        Scanner scanner = new Scanner(filePath);
        Constructor<?> constructor = clazz.getDeclaredConstructor();

        @SuppressWarnings("unchecked")
        T configInstance = (T) constructor.newInstance();

        while (scanner.hasNextLine()) {
            String configLine = scanner.nextLine();
            String[] nameValuePair = configLine.split("=");
            String propertyName = nameValuePair[0];
            String propertyValue = nameValuePair[1];

            Field field;
            try {
                field = clazz.getDeclaredField(propertyName);
            } catch (NoSuchFieldException e) {
                System.out.println("No such field: " + propertyName);
                continue;
            }
            field.setAccessible(true);
            Object parsedValue = parseValue(field.getType(), propertyValue);
            field.set(configInstance, parsedValue);
        }
        return configInstance;
    }

    private static Object parseValue(Class<?> type, String value) {
        if (type == int.class) {
            return Integer.parseInt(value);
        } else if (type == short.class) {
            return Short.parseShort(value);
        } else if (type == long.class) {
            return Long.parseLong(value);
        } else if (type == double.class) {
            return Double.parseDouble(value);
        } else if (type == float.class) {
            return Float.parseFloat(value);
        } else if (type == String.class) {
            return value;
        }
        throw new IllegalArgumentException("Unsupported field type: " + type);
    }
}
```

5. Setting Final Field Values
	1. Setting `final` fields using reflection is discouraged
		1. The results may be unexpected
		
		```
		private final int releaseYear = 2020; // retained even if set to 2021 in the config file
		```
		
			1. Compiler might just replace the variable with a constant (2000)
	2. `static final` field is a read-only field
		1. Cannot set value at runtime (even if it were initialized in a constructor)
6. Why didn't we use a constructor to set the values?
	1. The argument names are erased by the compiler (name mis-match)
7. Summary:
	1. Learned how to set Field values of an object using Reflection
	2. Learned about a family of use cases the Object Deserializers
		1. Object Deserializers convert data in formats optimized for human readability / size to Java objects optimal for our application
	3. Implemented a Configuration File Parser
	4. Talked about the issues of setting `final` object fields
	5. Constructor parameter name erasure in compile time

### Array Creation and Initialization ###
1. What we will learn in this lecture
	1. Array Creations using Reflection
	2. Setting Array values using Reflection
	3. Parsing arrays from Configuration File
2. Array Creations using Reflection
	1. We learned about the `java.lang.reflect.Array` helper class for reading arrays using Reflection
	2. We can use the `java.lang.reflect.Array` class to construct arrays of any type and dimension
	3. One Dimensional Array Creation
		1. `Array.newInstance(Class<?> componentType, int length)` **(M)**
			1. Construct a 1D array with elements of type componentType and length length
			
			```java
			Array.newInstance(int.class, 10); // new int [10];
			```
			
				1. It works for any type.
				2. The size and type are decided at runtime
			
3. Setting Array values using Reflection

```java
Array.set(Object arrayObject, int index, Object value);
```
	1. The passed value must be of the correct type, otherwise an exception will be thrown
	2. For compile time safety:
		1. `Array.setBoolean(Object arrayObject, int index, boolean value)`
		2. `Array.setInt(Object arrayObject, int index, int value)`
		3. `Array.setDouble(Object arrayObject, int index, int value)`
		4. `Array.setLong(Object arrayObject, int index, long vaue)`
		5. ...
4. Parsing arrays from configuration file
	1. 

### Coding Exercise 5: Smart Array Concatenation ###
### Solution - Smart Array Concatenation ###

## Section 5: Methods Discovery & Invocation ##
### Introduction to Methods - Discovery & Analysis ###
### Method Discovery by Name and Parameters ###
### Method Invocation - Polymorphism Use Case ###
### Coding Exercise 6: Simple Testing Framework ###
### Solution - Simple Testing Framework ###

## Section 6: Java Modifiers Discovery and Analysis ##
### Java Modifiers & Reflection ###
### Coding Exercise 7: Improved JSON Serializer ###
### Solution - Improved JSON Serializer ###

## Section 7: Annotations with Java Reflection ##
### Introduction to Annotations & Meta-Annotations ###
### Annotation Creation & Discovery. Automatic Class Loading ###
### Coding Exercise 8: Annotation Discovery ###
### Solution - Annotation Discovery ###
### Reading Annotation Objects & Annotation Elements ###
### Parameter Annotations & Graph Execution Example ###
### Field Annotations & Graph Execution ###
### Repeatable Annotations - Automatic Scheduling ###
### Coding Exercise 9: Security with Annotations - Part 1 ###
### Solution - Security with Annotations - Part 1 ###
### Coding Exercise 10: Security with Annotations - Part 2 ###
### Solution - Security with Annotations - Part 2 ###

## Section 8: Dynamic Proxies ##
### Introduction to the Proxy Design Pattern ###
### Dynamic Proxy Implementation ###
### Coding Exercise 11: Dynamic Caching Proxy Implementation ###
### Solution - Caching Dynamic Proxy Implementation ###

## Section 9: Final Section - Performance, Safety, and Best Practices ##
### Performance, Safety, and Best Practices ###

## Section 10: Bonus Material ##
### Bonus Lecture - Keep Learning ###