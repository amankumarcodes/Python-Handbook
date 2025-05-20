# Chapter 3: Control Flow (Conditionals)

## Decision Making in Programming

Decision making is a fundamental aspect of programming that allows a program to execute different code blocks based on certain conditions. This ability to make decisions makes programs dynamic and responsive to different inputs and situations.

In Python, decision making is implemented through conditional statements that evaluate expressions to either `True` or `False`. Based on these evaluations, the program follows different execution paths.

## if Statement

The `if` statement is the most basic form of conditional execution in Python. It executes a block of code only if a specified condition is true.

### Syntax:
```python
if condition:
    # code to execute if condition is True
```

### Example:
```python
age = 18

if age >= 18:
    print("You are eligible to vote.")
```

In this example, the message will be printed only if the value of `age` is greater than or equal to 18.

## if-else Statement

The `if-else` statement provides an alternative execution path when the condition is false.

### Syntax:
```python
if condition:
    # code to execute if condition is True
else:
    # code to execute if condition is False
```

### Example:
```python
age = 16

if age >= 18:
    print("You are eligible to vote.")
else:
    print("You are not eligible to vote yet.")
```

In this example, since `age` is 16 (less than 18), the program will execute the code in the `else` block and print "You are not eligible to vote yet."

## if-elif-else Ladder

When you need to check multiple conditions, you can use the `if-elif-else` ladder (also known as an `if-else-if` ladder).

### Syntax:
```python
if condition1:
    # code to execute if condition1 is True
elif condition2:
    # code to execute if condition1 is False and condition2 is True
elif condition3:
    # code to execute if condition1 and condition2 are False and condition3 is True
else:
    # code to execute if all conditions are False
```

### Example:
```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"Your grade is {grade}")
```

In this example, the program assigns a letter grade based on the score. Since the score is 85, the program will assign the grade "B" and print "Your grade is B".

## Nested if Statements

You can also place an `if` statement inside another `if` statement, creating nested conditional structures.

### Syntax:
```python
if outer_condition:
    # code to execute if outer_condition is True
    if inner_condition:
        # code to execute if both outer_condition and inner_condition are True
    else:
        # code to execute if outer_condition is True but inner_condition is False
else:
    # code to execute if outer_condition is False
```

### Example:
```python
age = 25
has_license = True

if age >= 18:
    print("You are old enough to drive.")
    if has_license:
        print("You can drive legally.")
    else:
        print("You need to get a license first.")
else:
    print("You are not old enough to drive yet.")
```

In this example, since `age` is 25 (greater than 18) and `has_license` is `True`, the program will print both "You are old enough to drive." and "You can drive legally."

## Conditional Expressions (Ternary Operator)

Python provides a concise way to write simple if-else statements using conditional expressions, also known as the ternary operator.

### Syntax:
```python
value_if_true if condition else value_if_false
```

### Example:
```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)  # Output: Adult
```

This is equivalent to:
```python
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
print(status)
```

Conditional expressions are useful for simple assignments based on conditions, but for more complex logic, traditional if-else statements are more readable.

## match-case Statement (Python 3.10+)

Python 3.10 introduced the `match-case` statement, which is similar to switch-case statements in other languages but with more powerful pattern matching capabilities.

### Syntax:
```python
match expression:
    case pattern1:
        # code to execute if expression matches pattern1
    case pattern2:
        # code to execute if expression matches pattern2
    case _:
        # default case (like else)
```

### Example:
```python
# Requires Python 3.10 or newer
day = "Monday"

match day:
    case "Monday":
        print("Start of the work week")
    case "Tuesday" | "Wednesday" | "Thursday":
        print("Middle of the work week")
    case "Friday":
        print("End of the work week")
    case "Saturday" | "Sunday":
        print("Weekend")
    case _:
        print("Invalid day")
```

In this example, since `day` is "Monday", the program will print "Start of the work week".

The `match-case` statement can also match against more complex patterns, including sequences, mappings, and class instances, making it a powerful tool for pattern matching.

## Practice Set

### Review Questions
1. What is the purpose of conditional statements in programming?
2. Explain the difference between `if-else` and `if-elif-else` statements.
3. When would you use nested if statements?
4. What is the advantage of using a conditional expression (ternary operator)?

### Coding Exercises
1. Write a program that checks if a number is positive, negative, or zero.
2. Create a program that determines if a year is a leap year. (Hint: A leap year is divisible by 4, except for century years which must be divisible by 400).
3. Write a program that takes a student's score as input and outputs their letter grade according to the following scale:
   - 90-100: A
   - 80-89: B
   - 70-79: C
   - 60-69: D
   - Below 60: F
4. Create a simple calculator program that takes two numbers and an operator (+, -, *, /) as input and performs the corresponding operation.

### Challenge Problem
Create a program that simulates a simple authentication system:
1. Define a username and password in your code
2. Ask the user to enter their username and password
3. If both match, display "Login successful"
4. If the username is correct but the password is wrong, display "Incorrect password"
5. If the username is wrong, display "User not found"
6. Give the user a maximum of 3 attempts to log in
7. After 3 failed attempts, display "Account locked"
