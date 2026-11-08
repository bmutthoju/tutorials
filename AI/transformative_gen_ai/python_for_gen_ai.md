---

# Agentic AI: Python for GenAI (SWEs)

## 1. Course Agenda

The course covers the following topics:

1. Python Fundamentals

   * Variables and Data Types
   * Operators
   * Strings
   * Lists
   * Tuples
   * Sets
   * Dictionaries
   * Conditionals
   * Loops
   * Functions
   * Modules and Packages
   * Virtual Environments
2. NumPy
3. Pandas

---

# Why Learn Python?

Python is one of the easiest programming languages to learn and is the primary programming language used in Artificial Intelligence, Machine Learning, Data Science, Automation, and Backend Development.

### Why Python is Popular

* Easy to read and write
* Beginner-friendly syntax
* Huge ecosystem of libraries
* Large community support
* Cross-platform
* Open source
* Excellent IDE support

Python is widely used in:

* Artificial Intelligence
* Machine Learning
* Deep Learning
* Data Science
* Backend APIs
* Automation
* DevOps
* Web Development
* Scientific Computing

---

# Why Python for Generative AI?

Python has become the standard language for Generative AI because almost every major AI framework provides first-class Python support.

Examples include:

* TensorFlow
* PyTorch
* Keras
* Hugging Face Transformers
* LangChain
* LlamaIndex
* OpenAI SDK
* Anthropic SDK

Python is commonly used for:

* Building AI applications
* Training machine learning models
* Prompt engineering
* Data preprocessing
* Model deployment
* Cloud integrations (AWS, Azure, Google Cloud)

---

# Python Characteristics

## Easy to Learn

Python has a simple syntax that closely resembles English, making it easier to learn than many traditional programming languages.

---

## Interpreted Language

Python is an interpreted language.

Instead of compiling the entire program before execution, Python executes code line by line.

### Advantages

* Faster development
* Easy debugging
* Interactive programming

### Disadvantages

* Generally slower than compiled languages like C++

---

## Current Version

The lecture notes reference **Python 3.14** as the latest version.

---

# Development Environments (IDEs)

Popular Python IDEs include:

* Visual Studio Code
* PyCharm
* Spyder
* Jupyter Notebook

---

# Google Colab

Google Colab is a cloud-based Jupyter Notebook environment.

## Advantages

* No installation required
* Free GPU (limited)
* Supports notebooks
* Code, documentation, and outputs are stored together
* Ideal for AI and Data Science experiments

---

# Variables and Data Types

Python is **dynamically typed**, meaning you do not need to declare the data type before creating a variable.

The interpreter determines the type automatically.

```python
a = 10
b = 6.2
c = True
name = "Alice"
```

---

## Common Data Types

| Data Type | Description                  | Example          |
| --------- | ---------------------------- | ---------------- |
| `int`     | Integer                      | `10`             |
| `float`   | Decimal number               | `3.14`           |
| `str`     | Text                         | `"Hello"`        |
| `bool`    | Boolean                      | `True`           |
| `list`    | Ordered mutable collection   | `[1,2,3]`        |
| `tuple`   | Ordered immutable collection | `(1,2,3)`        |
| `set`     | Unordered unique collection  | `{1,2,3}`        |
| `dict`    | Key-value pairs              | `{"name":"Bob"}` |

---

# Arithmetic and Comparison Operators

```python
x = 10
y = 3

print(x + y)
print(x - y)
print(x * y)
print(x / y)
print(x % y)
print(x > y)
print(x < y)
```

---

# Logical Operators

Python provides three logical operators.

| Operator | Description                         |
| -------- | ----------------------------------- |
| `and`    | Both conditions must be true        |
| `or`     | At least one condition must be true |
| `not`    | Reverses a Boolean value            |

Example:

```python
print(x > 0 and y > 0)
print(not x < 0)
```

---

# Lists

A **list** is an ordered, mutable collection enclosed in square brackets (`[]`).

Lists can store multiple data types.

```python
fruits = ["apple", 32, 3.14, [1, 2, 3]]
```

## Characteristics

* Ordered
* Mutable
* Zero-indexed
* Allows duplicate values
* Supports heterogeneous data

---

## Common List Operations

Add an element:

```python
fruits.append("mango")
```

Remove an element:

```python
fruits.remove("apple")
```

Update an element:

```python
fruits[1] = "banana"
```

---

# List Slicing

Python uses the following syntax:

```text
sequence[start : stop : step]
```

* `start` is inclusive.
* `stop` is exclusive.
* `step` determines how many elements to skip.

Example:

```python
numbers = [0,1,2,3,4,5,6,7,8,9,10]

subset = numbers[2:6]
print(subset)
```

Output:

```text
[2,3,4,5]
```

---

## Negative Indexing

Negative indexes start from the end of the list.

```python
numbers[-1]
```

returns the last element.

Example:

```python
numbers[-5:-2]
```

---

# Tuples

A **tuple** is an ordered, immutable collection enclosed in parentheses.

```python
person = ("Alice", 25, "Engineer")
```

## Characteristics

* Ordered
* Immutable
* Allows duplicates
* Faster than lists for read-only data

Typical use cases include:

* Coordinates
* Configuration values
* Bank account details
* Fixed records

---

# Sets

A **set** is an unordered collection of unique elements.

```python
numbers = {1,2,3,4}
```

## Characteristics

* Unordered
* Mutable
* No duplicate values
* Cannot contain mutable objects such as lists or dictionaries

---

## Common Operations

Add an element:

```python
fruits.add("date")
```

Remove an element:

```python
fruits.remove("banana")
```

---

## Set Operations

Union

```python
A | B
```

Intersection

```python
A & B
```

Difference

```python
A - B
```

---

# Dictionaries

A dictionary stores data as **key-value pairs**.

```python
user = {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com",
    "city": "New York"
}
```

## Characteristics

* Keys are unique.
* Keys must be immutable.
* Values can be any data type.
* Lookup by key is very fast.

---

## Accessing Values

```python
email = user["email"]
```

---

## Adding a New Entry

```python
user["country"] = "USA"
```

---

## Nested Dictionaries

```python
students = {
    1001: {
        "name": "Alice",
        "age": 20
    },
    1002: {
        "name": "Bob",
        "age": 22
    }
}
```

Nested dictionaries are commonly used to represent structured data such as student records, user profiles, or configuration objects.

---

## Key Takeaways

* Python is dynamically typed and easy to learn.
* Lists are mutable and ordered.
* Tuples are immutable and useful for fixed data.
* Sets store unique values and support mathematical set operations.
* Dictionaries provide fast key-based lookups and are one of the most important Python data structures.
* Google Colab is an excellent environment for experimenting with AI and data science code.
* Python's rich ecosystem makes it the preferred language for Generative AI.

---

This completes **Part 1: Python Fundamentals (Variables, Data Types, Operators, Lists, Tuples, Sets, and Dictionaries)**.

In the next section, I'll cover **Strings, Conditionals, Loops, and Functions** in the same polished course-note format.

---

Certainly! Continuing from **Part 1**, here's the next section in the same polished **course-note** style. This content is based on your uploaded lecture notes, with improved organization and minor clarifications for readability. 

---

# Part 2: Strings, Conditionals, Loops, and Functions

# Strings

A **string** is an ordered sequence of characters used to represent text.

Strings are one of the most frequently used data types in Python.

```python
name = "Alice"
message = 'Hello World'
```

## Characteristics

* Ordered
* Immutable
* Zero-indexed
* Supports slicing
* Supports iteration

Since strings are immutable, modifying a string actually creates a new string rather than changing the existing one.

---

# Creating Strings

Python supports both single and double quotes.

```python
name = 'Alice'
city = "New York"
```

Both forms are equivalent.

---

## Multi-line Strings

Python supports multi-line strings using triple quotes.

```python
text = '''
This is
a multiline
string.
'''
```

or

```python
text = """
This is
another multiline
string.
"""
```

These are commonly used for:

* Documentation
* Prompt engineering
* SQL queries
* JSON templates

---

# String Indexing

Strings can be accessed using indexes.

```python
text = "Hello World"

print(text[0])     # H
print(text[6])     # W
```

---

# String Slicing

The slicing syntax is identical to lists.

```text
sequence[start : stop : step]
```

Example:

```python
text = "Hello World"

print(text[6:])
```

Output

```text
World
```

Another example

```python
print(text[:5])
```

Output

```text
Hello
```

---

# Negative Indexing

Negative indexes count from the end.

```python
text = "Hello"

print(text[-1])
```

Output

```text
o
```

---

# Common String Functions

Convert to lowercase

```python
text.lower()
```

Convert to uppercase

```python
text.upper()
```

Capitalize first letter

```python
text.capitalize()
```

Convert every word to title case

```python
text.title()
```

Remove whitespace

```python
text.strip()
```

Remove leading whitespace

```python
text.lstrip()
```

Remove trailing whitespace

```python
text.rstrip()
```

Split into a list

```python
text.split()
```

Join a list into a string

```python
" ".join(["Hello", "World"])
```

Output

```text
Hello World
```

---

# String Concatenation

Strings can be combined using the `+` operator.

```python
first = "Hello"
second = "World"

result = first + " " + second
```

Output

```text
Hello World
```

---

# String Formatting

## f-Strings (Recommended)

```python
name = "Alice"
age = 25

print(f"My name is {name} and I am {age} years old.")
```

---

## format()

```python
print(
    "My name is {} and I am {} years old.".format(name, age)
)
```

Both approaches produce the same output, but **f-strings** are generally preferred because they are easier to read.

---

# Conditionals

Conditionals allow programs to make decisions based on Boolean expressions.

Python uses indentation instead of braces (`{}`) to define code blocks.

The recommended indentation is **4 spaces**.

---

# if Statement

```python
x = 10

if x > 5:
    print("x is greater than 5")
```

---

# if-else Statement

```python
x = 3

if x > 5:
    print("Greater than 5")
else:
    print("5 or smaller")
```

---

# if-elif-else Statement

```python
x = 10

if x > 15:
    print("Greater than 15")
elif x > 5:
    print("Greater than 5")
else:
    print("5 or less")
```

---

# Nested Conditions

Conditionals can be nested, although excessive nesting should generally be avoided.

```python
if age >= 18:
    if citizen:
        print("Eligible to vote")
```

---

# Comparison Operators

| Operator | Meaning               |
| -------- | --------------------- |
| `==`     | Equal                 |
| `!=`     | Not equal             |
| `>`      | Greater than          |
| `<`      | Less than             |
| `>=`     | Greater than or equal |
| `<=`     | Less than or equal    |

---

# Logical Operators

| Operator | Meaning                             |
| -------- | ----------------------------------- |
| `and`    | Both conditions must be true        |
| `or`     | At least one condition must be true |
| `not`    | Negates a Boolean expression        |

Example

```python
age = 25
salary = 80000

if age > 18 and salary > 50000:
    print("Eligible")
```

---

# Loops

Loops execute a block of code repeatedly.

Python provides two loop types:

* `for`
* `while`

---

# for Loop

A `for` loop iterates over a sequence.

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

Output

```text
apple
banana
cherry
```

---

# Iterating Over Numbers

```python
for i in range(5):
    print(i)
```

Output

```text
0
1
2
3
4
```

---

# while Loop

A `while` loop executes as long as a condition remains true.

```python
count = 1

while count <= 3:
    print(count)
    count += 1
```

Output

```text
1
2
3
```

---

# Nested Loops

Loops can be nested.

```python
items = ["a", "b", "c"]

pairs = []

for i in items:
    for j in items:
        pairs.append((i, j))

print(pairs)
```

Output

```text
[
 ('a','a'),
 ('a','b'),
 ('a','c'),
 ...
]
```

The lecture recommends **avoiding excessive nesting**, typically more than three levels, as it reduces readability and maintainability.

---

# Functions

A function is a reusable block of code that performs a specific task.

Functions are defined using the `def` keyword.

---

# Defining a Function

```python
def greet():
    print("Hello")
```

Calling the function

```python
greet()
```

---

# Function with Parameters

```python
def add(a, b):
    return a + b
```

Calling the function

```python
result = add(10, 20)
```

---

# Return Values

Functions may return a value or return nothing.

```python
def square(x):
    return x * x
```

---

# Example: Summarizing Text Using an LLM

```python
texts = [
    "Python is a versatile programming language."
]

def summarize_texts(texts):
    summaries = []

    for text in texts:

        prompt = f"""
Summarize the following text into one sentence.

{text}
"""

        summary = call_llm(prompt)
        summaries.append(summary)

    return summaries

summary_results = summarize_texts(texts)
```

This example illustrates how functions can encapsulate reusable AI workflows.

---

# Parameters vs Arguments

Consider the following function:

```python
def subtract(a, b):
    return a - b
```

Here:

* `a` and `b` are **parameters**.
* `10` and `5` are **arguments**.

Example

```python
result = subtract(10, 5)
```

---

# Positional Arguments

Arguments are matched according to their position.

```python
subtract(10, 5)
```

---

# Keyword Arguments

Arguments can also be passed using their names.

```python
def greet(name, message):
    print(f"{message}, {name}")

greet(name="Alice", message="Hello")
greet(message="Hi", name="Bob")
```

---

# Default Parameters

Functions can define default values.

```python
def greet(name, message="Hello"):
    print(f"{message}, {name}")
```

Usage

```python
greet("Alice")
```

Output

```text
Hello, Alice
```

---

# Variable-Length Arguments

## *args

Accepts any number of positional arguments.

```python
def total(*numbers):
    return sum(numbers)

print(total(1, 2, 3, 4))
```

---

## **kwargs

Accepts any number of keyword arguments.

```python
def print_user(**details):
    print(details)

print_user(name="Alice", age=25)
```

Output

```python
{
    'name': 'Alice',
    'age': 25
}
```

---

# Functions are First-Class Objects

Functions can be:

* Assigned to variables
* Passed as arguments
* Returned from other functions
* Nested inside functions

Example

```python
def outer():

    x = 20

    def inner():
        print(x)

    return inner

outer()()
```

---

# Type Hints

Python supports optional type hints.

```python
def add_two_numbers(num1: int, num2: int) -> int:
    return num1 + num2
```

Type hints improve readability and IDE support but **are not enforced at runtime**.

For example:

```python
print(add_two_numbers("a", "b"))
```

Output

```text
ab
```

---

# Lambda Functions

Lambda functions are small anonymous functions.

General syntax

```python
lambda arguments: expression
```

Example

```python
length = lambda x: len(x)

print(length("Alhamdulillah"))
```

---

# Key Takeaways

* Strings are immutable sequences of characters.
* String slicing follows the same syntax as list slicing.
* Use **f-strings** for readable string formatting.
* Python uses **indentation** instead of braces for defining code blocks.
* Use `for` loops to iterate over sequences and `while` loops for condition-based repetition.
* Functions improve code reuse and readability.
* Python functions support positional, keyword, default, and variable-length arguments.
* Functions are first-class objects and can be passed around like any other value.
* Type hints improve documentation and tooling but do not enforce runtime type checking.
* Lambda functions provide a concise way to define simple anonymous functions.

---

The next part will cover **Modules, Packages, Libraries, Virtual Environments, and `pip`**, followed by **NumPy**. This section naturally transitions into Python project organization before moving into data science libraries.

---

Certainly! Continuing in the same **course-note** style.

This section covers how Python code is organized into reusable components and how external packages are managed. These concepts are fundamental for building real-world Python and AI applications. The content is based on your uploaded lecture notes with improved formatting and minor clarifications. 

---

# Part 3: Modules, Packages, Libraries, Virtual Environments, and `pip`

# Why Organize Python Code?

As applications grow larger, writing all code in a single file becomes difficult to maintain.

Python encourages dividing code into smaller, reusable units that can be imported wherever needed.

Python organizes code using the following hierarchy:

```text
Library
│
├── Package
│      ├── Module
│      ├── Module
│      └── Module
│
└── Package
       ├── Module
       └── Module
```

Understanding this hierarchy is essential for working with large applications and third-party libraries.

---

# Modules

A **module** is simply a Python file (`.py`) containing Python code.

A module can contain:

* Variables
* Functions
* Classes
* Constants
* Executable code

Example:

```text
calculator.py
```

```python
PI = 3.14159

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

This file itself is a Python module.

---

# Importing a Module

A module can be imported into another Python file.

```python
import calculator

print(calculator.add(10, 20))
```

Output

```text
30
```

---

## Import Specific Functions

Instead of importing the entire module, individual functions can be imported.

```python
from calculator import add

print(add(5, 6))
```

---

## Import with an Alias

Long module names can be shortened.

```python
import numpy as np

arr = np.array([1, 2, 3])
```

Using aliases improves readability and is common practice.

---

# Packages

A **package** is a collection of related Python modules.

Packages help organize large codebases.

Example:

```text
payments/
│
├── __init__.py
├── phonepe.py
├── gpay.py
└── paypal.py
```

Each file is an individual module.

The entire `payments` directory is a package.

---

## The `__init__.py` File

Traditionally, every package contained an `__init__.py` file.

```text
payments/
│
├── __init__.py
├── phonepe.py
└── gpay.py
```

The file indicates that the directory should be treated as a Python package.

Although modern versions of Python support **namespace packages** (which may omit `__init__.py`), many projects still include it for compatibility and package initialization.

---

# Importing from Packages

Suppose we have:

```text
payments/
│
├── __init__.py
├── phonepe.py
└── gpay.py
```

Importing the entire module:

```python
from payments import phonepe

phonepe.make_payment()
```

Importing multiple modules:

```python
from payments import phonepe, gpay
```

---

# Module vs Package

| Module                 | Package                                 |
| ---------------------- | --------------------------------------- |
| A single `.py` file    | A directory containing multiple modules |
| Contains Python code   | Organizes related modules               |
| Smallest reusable unit | Collection of reusable modules          |

---

# Libraries

A **library** is a collection of packages and modules that provide reusable functionality.

Examples:

| Library      | Purpose             |
| ------------ | ------------------- |
| NumPy        | Numerical computing |
| Pandas       | Data analysis       |
| Requests     | HTTP requests       |
| Matplotlib   | Data visualization  |
| TensorFlow   | Deep Learning       |
| PyTorch      | Deep Learning       |
| Scikit-learn | Machine Learning    |

In practice, the terms **package** and **library** are often used interchangeably, although a library typically encompasses multiple packages and modules.

---

# The Python Package Index (PyPI)

The **Python Package Index (PyPI)** is the official repository of Python packages.

It hosts hundreds of thousands of open-source packages that can be installed into your projects.

Examples include:

* NumPy
* Pandas
* Flask
* Django
* FastAPI
* Requests
* LangChain
* OpenAI SDK

---

# `pip` – Python Package Manager

`pip` is the standard package manager for Python.

It downloads and installs packages from PyPI.

---

## Installing a Package

```bash
pip install requests
```

---

## Install a Specific Version

```bash
pip install requests==2.24.0
```

Specifying versions ensures that all developers use the same package version, improving reproducibility.

---

## Upgrade a Package

```bash
pip install --upgrade requests
```

---

## Remove a Package

```bash
pip uninstall requests
```

---

## List Installed Packages

```bash
pip list
```

---

## Show Package Information

```bash
pip show pandas
```

---

# Example: Using the `requests` Library

```python
import requests

response = requests.get(
    "https://api.example.com/data"
)

print(response.json())
```

The `requests` library simplifies making HTTP requests and handling API responses.

---

# Virtual Environments

A **virtual environment** is an isolated Python environment that maintains its own interpreter and installed packages.

Each project can have its own dependencies without affecting other projects.

---

## Why Use Virtual Environments?

Without virtual environments:

```text
Project A
requests 2.24

Project B
requests 2.31
```

Only one version could be installed globally, leading to dependency conflicts.

With virtual environments:

```text
Project A
│
└── venv
      requests 2.24

Project B
│
└── venv
      requests 2.31
```

Each project maintains its own isolated environment.

---

# Creating a Virtual Environment

```bash
python -m venv projectA_env
```

This creates a directory named `projectA_env` containing the isolated Python environment.

---

# Activating the Environment

### Windows

```bash
projectA_env\Scripts\activate
```

### macOS / Linux

```bash
source projectA_env/bin/activate
```

After activation, the shell prompt typically changes to indicate the active environment:

```text
(projectA_env)
```

---

# Installing Packages in a Virtual Environment

Once activated:

```bash
pip install requests==2.24.0
```

The package is installed only within that virtual environment.

---

# Deactivating the Environment

When finished:

```bash
deactivate
```

This returns you to the system's default Python environment.

---

# Common Project Structure

A typical Python project might look like:

```text
my_project/
│
├── venv/
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── models.py
│   └── services.py
│
├── tests/
│
├── requirements.txt
│
└── README.md
```

---

# `requirements.txt`

Projects often include a `requirements.txt` file listing all dependencies.

Example:

```text
numpy==2.2.0
pandas==2.3.0
requests==2.32.0
```

Install all dependencies with:

```bash
pip install -r requirements.txt
```

This helps ensure consistent environments across development, testing, and production.

---

# Best Practices

* Use one virtual environment per project.
* Pin dependency versions in `requirements.txt` for reproducible builds.
* Prefer importing only what you need to improve readability.
* Organize related modules into packages.
* Use descriptive module and package names.
* Avoid placing all code in a single file for larger applications.

---

# Key Takeaways

* A **module** is a single Python file containing code.
* A **package** is a directory that groups related modules.
* A **library** provides reusable functionality through packages and modules.
* **PyPI** is the official repository for Python packages.
* **`pip`** is the standard tool for installing and managing Python packages.
* **Virtual environments** isolate project dependencies and prevent version conflicts.
* Well-organized modules and packages improve maintainability, readability, and code reuse.

---

This completes **Part 3: Modules, Packages, Libraries, Virtual Environments, and `pip`**.

The next section, **Part 4: NumPy**, will introduce numerical computing with arrays, vectorized operations, broadcasting, array reshaping, filtering, and common mathematical functions—the foundation for efficient data processing in AI and machine learning.

---

Certainly! Let's continue with **Part 4** in the same polished course-note format.

This section introduces **NumPy (Numerical Python)**, one of the most important libraries in the Python ecosystem. NumPy serves as the foundation for many scientific computing, machine learning, and deep learning libraries, including Pandas, SciPy, TensorFlow, PyTorch, and Scikit-learn. The content below is based on your uploaded lecture notes with improved structure and minor clarifications. 

---

# Part 4: NumPy

# Introduction to NumPy

**NumPy** (Numerical Python) is an open-source Python library designed for **fast numerical computing**.

It provides a powerful multidimensional array object along with a rich collection of mathematical functions for performing operations efficiently on large datasets.

NumPy is implemented primarily in **C and Fortran**, allowing it to execute numerical operations significantly faster than native Python lists.

---

# Why NumPy?

NumPy is widely used because it provides:

* Fast numerical computation
* Efficient memory usage
* Vectorized operations
* Multi-dimensional arrays
* Mathematical and statistical functions
* Foundation for many AI and data science libraries

Many Python libraries, including **Pandas**, use NumPy internally.

---

# Why NumPy for AI?

NumPy plays an essential role in Artificial Intelligence and Machine Learning.

It is commonly used for:

* Numerical computations
* Feature engineering
* Data preprocessing
* Matrix operations
* Statistical analysis
* Tensor preparation before model training

Although deep learning frameworks like PyTorch and TensorFlow use tensors internally, NumPy arrays are frequently used during data preparation and experimentation.

---

# NumPy Arrays

The core data structure in NumPy is the **ndarray (N-dimensional array)**.

Unlike Python lists, NumPy arrays are **homogeneous**, meaning all elements have the same data type.

Example:

```python id="kp4z7w"
import numpy as np

arr = np.array([1, 2, 3, 4])

print(arr)
```

Output

```text id="9a7hkg"
[1 2 3 4]
```

---

# Python List vs NumPy Array

| Python List                     | NumPy Array                               |
| ------------------------------- | ----------------------------------------- |
| Can store mixed data types      | Stores one data type                      |
| Slower for numerical operations | Highly optimized for numerical operations |
| More flexible                   | More memory efficient                     |
| General-purpose                 | Numerical computing                       |

Example:

```python id="pgm0ir"
numbers = [1, 2, 3]
```

```python id="vjlwmr"
arr = np.array([1, 2, 3])
```

---

# Checking the Data Type

Every NumPy array has a specific data type (`dtype`).

```python id="uqgqgm"
arr = np.array([1, 2, 3])

print(arr.dtype)
```

Output

```text id="9l2dlu"
int64
```

The exact output may vary depending on your operating system and processor architecture.

---

# Creating Arrays

## Using `array()`

```python id="q7t0xk"
arr = np.array([10, 20, 30])
```

---

## Using `arange()`

Creates evenly spaced values.

```python id="0sdrhl"
np.arange(10)
```

Output

```text id="yj9nlq"
[0 1 2 3 4 5 6 7 8 9]
```

---

## Creating Arrays Filled with Zeros

```python id="g57rpx"
np.zeros((4, 4))
```

Creates a 4 × 4 matrix of zeros.

---

## Creating Arrays Filled with Ones

```python id="2zkjlwm"
np.ones((2, 3))
```

Output

```text id="5sh3iq"
[[1. 1. 1.]
 [1. 1. 1.]]
```

---

## Specifying the Data Type

```python id="xzfp66"
np.ones((2, 2), dtype=int)
```

Output

```text id="vtzowp"
[[1 1]
 [1 1]]
```

---

# Array Shape

Every NumPy array has a **shape**, which describes its dimensions.

Example:

```python id="jlwm8u"
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.shape)
```

Output

```text id="d2aq5q"
(2, 3)
```

Meaning:

* 2 rows
* 3 columns

---

# Reshaping Arrays

The `reshape()` function changes the dimensions of an array without changing its data.

Example:

```python id="hnr60q"
arr = np.arange(10)

arr.reshape((2, 5))
```

Output

```text id="lwtjlwm"
[[0 1 2 3 4]
 [5 6 7 8 9]]
```

The total number of elements must remain the same.

---

# Vectorized Operations

One of NumPy's biggest advantages is **vectorization**.

Instead of looping over every element manually, operations are performed on the entire array simultaneously.

Example:

```python id="sq1utn"
arr = np.array([1, 2, 3, 4])

arr + 2
```

Output

```text id="vqqjlwm"
[3 4 5 6]
```

Every element increases by 2.

---

## Multiplication

```python id="e2wdlo"
arr * 3
```

Output

```text id="x6vcap"
[3 6 9 12]
```

---

# NumPy vs Python Lists

Consider:

```python id="pgh5z5"
[1, 2, 3, 4] * 2
```

Output

```text id="jlwm6i"
[1, 2, 3, 4, 1, 2, 3, 4]
```

Lists repeat themselves.

Now compare with NumPy:

```python id="axt9tr"
np.array([1, 2, 3, 4]) * 2
```

Output

```text id="0ebqzb"
[2 4 6 8]
```

Each element is multiplied individually.

This behavior makes NumPy ideal for scientific computing.

---

# Mathematical Functions

NumPy includes many built-in mathematical functions.

## Mean

```python id="d5m8qh"
arr.mean()
```

---

## Median

```python id="e2mvlh"
np.median(arr)
```

---

## Other Common Functions

| Function      | Purpose            |
| ------------- | ------------------ |
| `np.min()`    | Minimum value      |
| `np.max()`    | Maximum value      |
| `np.sum()`    | Sum of values      |
| `np.mean()`   | Average            |
| `np.median()` | Median             |
| `np.std()`    | Standard deviation |
| `np.var()`    | Variance           |

---

# Trigonometric Functions

NumPy provides many mathematical functions.

Examples include:

```python id="jlwmcv"
np.sin(arr)
np.cos(arr)
np.tan(arr)
```

---

# Boolean Filtering

One of NumPy's most useful features is filtering using Boolean expressions.

Example:

```python id="f6b7vp"
arr = np.arange(10)

arr[arr > 4]
```

Output

```text id="jlwmyn"
[5 6 7 8 9]
```

---

# Chaining Operations

Because filtering returns another NumPy array, operations can be chained.

Example:

```python id="0bx2up"
arr[arr > 4].mean()
```

This computes the average of all values greater than 4.

---

# Multiple Conditions

Multiple conditions can be combined using logical operators.

Example:

```python id="qjlwmu"
arr[(arr > 4) & (arr < 7)]
```

Output

```text id="jlwm0j"
[5 6]
```

Calculating the average:

```python id="jlwm7d"
arr[(arr > 4) & (arr < 7)].mean()
```

---

# Performance

The lecture notes emphasize that NumPy performs extremely well even for **very large datasets**, including arrays containing **tens of millions of numbers**.

Its speed comes from:

* Optimized C/Fortran implementation
* Contiguous memory layout
* Vectorized operations
* Reduced Python interpreter overhead

---

# Best Practices

* Use NumPy arrays instead of Python lists for numerical computations.
* Prefer vectorized operations over explicit Python loops.
* Keep array data types consistent.
* Use built-in mathematical functions instead of writing custom loops.
* Filter data using Boolean indexing for concise and efficient code.

---

# Key Takeaways

* **NumPy** is the foundation of numerical computing in Python.
* The primary data structure is the **ndarray**, which stores homogeneous data efficiently.
* NumPy arrays are significantly faster and more memory-efficient than Python lists for numerical tasks.
* Use `array()`, `arange()`, `zeros()`, and `ones()` to create arrays.
* `reshape()` changes an array's dimensions without changing its data.
* Vectorized operations eliminate the need for explicit loops.
* Boolean indexing enables powerful filtering and chaining of operations.
* NumPy provides a comprehensive set of mathematical and statistical functions for scientific computing.

---

This completes **Part 4: NumPy**.

The next and final section, **Part 5: Pandas**, will cover:

* `Series` and `DataFrame`
* Reading data from CSV, Excel, JSON, SQL, and other sources
* Inspecting and cleaning data
* Filtering and sorting
* Handling missing values
* Grouping and aggregation
* `loc` and `iloc`
* Creating new columns
* Practical data analysis workflows

After that, I'll also create a **one-page Python + NumPy + Pandas Cheat Sheet** as a quick interview reference.

---

You're right. So far we've completed:

1. ✅ Python Fundamentals
2. ✅ Strings, Conditionals, Loops & Functions
3. ✅ Modules, Packages, Virtual Environments & `pip`
4. ✅ NumPy

We haven't done **Part 5: Pandas** yet. Below is the polished version in the same course-note style based on your uploaded lecture notes. 

---

# Part 5: Pandas

# Introduction to Pandas

**Pandas** is one of the most popular Python libraries for **data manipulation and analysis**.

It provides powerful data structures and functions that simplify working with structured (tabular) data such as CSV, Excel, SQL tables, and JSON.

Pandas is built **on top of NumPy**, inheriting NumPy's performance while providing higher-level abstractions for data analysis.

---

# Why Pandas?

Pandas is designed for working with structured datasets.

Typical use cases include:

* Reading datasets
* Cleaning data
* Transforming data
* Filtering records
* Aggregating information
* Handling missing values
* Statistical analysis
* Preparing datasets for Machine Learning

---

# Why Pandas in AI?

Before training Machine Learning or Generative AI models, data must usually be cleaned and transformed.

Pandas is commonly used for:

* Feature engineering
* Data preprocessing
* Exploratory Data Analysis (EDA)
* Preparing datasets for model training
* Cleaning LLM training data
* Working with structured business data

---

# Core Data Structures

Pandas provides two primary data structures.

## Series

A **Series** is a one-dimensional labeled array.

It is similar to a single column in an Excel spreadsheet.

Example:

```python
import pandas as pd

ages = pd.Series([25, 30, 22])

print(ages)
```

---

## DataFrame

A **DataFrame** is a two-dimensional table consisting of rows and columns.

Each column is a **Series**.

Example:

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Alice", "Bob"],
    "Age": [25, 30]
})
```

Think of a DataFrame as an Excel spreadsheet stored in memory.

---

# Reading Data

Pandas can load data from many sources.

Common formats include:

* CSV
* Excel
* JSON
* SQL databases
* HTML tables
* Parquet
* Google BigQuery

Example:

```python
import pandas as pd

csv_url = "https://raw.githubusercontent.com/agconti/kaggle-titanic/master/data/train.csv"

df = pd.read_csv(csv_url)
```

---

# Viewing Data

## Display First Rows

```python
df.head()
```

Default output:

First **5 rows**

---

Display a specific number of rows.

```python
df.head(10)
```

---

# Inspecting the Dataset

## Information

```python
df.info()
```

Displays:

* Column names
* Data types
* Number of rows
* Missing values
* Memory usage

---

## Summary Statistics

```python
df.describe()
```

Returns statistics such as:

* Count
* Mean
* Standard deviation
* Minimum
* 25%
* Median (50%)
* 75%
* Maximum

---

# Selecting Columns

Single column:

```python
df["Age"]
```

Returns a **Series**.

---

Multiple columns:

```python
df[["Age", "Fare"]]
```

Returns a **DataFrame**.

---

# Filtering Rows

Example:

```python
df[df["Age"] > 15]
```

Returns passengers older than 15.

---

Filter by Fare:

```python
df[df["Fare"] > 15]
```

---

Calculate the average Fare after filtering.

```python
df[df["Fare"] > 15]["Fare"].mean()
```

Filtering operations can be chained together.

---

# Sorting Data

Ascending order:

```python
df.sort_values("Age")
```

Descending order:

```python
df.sort_values("Age", ascending=False)
```

---

# Missing Values

Missing values are represented as:

```text
NaN
```

(**Not a Number**)

---

## Remove Missing Values

```python
df.dropna()
```

Removes rows containing missing values.

---

## Count Missing Values

```python
df["Age"].isna().sum()
```

---

## Average Age

```python
df["Age"].mean()
```

---

# Filling Missing Values

Replace missing ages with the average age.

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)
```

Check again.

```python
df["Age"].isna().sum()
```

Should now return:

```text
0
```

---

## Filling Categorical Values

For categorical columns, use the **mode** (most frequent value).

Example:

```python
df["Embarked"] = df["Embarked"].fillna(
    df["Embarked"].mode()[0]
)
```

---

# Grouping Data

Grouping summarizes data by categories.

Example:

Average survival rate by passenger class.

```python
df.groupby("Pclass").agg({
    "Survived": "mean"
})
```

---

Average survival by gender.

```python
df.groupby("Sex").agg({
    "Survived": "mean"
})
```

---

Group by multiple columns.

```python
df.groupby(
    ["Sex", "Pclass"]
).agg({
    "Survived": "mean"
})
```

---

Multiple aggregations.

```python
df.groupby("Survived").agg({
    "Age": ["mean", "median"],
    "Fare": "mean"
})
```

This computes:

* Mean age
* Median age
* Mean fare

for each survival category.

---

# Resetting the Index

After grouping, grouped columns become the DataFrame index.

Convert them back into regular columns.

```python
grouped = (
    df.groupby("Sex")
      .agg({
          "Survived": "mean"
      })
      .reset_index()
)
```

---

# `iloc`

`iloc` selects data using **integer positions**.

Example:

```python
grouped.iloc[0, 0]
```

Returns:

First row, first column.

---

# `loc`

`loc` selects data using **labels**.

Example:

```python
grouped.loc[0, "Survived"]
```

Returns the survival rate stored in that row.

---

# Dropping Columns

Remove a column.

```python
df.drop(
    "PassengerId",
    axis=1
)
```

`axis=1` indicates columns.

`axis=0` refers to rows.

---

# Creating New Columns

New columns can be generated from existing data.

Example:

```python
df["eligible_to_vote"] = (
    df["Age"].apply(
        lambda age: age >= 18
    )
)
```

The new column contains Boolean values.

Example output:

| Age | eligible_to_vote |
| --- | ---------------- |
| 25  | True             |
| 14  | False            |
| 31  | True             |

---

# Applying Functions

`apply()` executes a function for every value in a Series.

Example:

```python
df["Age"].apply(
    lambda age: age + 5
)
```

---

# Data Cleaning Workflow

A typical Pandas workflow looks like this:

```text
Read Data
      │
      ▼
Inspect Data
      │
      ▼
Handle Missing Values
      │
      ▼
Filter Rows
      │
      ▼
Sort Data
      │
      ▼
Group & Aggregate
      │
      ▼
Create New Columns
      │
      ▼
Export or Train ML Model
```

---

# Performance Notes

According to the lecture:

* Pandas can efficiently process datasets with **millions of rows**.
* Modern versions support GPU acceleration in certain ecosystems.
* All data is typically loaded into memory, so very large datasets may require distributed tools such as **Dask**, **Spark**, or **Polars**.

---

# Best Practices

* Inspect data using `head()`, `info()`, and `describe()` before analysis.
* Handle missing values before building models.
* Use vectorized operations instead of Python loops.
* Use `groupby()` for aggregations rather than manual iteration.
* Use `loc` for label-based indexing and `iloc` for position-based indexing.
* Prefer meaningful column names and consistent data types.

---

# Key Takeaways

* **Pandas** is the standard library for structured data analysis in Python.
* A **Series** represents a single column, while a **DataFrame** represents a table.
* Use `read_csv()` and related functions to import data from multiple sources.
* Inspect datasets with `head()`, `info()`, and `describe()`.
* Filter, sort, and group data efficiently using built-in Pandas operations.
* Handle missing values using `dropna()` or `fillna()`.
* Create new columns with `apply()` and lambda functions.
* `loc` uses labels, whereas `iloc` uses integer positions.
* Pandas is an essential tool for data preprocessing in AI, machine learning, and analytics.

---

This completes the entire set of notes from your uploaded lecture:

* ✅ Part 1: Python Fundamentals
* ✅ Part 2: Strings, Conditionals, Loops & Functions
* ✅ Part 3: Modules, Packages, Libraries & Virtual Environments
* ✅ Part 4: NumPy
* ✅ Part 5: Pandas

I also noticed a few places in the original lecture where the instructor moved quickly (for example, `loc` vs `iloc`, `apply()`, `groupby()`, and `fillna()`), so I expanded those just enough to make the notes useful as a future quick reference without turning them into a textbook.
