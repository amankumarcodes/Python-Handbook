# Chapter 9: Object-Oriented Programming

## Introduction to OOP Concepts

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data and code. The data is in the form of fields (often known as attributes or properties), and the code is in the form of procedures (often known as methods).

OOP focuses on creating reusable code and organizing related data and behaviors together. It is built around several key concepts:

1. **Classes and Objects**: Classes are blueprints for creating objects, while objects are instances of classes.
2. **Encapsulation**: Bundling data and methods that work on that data within a single unit (class).
3. **Inheritance**: Creating new classes that inherit properties and methods from existing classes.
4. **Polymorphism**: The ability to present the same interface for different underlying forms or data types.

Python is a multi-paradigm language that supports OOP principles, making it flexible and powerful for various programming tasks.

## Classes and Objects

### Creating Classes

In Python, you define a class using the `class` keyword:

```python
class Person:
    """A simple class representing a person"""
    
    def __init__(self, name, age):
        """Initialize the person with a name and age"""
        self.name = name
        self.age = age
    
    def greet(self):
        """Return a greeting message"""
        return f"Hello, my name is {self.name} and I am {self.age} years old."
```

Key components of a class definition:
- The `class` keyword followed by the class name (conventionally in CamelCase)
- A docstring describing the class (optional but recommended)
- The `__init__` method (constructor) that initializes new instances
- Instance methods that define behaviors
- The `self` parameter, which refers to the instance being operated on

### Class Attributes and Methods

Classes can have two types of attributes and methods:

1. **Instance attributes and methods**: Belong to each individual instance
2. **Class attributes and methods**: Shared among all instances of the class

```python
class Student:
    # Class attribute - shared by all instances
    school = "Python High School"
    
    def __init__(self, name, grade):
        # Instance attributes - unique to each instance
        self.name = name
        self.grade = grade
    
    def display_info(self):
        # Instance method - operates on instance data
        return f"{self.name} is in grade {self.grade} at {Student.school}"
    
    @classmethod
    def change_school(cls, new_school):
        # Class method - can modify class state
        cls.school = new_school
    
    @staticmethod
    def is_passing_grade(grade):
        # Static method - doesn't access instance or class data
        return grade >= 60
```

### Instantiating Objects

To create an object (instance) from a class, you call the class name as if it were a function:

```python
# Create instances of the Person class
alice = Person("Alice", 30)
bob = Person("Bob", 25)

# Access attributes
print(alice.name)  # Output: Alice
print(bob.age)     # Output: 25

# Call methods
print(alice.greet())  # Output: Hello, my name is Alice and I am 30 years old.
```

## Constructors and Destructors

### Constructors

The `__init__` method is a special method that Python calls when creating a new instance of a class. It initializes the object's attributes:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        print(f"Rectangle created with width={width} and height={height}")
    
    def area(self):
        return self.width * self.height

# Creating an instance calls the __init__ method
rect = Rectangle(5, 3)  # Output: Rectangle created with width=5 and height=3
print(rect.area())      # Output: 15
```

### Destructors

The `__del__` method is called when an object is about to be destroyed (garbage collected):

```python
class Resource:
    def __init__(self, name):
        self.name = name
        print(f"Resource {name} has been allocated")
    
    def __del__(self):
        print(f"Resource {self.name} is being freed")

# Create and then destroy a Resource object
def create_resource():
    r = Resource("database_connection")
    # r goes out of scope when the function returns
    return

create_resource()  # Output: Resource database_connection has been allocated
                   #         Resource database_connection is being freed
```

Note: You should not rely on `__del__` for critical cleanup operations because Python's garbage collection timing is not deterministic. For resource cleanup, use context managers (`with` statement) instead.

## Inheritance

Inheritance allows a class to inherit attributes and methods from another class, promoting code reuse and establishing a hierarchy of classes.

### Single Inheritance

In single inheritance, a class inherits from one parent class:

```python
# Parent (base) class
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return "Some generic animal sound"

# Child (derived) class
class Dog(Animal):
    def speak(self):
        return "Woof!"

# Child class that calls parent's methods
class Cat(Animal):
    def speak(self):
        return "Meow!"
    
    def introduce(self):
        return f"I am {self.name}, and I say {self.speak()}"

# Create instances
generic_animal = Animal("Generic")
dog = Dog("Buddy")
cat = Cat("Whiskers")

print(generic_animal.speak())  # Output: Some generic animal sound
print(dog.speak())             # Output: Woof!
print(cat.introduce())         # Output: I am Whiskers, and I say Meow!
```

### Multiple Inheritance

Python supports multiple inheritance, where a class can inherit from multiple parent classes:

```python
class Flyer:
    def fly(self):
        return "I can fly!"

class Swimmer:
    def swim(self):
        return "I can swim!"

# Multiple inheritance
class Duck(Animal, Flyer, Swimmer):
    def speak(self):
        return "Quack!"

duck = Duck("Donald")
print(duck.name)    # From Animal
print(duck.speak()) # Overridden in Duck
print(duck.fly())   # From Flyer
print(duck.swim())  # From Swimmer
```

### Method Resolution Order (MRO)

When a class inherits from multiple classes, Python uses the Method Resolution Order (MRO) to determine which method to call:

```python
class A:
    def who_am_i(self):
        return "I am A"

class B(A):
    def who_am_i(self):
        return "I am B"

class C(A):
    def who_am_i(self):
        return "I am C"

class D(B, C):
    pass

d = D()
print(d.who_am_i())  # Output: I am B
print(D.__mro__)     # Shows the method resolution order
```

### Method Overriding

Method overriding occurs when a child class provides a specific implementation of a method that is already defined in its parent class:

```python
class Vehicle:
    def __init__(self, name):
        self.name = name
    
    def get_info(self):
        return f"Vehicle: {self.name}"

class Car(Vehicle):
    def __init__(self, name, model):
        super().__init__(name)  # Call parent's __init__
        self.model = model
    
    def get_info(self):
        return f"Car: {self.name}, Model: {self.model}"

car = Car("Toyota", "Corolla")
print(car.get_info())  # Output: Car: Toyota, Model: Corolla
```

The `super()` function is used to call methods from the parent class.

## Encapsulation

Encapsulation is the bundling of data and methods that work on that data within a single unit (class), and restricting access to some of the object's components.

### Access Modifiers

Python doesn't have strict access modifiers like some other languages, but it follows these conventions:

1. **Public**: Attributes and methods that can be accessed from anywhere (no prefix)
2. **Protected**: Attributes and methods that should only be accessed within the class and its subclasses (prefix with a single underscore `_`)
3. **Private**: Attributes and methods that should only be accessed within the class itself (prefix with double underscore `__`)

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner          # Public attribute
        self._balance = balance     # Protected attribute
        self.__account_number = self.__generate_account_number()  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self._balance
    
    def __generate_account_number(self):
        # Private method
        import random
        return random.randint(10000000, 99999999)
    
    def get_account_info(self):
        # Accessing private attribute within the class
        return f"Owner: {self.owner}, Account: ****{str(self.__account_number)[-4:]}"
```

Note: Python's name mangling for private attributes (with double underscores) is not a security feature but a way to avoid name clashes in inherited classes.

## Polymorphism

Polymorphism allows objects of different classes to be treated as objects of a common superclass. It enables the same interface to be used for different underlying forms.

### Method Overloading

Python doesn't support traditional method overloading (multiple methods with the same name but different parameters), but you can simulate it using default parameters or variable-length arguments:

```python
class Calculator:
    def add(self, *args):
        return sum(args)

calc = Calculator()
print(calc.add(1, 2))      # Output: 3
print(calc.add(1, 2, 3))   # Output: 6
print(calc.add(1, 2, 3, 4)) # Output: 10
```

### Method Overriding

As seen earlier, method overriding is a form of polymorphism where a subclass provides a specific implementation of a method that is already defined in its parent class.

### Duck Typing

Python follows the principle of "duck typing": if it walks like a duck and quacks like a duck, then it's a duck. This means that the type or class of an object is less important than the methods it defines or the properties it has:

```python
class Duck:
    def sound(self):
        return "Quack"
    
    def walk(self):
        return "Walking like a duck"

class Person:
    def sound(self):
        return "Hello"
    
    def walk(self):
        return "Walking like a human"

def make_sound_and_walk(entity):
    print(entity.sound())
    print(entity.walk())

duck = Duck()
person = Person()

make_sound_and_walk(duck)    # Works with Duck
make_sound_and_walk(person)  # Works with Person too
```

In this example, `make_sound_and_walk()` works with any object that has `sound()` and `walk()` methods, regardless of its type.

## Abstract Classes and Interfaces

### Abstract Base Classes

Abstract base classes (ABCs) are classes that cannot be instantiated and are designed to be subclassed. They often include abstract methods that must be implemented by subclasses.

Python's `abc` module provides tools for defining ABCs:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass
    
    def describe(self):
        return f"This shape has an area of {self.area()} and a perimeter of {self.perimeter()}"

# Cannot instantiate abstract class
# shape = Shape()  # TypeError

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        import math
        return math.pi * self.radius ** 2
    
    def perimeter(self):
        import math
        return 2 * math.pi * self.radius

circle = Circle(5)
print(circle.area())       # Output: 78.53981633974483
print(circle.describe())   # Output: This shape has an area of 78.53981633974483 and a perimeter of 31.41592653589793
```

### Interfaces

Python doesn't have a formal interface concept like some other languages, but abstract base classes can be used to define interfaces:

```python
from abc import ABC, abstractmethod

class Drawable(ABC):
    @abstractmethod
    def draw(self):
        pass

class Resizable(ABC):
    @abstractmethod
    def resize(self, width, height):
        pass

# A class implementing multiple interfaces
class Rectangle(Drawable, Resizable):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def draw(self):
        return f"Drawing a rectangle of width {self.width} and height {self.height}"
    
    def resize(self, width, height):
        self.width = width
        self.height = height
        return f"Resized to width {self.width} and height {self.height}"

rect = Rectangle(10, 20)
print(rect.draw())              # Output: Drawing a rectangle of width 10 and height 20
print(rect.resize(15, 25))      # Output: Resized to width 15 and height 25
```

## Magic Methods (Dunder Methods)

Magic methods, also known as dunder methods (double underscore methods), are special methods in Python that start and end with double underscores. They allow you to define how objects of your class behave with built-in functions and operators.

### Common Magic Methods

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    # String representation
    def __str__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __repr__(self):
        return f"Vector({self.x}, {self.y})"
    
    # Arithmetic operations
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)
    
    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)
    
    # Comparison operations
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y
    
    # Container methods
    def __len__(self):
        import math
        return int(math.sqrt(self.x ** 2 + self.y ** 2))
    
    # Context manager methods
    def __enter__(self):
        print("Entering context")
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exiting context")

# Using the magic methods
v1 = Vector(1, 2)
v2 = Vector(3, 4)

print(v1)              # Output: Vector(1, 2)
print(v1 + v2)         # Output: Vector(4, 6)
print(v1 - v2)         # Output: Vector(-2, -2)
print(v1 * 3)          # Output: Vector(3, 6)
print(v1 == v2)        # Output: False
print(len(v1))         # Output: 2

# Using as a context manager
with v1 as v:
    print(f"Inside context with {v}")
```

### Common Magic Methods Table

| Method | Description | Example Usage |
|--------|-------------|---------------|
| `__init__(self, ...)` | Constructor | `obj = MyClass()` |
| `__del__(self)` | Destructor | When object is garbage collected |
| `__str__(self)` | String representation for end users | `print(obj)` |
| `__repr__(self)` | String representation for developers | `repr(obj)` |
| `__len__(self)` | Length of the object | `len(obj)` |
| `__getitem__(self, key)` | Access items using index notation | `obj[key]` |
| `__setitem__(self, key, value)` | Set items using index notation | `obj[key] = value` |
| `__delitem__(self, key)` | Delete items using index notation | `del obj[key]` |
| `__iter__(self)` | Iterator for the object | `for item in obj` |
| `__next__(self)` | Get next item in iteration | `next(obj)` |
| `__contains__(self, item)` | Check if item is in object | `item in obj` |
| `__call__(self, ...)` | Make object callable | `obj()` |
| `__add__(self, other)` | Addition | `obj + other` |
| `__sub__(self, other)` | Subtraction | `obj - other` |
| `__mul__(self, other)` | Multiplication | `obj * other` |
| `__truediv__(self, other)` | Division | `obj / other` |
| `__eq__(self, other)` |
(Content truncated due to size limit. Use line ranges to read in chunks)