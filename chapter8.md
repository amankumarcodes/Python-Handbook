# Chapter 8: Error Handling

## Types of Errors

When writing Python programs, you'll inevitably encounter errors. Understanding the different types of errors and how to handle them is crucial for developing robust applications. Python errors generally fall into three categories:

### Syntax Errors

Syntax errors occur when the Python parser is unable to understand your code due to incorrect syntax. These errors are detected during the parsing phase, before the code is executed.

```python
# Syntax error example: missing closing parenthesis
print("Hello, World!"
```

When you run this code, Python will display an error message like:
```
  File "example.py", line 1
    print("Hello, World!"
                        ^
SyntaxError: unexpected EOF while parsing
```

Common syntax errors include:
- Missing colons after conditional statements or loop declarations
- Incorrect indentation
- Unmatched parentheses, brackets, or quotes
- Invalid assignment operations
- Using Python keywords as variable names

Syntax errors must be fixed before your code can run.

### Logical Errors

Logical errors (also called semantic errors) occur when your code runs without raising exceptions but produces incorrect results due to flawed logic. These are often the most difficult errors to detect because Python doesn't report them as errors.

```python
# Logical error example: calculating average incorrectly
def calculate_average(numbers):
    total = 0
    for num in numbers:
        total += num
    return total  # Forgot to divide by the count of numbers
```

In this example, the function will run without errors but will return the sum instead of the average.

Common logical errors include:
- Off-by-one errors (e.g., incorrect loop boundaries)
- Using the wrong operator (e.g., `+` instead of `*`)
- Incorrect algorithm implementation
- Misunderstanding of requirements

Logical errors require careful debugging and testing to identify and fix.

### Runtime Errors (Exceptions)

Runtime errors, or exceptions, occur during program execution when something unexpected happens. Unlike syntax errors, the code is syntactically correct but encounters a problem during execution.

```python
# Runtime error example: division by zero
numerator = 10
denominator = 0
result = numerator / denominator  # Raises ZeroDivisionError
```

When you run this code, Python will display an error message like:
```
Traceback (most recent call last):
  File "example.py", line 3, in <module>
    result = numerator / denominator
ZeroDivisionError: division by zero
```

Common runtime errors include:
- `ZeroDivisionError`: Attempting to divide by zero
- `TypeError`: Performing an operation on incompatible types
- `NameError`: Trying to use a variable that hasn't been defined
- `IndexError`: Trying to access an index that's out of range
- `KeyError`: Trying to access a dictionary key that doesn't exist
- `FileNotFoundError`: Trying to open a file that doesn't exist
- `ValueError`: Passing an invalid value to a function
- `AttributeError`: Trying to access an attribute that doesn't exist

Runtime errors can be handled using exception handling mechanisms.

## Exception Handling

Exception handling allows you to gracefully manage runtime errors, preventing your program from crashing and providing appropriate responses to error conditions.

### try-except Blocks

The basic structure for exception handling in Python is the `try-except` block:

```python
try:
    # Code that might raise an exception
    result = 10 / 0
except:
    # Code to handle the exception
    print("An error occurred")
```

When an exception occurs in the `try` block, Python immediately jumps to the corresponding `except` block, skipping any remaining code in the `try` block.

### Multiple except Blocks

You can handle different types of exceptions with separate `except` blocks:

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
    print(f"Result: {result}")
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError:
    print("Error: Please enter a valid number")
```

You can also catch multiple exception types in a single `except` block:

```python
try:
    # Code that might raise exceptions
    pass
except (ZeroDivisionError, ValueError) as e:
    print(f"An error occurred: {e}")
```

The `as` keyword allows you to capture the exception object, which contains details about the error.

### try-except-else

The `else` clause in a `try-except` block executes if no exceptions are raised in the `try` block:

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError:
    print("Error: Please enter a valid number")
else:
    print(f"Result: {result}")  # Only executes if no exceptions occurred
```

The `else` clause is useful for code that should run only if the `try` block succeeds.

### try-except-finally

The `finally` clause in a `try-except` block always executes, regardless of whether an exception occurred:

```python
try:
    file = open("example.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("Error: File not found")
finally:
    # This will always execute, even if an exception occurred
    if 'file' in locals() and not file.closed:
        file.close()
        print("File closed")
```

The `finally` clause is ideal for cleanup operations, such as closing files or releasing resources.

### Combining else and finally

You can use both `else` and `finally` in the same `try-except` block:

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError:
    print("Error: Please enter a valid number")
else:
    print(f"Result: {result}")  # Executes if no exceptions occurred
finally:
    print("Execution completed")  # Always executes
```

## Raising Exceptions

You can deliberately raise exceptions in your code using the `raise` statement:

```python
def set_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age

try:
    user_age = set_age(-5)
except ValueError as e:
    print(f"Error: {e}")
```

Raising exceptions is useful when:
- You detect an error condition that should be handled by the calling code
- You want to provide specific error messages for invalid inputs
- You need to enforce certain constraints or preconditions

### Re-raising Exceptions

Sometimes you want to catch an exception, perform some action, and then re-raise the exception for the caller to handle:

```python
try:
    # Some code that might raise an exception
    result = 10 / 0
except ZeroDivisionError:
    print("Logging: Division by zero occurred")
    raise  # Re-raise the caught exception
```

You can also catch one exception and raise a different one:

```python
try:
    value = int("abc")
except ValueError:
    raise RuntimeError("Failed to convert string to integer")
```

## Creating Custom Exceptions

You can create your own exception classes by inheriting from the built-in `Exception` class or one of its subclasses:

```python
class InsufficientFundsError(Exception):
    """Raised when a withdrawal exceeds the available balance"""
    pass

class BankAccount:
    def __init__(self, balance=0):
        self.balance = balance
        
    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError(f"Cannot withdraw ${amount}. Only ${self.balance} available.")
        self.balance -= amount
        return amount

try:
    account = BankAccount(100)
    account.withdraw(150)
except InsufficientFundsError as e:
    print(f"Error: {e}")
```

Custom exceptions help make your code more readable and allow for more specific error handling.

## Best Practices for Error Handling

### 1. Be Specific with Exception Types

Avoid using bare `except` clauses, which catch all exceptions:

```python
# Not recommended
try:
    # Code that might raise exceptions
    pass
except:  # Catches all exceptions, including KeyboardInterrupt, SystemExit, etc.
    print("An error occurred")

# Recommended
try:
    # Code that might raise exceptions
    pass
except Exception as e:  # Catches only exceptions derived from Exception
    print(f"An error occurred: {e}")
```

### 2. Handle Exceptions at the Appropriate Level

Catch exceptions where you can handle them appropriately:

```python
def read_file_content(filename):
    try:
        with open(filename, 'r') as file:
            return file.read()
    except FileNotFoundError:
        # Handle the specific error at this level
        return f"File '{filename}' not found"

# Instead of:
def read_file_content_bad(filename):
    # Let the exception propagate to the caller
    with open(filename, 'r') as file:
        return file.read()

try:
    content = read_file_content_bad("nonexistent.txt")
except FileNotFoundError:
    content = "File not found"
```

### 3. Provide Meaningful Error Messages

Error messages should be clear and informative:

```python
def divide(a, b):
    if b == 0:
        raise ValueError("Division by zero is not allowed")
    return a / b
```

### 4. Use Context Managers for Resource Cleanup

Use context managers (`with` statement) for resources that need cleanup:

```python
# Recommended
with open("example.txt", "r") as file:
    content = file.read()
# File is automatically closed

# Instead of:
file = open("example.txt", "r")
try:
    content = file.read()
finally:
    file.close()
```

### 5. Log Exceptions

For larger applications, log exceptions for debugging:

```python
import logging

logging.basicConfig(filename='app.log', level=logging.ERROR)

try:
    # Code that might raise exceptions
    result = 10 / 0
except Exception as e:
    logging.error(f"An error occurred: {e}", exc_info=True)
    # Handle the exception or re-raise it
```

## Debugging Techniques

Debugging is the process of finding and fixing errors in your code. Python provides several tools and techniques for effective debugging:

### 1. Print Statements

The simplest debugging technique is to insert print statements to display variable values and program flow:

```python
def calculate_total(items):
    print(f"Items received: {items}")  # Debug print
    total = 0
    for item in items:
        print(f"Processing item: {item}")  # Debug print
        total += item['price'] * item['quantity']
        print(f"Running total: {total}")  # Debug print
    return total
```

### 2. The assert Statement

The `assert` statement tests if a condition is true and raises an `AssertionError` if it's not:

```python
def calculate_average(numbers):
    assert len(numbers) > 0, "Cannot calculate average of empty list"
    return sum(numbers) / len(numbers)
```

### 3. The pdb Module (Python Debugger)

Python's built-in debugger, `pdb`, allows for interactive debugging:

```python
import pdb

def complex_function(data):
    result = []
    for item in data:
        pdb.set_trace()  # Start the debugger here
        # Process item
        processed = item * 2
        result.append(processed)
    return result

complex_function([1, 2, 3])
```

When the debugger starts, you can:
- Examine variable values
- Step through code line by line
- Set breakpoints
- Execute arbitrary Python code

Common pdb commands:
- `n` (next): Execute the current line and move to the next line
- `s` (step): Step into a function call
- `c` (continue): Continue execution until the next breakpoint
- `p` (print): Print the value of an expression
- `q` (quit): Quit the debugger

### 4. Using Breakpoints (Python 3.7+)

In Python 3.7 and later, you can use the `breakpoint()` function instead of `import pdb; pdb.set_trace()`:

```python
def complex_function(data):
    result = []
    for item in data:
        breakpoint()  # Start the debugger here
        # Process item
        processed = item * 2
        result.append(processed)
    return result
```

### 5. Using IDEs with Debugging Support

Modern IDEs like PyCharm, Visual Studio Code, and others provide graphical debugging interfaces that allow you to:
- Set breakpoints by clicking in the margin
- Step through code using buttons or keyboard shortcuts
- Inspect variables in a dedicated panel
- View the call stack
- Evaluate expressions

### 6. Logging

For more complex applications, use the `logging` module instead of print statements:

```python
import logging

# Configure logging
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    filename='app.log'
)

def process_data(data):
    logging.debug(f"Processing data: {data}")
    try:
        result = data['value'] * 2
        logging.info(f"Processed data successfully: {result}")
        return result
    except KeyError:
        logging.error("KeyError: 'value' key not found in data")
        return None
```

Logging levels, from lowest to highest severity:
- `DEBUG`: Detailed information, typically useful only for diagnosing problems
- `INFO`: Confirmation that things are working as expected
- `WARNING`: An indication that something unexpected happened, or may happen in the near future
- `ERROR`: Due to a more serious problem, the software has not been able to perform some function
- `CRITICAL`: A serious error, indicating that the program itself may be unable to continue running

## Practice Set

### Review Questions
1. What is the difference between syntax errors, logical errors, and runtime errors?
2. Explain the purpose of the `try`, `except`, `else`, and `finally` clauses in exception handling.
3. When would you create a custom exception class instead of using built-in exceptions?
4. What are some best practices for error handling in Python?

### Coding Exercises
1. Write a function that takes a filename as input and returns the content of the file. Handle the case where the file doesn't exist by returning an appropriate message.
2. Create a function that converts a string to an integer. Handle the case where the string cannot be converted and return 0 in that case.
3. Write a program that asks the user for two numbers and performs division. Handle potential errors such as invalid input or division by zero.
4. Create a custom exception class called `NegativeValueError` and use it in a function that calculates the square root of a number, raising the exception if the input is negative.

### Challenge Problem
Create a simple banking system with error handling:
1. Define custom exceptions for various error conditions (e.g., `InsufficientFundsError`, `NegativeAmountError`, `AccountNotFoundError`)
2. Implement a `BankAccount` class with methods for deposit, withdrawal, and transfer
3. Implement a `Bank` class that manages multiple accounts
4. Add appropriate error handling for all operations
5. Include logging to record all transactions and errors
6. Create a simple command-line interface to interact with the banking system
7. Ensure that the system handles all potential error conditions gracefully
