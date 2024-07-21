# Bridge #
## Intent ##
1. A structural design pattern that lets us split a large class or a set of closely related classes into two separate hierarchies
	1. Abstraction
	2. Implementation
2. Both can be implemented independently of each other

## Problem ##
1. Example:
	1. Consider `Shape` class with subclasses `Circle`, and `Square`
	2. To extend the class hierarchy to incorporate colors, we can have
		1. `Red` and `Blue` shape subclasses
			1. This requires constructing four class combinations such as `BlueCircle` and `RedSquare`

					Shape
						RedCircle
						RedSquare
						BlueCircle
						BlueSquare

				1. The combinations will make the hierarchy grow exponentially
					1. Adding one more color would require creation of one more class for each shape

## Solution ##
1. **The problem is because we are trying to extend shape classes in two independent dimensions**
	1. Form
	2. Color
2. Bridge pattern attempts to solve the problem by switching from inheritance to object composition
	1. **Extract one of the dimensions into a separate class hierarchy**
		1. The original class can reference an object of the new hierarchy
			1. We don't have to have all state and behavior in one class

					Shape <>------> Color
						Circle			Red
						Square			Blue

				1. Color-related code can be extracted into its own class with two sub-classes
					1. `Red`
					2. `Blue`
				2. `Shape` class gets a reference field pointing to one of the color objects
					1. It can delegate color-related work to linked color object
						1. **The reference will act as bridge between Shape and Color classes**
							1. Adding new colors doesn't require changing shape hierarchy and vice versa

### Abstraction and Implementation ###
1. Abstraction (interface) is high-level control layer for some entity
	1. The layer isn't supposed to do any real work on its own
		1. It must delegate work to implementation layer (platform)
	2. Abstraction is not related to interfaces and abstract classes
		1. Examples:
			1. GUI: Abstraction
			2. OS Code (API): Implementation
				1. Called by GUI layer in response to user interactions
			3. We can extend an app in two independent dimensions
				1. We can have several different GUIs (tailored for regular customers or admins)
				2. Support different APIs (example, Windows, Linux, and MacOS)
	3. Implementation:
		1. Abstraction: the GUI layer of the app
			1. Demo 1.0, 1.1, 2.0, 3.0
		2. Implementation: the OS APIs
			1. MacOS APIs
			2. Windows APIs
			3. Linux APIs
	4. We can change the GUI classes without touching the API classes
		1. Adding support to another OS requires adding subclasses to the implementation hierarchy

## Structure ##

		Client (abstraction.feature1())
			|
			v
		Abstraction
			-i: Implementation <>---> Implementation <<interface>>
			+ feature1()				+ method1()
			+ feature2()				+ method2()
										+ method3()
				^							^
			   /_\						   /_\
				|							|
			Refined						Concrete
			Abstraction					Implementations
				+ featureN()
					i.methodN()
					i.methodM()
	
		1. Abstraction: Provides high-level control
			1. It relies on implementation object to do the actual low-level work
		2. Implementation: Declares interface that's common for all concrete implementations
			1. Abstraction can only communicate with an implementation object via methods declared here
			2. Abstraction may list same methods as implementation, but abstractions usually declare complex behaviors that rely on primitive operations declared in the implementation
		3. Concrete Implementations: Contain platform-specific code
		4. Refined Abstractions: Variants of control logic
			1. They work with different implementations like their parent
		5. Client: Only works with abstraction
			1. It is client's job to link the abstraction to one of the implementations

## Pseudocode ##

		Client -- remote.togglePower()
			|
			v
		Remote <>-------------------> Device <<interface>>
			- device: Device			+ isEnabled()
			+ togglePower()				+ enable()
			+ volumeDown()				+ disable()
			+ volumeUp()				+ getVolume()
			+ channelDown()				+ setVolume(percent)
			+ channelUp()				+ getChannel()
										+ setChannel()

			^							^
		   /_\						   /_\
			|							|
		AdvancedRemote				+---+---+
			+ mute()				|		|
								Radio		TV


	1. `togglePower()`

			if (device.isEnabled())
				device.disable()
			else
				device.enable()

	2. `channelUp()`

			old = device.getChannel()
			device.setChannel(old + 1)

	3. `mute()`

			device.setVolume(0)

## Applicability ##
1. If we want to divide a class that has several variants of some functionality
	1. Example: Class can work with various DB servers
2. Bridge patterns lets us split monolithic class into several class hierarchies
	1. We can change classes in each hierarchy independently of classes in the others
3. Advantages:
	1. Simplifies code maintenance
	2. Minimizes risk of breaking existing code
4. **Use the pattern when we need to extend a class in several orthogonal (independent) dimensions**
	1. Extract a separate class hierarchy in each dimensions
		1. Original class delegates related work to objects belonging to the hierarchies instead of doing everything on its own
5. **Use bridge if we need to be able to switch implementations at runtime**

## How to Implement ##
1. Identify the orthogonal dimensions in the classes
	1. abstraction/platform
	2. domain/infrastructure
	3. front-end/back-end
	4. interface/implementation
2. See what operations client needs and define them in base abstraction class
3. Determine the operations available on all platforms
	1. Declare the ones that the abstraction needs in the general implementation interface
4. For all platforms in domain construct concrete implementation classes
	1. Ensure that they follow the implementation interface
5. Inside abstraction class, add a reference field for the implementation type
	1. Abstraction delegates most of the work to implementation object that's referenced in that field
6. If we have several variants of high-level logic, construct refined abstractions for each variant by extending base abstraction class
7. Client code should pass implementation object to abstraction's constructor to associate one with the other
	1. After that client can forget about the implementation and work only with abstraction object

## Pros and Cons ##
1. Pros:
	1. We can construct platform independent classes and apps
	2. Client code works with high-level abstractions
		1. It is not exposed to platform details
	3. Open/Closed Principle
		1. We can introduct new abstractions and implementations independently for each other
	4. Single Responsibility Principle
		1. We can focus on high-level logic in the abstraction and on platfor details in the implementation
2. Cons:
	1. We might make code more complicated by applying pattern to a highly cohesive class

## Relations with Other Patterns ##
1. Bridge is usually designed upfront
	1. It lets us develop parts of the application independently of each other
	2. Adapter:
		1. It is commonly used in existing apps to make some otherwise-incompatible classes work together nicely
2. Bridge, state, strategy, Adapter:
	1. They have similar structures
		1. All of them are based on composition
			1. Composition: Delegating work to other objects
		2. **They solve different problems**
			1. Pattern is not a recipe to structure code in a specific way
				1. **It communicates developers the problem the pattern solves**
3. We can use Abstract Factory along with Bridge
	1. When to use?
		1. **If some abstractions defined by Bridge only work with specific implementations**
			1. **Abstract Factory can encapsulate the relationships and hide the complexity from client code**
4. We can combine Builder and Bridge
	1. Director class plays the role of the abstraction
		1. Director:
			1. Defines the order in which to execute building steps
			2. We can put in construction routines to re-use the recipe across programs
		2. Builder:
			1. Provides implementation of the steps
	2. Different builders can act as implementations
5. Abstract Factories, Builders, and Prototypes can all be implemented as Singletons