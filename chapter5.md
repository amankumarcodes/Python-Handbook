# Chapter 5: Functions and Modules

## What is a Function?

A function is a block of organized, reusable code that performs a specific task. Functions provide better modularity for your application and a high degree of code reuse. In Python, functions are first-class objects, which means they can be assigned to variables, stored in data structures, passed as arguments to other functions, and even returned as values from other functions.

## Function Definition and Syntax

In Python, you define a function using the `def` keyword, followed by the function name, parentheses `()`, and a colon `:`. Any parameters (inputs) to the function are placed within the parentheses. The function body is indented below the definition line.

### Basic Syntax:
```python
def function_name(parameters):
    """Docstring - explains what the function does"""
    # Function body
    # Code to execute
    return value  # Optional return statement
```

### Example:
```python
def greet(name):
    """This function greets the person passed in as a parameter"""
    return f"Hello, {name}!"

# Function call
message = greet("Alice")
print(message)  # Output: Hello, Alice!
```

## Function Calls

To use a function, you "call" it by using its name followed by parentheses containing any arguments (values) you want to pass to it.

```python
# Define the function
def add_numbers(a, b):
    return a + b

# Call the function
result = add_numbers(5, 3)
print(result)  # Output: 8

# You can also call it directly in expressions
print(add_numbers(10, 20) + 5)  # Output: 35
```

## Parameters and Arguments

### Default Parameters

You can specify default values for parameters, which will be used if the function is called without the corresponding argument:

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("Alice"))  # Output: Hello, Alice!
print(greet("Bob", "Hi"))  # Output: Hi, Bob!
```

### Keyword Arguments

You can specify arguments by parameter name, which allows you to skip arguments or place them in a different order:

```python
def describe_person(name, age, city):
    return f"{name} is {age} years old and lives in {city}."

# Using positional arguments
print(describe_person("Alice", 30, "New York"))

# Using keyword arguments
print(describe_person(age=25, name="Bob", city="Boston"))

# Mixing positional and keyword arguments
# Positional arguments must come before keyword arguments
print(describe_person("Charlie", city="Chicago", age=35))
```

### Variable-Length Arguments (*args, **kwargs)

Python allows functions to accept a variable number of arguments:

#### *args (Variable-Length Positional Arguments)

The `*args` parameter allows a function to accept any number of positional arguments:

```python
def sum_all(*args):
    """Sum all the numbers passed to the function"""
    total = 0
    for num in args:
        total += num
    return total

print(sum_all(1, 2))  # Output: 3
print(sum_all(1, 2, 3, 4, 5))  # Output: 15
```

#### **kwargs (Variable-Length Keyword Arguments)

The `**kwargs` parameter allows a function to accept any number of keyword arguments:

```python
def print_info(**kwargs):
    """Print all the keyword arguments"""
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=30, city="New York")
# Output:
# name: Alice
# age: 30
# city: New York
```

#### Combining Different Types of Parameters

You can combine all types of parameters in a single function, but they must be in the correct order:
1. Positional parameters
2. Default parameters
3. *args
4. **kwargs

```python
def example_function(pos1, pos2, default1="default", default2="default", *args, **kwargs):
    print(f"Positional: {pos1}, {pos2}")
    print(f"Default: {default1}, {default2}")
    print(f"Variable positional: {args}")
    print(f"Variable keyword: {kwargs}")

example_function(1, 2, "custom", *[3, 4, 5], name="Alice", age=30)
# Output:
# Positional: 1, 2
# Default: custom, default
# Variable positional: (3, 4, 5)
# Variable keyword: {'name': 'Alice', 'age': 30}
```

## Return Values

Functions can return values using the `return` statement. If no `return` statement is used, the function returns `None` by default.

```python
# Function with a return value
def square(x):
    return x * x

result = square(5)
print(result)  # Output: 25

# Function with multiple return values
def get_min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = get_min_max([5, 3, 8, 1, 7])
print(f"Min: {minimum}, Max: {maximum}")  # Output: Min: 1, Max: 8

# Function with no return statement
def print_message(message):
    print(message)

result = print_message("Hello")
print(result)  # Output: None (after printing "Hello")
```

## Scope of Variables

### Local and Global Variables

Variables defined inside a function have a local scope, meaning they can only be accessed within that function. Variables defined outside all functions have a global scope, meaning they can be accessed throughout the program.

```python
# Global variable
global_var = "I am global"

def my_function():
    # Local variable
    local_var = "I am local"
    print(global_var)  # Can access global variable
    print(local_var)   # Can access local variable

my_function()
print(global_var)  # Can access global variable
# print(local_var)  # Error: local_var is not defined in this scope
```

### The global Keyword

If you need to modify a global variable from within a function, you must use the `global` keyword:

```python
counter = 0

def increment():
    global counter  # Declare that we're using the global variable
    counter += 1
    print(counter)

increment()  # Output: 1
increment()  # Output: 2
print(counter)  # Output: 2
```

Without the `global` keyword, Python would create a new local variable with the same name, leaving the global variable unchanged.

## Lambda Functions

Lambda functions are small, anonymous functions defined with the `lambda` keyword. They can have any number of arguments but only one expression.

```python
# Regular function
def square(x):
    return x * x

# Equivalent lambda function
square_lambda = lambda x: x * x

print(square(5))       # Output: 25
print(square_lambda(5))  # Output: 25
```

Lambda functions are often used with functions like `map()`, `filter()`, and `sorted()`:

```python
# Using lambda with map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x * x, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]

# Using lambda with filter()
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Output: [2, 4]

# Using lambda with sorted()
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]
sorted_students = sorted(students, key=lambda student: student["grade"], reverse=True)
for student in sorted_students:
    print(f"{student['name']}: {student['grade']}")
# Output:
# Bob: 92
# Alice: 85
# Charlie: 78
```

## Recursion

Recursion is a programming technique where a function calls itself to solve a problem. A recursive function must have a base case (a condition to stop recursion) and a recursive case (where the function calls itself).

### Example: Factorial Calculation

```python
def factorial(n):
    """Calculate the factorial of n recursively"""
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    else:
        return n * factorial(n - 1)

print(factorial(5))  # Output: 120 (5 * 4 * 3 * 2 * 1)
```

### Example: Fibonacci Sequence

```python
def fibonacci(n):
    """Return the nth Fibonacci number"""
    # Base cases
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

for i in range(10):
    print(fibonacci(i), end=" ")  # Output: 0 1 1 2 3 5 8 13 21 34
```

### Advantages and Limitations of Recursion

**Advantages:**
- Makes code cleaner and more elegant for certain problems
- Natural solution for problems that are recursive in nature (e.g., tree traversals, fractals)
- Can reduce the need for complex loops and state tracking

**Limitations:**
- Can be less efficient than iterative solutions due to function call overhead
- Risk of stack overflow for deep recursion (Python has a default recursion limit)
- Sometimes harder to trace and debug

## Built-in Functions

Python comes with many built-in functions that you can use without importing any modules:

```python
# Numeric functions
print(abs(-5))         # Output: 5
print(max(3, 7, 2))    # Output: 7
print(min(3, 7, 2))    # Output: 2
print(sum([1, 2, 3]))  # Output: 6
print(round(3.75, 1))  # Output: 3.8

# Type conversion
print(int("123"))      # Output: 123
print(float("3.14"))   # Output: 3.14
print(str(42))         # Output: "42"
print(bool(0))         # Output: False
print(list("abc"))     # Output: ['a', 'b', 'c']

# Sequence functions
numbers = [1, 2, 3, 4, 5]
print(len(numbers))    # Output: 5
print(sorted(numbers, reverse=True))  # Output: [5, 4, 3, 2, 1]
print(any([0, False, 5]))  # Output: True
print(all([1, True, 5]))   # Output: True

# Other useful functions
print(dir(str))        # Lists all attributes of the string class
print(help(print))     # Shows documentation for the print function
print(isinstance(42, int))  # Output: True
print(id(numbers))     # Returns the memory address of the object
```

## Modules

A module is a file containing Python code that can be imported and used in other Python programs. Modules help organize code into logical units and provide reusability.

### Importing Modules

```python
# Import the entire module
import math
print(math.sqrt(16))  # Output: 4.0

# Import specific functions from a module
from math import sqrt, pi
print(sqrt(16))  # Output: 4.0
print(pi)       # Output: 3.141592653589793

# Import with an alias
import math as m
print(m.sqrt(16))  # Output: 4.0

# Import all functions from a module (not recommended)
from math import *
print(sqrt(16))  # Output: 4.0
print(cos(0))    # Output: 1.0
```

### Creating Your Own Modules

You can create your own modules by saving Python code in a `.py` file:

**mymodule.py:**
```python
# Define variables
pi = 3.14159

# Define functions
def square(x):
    return x * x

def cube(x):
    return x * x * x

# Define classes
class Circle:
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return pi * self.radius ** 2
```

**main.py:**
```python
# Import your module
import mymodule

print(mymodule.pi)  # Output: 3.14159
print(mymodule.square(4))  # Output: 16

circle = mymodule.Circle(5)
print(circle.area())  # Output: 78.53975
```

### Standard Library Modules

Python comes with a rich standard library of modules:

```python
# Working with dates and times
import datetime
now = datetime.datetime.now()
print(now)  # Output: Current date and time

# Working with random numbers
import random
print(random.randint(1, 10))  # Output: Random integer between 1 and 10
print(random.choice(["apple", "banana", "cherry"]))  # Output: Random item from list

# Working with operating system
import os
print(os.getcwd())  # Output: Current working directory
print(os.listdir())  # Output: List of files in current directory

# Working with JSON
import json
data = {"name": "Alice", "age": 30}
json_string = json.dumps(data)
print(json_string)  # Output: {"name": "Alice", "age": 30}
parsed_data = json.loads(json_string)
print(parsed_data["name"])  # Output: Alice
```

## Packages

A package is a collection of modules organized in directories. Packages help organize related modules into a hierarchy.

### Installing Packages with pip

`pip` is Python's package installer, which allows you to install packages from the Python Package Index (PyPI):

```bash
# Install a package
pip install requests

# Install a specific version
pip install requests==2.25.1

# Upgrade a package
pip install --upgrade requests

# Uninstall a package
pip uninstall requests

# List installed packages
pip list
```

### Using Installed Packages

```python
# Using the requests package to make HTTP requests
import requests

response = requests.get("https://api.example.com/data")
if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print(f"Error: {response.status_code}")
```

## Practice Set

### Review Questions
1. What is the difference between a parameter and an argument in a function?
2. Explain the purpose of the `return` statement in a function.
3. What is the difference between local and global variables?
4. What are lambda functions and when would you use them?

### Coding Exercises
1. Write a function that takes a list of numbers and returns the average.
2. Create a function that checks if a given number is prime.
3. Write a recursive function to calculate the sum of the first n natural numbers.
4. Create a module with functions to calculate the area and perimeter of various shapes (circle, rectangle, triangle).

### Challenge Problem
Create a simple calculator program using functions:
1. Define separate functions for addition, subtraction, multiplication, and division
2. Create a main function that:
   - Displays a menu of operations
   - Takes user input for the operation choice
   - Takes user input for two numbers
   - Calls the appropriate function based on the operation choice
   - Displays the result
   - Asks if the user wants to perform another calculation
3. Handle potential errors, such as division by zero
4. Use recursion to allow the user to perform multiple calculations
