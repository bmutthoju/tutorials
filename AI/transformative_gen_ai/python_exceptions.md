## Exception Handling in Python
1. If code fails to run
2. Types of errors
	1. Syntax errors
		1. Pattern is not followed
	2. Exceptions
		1. Even if syntax is correct
3. Built-in exceptions
	1. TypeError - data type mismatch
	2. NameError - If variable is not accessible (not in scope or not defined)
	3. IndexError - Index does not exist
	4. KeyError - Key does not exist in a dictionary
	5. ValueError - Invalid values (-ve value to sqrt function)
	6. AttributeError - Attribute doesn't exist in the data type
	7. IOError - IO operations on files can fail if not accessible
	8. ZeroDivisionError - Divide by 0
	9. ImportError - Importing non-available modules, etc.
	10. IndentationError - Syntax error - improper indentation
	11. EOFError - Reading even after reaching the EOF
	12. Examples:
	
	```
	# TypeError
	val = 'python'
	print(val+3)
	
	# NameError
	print(x)
	
	# IndexError 
	l = [1, 2, 3]
	print(l[5])
	
	# KeyError 
	d = {0: 1, 1: 2}
	print(d[2])
	
	# ValueError
	import math
	print(math.sqrt(-2))
	
	# AttributeError
	name = 43
	print(name.split(','))
	
	# IOError, FileNotFoundError
	with open('nonexistent_file.txt') as f:
	  text = f.read()
	  print(text)
	  
	# ZeroDivisionError
	print(5 / 0)
	
	# ImportError, ModuleNotFoundError
	import NoNameModule
	
	# IndentationError
	for i in range(10):
	print(i)
	```
	
4. Custom exceptions

```
number = 9
if number % 2 != 0:
  raise Exception(f'The number should be even, ({number})')
```

## AssertionError
1. Exception that asserts a condition and throws an error if the condition is not met
2. Uses `assert` keyword
3. Python globally disables assertions when we run it in optimized mode using `-O` and `-OO` command line options

```
number = 4
assert (number % 2 == 0), f'The number should be even. ({number})'
print(number)
```

## try and except
Can throw an exception
Handled in except block

```
def divide(x, y):
  return x / y

def calculate(a, b):
  default = 1
  try:
    result = divide(a, b)
    print('result', result)
  except ZeroDivisionError as z:
    print('You cannot divide by zero')
    print(z)
  except TypeError:
    print('Please pass only integers or floats')
  except:
    print('There was some error. Could not calculate.')
    result = default

calculate(5, 0)
calculate(3, 'a')
```