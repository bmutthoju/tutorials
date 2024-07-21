## Command ##
### Intent ###
1. **Command** is behavioral design pattern
2. It turns a request into stand-alone object
	1. The object contains all the info about the request
3. Benefits
	1. Lets us pass requests as method arguments
	2. Lets us delay or queue a request's execution
	3. Lets us support undoable operations

### Problem ###
1. Example: Text editor app
	1. A toolbar with buttons for operations of the editor
		1. `Button` class can be used for buttons on toolbar & for other buttons in dialogs
			1. The buttons look similar but do different things
				1. Where to put the click handlers?
					1. Simple solution: Subclasses for each place a button is used
						1. Each subclass contains code that will be executed on button click
			2. Example:

					Button
						OKButton
						CancelButton
						ApplyButton
						SaveButton
						OpenButton
						PrintButton
			3. Flaws
				1. Enormous number of subclasses
					1. Each time we modify the based class `Button`, we might break the sub-classes
				2. GUI code has become dependent on the business logic

						SaveButton
							Code

						SaveMenuItem
							Code

						SaveShortcut
							Code

				3. Some operations (copying and pasting text say) need to be invoked from multiple places
					1. "Copy" button is clicked on toolbar OR copy via context menu OR `ctrl+c` on keyboard
						1. For toolbar having code in `CopyButton` was fine
							1. However, if we implement context menus, shortcuts, and other stuff, we have to duplicate the operation's code in many classes OR make menu dependent on buttons (worse) 

### Solution ###
1. Good software design is based on **separation of concerns**
	1. Can be achieved by breaking an app into layers
		1. Example:
			1. GUI layer
				1. Responsible for rendering a beautiful picture on the screen
					1. It captures input
					2. It shows results of what user and app are doing
			2. Business logic layer
				1. For important work like calculating trajectory of moon or composing annual report, GUI delegates work to underlying business logic
		2. GUI might send requests to business logic
			1. Command pattern:
				1. GUI objects shouldn't send requests directly
					1. Extract all request details (object called, name of method, list of arguments) into separate *command* class with a single method to trigger the request
				2. Command objects serve as links between GUI and business logic objects
					1. GUI object doesn't need to know what business logic obect will receive request & how it will be processed
						1. GUI triggers command that handles all details
		3. Request: Commands must implement the same interface
			1. It has single execution method that takes no params
				1. Interface: It lets us send different commands with same request sender without coupling the request sender to concrete classes of commands
					1. **Allows us to switch command objects linked to sender**
						1. This changes sender's behavior at runtime
		4. Request parameters:
			1. How to pass parameters if execution method doesn't take arguments?
				1. Command should be pre-configured with the request params OR
				2. Command should get parameters on its own
		5. Example:

				Button -> <<interface>> <- Shortcut
							Command
							+ execute()
								^
								|
						+-------+-------+
						|		|		|
					Save		Open	Print
					Command		Command	Command
					  Code		  Code	  Code

			1. A single field in `Button` class can store reference to command object
				1. `Button` executes the command on click
			2. A command class is created for each operation
				1. Each command class is linked to button based on button's intended behavior
					1. Other GUI elements can be implemented the same way
				2. Elements related to the same operations will be linked to the same commands preventing code duplications

### Structure ###


### Pseudocode ###
### Applicability ###
### How to Implement ###
### Pros and Cons ###
### Relations with Other Patterns ###
### Java ###