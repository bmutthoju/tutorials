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
	public class Main {
		public static void main(String[] args) {
		
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
				this.name = name;
				this.age = age;
				this.address = address;
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

### Restricted Constructor Access ###
### Restricted Classes Instantiation - Automatic Dependency Injection Implementation ###

## Section 3: Inspection of Fields & Arrays ##
### Introduction to Fields ###
### Reading Fields - JSON Serializer ###
### Solution - Object Size Calculator ###
### Introduction to Arrays ###
### Reading Arrays - JSON Serializer ###
### Coding Exercise 4: Reading Arrays ###
### Solution - Reading Arrays ###

## Section 4: Field Modification & Arrays Creation ##
### Setting Field Values - Generic Configuration File Parser ###
### Array Creation and Initialization ###
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