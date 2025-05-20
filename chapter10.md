# Chapter 10: Advanced Topics

## Generators and Iterators

### Iterators

An iterator is an object that implements the iterator protocol, which consists of the methods `__iter__()` and `__next__()`. Iterators are used to iterate over a container (like a list) one element at a time.

```python
# Using built-in iterators
my_list = [1, 2, 3, 4, 5]
iterator = iter(my_list)  # Get an iterator

print(next(iterator))  # Output: 1
print(next(iterator))  # Output: 2
print(next(iterator))  # Output: 3
print(next(iterator))  # Output: 4
print(next(iterator))  # Output: 5
# print(next(iterator))  # StopIteration exception
```

### Creating Custom Iterators

You can create your own iterator by implementing the iterator protocol:

```python
class Countdown:
    def __init__(self, start):
        self.start = start
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.start <= 0:
            raise StopIteration
        self.start -= 1
        return self.start + 1

# Using the custom iterator
countdown = Countdown(5)
for number in countdown:
    print(number)  # Output: 5, 4, 3, 2, 1
```

### Generators

Generators provide a convenient way to implement the iterator protocol. Instead of creating a class with `__iter__()` and `__next__()` methods, you can define a function that uses the `yield` statement:

```python
def countdown(start):
    while start > 0:
        yield start
        start -= 1

# Using the generator
for number in countdown(5):
    print(number)  # Output: 5, 4, 3, 2, 1
```

Generators are memory-efficient because they generate values on-the-fly instead of storing them all in memory:

```python
# Generator for Fibonacci sequence
def fibonacci(n):
    a, b = 0, 1
    count = 0
    while count < n:
        yield a
        a, b = b, a + b
        count += 1

# Print first 10 Fibonacci numbers
for number in fibonacci(10):
    print(number)  # Output: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
```

### Generator Expressions

Similar to list comprehensions, generator expressions create generators:

```python
# List comprehension (creates the entire list in memory)
squares_list = [x**2 for x in range(1000000)]  # Uses more memory

# Generator expression (generates values on-the-fly)
squares_gen = (x**2 for x in range(1000000))  # Uses less memory

# Using the generator expression
print(next(squares_gen))  # Output: 0
print(next(squares_gen))  # Output: 1
print(next(squares_gen))  # Output: 4
```

### Generator Methods: send(), throw(), and close()

Generators can also receive values, throw exceptions, and be closed:

```python
def echo_generator():
    while True:
        received = yield
        print(f"Received: {received}")

# Using send() to communicate with the generator
echo = echo_generator()
next(echo)  # Prime the generator
echo.send("Hello")  # Output: Received: Hello
echo.send("World")  # Output: Received: World
echo.close()        # Close the generator
```

## Decorators

Decorators are a powerful feature in Python that allow you to modify the behavior of functions or methods without changing their source code.

### Basic Decorators

A decorator is a function that takes another function as an argument and returns a new function that usually extends or modifies the behavior of the original function:

```python
def simple_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@simple_decorator
def say_hello():
    print("Hello!")

# Calling the decorated function
say_hello()
# Output:
# Something is happening before the function is called.
# Hello!
# Something is happening after the function is called.
```

The `@simple_decorator` syntax is equivalent to:

```python
def say_hello():
    print("Hello!")

say_hello = simple_decorator(say_hello)
```

### Decorators with Arguments

To create decorators that work with functions that take arguments:

```python
def decorator_with_args(func):
    def wrapper(*args, **kwargs):
        print(f"Arguments: {args}, Keyword arguments: {kwargs}")
        return func(*args, **kwargs)
    return wrapper

@decorator_with_args
def add(a, b):
    return a + b

result = add(3, 5)
print(result)  # Output: Arguments: (3, 5), Keyword arguments: {}
               #         8
```

### Decorators with Parameters

You can also create decorators that take parameters:

```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            results = []
            for _ in range(n):
                results.append(func(*args, **kwargs))
            return results
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Output: ['Hello, Alice!', 'Hello, Alice!', 'Hello, Alice!']
```

### Practical Examples of Decorators

#### Timing Decorator

```python
import time

def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} executed in {end_time - start_time:.4f} seconds")
        return result
    return wrapper

@timing_decorator
def slow_function():
    time.sleep(1)
    return "Function completed"

print(slow_function())  # Output: slow_function executed in 1.0012 seconds
                        #         Function completed
```

#### Memoization Decorator

```python
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper

@memoize
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(35))  # Much faster than without memoization
```

#### Authentication Decorator

```python
def require_auth(func):
    def wrapper(user, *args, **kwargs):
        if user.get('authenticated', False):
            return func(user, *args, **kwargs)
        else:
            return "Authentication required"
    return wrapper

@require_auth
def get_sensitive_data(user):
    return f"Sensitive data for {user['name']}"

# Test with authenticated user
authenticated_user = {'name': 'Alice', 'authenticated': True}
print(get_sensitive_data(authenticated_user))  # Output: Sensitive data for Alice

# Test with unauthenticated user
unauthenticated_user = {'name': 'Bob', 'authenticated': False}
print(get_sensitive_data(unauthenticated_user))  # Output: Authentication required
```

## Context Managers

Context managers are objects that define the methods `__enter__()` and `__exit__()` and are designed to be used with the `with` statement. They ensure proper acquisition and release of resources.

### Using Built-in Context Managers

The most common use of context managers is for file operations:

```python
# Using a file as a context manager
with open("example.txt", "w") as file:
    file.write("Hello, World!")
# File is automatically closed when the block exits
```

### Creating Context Managers with Classes

You can create your own context managers by implementing the context manager protocol:

```python
class DatabaseConnection:
    def __init__(self, host, username, password):
        self.host = host
        self.username = username
        self.password = password
        self.connection = None
    
    def __enter__(self):
        print(f"Connecting to database at {self.host}")
        # In a real implementation, this would establish a database connection
        self.connection = {"status": "connected"}
        return self.connection
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection")
        # In a real implementation, this would close the connection
        self.connection = None
        # Return True to suppress exceptions, False to propagate them
        return False

# Using the custom context manager
with DatabaseConnection("localhost", "user", "password") as conn:
    print(f"Connection status: {conn['status']}")
# Output:
# Connecting to database at localhost
# Connection status: connected
# Closing database connection
```

### Creating Context Managers with contextlib

The `contextlib` module provides utilities for working with context managers:

```python
from contextlib import contextmanager

@contextmanager
def temporary_file(filename):
    try:
        file = open(filename, "w")
        yield file
    finally:
        file.close()
        import os
        os.remove(filename)

# Using the context manager
with temporary_file("temp.txt") as file:
    file.write("This is temporary content")
    # File exists here
# File is closed and removed after the block exits
```

### Nested Context Managers

You can use multiple context managers in a single `with` statement:

```python
with open("input.txt", "r") as input_file, open("output.txt", "w") as output_file:
    content = input_file.read()
    output_file.write(content.upper())
```

## Regular Expressions

Regular expressions (regex) are powerful patterns used to match character combinations in strings. Python's `re` module provides regex functionality.

### Basic Pattern Matching

```python
import re

text = "The quick brown fox jumps over the lazy dog"

# Search for a pattern
match = re.search(r"fox", text)
if match:
    print(f"Found 'fox' at position {match.start()}")  # Output: Found 'fox' at position 16

# Check if a pattern exists
if re.search(r"cat", text):
    print("Found 'cat'")
else:
    print("No 'cat' found")  # Output: No 'cat' found
```

### Common Regex Patterns

```python
import re

# Match any digit
result = re.findall(r"\d", "abc123def456")
print(result)  # Output: ['1', '2', '3', '4', '5', '6']

# Match any word character (alphanumeric + underscore)
result = re.findall(r"\w+", "Hello, World! 123_456")
print(result)  # Output: ['Hello', 'World', '123_456']

# Match whitespace
result = re.split(r"\s+", "Hello   World   Test")
print(result)  # Output: ['Hello', 'World', 'Test']

# Match specific number of occurrences
result = re.findall(r"\d{2,4}", "12 345 6789 01")
print(result)  # Output: ['12', '345', '6789', '01']

# Match email addresses (simplified)
emails = "Contact us at info@example.com or support@company.co.uk"
result = re.findall(r"[\w.+-]+@[\w-]+\.[\w.-]+", emails)
print(result)  # Output: ['info@example.com', 'support@company.co.uk']
```

### Regex Functions

The `re` module provides several functions for working with regular expressions:

```python
import re

text = "The quick brown fox jumps over the lazy dog. The fox is quick."

# re.search() - Find the first match
match = re.search(r"fox", text)
print(match.group())  # Output: fox

# re.findall() - Find all matches
matches = re.findall(r"fox", text)
print(matches)  # Output: ['fox', 'fox']

# re.finditer() - Return an iterator of match objects
for match in re.finditer(r"fox", text):
    print(f"Found at position {match.start()}")

# re.sub() - Substitute matches with a replacement
new_text = re.sub(r"fox", "cat", text)
print(new_text)  # Output: The quick brown cat jumps over the lazy dog. The cat is quick.

# re.split() - Split string by pattern
parts = re.split(r"\.", text)
print(parts)  # Output: ['The quick brown fox jumps over the lazy dog', ' The fox is quick', '']
```

### Regex Groups and Capturing

Groups allow you to extract specific parts of a match:

```python
import re

# Basic grouping
text = "John Smith (john.smith@example.com)"
match = re.search(r"([\w\s]+) \(([\w.]+@[\w.]+)\)", text)
if match:
    print(f"Name: {match.group(1)}")  # Output: Name: John Smith
    print(f"Email: {match.group(2)}")  # Output: Email: john.smith@example.com

# Named groups
match = re.search(r"(?P<name>[\w\s]+) \((?P<email>[\w.]+@[\w.]+)\)", text)
if match:
    print(f"Name: {match.group('name')}")  # Output: Name: John Smith
    print(f"Email: {match.group('email')}")  # Output: Email: john.smith@example.com
```

### Compiling Regular Expressions

For better performance when using the same pattern multiple times, you can compile it:

```python
import re

# Compile a regex pattern
pattern = re.compile(r"\b\w+\b")

text = "Hello world, how are you?"

# Use the compiled pattern
words = pattern.findall(text)
print(words)  # Output: ['Hello', 'world', 'how', 'are', 'you']

# Match at the beginning of the string
pattern = re.compile(r"^Hello")
print(pattern.match(text) is not None)  # Output: True

# Search anywhere in the string
pattern = re.compile(r"world")
print(pattern.search(text) is not None)  # Output: True
```

## Working with Dates and Times

Python's `datetime` module provides classes for working with dates and times.

### Basic Date and Time Operations

```python
from datetime import datetime, date, time, timedelta

# Current date and time
now = datetime.now()
print(f"Current datetime: {now}")

# Creating date objects
today = date.today()
print(f"Today's date: {today}")

# Creating time objects
current_time = time(hour=15, minute=30, second=45)
print(f"Time: {current_time}")

# Creating datetime objects
specific_datetime = datetime(2023, 12, 31, 23, 59, 59)
print(f"Specific datetime: {specific_datetime}")

# Date arithmetic
tomorrow = today + timedelta(days=1)
print(f"Tomorrow: {tomorrow}")

next_week = today + timedelta(weeks=1)
print(f"Next week: {next_week}")

# Time difference
time_diff = specific_datetime - now
print(f"Time until New Year: {time_diff}")
```

### Formatting Dates and Times

```python
from datetime import datetime

now = datetime.now()

# Format using strftime()
formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
print(f"Formatted: {formatted_date}")

formatted_date = now.strftime("%A, %B %d, %Y")
print(f"Formatted: {formatted_date}")  # e.g., "Monday, January 01, 2023"

# Common format codes:
# %Y - Year with century (e.g., 2023)
# %m - Month as a zero-padded number (e.g., 01)
# %d - Day of the month as a zero-padded number (e.g., 01)
# %H - Hour (24-hour clock) as a zero-padded number (e.g., 13)
# %M - Minute as a zero-padded number (e.g., 05)
# %S - Second as a zero-padded number (e.g., 09)
# %A - Weekday name (e.g., Monday)
# %B - Month name (e.g., January)
```

### Parsing Dates and Times

```python
from datetime import datetime

# Parse a date string
date_string = "2023-12-31 23:59:59"
parsed_date = datetime.strptime(date_string, "%Y-%m-%d %H:%M:%S")
print(f"Parsed date: {parsed_date}")

# Parse different formats
date_string = "December 31, 2023"
parsed_date = datetime.strptime(date_string, "%B %d, %Y")
print(f"Parsed date: {parsed_date}")
```

### Working with Time Zones

The `datetime` module doesn't handle time zones by default. For time zone support, you can use the `pytz` library:

```python
from datetime import datetime
import pytz

# Create a timezone-aware datetime
utc_now = datetime.now(pytz.UTC)
print(f"UTC time: {utc_now}")

# Convert to a different timezone
ny_timezone = pytz.timezone('America/New_York')
ny_time = utc_now.astimezone(ny_timezone)
print(f"New York time: {ny_time}")

# List available timezones
print(pytz.all_timezones[:5])  # Print first 5 timezones
```

## Virtual Environments

Virtual environments are isolated Python environments that allow you to install packages without affecting the global Python installation.

### Creating and Using Virtual Environments

#### Using venv (built-in)

```bash
# Create a virtual environment
python -m venv myenv

# Activate the virtual environment
# On Windows:
myenv\Scripts\activate
# On Unix or MacOS:
source myenv/bin/activate

# Deactivate the virtual environment
deactivate
```

#### Using virtualenv (third-party)

```bash
# Install virtualenv
pip install virtualenv

# Create a virtual environment
virtualenv myenv

# Activate the virtual environment (same as venv)
```

### Managing Packages in Virtual Environments

```bash
# Install packages
pip install package_name

# Install specific ver
(Content truncated due to size limit. Use line ranges to read in chunks)