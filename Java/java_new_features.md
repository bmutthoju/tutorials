# Java New Features - Java 9, Java 10, Java 11, Java 12, Java 13, Java 14, Java 15 #
1. LTS
	1. Every 3 years - Java SE 8, Java SE 11, Java SE 17, Java SE 21
		1. Supported for a long time

## Java New Features ##
1. J2SE5.0
	1. Enhanced for loop, generics, enums, autoboxing
2. Java SE 8 (LTS)
	1. Functional programming - lambdas & streams, static methods in interface
3. Java SE 9 - Modularization (Java Platform Module System)
	1. Entire JDK is modularized
4. Java SE 10 - Local variable type inference
	1. Variable type declaration can get complex which is simplified using auto-inference
5. Java SE 14 - Switch expressions (Preview in 12 and 13)
6. Java SE 15 - Text blocks (Preview in 13)
	1. Multi-line with punctuation & 
7. Java SE 16 - Record classes (Preview in 14 and 15)
8. All Java Versions - API improvements, performance and garbage collection improvements

## Record Classes ##
1. Classes with:
	1. Fields
	2. Constructor
	3. toString()
	4. hashCode()
	5. equals()
	6. getters
2. Record classes makes the above easy

## New APIs in Java ##
1. New Project:
	1. name: java-new-api-features
	2. choose latest execution environments
	3. Uncheck: Create module-info.java
	4. New file:
		1. com.in28minutes.api.a.CopyOfApiRunner
		
				List<String> names = new ArrayList<>();
				names.add("Ranga");
				names.add("Ravi");
				names.add("John");
				
				// doNotChange(names); // can modify the original list
				doNotChange(List.copyOf(names));
				
				// List.of("Ranga", "Ravi", "John"); // Java 9
		
				// List.copyOf(); // returns an unmodifiable list of the given collection 
				
				// Set.copyOf();
				
				// Map.copyOf();
				
				...
				doNotChange(List<String> names) {
					names.add("ShouldNotBeAllowed");
				}
				
			1. If the original list, map or set are unmodifiable, then `List.copyOf` will return the original list, map or set respectively
	2. New Class:
		1. com.in28minutes.api.b.FileReadWriteRunner
		2. New file: resources/sample.txt
		
				Path path = Paths.get("./resources/sample.txt");
				String fileContent = Files.readString(path); // **(M)**
				System.out.println(fileContent);
				
				String newFileContent = fileContent.replace("Line", "Lines");
				
				Path newFilePath = Paths.get("./resources/sample-new.txt");
				Files.writeString(newFilePath, newFileContent); // **(M)**
				
			1. Uses UTF-8 as encoding by default
	3. New Class:
		1. com.in28minutes.api.b.PredicateNotRunner
		
				List<Integer> numbers = List.of(2, 5, 2, 6, 7);
				Predicate<Integer> evenNumberPredicate = number -> number % 2 == 0;
				number.stream().filter(evenNumberPredicate).forEach(System.out::println);
				
				// Not of even numbers
				
				number.stream().filter(evenNumberPredicate.negate()).forEach(System.out::println);
				
				// Another way
				
				public static boolean isEven(Integer number) {
					return number % 2 == 0;
				}
				...
				numbers.stream().filter(Predicate.not(PredicateNotRunner::isEven)).forEach(System.out::println); // since isEven.negate() cannot be used
				
	4. String Utility Methods:
		1. New class: StringNewApiRunner
		
				System.out.println("".isBlank()); // **(M)** - if string is empty or contains whitespace characters only
				
				System.out.println("".strip()); // **(M)**
				System.out.println(" LR   ".stripLeading()); // **(M)**
				System.out.println(" LR   ".stripTrailing()); // **(M)**
				"Line1\nLine2\nLine3".lines().forEach(System.out::println); // **(M)**
				
				System.out.println("UPPER".transform(s -> s.substring(2))); // **(M)**
				
				System.out.println("My name is %s. Age is %d".formatted("Ranga", 25)); // **(M)**
				
				String str = null;
				System.out.println(str.isBlank()); // Has additional details
				
				SampleClass sampleClass = new SampleClass();
				String str = sampleClass;
				System.out.println(sample.str.isBlank());
				
	5. Local variable type inference
		1. TypeInferencesRunner
		
				List<String> names1 = List.of("Ranga", "Ravi");
				List<String> names2 = List.of("John", "Adam");
				List<List<String>> names = List.of(names1, names2); // very complex
				
				var names = List.of(names1, names2); // new
				
				names.stream().forEach(System.out::println);
				
			1. Java compiler infers the type of the variable at compile time
			2. Introduced in Java 10
			3. `final` variables
			
					final var names = List.of(names1, names2); // If we don't want anyone to modify the variable
					
			4. Loops:
			
					for (var i = 1; i <= 10; i++) {
						System.out.println(i);
					}
					
					for (var name : names1) {
						System.out.println(name);
					}
					
			5. Notes:
				1. Cannot assign null to it
				2. Type inference is not applicable for Member variables
				3. Ensure variable names are good and expressive (to make it more readable)
				4. Have small scope for `var` variables
				5. For huge list of method calls:
				
						List.of("Ranga", "Ravi").stream().filter(s -> s.length() < 5).forEach(System.out::println);
						
						// can be broken down using var
						
						var stringsStream = List.of("Ranga", "Ravi").stream();
						var filteredStringsStream = stringsStream.filter(s -> s.length() < 5);
						filteredStringsStream.forEach(System.out::println);
						
	6. Switch Expression:
		1. Used for creation of expressions using switch statement
		2. Released in JDK 14
		3. Example:
		
				String monthName = switch (monthNumber) {
					case 1 -> {
						System.out.println("January");
						// yield statement is used in a Switch Expression
						// break.continue statements are unsed in a Switch statement
						yield "January"; // yield mandatory!
					}
					case 2 -> "February";
					case 3 -> "March";
					case 4 -> "April";
					default -> "Invalid Month";
				};
				
		4. Preview - JDK 12 and 13
		5. Examples:
		
				SwitchExpressionRunner:
				
				public static String findDayOfTheWeek(int day) {
					String dayOfWeek = "";
					switch(day) {
						case 0: dayOfWeek = "Sunday"; break;
						case 1: dayOfWeek = "Monday"; break;
						case 2: dayOfWeek = "Tuesday"; break;
						case 3: dayOfWeek = "Wednesday"; break;
						case 4: dayOfWeek = "Thursday"; break;
						case 5: dayOfWeek = "Friday"; break;
						default: throw new IllegalArgumentException("Invalid Option" + day);
					}
					return dayOfWeek;
				}
				
				public static String findDayOfTheWeekSwitchExpression(int day) {
					String dayOfWeek = switch(day) {
						case 0 -> {
							System.out.println("Do some complex logic");
							yield "Sunday"; // cannot use return
						} // ; is not required with braces
						case 1 -> "Monday";
						case 2 -> "Tuesday";
						case 3 -> "Wednesday";
						case 4 -> "Thursday";
						case 5 -> "Friday";
						default -> throw new IllegalArgumentException("Invalid Option" + day);
					};
				}
				
			1. There is no fall-through in switch expression
	7. Text Blocks:
		1. Example:
			
				System.out.println("\"First Line\"\nSecond Line\nThird Line");
				System.out.println("""
					"First Line"
					Second Line
					Third Line
				""");
				
			1. Note: After first """, there must be a \n
			2. Note: We can use " inside a text-block
			3. Note: Trailing whitespace after each line is stripped of
			4. Supports all string operations
			5. Note: Align closing """ with the left-most characters to avoid printing tabs before.
		2. Formatting:
		
				"""
				Line 1: %s
				Line 2: %s
				Line 3
				Line 4
				""".formatted("Some Value", "Some Other Value");
				
			1. We can use this technique to define templates
	8. Records:
		1. Classes with constructor, getters, toString, hashCode, equals, ...
			1. Records eliminate verbosity in defining Java beans
			2. You can define custom implementations for the methods if we need
		2. Example:
			1. RecordsRunner
			
					record Person (String name, String email, String phoneNumber) {
					}
					
					public static void main(String[] args) {
						Person person1 = new Person("Ranga", "ranga@in28minutes.com", "123-456-7890");
						System.out.println(person);
						Person person2 = new Person("Ranga", "ranga@in28minutes.com", "123-456-7890");
						Person person3 = new Person("Ranga1", "ranga@in28minutes.com", "123-456-7890");
						
						System.out.println(person1.equals(person2));
						// ...
						System.out.println(person.name());
					}
					
					// Custom constructor
					
					Person (String name, String email, String phoneNumber) {
						if (name == null) {
							throw IllegalArgumentException("Name is null");
						}
						this.name = name;
						this.email = email;
						this.phoneNumber = phoneNumber;
					}
					
					// Compact constructor
					Person {
						if (name == null)
							throw new IllegalArgumentException("name is null");
					}
				1. Remember:
					1. Compact constructors are allowed only in records.
					2. You can add static fields, static initializers, and static methods
						1. You cannot add instance variables and instance initializers
				2. Custom accessor methods:
				
						public String name() {
							System.out.println("Do Something");
							return name;
						}