# Chapter 7: File Handling

## File Operations

File handling is an essential aspect of programming that allows you to work with external data stored in files. Python provides built-in functions and methods to perform various file operations such as reading from files, writing to files, and managing file resources.

## Opening and Closing Files

Before you can read from or write to a file, you need to open it using the `open()` function.

### The open() Function

The `open()` function takes two main parameters:
- The file path (required)
- The mode (optional, defaults to read mode 'r')

```python
# Basic syntax
file = open(filename, mode)
```

### File Modes

Python supports various file modes:

| Mode | Description |
|------|-------------|
| 'r' | Read (default) - Opens file for reading |
| 'w' | Write - Opens file for writing; creates new file or truncates existing file |
| 'a' | Append - Opens file for writing; creates new file or appends to existing file |
| 'x' | Exclusive creation - Creates a new file, fails if file already exists |
| 'b' | Binary mode - Opens file in binary mode (e.g., 'rb', 'wb') |
| 't' | Text mode (default) - Opens file in text mode (e.g., 'rt', 'wt') |
| '+' | Update mode - Opens file for reading and writing (e.g., 'r+', 'w+') |

### Closing Files

It's important to close files after you're done with them to free up system resources:

```python
file = open("example.txt", "r")
# Perform operations with the file
file.close()  # Close the file
```

### Using the with Statement (Context Manager)

The recommended way to work with files is using the `with` statement, which automatically closes the file when you're done:

```python
# Using with statement (context manager)
with open("example.txt", "r") as file:
    # Perform operations with the file
    content = file.read()
    print(content)
# File is automatically closed when the block ends
```

Benefits of using the `with` statement:
- Automatically closes the file, even if an exception occurs
- More readable and concise code
- Follows the "Resource Acquisition Is Initialization" (RAII) pattern

## Reading from Files

Python provides several methods to read data from files:

### read() Method

Reads the entire file content as a string:

```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
```

You can also specify the number of characters to read:

```python
with open("example.txt", "r") as file:
    first_10_chars = file.read(10)
    print(first_10_chars)
```

### readline() Method

Reads a single line from the file:

```python
with open("example.txt", "r") as file:
    first_line = file.readline()
    second_line = file.readline()
    print(first_line)
    print(second_line)
```

### readlines() Method

Reads all lines and returns them as a list of strings:

```python
with open("example.txt", "r") as file:
    lines = file.readlines()
    print(lines)  # List of strings, each representing a line
```

### Iterating Through a File

You can iterate through a file line by line, which is memory-efficient for large files:

```python
with open("example.txt", "r") as file:
    for line in file:
        print(line, end="")  # The line already contains a newline character
```

## Writing to Files

Python provides methods to write data to files:

### write() Method

Writes a string to the file:

```python
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a new line.")
```

### writelines() Method

Writes a list of strings to the file:

```python
lines = ["First line\n", "Second line\n", "Third line\n"]
with open("output.txt", "w") as file:
    file.writelines(lines)
```

Note that `writelines()` doesn't add newline characters automatically; you need to include them in your strings if needed.

## Appending to Files

To add content to an existing file without overwriting it, use append mode ('a'):

```python
with open("log.txt", "a") as file:
    file.write("New log entry: " + str(datetime.now()) + "\n")
```

## File Positions

The file object maintains a position indicator that determines where the next read or write operation will occur:

### tell() Method

Returns the current position in the file:

```python
with open("example.txt", "r") as file:
    content = file.read(5)
    position = file.tell()
    print(f"After reading 5 characters, position is at: {position}")
```

### seek() Method

Changes the current position in the file:

```python
with open("example.txt", "r") as file:
    # Move to the 10th byte in the file
    file.seek(10)
    # Read from the new position
    content = file.read(5)
    print(content)
    
    # Move to the beginning of the file
    file.seek(0)
    # Read from the beginning
    beginning = file.read(5)
    print(beginning)
```

The `seek()` method takes two parameters:
- `offset`: The position to move to
- `whence`: The reference point (0 = beginning, 1 = current position, 2 = end of file)

```python
with open("example.txt", "r") as file:
    # Move 5 bytes forward from the beginning
    file.seek(5, 0)
    # Move 3 bytes forward from the current position
    file.seek(3, 1)
    # Move 10 bytes backward from the end
    file.seek(-10, 2)
```

## Working with CSV Files

CSV (Comma-Separated Values) is a common file format for storing tabular data. Python's `csv` module provides functionality to work with CSV files:

### Reading CSV Files

```python
import csv

with open("data.csv", "r", newline="") as file:
    # Create a CSV reader
    csv_reader = csv.reader(file)
    
    # Skip the header row (if present)
    header = next(csv_reader)
    print(f"Header: {header}")
    
    # Process each row
    for row in csv_reader:
        print(row)
```

### Reading CSV Files with DictReader

The `DictReader` class creates dictionaries from CSV rows, using the header row for keys:

```python
import csv

with open("data.csv", "r", newline="") as file:
    # Create a CSV DictReader
    csv_reader = csv.DictReader(file)
    
    # Process each row as a dictionary
    for row in csv_reader:
        print(f"Name: {row['name']}, Age: {row['age']}")
```

### Writing CSV Files

```python
import csv

data = [
    ["Name", "Age", "City"],
    ["Alice", "30", "New York"],
    ["Bob", "25", "Boston"],
    ["Charlie", "35", "Chicago"]
]

with open("output.csv", "w", newline="") as file:
    # Create a CSV writer
    csv_writer = csv.writer(file)
    
    # Write multiple rows
    csv_writer.writerows(data)
```

### Writing CSV Files with DictWriter

```python
import csv

data = [
    {"name": "Alice", "age": 30, "city": "New York"},
    {"name": "Bob", "age": 25, "city": "Boston"},
    {"name": "Charlie", "age": 35, "city": "Chicago"}
]

with open("output.csv", "w", newline="") as file:
    # Define the field names
    fieldnames = ["name", "age", "city"]
    
    # Create a CSV DictWriter
    csv_writer = csv.DictWriter(file, fieldnames=fieldnames)
    
    # Write the header row
    csv_writer.writeheader()
    
    # Write multiple rows
    csv_writer.writerows(data)
```

## Working with JSON Files

JSON (JavaScript Object Notation) is a popular data interchange format. Python's `json` module provides functionality to work with JSON data:

### Reading JSON Files

```python
import json

with open("data.json", "r") as file:
    # Load JSON data from file
    data = json.load(file)
    
    # Access the data
    print(data["name"])
    print(data["age"])
    print(data["city"])
```

### Writing JSON Files

```python
import json

data = {
    "name": "Alice",
    "age": 30,
    "city": "New York",
    "languages": ["Python", "JavaScript", "Java"],
    "is_student": False
}

with open("output.json", "w") as file:
    # Write JSON data to file
    json.dump(data, file, indent=4)  # indent for pretty formatting
```

### Converting Between JSON and Python Objects

```python
import json

# Python object to JSON string
data = {"name": "Alice", "age": 30}
json_string = json.dumps(data)
print(json_string)  # Output: {"name": "Alice", "age": 30}

# JSON string to Python object
json_string = '{"name": "Bob", "age": 25}'
data = json.loads(json_string)
print(data["name"])  # Output: Bob
```

## Exception Handling in File Operations

File operations can raise various exceptions, which should be handled properly:

```python
try:
    with open("nonexistent_file.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("The file does not exist.")
except PermissionError:
    print("You don't have permission to access this file.")
except IOError as e:
    print(f"An I/O error occurred: {e}")
```

## Working with Directories

Python's `os` module provides functions to work with directories:

### Getting the Current Working Directory

```python
import os

current_dir = os.getcwd()
print(f"Current directory: {current_dir}")
```

### Creating Directories

```python
import os

# Create a single directory
os.mkdir("new_directory")

# Create multiple nested directories
os.makedirs("parent/child/grandchild")
```

### Listing Directory Contents

```python
import os

# List all files and directories
contents = os.listdir(".")
print(contents)

# List with full paths
contents_with_paths = [os.path.join(".", item) for item in os.listdir(".")]
print(contents_with_paths)
```

### Checking if a Path Exists

```python
import os

# Check if a file exists
if os.path.exists("example.txt"):
    print("The file exists.")

# Check if it's a file
if os.path.isfile("example.txt"):
    print("It's a file.")

# Check if it's a directory
if os.path.isdir("new_directory"):
    print("It's a directory.")
```

### Joining Paths

```python
import os

# Join path components
path = os.path.join("parent", "child", "file.txt")
print(path)  # Output: parent/child/file.txt (on Unix-like systems)
```

### Getting File Information

```python
import os

# Get file size
size = os.path.getsize("example.txt")
print(f"File size: {size} bytes")

# Get last modification time
import time
mod_time = os.path.getmtime("example.txt")
print(f"Last modified: {time.ctime(mod_time)}")
```

### Removing Files and Directories

```python
import os

# Remove a file
os.remove("file_to_delete.txt")

# Remove an empty directory
os.rmdir("empty_directory")

# Remove a directory and all its contents
import shutil
shutil.rmtree("directory_to_delete")
```

## Context Managers (with Statement)

The `with` statement is a context manager that ensures proper acquisition and release of resources. We've already seen it with file operations, but you can also create your own context managers:

### Using contextlib

```python
from contextlib import contextmanager

@contextmanager
def open_file(filename, mode):
    try:
        file = open(filename, mode)
        yield file
    finally:
        file.close()

# Using the custom context manager
with open_file("example.txt", "r") as file:
    content = file.read()
    print(content)
```

### Creating a Context Manager Class

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

# Using the custom context manager class
with FileManager("example.txt", "r") as file:
    content = file.read()
    print(content)
```

## Practice Set

### Review Questions
1. What is the difference between the 'w' and 'a' file modes in Python?
2. Explain the benefits of using the `with` statement when working with files.
3. What is the purpose of the `seek()` method in file handling?
4. How do CSV and JSON file formats differ, and when would you use each?

### Coding Exercises
1. Write a program that reads a text file and counts the number of lines, words, and characters in it.
2. Create a program that reads a CSV file containing student records (name, age, grade) and calculates the average grade.
3. Write a program that merges multiple text files into a single file, adding a header before each file's content to indicate its source.
4. Create a program that reads a JSON file containing a list of products (name, price, quantity) and calculates the total inventory value.

### Challenge Problem
Create a simple log analysis tool:
1. Read a log file with entries in the format: `[TIMESTAMP] [LEVEL] Message`
2. Parse each log entry to extract the timestamp, log level, and message
3. Count the occurrences of each log level (INFO, WARNING, ERROR, etc.)
4. Find the time range of the logs (earliest to latest timestamp)
5. Identify the top 5 most frequent error messages
6. Generate a summary report and save it to a new file
7. Implement error handling for malformed log entries
