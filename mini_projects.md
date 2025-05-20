# Mini-Projects

## Project 1: Number Guessing Game

This project will help you practice using loops, conditionals, and random number generation.

### Requirements:
1. Generate a random number between 1 and 100
2. Ask the user to guess the number
3. Tell the user if their guess is too high or too low
4. Keep track of the number of guesses
5. End the game when the user guesses correctly
6. Display the number of guesses it took
7. Ask if the user wants to play again

### Sample Code:
```python
import random

def play_game():
    # Generate a random number between 1 and 100
    secret_number = random.randint(1, 100)
    attempts = 0
    guess = 0
    
    print("Welcome to the Number Guessing Game!")
    print("I'm thinking of a number between 1 and 100.")
    
    while guess != secret_number:
        try:
            guess = int(input("Make a guess: "))
            attempts += 1
            
            if guess < secret_number:
                print("Too low! Try again.")
            elif guess > secret_number:
                print("Too high! Try again.")
            else:
                print(f"Congratulations! You guessed the number in {attempts} attempts!")
        except ValueError:
            print("Please enter a valid number.")
    
    return attempts

def main():
    play_again = "yes"
    
    while play_again.lower() == "yes" or play_again.lower() == "y":
        play_game()
        play_again = input("Would you like to play again? (yes/no): ")
    
    print("Thanks for playing!")

if __name__ == "__main__":
    main()
```

## Project 2: To-Do List Application

This project will help you practice working with data structures, file handling, and user input.

### Requirements:
1. Create a command-line to-do list application
2. Allow users to add, view, mark as complete, and delete tasks
3. Save tasks to a file so they persist between program runs
4. Include a menu system for user interaction
5. Implement error handling for invalid inputs

### Sample Code:
```python
import json
import os

def load_tasks():
    if os.path.exists("tasks.json"):
        with open("tasks.json", "r") as file:
            try:
                return json.load(file)
            except json.JSONDecodeError:
                return []
    return []

def save_tasks(tasks):
    with open("tasks.json", "w") as file:
        json.dump(tasks, file, indent=4)

def display_tasks(tasks):
    if not tasks:
        print("No tasks found.")
        return
    
    print("\nYour To-Do List:")
    for i, task in enumerate(tasks, 1):
        status = "✓" if task["completed"] else " "
        print(f"{i}. [{status}] {task['description']}")
    print()

def add_task(tasks, description):
    tasks.append({"description": description, "completed": False})
    save_tasks(tasks)
    print(f"Task '{description}' added successfully!")

def mark_completed(tasks, task_index):
    if 1 <= task_index <= len(tasks):
        tasks[task_index - 1]["completed"] = True
        save_tasks(tasks)
        print("Task marked as completed!")
    else:
        print("Invalid task number.")

def delete_task(tasks, task_index):
    if 1 <= task_index <= len(tasks):
        deleted_task = tasks.pop(task_index - 1)
        save_tasks(tasks)
        print(f"Task '{deleted_task['description']}' deleted!")
    else:
        print("Invalid task number.")

def main():
    tasks = load_tasks()
    
    while True:
        print("\n==== To-Do List Application ====")
        print("1. View tasks")
        print("2. Add a task")
        print("3. Mark task as completed")
        print("4. Delete a task")
        print("5. Exit")
        
        choice = input("\nEnter your choice (1-5): ")
        
        if choice == "1":
            display_tasks(tasks)
        elif choice == "2":
            description = input("Enter task description: ")
            add_task(tasks, description)
        elif choice == "3":
            display_tasks(tasks)
            try:
                task_index = int(input("Enter the task number to mark as completed: "))
                mark_completed(tasks, task_index)
            except ValueError:
                print("Please enter a valid number.")
        elif choice == "4":
            display_tasks(tasks)
            try:
                task_index = int(input("Enter the task number to delete: "))
                delete_task(tasks, task_index)
            except ValueError:
                print("Please enter a valid number.")
        elif choice == "5":
            print("Thank you for using the To-Do List Application!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

## Project 3: Simple Calculator

This project will help you practice functions, error handling, and user interface design.

### Requirements:
1. Create a calculator that can perform basic arithmetic operations
2. Support addition, subtraction, multiplication, and division
3. Implement error handling for invalid inputs and operations (like division by zero)
4. Allow users to perform multiple calculations without restarting the program
5. Display the result of each operation

### Sample Code:
```python
def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

def multiply(x, y):
    return x * y

def divide(x, y):
    if y == 0:
        raise ValueError("Cannot divide by zero")
    return x / y

def get_number_input(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Invalid input. Please enter a number.")

def main():
    operations = {
        "1": ("Addition", add),
        "2": ("Subtraction", subtract),
        "3": ("Multiplication", multiply),
        "4": ("Division", divide)
    }
    
    print("Welcome to Simple Calculator!")
    
    while True:
        print("\nAvailable operations:")
        for key, (name, _) in operations.items():
            print(f"{key}. {name}")
        print("5. Exit")
        
        choice = input("\nEnter your choice (1-5): ")
        
        if choice == "5":
            print("Thank you for using Simple Calculator!")
            break
        
        if choice not in operations:
            print("Invalid choice. Please try again.")
            continue
        
        operation_name, operation_func = operations[choice]
        
        num1 = get_number_input("Enter first number: ")
        num2 = get_number_input("Enter second number: ")
        
        try:
            result = operation_func(num1, num2)
            print(f"\nResult of {operation_name}: {num1} {operation_name[0]} {num2} = {result}")
        except ValueError as e:
            print(f"Error: {e}")

if __name__ == "__main__":
    main()
```

## Project 4: File Organizer

This project will help you practice file handling, working with directories, and string manipulation.

### Requirements:
1. Create a program that organizes files in a directory based on their file types
2. Create separate folders for different file types (e.g., images, documents, videos)
3. Move files to their respective folders
4. Handle errors gracefully (e.g., permission issues, file already exists)
5. Display a summary of the organization process

### Sample Code:
```python
import os
import shutil
from pathlib import Path

def get_file_category(file_extension):
    """Determine the category of a file based on its extension."""
    extension = file_extension.lower()
    
    # Define file categories
    image_extensions = ['.jpg', '.jpeg', '.png', '.gif', '.bmp', '.svg']
    document_extensions = ['.pdf', '.doc', '.docx', '.txt', '.rtf', '.odt']
    video_extensions = ['.mp4', '.avi', '.mov', '.wmv', '.flv', '.mkv']
    audio_extensions = ['.mp3', '.wav', '.ogg', '.flac', '.aac']
    
    if extension in image_extensions:
        return "Images"
    elif extension in document_extensions:
        return "Documents"
    elif extension in video_extensions:
        return "Videos"
    elif extension in audio_extensions:
        return "Audio"
    else:
        return "Others"

def organize_files(directory_path):
    """Organize files in the specified directory into category folders."""
    # Convert to Path object for better path handling
    directory = Path(directory_path)
    
    if not directory.exists() or not directory.is_dir():
        print(f"Error: {directory_path} is not a valid directory.")
        return
    
    # Initialize counters for summary
    total_files = 0
    moved_files = 0
    skipped_files = 0
    
    # Process each file in the directory
    for item in directory.iterdir():
        if item.is_file():
            total_files += 1
            file_extension = item.suffix
            category = get_file_category(file_extension)
            
            # Create category folder if it doesn't exist
            category_folder = directory / category
            category_folder.mkdir(exist_ok=True)
            
            # Destination path for the file
            destination = category_folder / item.name
            
            try:
                # Move the file to its category folder
                shutil.move(str(item), str(destination))
                print(f"Moved: {item.name} -> {category}")
                moved_files += 1
            except (shutil.Error, PermissionError) as e:
                print(f"Error moving {item.name}: {e}")
                skipped_files += 1
    
    # Display summary
    print("\nOrganization Summary:")
    print(f"Total files processed: {total_files}")
    print(f"Files moved: {moved_files}")
    print(f"Files skipped: {skipped_files}")

def main():
    print("File Organizer")
    print("This program will organize files in a directory based on their types.")
    
    directory_path = input("Enter the directory path to organize: ")
    
    try:
        organize_files(directory_path)
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    main()
```

## Project 5: Data Analysis Project

This project will help you practice working with data science libraries like pandas and matplotlib.

### Requirements:
1. Read data from a CSV file
2. Clean and process the data
3. Perform basic statistical analysis
4. Create visualizations of the data
5. Save the results to a new file
6. Implement proper error handling

### Sample Code:
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import os

def load_data(file_path):
    """Load data from a CSV file."""
    try:
        return pd.read_csv(file_path)
    except FileNotFoundError:
        print(f"Error: File '{file_path}' not found.")
        return None
    except pd.errors.EmptyDataError:
        print(f"Error: File '{file_path}' is empty.")
        return None
    except pd.errors.ParserError:
        print(f"Error: Unable to parse file '{file_path}'.")
        return None
    except Exception as e:
        print(f"Error loading file: {e}")
        return None

def clean_data(df):
    """Clean and preprocess the data."""
    if df is None:
        return None
    
    # Make a copy to avoid modifying the original
    cleaned_df = df.copy()
    
    # Drop rows with missing values
    cleaned_df.dropna(inplace=True)
    
    # Convert date columns to datetime
    if 'date' in cleaned_df.columns:
        cleaned_df['date'] = pd.to_datetime(cleaned_df['date'], errors='coerce')
    
    # Remove duplicates
    cleaned_df.drop_duplicates(inplace=True)
    
    return cleaned_df

def analyze_data(df):
    """Perform basic statistical analysis on the data."""
    if df is None or df.empty:
        print("No data to analyze.")
        return None
    
    # Create a dictionary to store analysis results
    analysis = {
        'summary': df.describe(),
        'missing_values': df.isnull().sum(),
        'correlations': df.select_dtypes(include=['number']).corr()
    }
    
    return analysis

def create_visualizations(df, output_dir):
    """Create visualizations of the data."""
    if df is None or df.empty:
        print("No data to visualize.")
        return
    
    # Create output directory if it doesn't exist
    os.makedirs(output_dir, exist_ok=True)
    
    # Set the style
    sns.set(style="whitegrid")
    
    # Create a histogram for each numeric column
    numeric_columns = df.select_dtypes(include=['number']).columns
    for column in numeric_columns:
        plt.figure(figsize=(10, 6))
        sns.histplot(df[column], kde=True)
        plt.title(f'Distribution of {column}')
        plt.savefig(f"{output_dir}/{column}_histogram.png")
        plt.close()
    
    # Create a correlation heatmap
    if len(numeric_columns) > 1:
        plt.figure(figsize=(12, 10))
        sns.heatmap(df[numeric_columns].corr(), annot=True, cmap='coolwarm')
        plt.title('Correlation Heatmap')
        plt.savefig(f"{output_dir}/correlation_heatmap.png")
        plt.close()
    
    # If there's a date column, create a time series plot
    if 'date' in df.columns and pd.api.types.is_datetime64_dtype(df['date']):
        for column in numeric_columns:
            plt.figure(figsize=(12, 6))
            df.set_index('date')[column].plot()
            plt.title(f'{column} Over Time')
            plt.savefig(f"{output_dir}/{column}_timeseries.png")
            plt.close()

def save_results(analysis, output_file):
    """Save analysis results to a file."""
    if analysis is None:
        print("No analysis results to save.")
        return
    
    try:
        with open(output_file, 'w') as f:
            f.write("Data Analysis Results\n")
            f.write("====================\n\n")
            
            f.write("Summary Statistics:\n")
            f.write(str(analysis['summary']))
            f.write("\n\n")
            
            f.write("Missing Values:\n")
            f.write(str(analysis['missing_values']))
            f.write("\n\n")
            
            f.write("Correlations:\n")
            f.write(str(analysis['correlations']))
        
        print(f"Analysis results saved to {output_file}")
    except Exception as e:
        print(f"Error saving results: {e}")

def main():
    print("Data Analysis Project")
    
    # Get input file path
    file_path = input("Enter the path to the CSV file: ")
    
    # Load the data
    df = load_data(file_path)
    if df is None:
        return
    
    print(f"Loaded data with {df.shape[0]} rows and {df.shape[1]} columns.")
    
    # Clean the data
    cleaned_df = clean_data(df)
    if cleaned_df is None:
        return
    
    print(f"After cleaning: {cleaned_df.shape[0]} rows and {cleaned_df.shape[1]} columns.")
    
    # Analyze the data
    analysis = analyze_data(cleaned_df)
    
    # Create visualizations
    output_dir = "analysis_results"
    create_visualizations(cleaned_df, output_dir)
    
    # Save results
    save_results(analysis, f"{output_dir}/analysis_report.txt")
    
    print(f"Analysis complete. Results saved to {output_dir}/")

if __name__ == "__main__":
    main()
```

These mini-projects provide practical applications of the concepts covered in the handbook. They are designed to be challenging yet achievable for beginners and intermediate Python programmers. Each project focuses on different aspects of Python programming and can be extended with additional features as you become more comfortable with the language.
