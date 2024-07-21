# Flyweight #
## Intent ##
1. Structural design pattern
2. Purpose
	1. To fit more objects into available RAM by sharing common parts of state between multiple objects (avoids keeping all the data in each object)

## Problem ##
1. Game:

		Game
			+ particles: Particle[]
			+ addParticle(particle)
			+ draw(canvas)

		foreach (p in particles)
			p.draw(canvas)

		+ fireAt(target: Unit)
			p = new Particle()
			p.coords = coords
			p.vector = target.coords
			p.speed = weaponPower
			p.color = "red"
			p.sprite = load("bullet.jpeg")
			Game.addParticle(p)

		Particle
			+ coords
			+ vector
			+ speed
			+ color
			+ sprite
			+ move()
			+ draw(canvas)

## Solution ##
1. color & sprite fields consume a lot of memory than other fields
	1. All bullets have the same color and sprite
	2. State (coordinates, movement vector, and speed) are unique to each particle
		1. They change over time
2. Intrinsic state: constant data
	1. It lives within the object
		1. Other objects can only read it and not change it
3. Extrinsic state: Rest of the object's state
	1. Can be altered from the outside by other objects
	2. **Stop storing extrinsic state inside the object**
		1. **Pass the state to specific methods which rely on it**
4. Design:

		Game
			+ mps: MovingParticle[]
			+ particles: Particle[]
			+ addParticle(coords, vector, speed, color, sprite)
			+ draw(canvas)

		< >
		 |
		 v
		Particle
			- color
			- sprite
			+ Particle(color, sprite)
			+ move(coords, vector, speed)
			+ draw(coords, canvas)

			^
			|
		MovingParticle
			- particle
			- coords
			- vector
			- speed
			+ MovingParticle(...)
			+ move()
			+ draw(canvas)

	1. **The object that only stores the intrinsic state is called a flyweight**

### Extrinsic State Storage ###
1. Stored in a container object in most cases
	1. Container object aggregates objects
		1. Example: `Game` object stores all `Particle` (represents the type of object - flyweight) references and `MovingParticle`s (represents the dynamic information about the object)
	2. How are the arrays populated?

			Go over the particles array and try to find an existing particle with the given color and sprite. If ther's none then construct a new one

			Construct a moving particle with given data and the particle object from the first step
f
### Flyweight and Immutability ###
1. A flyweight should initialize its state only once
	1. It should not have any setters or public fields of other objects

### Flyweight Factory ###
1. Factory can manage a pool of flyweight objects
	1. A method accepts intrinsic state of the desired flyweight from a client, looks for an existing flyweight object matching the state, and returns it if it is found
		1. If not, it constructs a new flyweight and adds it to the pool

## Structure ##
## Pseudocode ##
1. Consider rendering millions of `Tree` objects on a canvas

		TreeFactory
			- treeTypes: TreeType[]
			- getTreeType(name, color, texture)

		TreeType
			- name
			- color
			- texture
			+ TreeType(name, color, texture)
			+ draw(canvas, x, y)

		Forest
			+ trees: Tree[]
			+ plantTree(x, y, name, color, texture): Tree
			+ draw(canvas)

		Tree
			+ x
			+ y
			+ type: TreeType
			+ draw(convas)

	1. `TreeType` is the flyweight class
	2. `Tree` objects are contexts
		1. Flyweights are linked to contexts
	3. Factory encapsulates the complexity of searching for the right object and re-using it

## Applicability ##
1. Use only if program must support a huge number of objects which barely fit into available RAM
2. It is most useful when
	1. An application needs to spawn a huge number of similar objects
		1. Drains available RAM on target device
	2. Objects contain duplicate states which can be extracted and shared between multiple objects

## How to Implement ##
1. Divide fields of a class (that will become flyweight) into two parts
	1. Intrinsic state: Fields that contain unchanging data duplicated across many objects
	2. Extrinsic state: Fields that contain contextual data unique to each object
2. Leave the fields that represent intrinsic state in the class
	1. Ensure they're immutable
		1. They should take their initial values only inside the constructor
3. Go over methods that use fields of extrinsic state
	1. For each field used in the method, introduce a new parameter and use it instead of the field
4. Optional:
	1. Construct a factory class to manage pool of flyweights
		1. It should check for an existing flyweight before constructing a new one
		2. Clients must request flyweights only through the factory
		3. Clients must describe desired flyweight by passing its intrinsic state to factory
5. Client must store or calculate the values of extrinsic state (context) to be able to call methods of flyweight objects
	1. Extrinsic state along with flyweight-referencing field may be moved to separate context class

## Pros and Cons ##
1. Pros:
	1. Saves lots of RAM
		1. If program has tons of similar objects
2. Cons:
	1. Trading RAM over CPU cycles
		1. Especially if some of the context data needs to be recalculated each time somebody calls flyweight method
	2. Code becomes more complicated
		1. New team members might wonder why the state of an object is separated.

## Relations with Other Patterns ##
