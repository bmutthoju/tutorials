## Scope of variables

Local, Global

non-local

local: defined inside function
Global: Script-level scope, main body of the program

`global` is required to modify a global variable inside a function (otherwise, it cannot be modified)

function inside a function:

scope of outer function can be made non-local to inner function

Call by value & call by reference

call by value: Immutable objects
	1. A copy is passed to a function
call by reference: Mutable objects
	1. A reference of the original object is passed
		1. Change is permanent
		2. List, object, Set, ...
		
```
def my_function():
  x = 5 # local variable
  print(x)

x = 4 # global variable
print(x)
my_function()
print(x)
```

```
def my_function():
  z = 5
  print(z + y)

y = 4
my_function()
print(y)
```

```
def f():
  global s 
  print(s)
  s = "CD" # global variable
  print(s)

s = "AB" # global variable
print(s)
f()
print(s)
```

```
s1 = "Maria"

def f():
  s3 = "Nicole"
  print(s1)
  print(s2)
  print(s3)

s2 = "Adam"
f()
```

```
def modify_dict(dict):
  dict['key3'] ='value3'

original_dict = {'key1': 'value1', 'key2': 'value2'}

print(original_dict)

modify_dict(original_dict)
print(original_dict)
```

```
x = 10 # global variable

def outer_function():
  y = 20 # local to outer_function

  def inner_function():
    global x
    nonlocal y # if we go one step outside, it is global to that function

    x = 30 # global variable
    y = 40 # local to innter_function

    print(x, end=' ')
    print(y, end=' ')

  inner_function()
  print(x, end=' ')
  print(y, end=' ')

outer_function()
print(x)
```