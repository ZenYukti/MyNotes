# Unit-4: Python File Operations

---

## 1. Introduction to File Operations

### Why File Operations?
- **Persistent storage** - Data survives program termination
- **Large data handling** - Process data too big for memory
- **Data sharing** - Share data between programs
- **Configuration** - Store settings and preferences

### File Types
1. **Text Files** - Human-readable (.txt, .csv, .json)
2. **Binary Files** - Machine-readable (.exe, .bin, .dat)

### File Operations Flow
```
1. Open file
2. Perform operations (read/write)
3. Close file
```

---

## 2. Opening and Closing Files

### open() Function

**Syntax:**
```python
file_object = open(filename, mode)
```

### File Modes

| Mode | Description | Creates if Not Exists |
|------|-------------|-----------------------|
| `'r'` | Read (default) | No (Error) |
| `'w'` | Write (overwrites) | Yes |
| `'a'` | Append (adds to end) | Yes |
| `'x'` | Exclusive create | No (Error if exists) |
| `'r+'` | Read + Write | No |
| `'w+'` | Write + Read | Yes |
| `'a+'` | Append + Read | Yes |
| `'rb'` | Read binary | No |
| `'wb'` | Write binary | Yes |

### Basic File Operations

```python
# Open file for reading
file = open("sample.txt", "r")

# Perform operations
content = file.read()
print(content)

# Close file
file.close()
```

### Using with Statement (Recommended)

```python
# Automatically closes file
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here
```

**Advantages of `with`:**
- Automatic file closing
- Exception safe
- Cleaner code

---

## 3. Writing Files

### write() Method

**Writes string to file**

```python
# Write mode - overwrites existing content
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is Python file handling.\n")
    file.write("Writing to files is easy!")

print("File written successfully!")
```

**output.txt content:**
```
Hello, World!
This is Python file handling.
Writing to files is easy!
```

### writelines() Method

**Writes list of strings to file**

```python
lines = [
    "Line 1\n",
    "Line 2\n",
    "Line 3\n"
]

with open("output.txt", "w") as file:
    file.writelines(lines)

print("Multiple lines written!")
```

**output.txt content:**
```
Line 1
Line 2
Line 3
```

### Append Mode

```python
# Append mode - adds to end of file
with open("output.txt", "a") as file:
    file.write("Line 4\n")
    file.write("Line 5\n")

print("Lines appended!")
```

**output.txt content (after append):**
```
Line 1
Line 2
Line 3
Line 4
Line 5
```

### Write Examples

#### Example 1: Write Numbers
```python
# Write numbers 1 to 10
with open("numbers.txt", "w") as file:
    for i in range(1, 11):
        file.write(f"{i}\n")

print("Numbers written to file")
```

**numbers.txt:**
```
1
2
3
4
5
6
7
8
9
10
```

#### Example 2: Write Dictionary Data
```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

with open("student.txt", "w") as file:
    for key, value in student.items():
        file.write(f"{key}: {value}\n")
```

**student.txt:**
```
name: Alice
age: 20
grade: A
```

#### Example 3: Write List to CSV
```python
data = [
    ["Name", "Age", "Grade"],
    ["Alice", "20", "A"],
    ["Bob", "22", "B"],
    ["Charlie", "21", "A"]
]

with open("students.csv", "w") as file:
    for row in data:
        file.write(",".join(row) + "\n")
```

**students.csv:**
```
Name,Age,Grade
Alice,20,A
Bob,22,B
Charlie,21,A
```

---

## 4. Reading Files

### read() Method

**Reads entire file as string**

```python
# Read entire file
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)
    print(f"Type: {type(content)}")  # <class 'str'>
```

**Read specific number of characters:**
```python
with open("sample.txt", "r") as file:
    # Read first 10 characters
    first_10 = file.read(10)
    print(first_10)
    
    # Read next 10 characters
    next_10 = file.read(10)
    print(next_10)
```

### readline() Method

**Reads single line from file**

```python
with open("sample.txt", "r") as file:
    # Read first line
    line1 = file.readline()
    print("Line 1:", line1)
    
    # Read second line
    line2 = file.readline()
    print("Line 2:", line2)
    
    # Read third line
    line3 = file.readline()
    print("Line 3:", line3)
```

**Example: Read Until Empty**
```python
with open("sample.txt", "r") as file:
    line = file.readline()
    while line:
        print(line.strip())  # strip() removes \n
        line = file.readline()
```

### readlines() Method

**Reads all lines into list**

```python
with open("sample.txt", "r") as file:
    lines = file.readlines()
    print(f"Total lines: {len(lines)}")
    print(f"Type: {type(lines)}")  # <class 'list'>
    
    # Print each line
    for line in lines:
        print(line.strip())
```

### Iterating Through File

**Most Pythonic way:**
```python
with open("sample.txt", "r") as file:
    for line in file:
        print(line.strip())
```

### Comparison of Read Methods

| Method | Returns | Use Case |
|--------|---------|----------|
| `read()` | Entire file as string | Small files, need all content |
| `read(n)` | n characters | Process specific bytes |
| `readline()` | Single line | Process line by line |
| `readlines()` | List of lines | Need all lines as list |
| `for line in file` | Iterator | Large files, line-by-line |

### Read Examples

#### Example 1: Count Words
```python
with open("sample.txt", "r") as file:
    content = file.read()
    words = content.split()
    print(f"Total words: {len(words)}")
```

#### Example 2: Count Lines
```python
with open("sample.txt", "r") as file:
    lines = file.readlines()
    print(f"Total lines: {len(lines)}")
```

#### Example 3: Count Characters
```python
with open("sample.txt", "r") as file:
    content = file.read()
    print(f"Total characters: {len(content)}")
    
    # Without spaces
    no_spaces = content.replace(" ", "").replace("\n", "")
    print(f"Characters (no spaces): {len(no_spaces)}")
```

#### Example 4: Find Specific Word
```python
search_word = "Python"

with open("sample.txt", "r") as file:
    line_num = 0
    for line in file:
        line_num += 1
        if search_word in line:
            print(f"Found '{search_word}' at line {line_num}")
            print(f"Content: {line.strip()}")
```

#### Example 5: Read CSV File
```python
# Assuming students.csv exists
with open("students.csv", "r") as file:
    # Skip header
    header = file.readline()
    print("Header:", header.strip())
    print("\nStudents:")
    
    for line in file:
        data = line.strip().split(",")
        name, age, grade = data
        print(f"Name: {name}, Age: {age}, Grade: {grade}")
```

**Output:**
```
Header: Name,Age,Grade

Students:
Name: Alice, Age: 20, Grade: A
Name: Bob, Age: 22, Grade: B
Name: Charlie, Age: 21, Grade: A
```

---

## 5. File Pointer and seek()

### File Pointer
- **Current position** in file
- Moves as you read/write
- Can be controlled using `seek()` and `tell()`

### tell() Method

**Returns current position**

```python
with open("sample.txt", "r") as file:
    print(f"Initial position: {file.tell()}")  # 0
    
    file.read(10)
    print(f"After reading 10 chars: {file.tell()}")  # 10
    
    file.read(5)
    print(f"After reading 5 more: {file.tell()}")  # 15
```

### seek() Method

**Move file pointer to specific position**

**Syntax:**
```python
file.seek(offset, whence)
```

**Parameters:**
- `offset`: Number of bytes to move
- `whence`: Reference point
  - `0`: Start of file (default)
  - `1`: Current position
  - `2`: End of file

```python
with open("sample.txt", "r") as file:
    # Read first 10 characters
    print(file.read(10))
    
    # Move pointer to beginning
    file.seek(0)
    
    # Read first 10 again
    print(file.read(10))
    
    # Move to position 20
    file.seek(20)
    print(file.read(10))
```

### seek() Examples

#### Example 1: Read File Multiple Times
```python
with open("sample.txt", "r") as file:
    print("First read:")
    print(file.read())
    
    # Reset pointer to beginning
    file.seek(0)
    
    print("\nSecond read:")
    print(file.read())
```

#### Example 2: Read Specific Portion
```python
with open("sample.txt", "r") as file:
    # Skip first 20 characters
    file.seek(20)
    
    # Read next 30 characters
    content = file.read(30)
    print(content)
```

#### Example 3: Read Last N Characters
```python
with open("sample.txt", "r") as file:
    # Move to end
    file.seek(0, 2)
    file_size = file.tell()
    
    # Move to last 50 characters
    file.seek(file_size - 50)
    
    last_50 = file.read()
    print(last_50)
```

---

## 6. File Operations Examples

### Example 1: Copy File
```python
# Copy content from source to destination
with open("source.txt", "r") as source:
    content = source.read()

with open("destination.txt", "w") as dest:
    dest.write(content)

print("File copied successfully!")
```

### Example 2: Merge Files
```python
# Merge multiple files into one
files_to_merge = ["file1.txt", "file2.txt", "file3.txt"]

with open("merged.txt", "w") as output:
    for filename in files_to_merge:
        with open(filename, "r") as input_file:
            content = input_file.read()
            output.write(content)
            output.write("\n")  # Separator

print("Files merged successfully!")
```

### Example 3: Count Vowels in File
```python
vowels = "aeiouAEIOU"
vowel_count = 0

with open("sample.txt", "r") as file:
    content = file.read()
    for char in content:
        if char in vowels:
            vowel_count += 1

print(f"Total vowels: {vowel_count}")
```

### Example 4: Word Frequency
```python
word_count = {}

with open("sample.txt", "r") as file:
    for line in file:
        words = line.lower().split()
        for word in words:
            # Remove punctuation
            word = word.strip('.,!?;:"')
            if word:
                word_count[word] = word_count.get(word, 0) + 1

# Display top 5 frequent words
sorted_words = sorted(word_count.items(), key=lambda x: x[1], reverse=True)
print("Top 5 frequent words:")
for word, count in sorted_words[:5]:
    print(f"{word}: {count}")
```

### Example 5: Replace Word in File
```python
# Replace all occurrences of a word
old_word = "Python"
new_word = "Java"

with open("sample.txt", "r") as file:
    content = file.read()

# Replace
new_content = content.replace(old_word, new_word)

# Write back
with open("sample.txt", "w") as file:
    file.write(new_content)

print(f"Replaced '{old_word}' with '{new_word}'")
```

### Example 6: Student Database (CRUD Operations)
```python
import os

def add_student(name, roll, grade):
    with open("students.txt", "a") as file:
        file.write(f"{roll},{name},{grade}\n")
    print("Student added successfully!")

def view_students():
    if not os.path.exists("students.txt"):
        print("No students found!")
        return
    
    print("\n{:<10} {:<20} {:<10}".format("Roll No", "Name", "Grade"))
    print("-" * 40)
    
    with open("students.txt", "r") as file:
        for line in file:
            roll, name, grade = line.strip().split(",")
            print(f"{roll:<10} {name:<20} {grade:<10}")

def search_student(roll):
    found = False
    with open("students.txt", "r") as file:
        for line in file:
            r, name, grade = line.strip().split(",")
            if r == roll:
                print(f"\nRoll: {r}, Name: {name}, Grade: {grade}")
                found = True
                break
    
    if not found:
        print("Student not found!")

def delete_student(roll):
    lines = []
    found = False
    
    with open("students.txt", "r") as file:
        for line in file:
            r = line.strip().split(",")[0]
            if r != roll:
                lines.append(line)
            else:
                found = True
    
    if found:
        with open("students.txt", "w") as file:
            file.writelines(lines)
        print("Student deleted successfully!")
    else:
        print("Student not found!")

# Usage
add_student("Alice", "101", "A")
add_student("Bob", "102", "B")
add_student("Charlie", "103", "A")

view_students()
search_student("102")
delete_student("102")
view_students()
```

**Output:**
```
Student added successfully!
Student added successfully!
Student added successfully!

Roll No    Name                 Grade     
----------------------------------------
101        Alice                A         
102        Bob                  B         
103        Charlie              A         

Roll: 102, Name: Bob, Grade: B
Student deleted successfully!

Roll No    Name                 Grade     
----------------------------------------
101        Alice                A         
103        Charlie              A         
```

### Example 7: Log File Analysis
```python
# Analyze log file
error_count = 0
warning_count = 0
info_count = 0

with open("app.log", "r") as file:
    for line in file:
        if "ERROR" in line:
            error_count += 1
        elif "WARNING" in line:
            warning_count += 1
        elif "INFO" in line:
            info_count += 1

print("Log Summary:")
print(f"Errors: {error_count}")
print(f"Warnings: {warning_count}")
print(f"Info: {info_count}")
```

### Example 8: CSV to Dictionary
```python
# Read CSV and convert to list of dictionaries
students = []

with open("students.csv", "r") as file:
    # Read header
    header = file.readline().strip().split(",")
    
    # Read data
    for line in file:
        values = line.strip().split(",")
        student = dict(zip(header, values))
        students.append(student)

# Display
for student in students:
    print(student)
```

**Output:**
```
{'Name': 'Alice', 'Age': '20', 'Grade': 'A'}
{'Name': 'Bob', 'Age': '22', 'Grade': 'B'}
{'Name': 'Charlie', 'Age': '21', 'Grade': 'A'}
```

### Example 9: Filter Lines
```python
# Copy only lines containing specific word
keyword = "Python"

with open("source.txt", "r") as source:
    with open("filtered.txt", "w") as dest:
        for line in source:
            if keyword in line:
                dest.write(line)

print(f"Lines containing '{keyword}' copied to filtered.txt")
```

### Example 10: File Statistics
```python
import os

def file_stats(filename):
    if not os.path.exists(filename):
        print("File not found!")
        return
    
    with open(filename, "r") as file:
        content = file.read()
        lines = content.split("\n")
        words = content.split()
        chars = len(content)
        
        # Count non-empty lines
        non_empty_lines = sum(1 for line in lines if line.strip())
    
    # File size
    size = os.path.getsize(filename)
    
    print(f"File: {filename}")
    print(f"Size: {size} bytes")
    print(f"Lines: {non_empty_lines}")
    print(f"Words: {len(words)}")
    print(f"Characters: {chars}")

file_stats("sample.txt")
```

**Output:**
```
File: sample.txt
Size: 1024 bytes
Lines: 25
Words: 150
Characters: 1024
```

---

## 7. Exception Handling with Files

### Common File Exceptions

```python
# FileNotFoundError
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("Error: File not found!")

# PermissionError
try:
    with open("/system/protected.txt", "w") as file:
        file.write("data")
except PermissionError:
    print("Error: Permission denied!")

# IOError
try:
    with open("sample.txt", "r") as file:
        content = file.read()
except IOError:
    print("Error: I/O operation failed!")
```

### Complete Error Handling
```python
def safe_file_read(filename):
    try:
        with open(filename, "r") as file:
            content = file.read()
            return content
    except FileNotFoundError:
        print(f"Error: {filename} not found!")
        return None
    except PermissionError:
        print(f"Error: No permission to read {filename}!")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

# Usage
content = safe_file_read("sample.txt")
if content:
    print(content)
```

---

## 8. Binary File Operations

### Writing Binary Files
```python
# Write binary data
data = bytes([65, 66, 67, 68, 69])  # ASCII codes for ABCDE

with open("binary.bin", "wb") as file:
    file.write(data)

print("Binary file written!")
```

### Reading Binary Files
```python
# Read binary data
with open("binary.bin", "rb") as file:
    data = file.read()
    print(data)  # b'ABCDE'
    print(list(data))  # [65, 66, 67, 68, 69]
```

### Copy Binary File (e.g., Image)
```python
# Copy image file
with open("source.jpg", "rb") as source:
    with open("destination.jpg", "wb") as dest:
        dest.write(source.read())

print("Image copied successfully!")
```

---

## 9. Working with os Module

```python
import os

# Check if file exists
if os.path.exists("sample.txt"):
    print("File exists!")

# Get file size
size = os.path.getsize("sample.txt")
print(f"File size: {size} bytes")

# Rename file
os.rename("old_name.txt", "new_name.txt")

# Delete file
os.remove("temp.txt")

# Get current directory
print(f"Current directory: {os.getcwd()}")

# List files in directory
files = os.listdir(".")
print("Files:", files)

# Create directory
os.mkdir("new_folder")

# Check if path is file or directory
print(os.path.isfile("sample.txt"))  # True
print(os.path.isdir("folder"))       # True
```

---

## 🚀 Quick Reference Summary

### File Modes

| Mode | Read | Write | Create | Truncate |
|------|------|-------|--------|----------|
| `'r'` | ✓ | ✗ | ✗ | ✗ |
| `'w'` | ✗ | ✓ | ✓ | ✓ |
| `'a'` | ✗ | ✓ | ✓ | ✗ |
| `'r+'` | ✓ | ✓ | ✗ | ✗ |
| `'w+'` | ✓ | ✓ | ✓ | ✓ |
| `'a+'` | ✓ | ✓ | ✓ | ✗ |

### Read Functions

| Function | Returns | Moves Pointer |
|----------|---------|---------------|
| `read()` | Entire file | End |
| `read(n)` | n characters | n positions |
| `readline()` | One line | Next line |
| `readlines()` | List of lines | End |

### Write Functions

| Function | Parameter | Description |
|----------|-----------|-------------|
| `write()` | String | Write string |
| `writelines()` | List | Write list of strings |

### File Pointer

```python
file.tell()        # Get current position
file.seek(0)       # Move to beginning
file.seek(0, 2)    # Move to end
```

---

## 📝 Exam Important Questions

1. **Explain** different file opening modes with examples.

2. **Write a program** to copy content from one file to another.

3. **Demonstrate** the difference between read(), readline(), and readlines().

4. **Write a program** to count number of lines, words, and characters in a file.

5. **Explain** file pointer manipulation using seek() and tell().

6. **Write a program** to merge two files into a third file.

7. **Create a program** for student record management (add, view, search, delete).

8. **Explain** the importance of closing files and advantages of `with` statement.

9. **Write a program** to find and replace a word in a file.

10. **Create a program** to:
    - Read a CSV file
    - Calculate average of numeric column
    - Write result to new file

---

*End of Unit-4*
