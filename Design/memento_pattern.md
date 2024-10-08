# Memento #
## Intent ##
1. **Memento**: Lets us save and restore previous state of an object without revealing the details of its implementation

## Problem ##
1. Example: Consider a text editor app
	1. Editor can:
		1. Format text
		2. Insert line images
		3. ...
	2. We can allow users to undo any operations carried out on text
	3. Direct approach
		1. Before performing any operation, the app records the state of all objects and saves it is some storage
		2. When user decides to revert an action, app fetches latest snapshot from history and uses it to restore sate of all objects

				Command -> Save -> Editor
							|			^
							v			|
							History - Undo

		3. Questions about snapshots
			1. How to produce one?
				1. We might have to go over all the fields in an object and copy their vales into storage
					1. **Only works if object has relaxed access restrictions to its contents**
						1. Most real objects do not allow anyone to peek inside them
							1. Significant data is hidden inside private fields
				2. If we keep all fields public
					1. Problems:
						1. We might refactor some of the classes or add or remove fields
							1. **This would require us to change classes responsible for copying state of affected objects**
						2. What data does a snapshot contain?
							1. Containers which contain the fields might be objects of one class
								1. The class may not have any methods but a lot of fields
							2. Containers might be in a list that represents history
							3. The above would expose all the fields (both private and public)

## Solution ##
## Structure ##
## Pseudocode ##
## Applicability ##
## How to Implement ##
## Pros and Cons ##
## Relations with Other Patterns ##
## Code Examples ##
