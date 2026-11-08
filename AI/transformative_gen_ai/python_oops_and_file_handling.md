## OOPs & File Handling Class
1. Prerequisites
2. Topics:
	1. Review: Scope of Variables
	2. Python OOP Concepts
	3. Custom Sort Functiosn in Python
	4. Exception Handling
	5. File Handling
	6. JSON Module in Python
	
## Scope of variables in Python
1. Scope: The region of the code where a variable can be accessed and modified
2. Importance: Proper scoping prevents unintended access or modification of variables
	1. Accidental modifications
3. Local Variables
	1. Declared within a function or a code block
		1. Accessible only inside the function or block
		
```
def example_function():
  local_var = 5
  print(local_var)
  
example_function()
print(local_var) # Error: NameError: name 'local var' is not defined
```

## Nonlocal variables
1. Variables defined in an outer function that are not in the global scope
2. Used in nested functions to modify the outer function's variable

```
def outer_function():
  nonlocal_var = 10
  
  def inner_function():
    nonlocal nonlocal_var
	nonlocal_var += 5
	
  inner_function()
  print(nonlocal_var)
  
outer_function()
```

## Global Variables
1. Variables declared outside any function or block
2. Accesible from any part of the code

```
global_var = 20
def example_function():
  print(global_var)
  
example_function()
print(global_var)
```

## Python OOP Concepts
1. What is OOP?
	1. Programming paradigm that uses objects to represent and manipulate data
	2. Focus on constructing reusable and modular code
	3. Different style from procedural programming (Top-down design)
2. Applications:
	1. Libraries define classes
3. Inheritance
4. OPP Concepts
	1. Benefits of OOP in Python
		1. Easier maintenance
			1. Class changes are reflected in the objects
		2. Code reusability
		3. Faster development
		4. Inheritance
		5. Encapsulation
		6. Polymorphism
		
```
class Dog:
  def bark(self):
    print('Woof!')
	
# Instantiating objects

my_dog = Dog()
my_dog.bark()
```

```
class Dog:

  # Define Constructor
  def __init__(self, name, age, wt):
    # Define attributes
    self.name = name
    self.age = age
    self.wt = wt

  # Define a Method
  def walk(self):
    print('I am walking: ' + self.name)

dog = Dog('Bob', 5, 10.0)
dog.walk()
print(dog.age)
print(dog.wt)

dog.ht = 6
print(dog.ht)

dog2 = Dog('Sharu', 20, 15)

def fun(dog: Dog):
  print(dog.name)
  dog.name = 'xyz'
  print(dog.name)

fun(dog)
print(dog.name)
```

```
list1 = []
list1.append(dog)
list1.append(dog2)

print(list1)
```

```
class Dog
  ...
  # Define Destructor
  def __del__(self):
    print('Deleting this object: ' + self.name)
	
del dog
print(dog) # Error
```

```
class Dog
  ...
  def __repr__(self):
    return 'name: ' + self.name + ' wt: ' + str(self.wt)
```

```
print(hasattr(employee1, 'salary')
print(getattr(employee1, 'salary')
print(setattr(employee1, 'salary', 7000)
```

### Inheritance
1. What is it?
	1. A mechanism that allow one class to inherit properties and methods from another class
	2. Used for code reusability and complexity
	
```
class Animal:
  def speak(self):
    pass

class Dog (Animal):
  def speak(self):
    print('Woof!')
```

2. Multiple inheritance

```
class Bird:
  def fly(self):
    print('I can fly!')
	
class Fish:
  def swim(self):
    print('I can swim!')
	
class FlyingFish (Bird, Fish):
  pass
```

```
class Book:
  def __init__(self, title, quantity, author, price):
    self.title = title 
    self.quantity = quantity
    self.author = author
    self.__price = price
    self.__discount = None

  def set_discount(self, discount):
    self.__discount = discount

  def get_price(self):
    if self.__discount:
      return self.__price * (1 - self.__discount)
    return self.__price

  def __repr__(self):
    return f'Book: {self.title}, Quantity: {self.quantity}, Author: {self.author}, Price: {self.__price}'

class Novel (Book):
  def __init__(self, title, quantity, author, price, pages):
    super().__init__(title, quantity, author, price)
    self.pages = pages

class Academic (Book):
  def __init__(self, title, quantity, author, price, branch):
    super().__init__(title, quantity, author, price)
```

## Encapsulation
1. Bundling data and methods to operate on the data

```python
class Car:
  wheels = 4 # Public attribute
  _color = "red" # Protected attribute
  __engine = "v8" # Private attribute
```

```python
# Public
class MyClass:
  def __init__(self):
    self.public_attribute = 42

  def public_method(self):
    return "This is a public method"

  def _protected_method(self):
    return "This is a protected method"

  def __private_method(self):
    return "This is a private method"

obj = MyClass()
print(obj.public_attribute)
print(obj.public_method())
print(obj._protected_method())
print(obj.__private_method())
```

## Polymorphism
1. Ability of different classes to share the same interface and be treated as objects of a common superclass 
2. Benefits:
	1. Flexibility of code
	2. Easier maintenance
	
```python
class Animal:
  def speak(self):
    print("Generic animal sound")
class Dog(Animal):
  def speak(self):
    print("Woof!")
```

```python
import math

class Shape:
  def area(self):
    pass

class Circle(Shape):
  def __init__(self, radius):
    self.radius = radius

  def area(self):
    return math.pi * (self.radius ** 2)

class Rectangle(Shape):
  def __init__(self, width, height):
    self.width = width
    self.height = height

  def area(self):
    return self.width * self.height

def calculate_area(shape):
  return shape.area()

# Instances of Circle and Rectangle
my_circle = Circle(2.4)
my_rectangle = Rectangle(1.3, 6.8)

# Calculate and print areas using polymorphism
print(f'Circle Area {calculate_area(my_circle)}')
print(f'Rectangle Area {calculate_area(my_rectangle)}')
```

## Custom Sort Funtions in Python
1. `sorted()` **(M)**
	1. List from iterable
2. `sort()` **(M)**
	1. Modifies the list in-place and returns `None`
3. `key` **(M)**: Function to be called on each list element to determine the sorting order
4. `reverse` **(M)**: If set to `True`, the list is sorted in descending order

```python
numbers = [4, 2, 9, 1, 5]
sorted(numbers)
```

```python
numbers = [4, 2, 9, 1, 5]
print(sorted(numbers))
numbers.sort()
print(numbers)

words = ['apple', 'banana', 'cherry', 'date', 'fig']
print(sorted(words, key=len, reverse=True))
print(sorted(words, key=lambda x: x[1]))
print(sorted(words, key=lambda x: x[-1]))
print(sorted(words, key=lambda x: x[0:1]))
print(sorted(words, key=lambda x: {x[1], x[0]}))

class Employee:
  def __init__(self, name, dept, age):
    self.name = name
    self.dept = dept
    self.age = age

  def __repr__(self):
    return '{' + self.name + ', ' + self.dept + ', ' + str(self.age) + '}'

employees = [
    Employee('John', 'IT', 20),
    Employee('Sam', 'Banking', 20),
    Employee('Joe', 'Finance', 25)
]

print(employees)
print(sorted(employees, key = lambda x: x.name))
print(sorted(employees, key = lambda x: {x.name, x.dept}))
```

## Exception Handling
1. Events that occur during the execution of a program
2. Common Exceptions
	1. `SyntaxError`
	2. `TypeError`
	3. `ValueError`
	4. `FileNotFoundError`
	
```python
try:
  # code that may cause exception
except:
  # code to run when exception occurs
```

```
try:
# Some Code ...
except:
# optional block
# Handling of exception (if required)
else:
# execute if no exception
finally:
# always executed
```

```
# SyntaxError
print('Hello world'

# TypError
result = "5" + 3

# ValueError
number_str = 'abc'

# ValueError
number_str = 'abc'
print(int(number_str))

# FileNotFoundError
file_path = 'non_existent_file.txt'
with open(file_path, 'r') as file:
  content = file.read()
  
# ZeroDivisionError
a = 5
b = 0

print(a / b)
```

```
# Handling
a = 5
b = 0

try:
  print(a / b)
except:
  print('Cannot divide by zero')
  
print('Completed')
```

```
try:
  x = x + 'abc'
except Exception as ex:
  print('Error: Something went wrong')
  print(ex)

print('This line is printed')
```

```
# using raise
def divide(a, b):
  if b == 0:
    raise ValueError('Cannot divide by zero')
  return a / b

try:
  result = divide(10, 0)
except Exception as e:
  print(e)
```

```
# Catching Specific Exceptions in Python
try:
  even_numbers = [2, 4, 6, 8]
  print(even_numbers[5])
  x = 5 / 0
  print(x)
except ZeroDivisionError as e:
  print('Denominator cannot be zero:', e)
except IndexError as e:
  print('Index out of bounds:', e)
```

```
# use else after except
try:
  num = int(input('Enter a number'))
  assert num % 2 == 0
except:
  print('Not an even number')
else:
  reciprocal = 1 / num
  print(reciprocal)
```

```
# Python try...finally
try:
  numerator = 10
  denominator = 0

  result = numberator / Denominator

  print(result)

except:
  print('Error: Denominator cannot be 0')

finally:
  print('This is finally block')
```

---

Custom Exceptions
	Two ways to handle
		
	```
	except:
	  print('Handled the error')
	```

```
super().some_method()
```
	
```
class GrandChild(Parent, Grandparent):
  def grand_child_method(self):
    print('Method is child")
```

	Methods are inherited in the order from left to right
	
File Handling:
	The process of reading from or writing to a file
	Reading/writing data from external sources, and generating reports
	
Different modes
	r - open a file for reading
	w - ope na file for writing
		Overwrites
	x - Exclusive creation
		If file exists, the operation fails
			No overwrite allowed
	a - Open a file for appedning at the end of the file without truncating it
		A new file is created if it does not exist
	
```
file = open('example.txt', 'w')
file.write('Assalamu Alaikum')
file.close()
```
	
```
file = open('example.txt', 'r')
content = file.read()
print(content)
file.close()
```

Auto open and close:

```
with open('test1.txt', 'r') as file:
  content = file.read()
  print(content)
```

Line-by-line:

```
with open('test1.txt', 'r') as file:
  cur_line = file.readline()
  print(cur_line)
```

	1. Pointer points to the next line, now
	
```
with open('example.txt', 'r') as file:
  while True:
    cur_line = file.readline()
	if cur_line:
	  # Some operations here
	  print(cur_line)
	else:
	  break
```

```
with open('example.txt', 'r') as file:
  lines = file.readlines()
  print(lines)
```

Indexing and pointers:

```
with open('example.txt', 'r') as file:
  # Move to 11th character
  file.seek(11)

  # find the position fo the current character
  position = file.tell()

  print(file.read())
  print(position)
```

Writing:

```
with open('example2.txt', 'w') as file:
  file.write('Alhamdulillah!')
  file.write('Masha ALLAH')
```

Writing multiple lines

```
with open('exmaple3.txt', 'w') as file:
  lines = ["This is line 1", "This is line 2", "This is line 3"]
  file.writelines(lines)
```

```
with open('example.txt', 'x') as file:
  file.write('Trying')
```

```
with open('example4.txt', 'a') as file:
  file.write('Insha ALLAH')
```

Exercise:

```
lines = ["This is line 1", "This is line 2", "This is line 3"]

for i in range(len(lines)):
  lines[i] = lines[i] + '\n'

with open('myfile.txt', 'w') as file:
  file.writelines(lines)

line = 'Yes! Python is great!'
with open('myfile.txt', 'a') as file:
  file.write(line)

with open('myfile.txt', 'r') as file:
  content = file.read()
  print(content)

indices = []
lines = []
with open('myfile.txt', 'r') as file:
  lines = file.readlines()

for i in range(len(lines)):
  try:
    index = lines[i].index('Python')
    indices.append(index)
  except:
    print('Not found')

print(indices)
```

JSON Module in Python:
	JavaScript Object Notation (JSON)
	
	Human-readable
	Lightweight
	Easy to parse and generate (Python dictionary)
	Language-independent
	Supports various data types
		Keys are immutable
		
`json.dump()` - Serialize Python object to a JSON-formatted file
`json.dumps()` - Serialize Python object to a JSON-formatted string
`json.load()` - Deserialize JSON data from a file into a Python object
`json.loads()` - Deserialize JSON data from a string into a Python object

```
import json

person = {
  "name": "John",
  "age": 30,
  "city": "New York",
  "hasChildren": False,
  "titles": ["engineer", "programmer"]
}

# Convert into JSON
person_json = json.dumps(person)
print(type(person_json))
print(person_json)
```

Options:

```
person_json2 = json.dumps(person, indent=4, seperators={"; ", "= "}, sort_keys=True)
print(person_json2)
```

```
{
    "age"= 30; 
    "city"= "New York"; 
    "hasChildren"= false; 
    "name"= "John"; 
    "titles"= [
        "engineer"; 
        "programmer"
    ]
}
```

Deserialization:

```
person_json = """
{
    "name": "John",
    "age": 30,
    "city": "New York",
    "hasChildren": false,
    "titles": [
        "engineer",
        "programmer"
    ]
}
"""

person = json.loads(person_json)
print(person)

print(person['age'])
print(person['titles'])
```

Built-in methods:

```
dict = laptop.__dict__
```