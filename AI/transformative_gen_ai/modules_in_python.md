# Modules in Python

Agenda:
	Intro to Programming with Python
		Introduction to Modules in Python
			Built-in Modules
			User Defined Modules
			
Python Modules
	Python files with a .py extension that contain Python code
	Can include functions, classes, and variables as in any Python code
	Organizes code into reusable blocks to improve readability and maintainability
	
	Python modules
		Built-in modules
			1. Pre-installed modules in Python that can be readily used
			2. Examples: math, random, os (to interface withe the OS), sys (to interface withe the OS), datetime, etc.
		User-defined modules
			1. Modules constructed by user to organize code into separate files
			2. Sorted with .py extension
			3. Can be imported and used in other Python scripts (without copying)
			
How to construct a module?
	1. Construct a new Python file and define functions, classes, or variables in it
	2. Save the file with a .py extension in the same directlry as other Python scripts
	3. In the main Python scripts, import the module using `import` statement
	
Example:

```python
# Contents of mymodule.py
def greet(name);
  print('Hello, ' + name)
  
def farewell(name):
  print('Goodbye, ' + name)
```

```python
# Main script
import mymodule

mymodule.greet('Alice')
mymodule.farewell('Bob')
```

Coding Session:

```
import math

math.sqrt(16)
```

```
math.factorial(4)
```

```
math.sin(math.pi)
math.cos(math.pi)
```

```
math.ceil(2.3)
math.floor(2.3)
```

```
math.exp(2)
math.log(math.e) # 1.0
```

```
import random

random.randint(1, 5) # inclusive

random.random() # float
```

```
random.choice([3, 4, 6, 10])
```

```
items = ['a', 'b', 'c', 'd', 'e']
random.shuffle(items)
print(items)
```

```
import datetime

datetime.datetime.now()
datetime.date.today()
```

```
date1 = datetime.date(2024, 3, 6)
date2 = datetime.date(2024, 3, 1)

difference = date1 - date2
difference.days
```

## User-defined modules

1. `math_calculator.py`

```
pi = 3.14
e = 2.71

# Define functions
def find_perimeter(radius):
  print('The perimeter of the circle is ', 2 * pi * radius)
```

2. Usage:

```
import math_calculator as mc

mc.pi
mc.e

mc.find_perimeter(2)
```