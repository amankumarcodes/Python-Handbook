# Chapter 2: Variables, Data Types, and Operators

## Variables in Python

Variables are containers for storing data values. In Python, a variable is created the moment you first assign a value to it. Unlike some other programming languages, Python has no command for declaring a variable.

### Naming Conventions and Rules

When naming variables in Python, you must follow these rules:
* Variable names must start with a letter or underscore
* Variable names cannot start with a number
* Variable names can only contain alphanumeric characters and underscores (A-z, 0-9, and _)
* Variable names are case-sensitive (`age`, `Age`, and `AGE` are three different variables)

Python conventions (PEP 8) recommend:
* Use lowercase letters for variable names
* Use underscores to separate words in variable names (snake_case)
* Choose descriptive names that explain what the variable represents

```python
# Good variable names
user_name = "John"
age = 25
is_student = True

# Poor variable names
a = "John"  # Not descriptive
UserName = "John"  # Not following snake_case convention
```

### Variable Assignment

In Python, you assign values to variables using the equal sign (`=`):

```python
x = 10  # x is assigned the integer value 10
name = "Alice"  # name is assigned the string value "Alice"
is_valid = True  # is_valid is assigned the boolean value True
```

You can also assign a new value to an existing variable:

```python
counter = 1
print(counter)  # Output: 1
counter = 2
print(counter)  # Output: 2
```

### Multiple Assignment

Python allows you to assign values to multiple variables in a single line:

```python
# Assign the same value to multiple variables
x = y = z = 0
print(x, y, z)  # Output: 0 0 0

# Assign different values to multiple variables
a, b, c = 5, 10, 15
print(a, b, c)  # Output: 5 10 15

# Swap values (without using a temporary variable)
a, b = b, a
print(a, b)  # Output: 10 5
```

## Data Types

Python has several built-in data types. Understanding these types is crucial for effective programming.

### Numeric Types

#### Integer (int)
Integers are whole numbers without a decimal point:

```python
age = 25
negative_number = -10
zero = 0

print(type(age))  # Output: <class 'int'>
```

#### Float
Floating-point numbers have a decimal point or use scientific notation:

```python
height = 5.11
pi_value = 3.14159
scientific = 1.23e4  # 12300.0

print(type(height))  # Output: <class 'float'>
```

#### Complex
Complex numbers have a real and imaginary part:

```python
complex_num = 3 + 4j
print(type(complex_num))  # Output: <class 'complex'>
print(complex_num.real)  # Output: 3.0
print(complex_num.imag)  # Output: 4.0
```

### Strings

Strings are sequences of characters enclosed in quotes (single, double, or triple):

```python
name = "Alice"
message = 'Hello, World!'
multi_line = """This is a
multi-line string"""

# String operations
print(len(name))  # Output: 5 (length of string)
print(name[0])  # Output: A (first character)
print(name[-1])  # Output: e (last character)
print(name[1:3])  # Output: li (slicing)
print(name + " Smith")  # Output: Alice Smith (concatenation)
print(name * 3)  # Output: AliceAliceAlice (repetition)
```

### Boolean

Boolean values represent truth values with two constants: `True` and `False`:

```python
is_student = True
has_license = False

print(type(is_student))  # Output: <class 'bool'>
```

Boolean values are often the result of comparisons:

```python
x = 5
print(x > 3)  # Output: True
print(x == 10)  # Output: False
```

### None Type

`None` is a special constant in Python that represents the absence of a value or a null value:

```python
result = None
print(result)  # Output: None
print(type(result))  # Output: <class 'NoneType'>
```

## Type Conversion

Python allows you to convert between different data types:

### Implicit Type Conversion

Python automatically converts one data type to another if needed:

```python
x = 10  # int
y = 3.14  # float
result = x + y  # int is implicitly converted to float
print(result)  # Output: 13.14
print(type(result))  # Output: <class 'float'>
```

### Explicit Type Conversion (Type Casting)

You can explicitly convert from one type to another using built-in functions:

```python
# Convert to integer
x = int(3.14)  # 3
y = int("10")  # 10

# Convert to float
a = float(5)  # 5.0
b = float("3.14")  # 3.14

# Convert to string
c = str(10)  # "10"
d = str(3.14)  # "3.14"

# Convert to boolean
e = bool(1)  # True
f = bool(0)  # False
g = bool("")  # False (empty string)
h = bool("Hello")  # True (non-empty string)
```

## Constants in Python

Python doesn't have built-in constant types, but by convention, constants are written in all capital letters:

```python
PI = 3.14159
MAX_CONNECTIONS = 1000
DATABASE_URL = "mongodb://localhost:27017"
```

These variables aren't true constants—they can still be changed—but the all-caps naming signals to other programmers that they shouldn't be modified.

## Operators

Operators are special symbols that perform operations on variables and values.

### Arithmetic Operators

Used for mathematical operations:

```python
a = 10
b = 3

print(a + b)  # Addition: 13
print(a - b)  # Subtraction: 7
print(a * b)  # Multiplication: 30
print(a / b)  # Division: 3.3333...
print(a // b)  # Floor division: 3
print(a % b)  # Modulus (remainder): 1
print(a ** b)  # Exponentiation: 1000
```

### Comparison Operators

Used to compare values:

```python
x = 5
y = 10

print(x == y)  # Equal to: False
print(x != y)  # Not equal to: True
print(x > y)   # Greater than: False
print(x < y)   # Less than: True
print(x >= y)  # Greater than or equal to: False
print(x <= y)  # Less than or equal to: True
```

### Logical Operators

Used to combine conditional statements:

```python
p = True
q = False

print(p and q)  # Logical AND: False
print(p or q)   # Logical OR: True
print(not p)    # Logical NOT: False
```

### Assignment Operators

Used to assign values to variables:

```python
x = 10  # Simple assignment

# Compound assignment operators
x += 5   # Equivalent to: x = x + 5
print(x)  # Output: 15

x -= 3   # Equivalent to: x = x - 3
print(x)  # Output: 12

x *= 2   # Equivalent to: x = x * 2
print(x)  # Output: 24

x /= 4   # Equivalent to: x = x / 4
print(x)  # Output: 6.0

x //= 2  # Equivalent to: x = x // 2
print(x)  # Output: 3.0

x %= 2   # Equivalent to: x = x % 2
print(x)  # Output: 1.0

y = 2
y **= 3  # Equivalent to: y = y ** 3
print(y)  # Output: 8
```

### Bitwise Operators

Used to perform bit-level operations:

```python
a = 10  # 1010 in binary
b = 4   # 0100 in binary

print(a & b)   # Bitwise AND: 0 (0000)
print(a | b)   # Bitwise OR: 14 (1110)
print(a ^ b)   # Bitwise XOR: 14 (1110)
print(~a)      # Bitwise NOT: -11 (invert all bits and add 1)
print(a << 1)  # Left shift: 20 (10100)
print(a >> 1)  # Right shift: 5 (0101)
```

### Identity Operators

Used to compare the memory locations of two objects:

```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x

print(x is z)     # True (x and z refer to the same object)
print(x is y)     # False (x and y are different objects)
print(x is not y) # True (x and y are different objects)
```

### Membership Operators

Used to test if a sequence contains a specific value:

```python
fruits = ["apple", "banana", "cherry"]

print("apple" in fruits)      # True
print("orange" in fruits)     # False
print("orange" not in fruits) # True
```

## Operator Precedence and Associativity

Operator precedence determines the order in which operations are performed:

1. Parentheses `()`
2. Exponentiation `**`
3. Unary plus `+x`, unary minus `-x`, bitwise NOT `~x`
4. Multiplication `*`, division `/`, floor division `//`, modulus `%`
5. Addition `+`, subtraction `-`
6. Bitwise shifts `<<`, `>>`
7. Bitwise AND `&`
8. Bitwise XOR `^`
9. Bitwise OR `|`
10. Comparisons `==`, `!=`, `>`, `>=`, `<`, `<=`, `is`, `is not`, `in`, `not in`
11. Logical NOT `not`
12. Logical AND `and`
13. Logical OR `or`

```python
# Example of precedence
result = 2 + 3 * 4  # Multiplication happens first
print(result)  # Output: 14

# Using parentheses to change precedence
result = (2 + 3) * 4  # Addition happens first
print(result)  # Output: 20
```

## Input and Output Functions

### print() Function

The `print()` function displays output to the console:

```python
print("Hello, World!")  # Simple string
print(10)  # Number
print(True)  # Boolean

# Multiple items
print("Name:", "Alice", "Age:", 25)  # Output: Name: Alice Age: 25

# Formatting with f-strings (Python 3.6+)
name = "Bob"
age = 30
print(f"Name: {name}, Age: {age}")  # Output: Name: Bob, Age: 30

# Using sep and end parameters
print("Hello", "World", sep="-")  # Output: Hello-World
print("Hello", end="! ")
print("World")  # Output: Hello! World
```

### input() Function

The `input()` function reads a line from the console:

```python
# Basic input
name = input("Enter your name: ")
print(f"Hello, {name}!")

# Converting input to other types
age = int(input("Enter your age: "))
print(f"In 5 years, you will be {age + 5} years old.")

height = float(input("Enter your height in meters: "))
print(f"Your height is {height} meters.")
```

## Practice Set

### Review Questions
1. What is the difference between an integer and a float in Python?
2. Explain the concept of variable assignment in Python.
3. What are the rules for naming variables in Python?
4. Describe the difference between implicit and explicit type conversion.

### Coding Exercises
1. Create variables of each basic data type (int, float, string, boolean) and print their types.
2. Write a program that calculates the area of a rectangle using variables for length and width.
3. Create a program that converts temperature from Celsius to Fahrenheit using the formula: F = (C × 9/5) + 32.
4. Write a program that takes a user's name and age as input, then outputs a message including how old they will be in 10 years.

### Challenge Problem
Create a program that calculates the Body Mass Index (BMI) of a person. The program should:
1. Ask for the user's weight in kilograms and height in meters
2. Calculate the BMI using the formula: BMI = weight / (height^2)
3. Display the BMI value
4. Provide a basic interpretation of the BMI value:
   - Below 18.5: Underweight
   - 18.5 to 24.9: Normal weight
   - 25 to 29.9: Overweight
   - 30 and above: Obesity
