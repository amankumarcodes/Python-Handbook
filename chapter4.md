# Chapter 4: Loops and Iterations

## Why Loops Are Necessary

Loops are essential programming constructs that allow you to execute a block of code repeatedly. Without loops, you would need to write the same code multiple times, making your programs longer, less efficient, and harder to maintain. Loops help solve problems that require repetitive tasks, such as:

- Processing each item in a collection
- Executing code until a specific condition is met
- Performing calculations iteratively
- Automating repetitive tasks

## Types of Loops in Python

Python provides several types of loops to handle different scenarios:

1. `while` loop: Executes a block of code as long as a condition is true
2. `for` loop: Iterates over a sequence (like a list, tuple, string) or other iterable objects
3. Nested loops: Loops inside other loops
4. Loop control statements: Special statements to alter the flow of loops

Let's explore each type in detail.

## while Loop

The `while` loop executes a block of code as long as a specified condition evaluates to `True`.

### Syntax:
```python
while condition:
    # code to execute while condition is True
```

### Example:
```python
count = 1
while count <= 5:
    print(count)
    count += 1
```

Output:
```
1
2
3
4
5
```

In this example, the loop continues as long as `count` is less than or equal to 5. Each iteration prints the current value of `count` and then increments it by 1.

### Infinite Loops

If the condition in a `while` loop never becomes `False`, the loop will run indefinitely, creating an infinite loop:

```python
# WARNING: This is an infinite loop
while True:
    print("This will print forever!")
```

To avoid infinite loops, ensure that:
1. The condition will eventually become `False`
2. You have a way to break out of the loop (using `break` statement)

### Example with a sentinel value:
```python
# Using a sentinel value to control the loop
while True:
    user_input = input("Enter a number (or 'q' to quit): ")
    if user_input.lower() == 'q':
        break
    number = float(user_input)
    print(f"The square of {number} is {number ** 2}")
```

## for Loop

The `for` loop is used to iterate over a sequence (like a list, tuple, string) or other iterable objects.

### Syntax:
```python
for variable in sequence:
    # code to execute for each item in sequence
```

### Example with a list:
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

Output:
```
apple
banana
cherry
```

### Example with a string:
```python
message = "Python"
for character in message:
    print(character)
```

Output:
```
P
y
t
h
o
n
```

### The range() Function

The `range()` function generates a sequence of numbers, which is commonly used with `for` loops:

```python
# range(stop) - generates numbers from 0 to stop-1
for i in range(5):
    print(i)
```

Output:
```
0
1
2
3
4
```

```python
# range(start, stop) - generates numbers from start to stop-1
for i in range(2, 6):
    print(i)
```

Output:
```
2
3
4
5
```

```python
# range(start, stop, step) - generates numbers from start to stop-1 with step increment
for i in range(1, 10, 2):
    print(i)
```

Output:
```
1
3
5
7
9
```

## Loop Control Statements

Python provides special statements to alter the flow of loops:

### break Statement

The `break` statement terminates the loop and transfers execution to the statement immediately following the loop.

```python
for i in range(1, 10):
    if i == 5:
        break
    print(i)
```

Output:
```
1
2
3
4
```

### continue Statement

The `continue` statement skips the rest of the code inside the loop for the current iteration and moves to the next iteration.

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
```

Output:
```
1
2
4
5
```

### pass Statement

The `pass` statement is a null operation; nothing happens when it executes. It's used as a placeholder when a statement is required syntactically but no action is needed.

```python
for i in range(1, 6):
    if i == 3:
        pass  # Do nothing special
    print(i)
```

Output:
```
1
2
3
4
5
```

## Nested Loops

You can place one loop inside another loop, creating nested loops. The inner loop will be executed once for each iteration of the outer loop.

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"({i}, {j})", end=" ")
    print()  # New line after each row
```

Output:
```
(1, 1) (1, 2) (1, 3) 
(2, 1) (2, 2) (2, 3) 
(3, 1) (3, 2) (3, 3) 
```

Nested loops are useful for working with multi-dimensional data structures like matrices or generating combinations.

## Loop Else Clause

Python allows an `else` clause with both `for` and `while` loops. The `else` block executes after the loop completes normally (i.e., not terminated by a `break` statement).

```python
# Loop with else clause
for i in range(1, 6):
    print(i)
else:
    print("Loop completed successfully!")
```

Output:
```
1
2
3
4
5
Loop completed successfully!
```

```python
# Loop with else clause and break
for i in range(1, 6):
    if i == 3:
        break
    print(i)
else:
    print("This won't be printed because the loop was broken!")
```

Output:
```
1
2
```

The `else` clause is particularly useful when you're searching for an item in a sequence and want to perform an action if the item is not found.

## Comprehensions

Python offers a concise way to create lists, dictionaries, and sets using comprehensions.

### List Comprehensions

List comprehensions provide a concise way to create lists based on existing lists or other iterable objects.

```python
# Traditional way
squares = []
for i in range(1, 6):
    squares.append(i ** 2)
print(squares)  # Output: [1, 4, 9, 16, 25]

# Using list comprehension
squares = [i ** 2 for i in range(1, 6)]
print(squares)  # Output: [1, 4, 9, 16, 25]
```

You can also add conditions to list comprehensions:

```python
# Only include even squares
even_squares = [i ** 2 for i in range(1, 11) if i % 2 == 0]
print(even_squares)  # Output: [4, 16, 36, 64, 100]
```

### Dictionary Comprehensions

Similar to list comprehensions, but create dictionaries:

```python
# Create a dictionary of squares
squares_dict = {i: i ** 2 for i in range(1, 6)}
print(squares_dict)  # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

### Set Comprehensions

Create sets using comprehensions:

```python
# Create a set of squares
squares_set = {i ** 2 for i in range(1, 6)}
print(squares_set)  # Output: {1, 4, 9, 16, 25}
```

Comprehensions make your code more concise and often more readable, especially for simple transformations and filtering operations.

## Practice Set

### Review Questions
1. What is the difference between a `for` loop and a `while` loop?
2. Explain the purpose of the `break` and `continue` statements in loops.
3. What is an infinite loop and how can you avoid it?
4. What is the purpose of the `else` clause in loops?

### Coding Exercises
1. Write a program that prints all even numbers from 1 to 20 using a `while` loop.
2. Create a program that calculates the factorial of a number using a `for` loop. (Factorial of n is the product of all positive integers less than or equal to n)
3. Write a program that prints the Fibonacci sequence up to a specified number of terms using a loop. (Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8, ...)
4. Create a program that uses nested loops to print a pattern like this:
   ```
   *
   **
   ***
   ****
   *****
   ```

### Challenge Problem
Create a program that generates a simple number guessing game:
1. Generate a random number between 1 and 100
2. Ask the user to guess the number
3. Tell the user if their guess is too high or too low
4. Keep track of the number of guesses
5. End the game when the user guesses correctly
6. Display the number of guesses it took
7. Ask if the user wants to play again
