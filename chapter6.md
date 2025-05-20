# Chapter 6: Data Structures (Lists, Tuples, Dictionaries)

## Lists

Lists are one of the most versatile and commonly used data structures in Python. They are ordered, mutable (changeable), and allow duplicate elements.

### Creating and Accessing Lists

Lists are created by placing elements inside square brackets `[]`, separated by commas:

```python
# Creating lists
empty_list = []
numbers = [1, 2, 3, 4, 5]
mixed_list = [1, "Hello", 3.14, True]
nested_list = [1, [2, 3], [4, 5, 6]]

# Accessing elements using indexing (0-based)
print(numbers[0])      # Output: 1 (first element)
print(numbers[2])      # Output: 3 (third element)
print(numbers[-1])     # Output: 5 (last element)
print(numbers[-2])     # Output: 4 (second-to-last element)

# Accessing elements in nested lists
print(nested_list[1][0])  # Output: 2
print(nested_list[2][1])  # Output: 5
```

### List Methods and Operations

Python provides many built-in methods to work with lists:

```python
fruits = ["apple", "banana", "cherry"]

# Adding elements
fruits.append("orange")        # Add to the end
print(fruits)  # Output: ['apple', 'banana', 'cherry', 'orange']

fruits.insert(1, "blueberry")  # Insert at specific position
print(fruits)  # Output: ['apple', 'blueberry', 'banana', 'cherry', 'orange']

# Removing elements
fruits.remove("banana")        # Remove by value
print(fruits)  # Output: ['apple', 'blueberry', 'cherry', 'orange']

popped = fruits.pop()          # Remove and return the last item
print(popped)  # Output: orange
print(fruits)  # Output: ['apple', 'blueberry', 'cherry']

popped_index = fruits.pop(1)   # Remove and return item at index
print(popped_index)  # Output: blueberry
print(fruits)  # Output: ['apple', 'cherry']

# Other useful methods
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
numbers.sort()                 # Sort in-place
print(numbers)  # Output: [1, 1, 2, 3, 4, 5, 6, 9]

numbers.reverse()              # Reverse in-place
print(numbers)  # Output: [9, 6, 5, 4, 3, 2, 1, 1]

count = numbers.count(1)       # Count occurrences
print(count)  # Output: 2

index = numbers.index(5)       # Find index of first occurrence
print(index)  # Output: 2

numbers.clear()                # Remove all items
print(numbers)  # Output: []
```

### List Operations

```python
# Concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # Output: [1, 2, 3, 4, 5, 6]

# Repetition
repeated = list1 * 3
print(repeated)  # Output: [1, 2, 3, 1, 2, 3, 1, 2, 3]

# Membership testing
print(2 in list1)      # Output: True
print(5 in list1)      # Output: False

# Length
print(len(combined))   # Output: 6
```

### List Slicing

List slicing allows you to access a specific range of elements:

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Basic slicing: list[start:stop]
# Returns elements from index 'start' to 'stop-1'
print(numbers[2:5])    # Output: [2, 3, 4]

# Omitting start (defaults to 0)
print(numbers[:5])     # Output: [0, 1, 2, 3, 4]

# Omitting stop (defaults to length of list)
print(numbers[7:])     # Output: [7, 8, 9]

# Negative indices
print(numbers[-5:-2])  # Output: [5, 6, 7]

# Step parameter: list[start:stop:step]
print(numbers[1:8:2])  # Output: [1, 3, 5, 7]

# Reverse a list
print(numbers[::-1])   # Output: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

### Nested Lists

Lists can contain other lists, creating multi-dimensional structures:

```python
# Creating a 3x3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Accessing elements
print(matrix[0][0])  # Output: 1 (first row, first column)
print(matrix[1][2])  # Output: 6 (second row, third column)

# Modifying elements
matrix[0][1] = 20
print(matrix)  # Output: [[1, 20, 3], [4, 5, 6], [7, 8, 9]]

# Iterating through a matrix
for row in matrix:
    for element in row:
        print(element, end=" ")
    print()  # New line after each row
# Output:
# 1 20 3
# 4 5 6
# 7 8 9
```

## Tuples

Tuples are similar to lists but are immutable (cannot be changed after creation). They are typically used to store collections of related data.

### Creating and Accessing Tuples

Tuples are created by placing elements inside parentheses `()`, separated by commas:

```python
# Creating tuples
empty_tuple = ()
single_item = (1,)  # Note the comma for single-item tuples
coordinates = (10, 20)
person = ("Alice", 30, "New York")
nested_tuple = (1, (2, 3), (4, 5, 6))

# Accessing elements (same as lists)
print(coordinates[0])      # Output: 10
print(person[1])           # Output: 30
print(nested_tuple[1][0])  # Output: 2
```

### Tuple Methods and Operations

Since tuples are immutable, they have fewer methods than lists:

```python
numbers = (1, 2, 3, 2, 4, 2)

# Counting occurrences
count = numbers.count(2)
print(count)  # Output: 3

# Finding index of first occurrence
index = numbers.index(3)
print(index)  # Output: 2

# Length
print(len(numbers))  # Output: 6

# Concatenation
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)
combined = tuple1 + tuple2
print(combined)  # Output: (1, 2, 3, 4, 5, 6)

# Repetition
repeated = tuple1 * 3
print(repeated)  # Output: (1, 2, 3, 1, 2, 3, 1, 2, 3)

# Membership testing
print(2 in tuple1)  # Output: True
print(5 in tuple1)  # Output: False
```

### Immutability of Tuples

Unlike lists, tuples cannot be modified after creation:

```python
coordinates = (10, 20)

# This will raise an error
# coordinates[0] = 15  # TypeError: 'tuple' object does not support item assignment

# But you can create a new tuple
coordinates = (15, 20)
print(coordinates)  # Output: (15, 20)
```

### When to Use Tuples vs Lists

Use tuples when:
- You need an immutable sequence (data that shouldn't change)
- You want to use the data as dictionary keys (lists can't be used as keys)
- You want to ensure data integrity (preventing accidental modifications)
- You're working with multiple return values from a function

Use lists when:
- You need a mutable sequence (data that might change)
- You need to add or remove elements frequently
- You need to sort or reverse the elements in-place

```python
# Tuple as dictionary key (works)
locations = {
    (40.7128, -74.0060): "New York",
    (34.0522, -118.2437): "Los Angeles"
}
print(locations[(40.7128, -74.0060)])  # Output: New York

# List as dictionary key (raises error)
# locations = {[40.7128, -74.0060]: "New York"}  # TypeError: unhashable type: 'list'

# Multiple return values as tuple
def get_dimensions():
    return 1920, 1080  # Returns a tuple

width, height = get_dimensions()  # Tuple unpacking
print(f"Width: {width}, Height: {height}")  # Output: Width: 1920, Height: 1080
```

## Dictionaries

Dictionaries are unordered collections of key-value pairs. They are mutable and optimized for retrieving values when the key is known.

### Creating and Accessing Dictionaries

Dictionaries are created using curly braces `{}` with key-value pairs separated by colons:

```python
# Creating dictionaries
empty_dict = {}
person = {"name": "Alice", "age": 30, "city": "New York"}
mixed_keys = {1: "one", "two": 2, (3, 4): "tuple key"}

# Accessing values using keys
print(person["name"])   # Output: Alice
print(person["age"])    # Output: 30

# Using get() method (safer, returns None or default if key doesn't exist)
print(person.get("city"))         # Output: New York
print(person.get("country"))      # Output: None
print(person.get("country", "Unknown"))  # Output: Unknown
```

### Dictionary Methods

Python provides many useful methods for working with dictionaries:

```python
person = {"name": "Alice", "age": 30, "city": "New York"}

# Adding or updating items
person["email"] = "alice@example.com"  # Add new key-value pair
person["age"] = 31                     # Update existing value
print(person)  # Output: {'name': 'Alice', 'age': 31, 'city': 'New York', 'email': 'alice@example.com'}

# Removing items
removed_value = person.pop("city")     # Remove and return value
print(removed_value)  # Output: New York
print(person)  # Output: {'name': 'Alice', 'age': 31, 'email': 'alice@example.com'}

# Get all keys, values, or items
keys = person.keys()
values = person.values()
items = person.items()

print(list(keys))    # Output: ['name', 'age', 'email']
print(list(values))  # Output: ['Alice', 31, 'alice@example.com']
print(list(items))   # Output: [('name', 'Alice'), ('age', 31), ('email', 'alice@example.com')]

# Check if key exists
print("name" in person)  # Output: True
print("city" in person)  # Output: False

# Merging dictionaries
person.update({"phone": "555-1234", "age": 32})
print(person)  # Output: {'name': 'Alice', 'age': 32, 'email': 'alice@example.com', 'phone': '555-1234'}

# Clear all items
person.clear()
print(person)  # Output: {}
```

### Dictionary Comprehensions

Similar to list comprehensions, dictionary comprehensions provide a concise way to create dictionaries:

```python
# Create a dictionary of squares
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Create a dictionary with conditions
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # Output: {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# Convert two lists to a dictionary
keys = ["a", "b", "c"]
values = [1, 2, 3]
dict_from_lists = {k: v for k, v in zip(keys, values)}
print(dict_from_lists)  # Output: {'a': 1, 'b': 2, 'c': 3}
```

### Nested Dictionaries

Dictionaries can contain other dictionaries, allowing for complex data structures:

```python
# Nested dictionary
employees = {
    "Alice": {
        "id": 101,
        "role": "Developer",
        "salary": 75000
    },
    "Bob": {
        "id": 102,
        "role": "Designer",
        "salary": 70000
    }
}

# Accessing nested values
print(employees["Alice"]["role"])  # Output: Developer
print(employees["Bob"]["salary"])  # Output: 70000

# Modifying nested values
employees["Alice"]["salary"] = 80000
print(employees["Alice"])  # Output: {'id': 101, 'role': 'Developer', 'salary': 80000}

# Adding a new nested dictionary
employees["Charlie"] = {"id": 103, "role": "Manager", "salary": 90000}
```

## Sets

Sets are unordered collections of unique elements. They are useful for membership testing, removing duplicates, and mathematical operations like union and intersection.

### Creating and Using Sets

Sets are created using curly braces `{}` or the `set()` constructor:

```python
# Creating sets
empty_set = set()  # Note: {} creates an empty dictionary, not a set
fruits = {"apple", "banana", "cherry"}
numbers = set([1, 2, 2, 3, 3, 3])  # Removes duplicates
print(numbers)  # Output: {1, 2, 3}

# Adding and removing elements
fruits.add("orange")
print(fruits)  # Output: {'apple', 'banana', 'cherry', 'orange'}

fruits.remove("banana")  # Raises KeyError if element doesn't exist
print(fruits)  # Output: {'apple', 'cherry', 'orange'}

fruits.discard("kiwi")  # No error if element doesn't exist
print(fruits)  # Output: {'apple', 'cherry', 'orange'}

popped = fruits.pop()  # Remove and return an arbitrary element
print(popped)  # Output could be any element from the set
print(fruits)  # Output: Set with one element removed

fruits.clear()  # Remove all elements
print(fruits)  # Output: set()
```

### Set Operations

Sets support mathematical operations like union, intersection, difference, and symmetric difference:

```python
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}

# Union (all elements from both sets)
print(A | B)        # Output: {1, 2, 3, 4, 5, 6, 7, 8}
print(A.union(B))   # Output: {1, 2, 3, 4, 5, 6, 7, 8}

# Intersection (elements common to both sets)
print(A & B)        # Output: {4, 5}
print(A.intersection(B))  # Output: {4, 5}

# Difference (elements in A but not in B)
print(A - B)        # Output: {1, 2, 3}
print(A.difference(B))  # Output: {1, 2, 3}

# Symmetric difference (elements in either A or B but not both)
print(A ^ B)        # Output: {1, 2, 3, 6, 7, 8}
print(A.symmetric_difference(B))  # Output: {1, 2, 3, 6, 7, 8}

# Subset and superset
C = {1, 2}
print(C.issubset(A))     # Output: True (all elements of C are in A)
print(A.issuperset(C))   # Output: True (A contains all elements of C)
```

### Set Comprehensions

Similar to list and dictionary comprehensions, set comprehensions provide a concise way to create sets:

```python
# Create a set of squares
squares = {x**2 for x in range(1, 6)}
print(squares)  # Output: {1, 4, 9, 16, 25}

# Create a set with conditions
even_squares = {x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # Output: {4, 16, 36, 64, 100}
```

## Collections Module

The `collections` module provides specialized container datatypes that extend the functionality of Python's built-in containers.

### Counter

`Counter` is a dict subclass for counting hashable objects:

```python
from collections import Counter

# Count occurrences of elements
text = "mississippi"
counter = Counter(text)
print(counter)  # Output: Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})

# Most common elements
print(counter.most_common(2))  # Output: [('i', 4), ('s', 4)]

# Update counts
counter.update("missouri")
print(counter)  # Output: Counter({'i': 6, 's': 6, 'm': 2, 'p': 2, 'o': 1, 'u': 1, 'r': 1})

# Arithmetic operations
c1 = Counter(a=3, b=1)
c2 = Counter(a=1, b=2)
print(c1 + c2)  # Output: Counter({'a': 4, 'b': 3})
print(c1 - c2)  # Output: Counter({'a': 2})
```

### defaultdict

`defaultdict` is a dict subclass that calls a factory function to supply missing values:

```python
from collections import defaultdict

# defaultdict with int factory (default value 0)
word_count = defaultdict(int)
for word in ["apple", "banana", "apple", "cherry", "banana", "apple"]:
    word_count[word] += 1

print(word_count)  # Output: defaultdict(<class 'int'>, {'apple': 3, 'banana': 2, 'cherry': 1})

# defaultdict with list factory (default value [])
grouped_words = defaultdict(list)
words = ["apple", "bat", "car", "apple", "bear", "cat"]
for word in words:
    grouped_words[word[0]].append(word)

print(grouped_words)  
# Output: defaultdict(<class 'list'>, {'a': ['apple', 'apple'], 'b': ['bat', 'bear'], 'c': ['car', 'cat']})
```

### OrderedDict

`OrderedDict` is a dict subclass that remembers the order entries were added:

```python
from collections import OrderedDict

# Create an ordered dictionary
ordered = OrderedDict([('a', 1), ('b', 2), ('c', 3)])

# Add new items (will be added at the end)
ordered['d'] = 4
print(ordered)  # Output: OrderedDict([('a', 1), ('b', 2), ('c', 3), ('d', 4)])

# Move to end
ordered.move_to_end('b')
print(ordered)  # Output: OrderedDict([('a', 1), ('c', 3), ('d', 4), ('b', 2)])

# Move to beginning
ordered.move_to_end('b', last=False)
print(ordered)  # Output: OrderedDict([('b', 2), ('a', 1), ('c', 3), ('d', 4)])
```

Note: As of Python 3.7, regular dictionaries also maintain insertion order, making `OrderedDict` less necessary for simple use cases.

### namedtuple

`namedtuple` creates tuple subclasses with named fields:

```python
from collections import namedtuple

# Define a named tuple type
Point = namedtuple('Point', ['x', 'y'])

# Create instances
p1 = Point(1, 2)
p2 = Point(x=3, y=4)

# Access by name or index
print(p1.x, p1.y)  # Output: 1 2
print(p1[0], p1[1])  # Output: 1 2

# Immutable like regular tuples
# p1.x = 5  # AttributeError: can't set attribute

# Convert to dictionary
print(p1._asdict())  # Output: {'x': 1, 'y': 2}

# Create new instance with updated values
p3 = p1._replace(x=5)
print(p3)  # Output: Point(x=5, y=2)
```

## Choosing the Right Data Structure

Selecting the appropriate data structure is crucial for efficient and readable code:

| Data Structure | When to Use |
|----------------|-------------|
| **List** | When you need an ordered, mutable collection that may contain duplicates |
| **Tuple** | When you need an immutable sequence, especially for multiple return values or dictionary keys |
| **Dictionary** | When you need to store key-value pairs for fast lookups |
| **Set** | When you need to store unique values and perform set operations |
| **C
(Content truncated due to size limit. Use line ranges to read in chunks)