1. Use interfaces more
2. API design - part of LLD
3. In OOP, everything revolves around entities
	1. Entity:
		1. Anything that has some info / attributes and can take some behavior
		2. Example:
			1. Student
			2. Instructor
			3. Class
			4. Mentor
			5. ...
			6. Problem
				1. Name
				2. Description
				3. List<SampleInput>
				4. List<SampleOutput>
				5. Score
			7. Admin
			8. VideoPlayer
			9. Assignment
				1. List<Problem>
		3. If we can say an entity can do something
		4. Definition:
			1. Any element in the visualization of a software system that has some attributes OR causes some behavior
				1. An entity can have only attributes
	2. Class:
		1. Blueprint of an entity
		2. Example: Blueprint of all students
			1. Student
				1. Attributes:
					1. Name
					2. Batch
					3. ID
					4. Age
					5. Email
				6. Behaviour
					1. PauseCourse
					2. Login
					3. AttendClass
	3. Object
		1. Real instance of a class
		2. They take up memory
	4. Attributes/Fields/Properties
		1. Data members in a class
	5. Methods/Behaviors
		1. Member functions in a class
		2. Constructor
4. Entity (think, concept) -> Class (realization) -> Object (real-world)
	1. Most of the time, an entity exists in the database
		1. ER diagrams
5. Java: https://adoptium.net/en-GB/
6. Google Java Style Guide: https://google.github.io/styleguide/javaguide.html
7. Two ways to identify entities
	1. Visualization
	2. Nouns
8. If a class has only behavior but no attributes, it becomes an interface
9. Anything that has individual existance is an entity
	1. State: Value of all the attributes of an object at a particular time
		1. Example: [name: null, age: 0, ...]
		2. Example: [name: "Alok", ...]
		3. Default state: All the default values of the data types