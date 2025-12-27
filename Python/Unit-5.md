# Unit-5: Python Packages and GUI Programming

---

## 1. Python Packages

### What are Packages?
- **Collection of modules** organized in directories
- Provide **reusable code** for common tasks
- Installed using `pip` (Python Package Installer)

### Installing Packages
```bash
pip install package_name
pip install numpy
pip install pandas matplotlib
```

### Importing Packages
```python
import numpy
import numpy as np  # with alias
from numpy import array  # specific function
```

---

## 2. NumPy Package

### Introduction
- **Numerical Python** - fundamental package for scientific computing
- Provides powerful **N-dimensional array** objects
- Mathematical functions for arrays
- Linear algebra, Fourier transforms, random numbers

### Installation
```bash
pip install numpy
```

### NumPy Arrays

#### Creating Arrays
```python
import numpy as np

# From list
arr1 = np.array([1, 2, 3, 4, 5])
print(arr1)

# 2D array
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2)

# Array of zeros
zeros = np.zeros((3, 4))
print(zeros)

# Array of ones
ones = np.ones((2, 3))
print(ones)

# Range array
range_arr = np.arange(0, 10, 2)  # start, stop, step
print(range_arr)

# Linearly spaced
linear = np.linspace(0, 1, 5)  # 5 values from 0 to 1
print(linear)
```

**Output:**
```
[1 2 3 4 5]
[[1 2 3]
 [4 5 6]]
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
[[1. 1. 1.]
 [1. 1. 1.]]
[0 2 4 6 8]
[0.   0.25 0.5  0.75 1.  ]
```

#### Array Attributes
```python
import numpy as np

arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])

print(f"Shape: {arr.shape}")      # (2, 4)
print(f"Size: {arr.size}")        # 8
print(f"Dimensions: {arr.ndim}")  # 2
print(f"Data type: {arr.dtype}")  # int32/int64
```

**Output:**
```
Shape: (2, 4)
Size: 8
Dimensions: 2
Data type: int64
```

#### Array Operations
```python
import numpy as np

arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([5, 6, 7, 8])

# Arithmetic operations
print("Addition:", arr1 + arr2)
print("Subtraction:", arr1 - arr2)
print("Multiplication:", arr1 * arr2)
print("Division:", arr1 / arr2)
print("Power:", arr1 ** 2)

# Scalar operations
print("Add 10:", arr1 + 10)
print("Multiply by 2:", arr1 * 2)
```

**Output:**
```
Addition: [ 6  8 10 12]
Subtraction: [-4 -4 -4 -4]
Multiplication: [ 5 12 21 32]
Division: [0.2        0.33333333 0.42857143 0.5       ]
Power: [ 1  4  9 16]
Add 10: [11 12 13 14]
Multiply by 2: [2 4 6 8]
```

#### Array Indexing and Slicing
```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50])

# Indexing
print(arr[0])    # 10
print(arr[-1])   # 50

# Slicing
print(arr[1:4])  # [20 30 40]
print(arr[::2])  # [10 30 50]

# 2D array
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(arr2d[1, 2])     # 6
print(arr2d[0:2, 1:])  # [[2 3] [5 6]]
```

#### Mathematical Functions
```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

print("Sum:", np.sum(arr))          # 15
print("Mean:", np.mean(arr))        # 3.0
print("Median:", np.median(arr))    # 3.0
print("Std Dev:", np.std(arr))      # 1.414...
print("Min:", np.min(arr))          # 1
print("Max:", np.max(arr))          # 5
print("Sqrt:", np.sqrt(arr))
```

**Output:**
```
Sum: 15
Mean: 3.0
Median: 3.0
Std Dev: 1.4142135623730951
Min: 1
Max: 5
Sqrt: [1.         1.41421356 1.73205081 2.         2.23606798]
```

#### Example: Grade Analysis
```python
import numpy as np

# Student marks in 5 subjects
marks = np.array([85, 92, 78, 95, 88])

print(f"Marks: {marks}")
print(f"Total: {np.sum(marks)}")
print(f"Average: {np.mean(marks):.2f}")
print(f"Highest: {np.max(marks)}")
print(f"Lowest: {np.min(marks)}")
print(f"Passed subjects (>80): {np.sum(marks > 80)}")
```

**Output:**
```
Marks: [85 92 78 95 88]
Total: 438
Average: 87.60
Highest: 95
Lowest: 78
Passed subjects (>80): 4
```

---

## 3. Pandas Package

### Introduction
- **Data manipulation** and analysis library
- Works with **DataFrames** (table-like structure)
- Read/write various file formats (CSV, Excel, SQL)
- Data cleaning, transformation, aggregation

### Installation
```bash
pip install pandas
```

### Pandas Series
```python
import pandas as pd

# Create series
s = pd.Series([10, 20, 30, 40, 50])
print(s)

# With custom index
s2 = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
print(s2)
print(s2['b'])  # 20
```

**Output:**
```
0    10
1    20
2    30
3    40
4    50
dtype: int64

a    10
b    20
c    30
dtype: int64
20
```

### Pandas DataFrame

#### Creating DataFrame
```python
import pandas as pd

# From dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [20, 22, 21],
    'Grade': ['A', 'B', 'A']
}

df = pd.DataFrame(data)
print(df)
```

**Output:**
```
      Name  Age Grade
0    Alice   20     A
1      Bob   22     B
2  Charlie   21     A
```

#### Reading CSV Files
```python
import pandas as pd

# Read CSV
df = pd.read_csv('students.csv')
print(df)

# Display first 5 rows
print(df.head())

# Display last 5 rows
print(df.tail())

# Display info
print(df.info())

# Display statistics
print(df.describe())
```

#### DataFrame Operations
```python
import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David'],
    'Age': [20, 22, 21, 23],
    'Grade': ['A', 'B', 'A', 'C'],
    'Marks': [85, 72, 90, 68]
}

df = pd.DataFrame(data)

# Select column
print(df['Name'])
print(df[['Name', 'Age']])

# Filter rows
print(df[df['Marks'] > 80])

# Sort
print(df.sort_values('Marks', ascending=False))

# Add new column
df['Pass'] = df['Marks'] > 70
print(df)
```

**Output:**
```
0      Alice
1        Bob
2    Charlie
3      David
Name: Name, dtype: object

      Name  Age
0    Alice   20
1      Bob   22
2  Charlie   21
3    David   23

      Name  Age Grade  Marks
0    Alice   20     A     85
2  Charlie   21     A     90

      Name  Age Grade  Marks
2  Charlie   21     A     90
0    Alice   20     A     85
1      Bob   22     B     72
3    David   23     C     68

      Name  Age Grade  Marks   Pass
0    Alice   20     A     85   True
1      Bob   22     B     72   True
2  Charlie   21     A     90   True
3    David   23     C     68  False
```

#### Grouping and Aggregation
```python
import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Department': ['CS', 'IT', 'CS', 'IT', 'CS'],
    'Marks': [85, 72, 90, 68, 88]
}

df = pd.DataFrame(data)

# Group by department
grouped = df.groupby('Department')

# Calculate mean marks by department
print(grouped['Marks'].mean())

# Count students by department
print(grouped.size())
```

**Output:**
```
Department
CS    87.666667
IT    70.000000
Name: Marks, dtype: float64

Department
CS    3
IT    2
dtype: int64
```

#### Example: Sales Data Analysis
```python
import pandas as pd

# Sales data
sales = {
    'Product': ['Laptop', 'Mouse', 'Keyboard', 'Monitor', 'Laptop', 'Mouse'],
    'Quantity': [2, 5, 3, 1, 1, 8],
    'Price': [50000, 500, 1500, 15000, 50000, 500]
}

df = pd.DataFrame(sales)
df['Total'] = df['Quantity'] * df['Price']

print(df)
print(f"\nTotal Sales: ₹{df['Total'].sum()}")
print(f"\nSales by Product:")
print(df.groupby('Product')['Total'].sum())
```

**Output:**
```
    Product  Quantity  Price   Total
0    Laptop         2  50000  100000
1     Mouse         5    500    2500
2  Keyboard         3   1500    4500
3   Monitor         1  15000   15000
4    Laptop         1  50000   50000
5     Mouse         8    500    4000

Total Sales: ₹176000

Sales by Product:
Product
Keyboard      4500
Laptop      150000
Monitor      15000
Mouse         6500
Name: Total, dtype: int64
```

---

## 4. Matplotlib Package

### Introduction
- **Data visualization** library
- Create **plots, charts, graphs**
- Supports various plot types (line, bar, scatter, pie, histogram)

### Installation
```bash
pip install matplotlib
```

### Line Plot
```python
import matplotlib.pyplot as plt

# Data
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

# Plot
plt.plot(x, y)
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Simple Line Plot')
plt.grid(True)
plt.show()
```

### Multiple Lines
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y1 = [1, 4, 9, 16, 25]
y2 = [1, 2, 3, 4, 5]

plt.plot(x, y1, label='Quadratic', color='red', marker='o')
plt.plot(x, y2, label='Linear', color='blue', marker='s')

plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Multiple Lines')
plt.legend()
plt.grid(True)
plt.show()
```

### Bar Chart
```python
import matplotlib.pyplot as plt

# Data
categories = ['A', 'B', 'C', 'D']
values = [25, 40, 30, 55]

# Bar chart
plt.bar(categories, values, color='skyblue')
plt.xlabel('Categories')
plt.ylabel('Values')
plt.title('Bar Chart')
plt.show()
```

### Horizontal Bar Chart
```python
import matplotlib.pyplot as plt

subjects = ['Math', 'Physics', 'Chemistry', 'English']
marks = [85, 92, 78, 88]

plt.barh(subjects, marks, color='coral')
plt.xlabel('Marks')
plt.ylabel('Subjects')
plt.title('Student Marks')
plt.show()
```

### Scatter Plot
```python
import matplotlib.pyplot as plt

# Data
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = [2, 4, 5, 7, 6, 8, 9, 11, 10, 12]

# Scatter plot
plt.scatter(x, y, color='green', marker='*', s=100)
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot')
plt.grid(True)
plt.show()
```

### Pie Chart
```python
import matplotlib.pyplot as plt

# Data
languages = ['Python', 'Java', 'JavaScript', 'C++']
popularity = [40, 25, 20, 15]

# Pie chart
plt.pie(popularity, labels=languages, autopct='%1.1f%%', startangle=90)
plt.title('Programming Language Popularity')
plt.show()
```

### Histogram
```python
import matplotlib.pyplot as plt

# Data - student marks
marks = [45, 67, 89, 56, 78, 90, 65, 54, 88, 92, 
         73, 68, 85, 91, 77, 62, 58, 95, 87, 71]

# Histogram
plt.hist(marks, bins=5, color='purple', edgecolor='black')
plt.xlabel('Marks Range')
plt.ylabel('Frequency')
plt.title('Distribution of Student Marks')
plt.show()
```

### Subplots
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

# Create 2x2 subplots
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

# Plot 1: Line
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title('Sine Wave')

# Plot 2: Cosine
axes[0, 1].plot(x, np.cos(x), 'r')
axes[0, 1].set_title('Cosine Wave')

# Plot 3: Exponential
axes[1, 0].plot(x, np.exp(x/10), 'g')
axes[1, 0].set_title('Exponential')

# Plot 4: Log
axes[1, 1].plot(x[1:], np.log(x[1:]), 'm')
axes[1, 1].set_title('Logarithm')

plt.tight_layout()
plt.show()
```

### Example: Sales Visualization
```python
import matplotlib.pyplot as plt

months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
sales = [15000, 18000, 22000, 19000, 25000, 28000]

# Create figure with subplots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5))

# Line plot
ax1.plot(months, sales, marker='o', color='blue', linewidth=2)
ax1.set_xlabel('Months')
ax1.set_ylabel('Sales (₹)')
ax1.set_title('Monthly Sales Trend')
ax1.grid(True)

# Bar plot
ax2.bar(months, sales, color='green')
ax2.set_xlabel('Months')
ax2.set_ylabel('Sales (₹)')
ax2.set_title('Monthly Sales Comparison')

plt.tight_layout()
plt.show()
```

---

## 5. Integrated Example: Data Analysis Pipeline

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Generate sample data
np.random.seed(42)
students = 50
marks = np.random.randint(40, 100, students)

# Step 2: Create DataFrame
df = pd.DataFrame({
    'Student_ID': range(1, students + 1),
    'Marks': marks
})

# Add grade column
def get_grade(mark):
    if mark >= 90:
        return 'A+'
    elif mark >= 80:
        return 'A'
    elif mark >= 70:
        return 'B'
    elif mark >= 60:
        return 'C'
    else:
        return 'F'

df['Grade'] = df['Marks'].apply(get_grade)

# Step 3: Analysis
print("Statistical Summary:")
print(df['Marks'].describe())
print(f"\nTotal Students: {len(df)}")
print(f"Average Marks: {df['Marks'].mean():.2f}")
print(f"Highest Marks: {df['Marks'].max()}")
print(f"Lowest Marks: {df['Marks'].min()}")

print("\nGrade Distribution:")
print(df['Grade'].value_counts())

# Step 4: Visualization
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Histogram
axes[0, 0].hist(df['Marks'], bins=10, color='skyblue', edgecolor='black')
axes[0, 0].set_xlabel('Marks')
axes[0, 0].set_ylabel('Frequency')
axes[0, 0].set_title('Distribution of Marks')
axes[0, 0].grid(True, alpha=0.3)

# Box plot
axes[0, 1].boxplot(df['Marks'])
axes[0, 1].set_ylabel('Marks')
axes[0, 1].set_title('Box Plot of Marks')
axes[0, 1].grid(True, alpha=0.3)

# Grade distribution - Bar
grade_counts = df['Grade'].value_counts()
axes[1, 0].bar(grade_counts.index, grade_counts.values, color='coral')
axes[1, 0].set_xlabel('Grade')
axes[1, 0].set_ylabel('Number of Students')
axes[1, 0].set_title('Grade Distribution')

# Grade distribution - Pie
axes[1, 1].pie(grade_counts.values, labels=grade_counts.index, 
               autopct='%1.1f%%', startangle=90)
axes[1, 1].set_title('Grade Distribution (%)')

plt.tight_layout()
plt.savefig('analysis_report.png')
plt.show()

# Step 5: Save report
df.to_csv('student_report.csv', index=False)
print("\nReport saved to 'student_report.csv'")
```

**Output:**
```
Statistical Summary:
count    50.000000
mean     69.340000
std      16.582644
min      40.000000
25%      57.250000
50%      69.500000
75%      83.750000
max      99.000000
Name: Marks, dtype: float64

Total Students: 50
Average Marks: 69.34
Highest Marks: 99
Lowest Marks: 40

Grade Distribution:
B     16
C     13
A     10
F      6
A+     5
Name: Grade, dtype: int64

Report saved to 'student_report.csv'
```

---

## 6. GUI Programming with Tkinter

### Introduction to Tkinter
- **Standard GUI library** for Python
- Built-in (no installation needed)
- Cross-platform (Windows, Mac, Linux)
- Event-driven programming

### First Tkinter Program
```python
import tkinter as tk

# Create main window
root = tk.Tk()
root.title("My First GUI")
root.geometry("400x300")

# Add label
label = tk.Label(root, text="Hello, Tkinter!", font=("Arial", 16))
label.pack(pady=20)

# Run application
root.mainloop()
```

### Tkinter Widgets

#### Label Widget
```python
import tkinter as tk

root = tk.Tk()
root.title("Label Example")

# Simple label
label1 = tk.Label(root, text="Simple Label")
label1.pack()

# Styled label
label2 = tk.Label(root, 
                  text="Styled Label",
                  font=("Arial", 14, "bold"),
                  fg="blue",
                  bg="yellow")
label2.pack(pady=10)

root.mainloop()
```

#### Button Widget
```python
import tkinter as tk

def button_click():
    label.config(text="Button Clicked!")

root = tk.Tk()
root.title("Button Example")

label = tk.Label(root, text="Click the button")
label.pack(pady=10)

button = tk.Button(root, 
                   text="Click Me",
                   command=button_click,
                   font=("Arial", 12),
                   bg="green",
                   fg="white")
button.pack(pady=10)

root.mainloop()
```

#### Entry Widget (Text Input)
```python
import tkinter as tk

def show_input():
    text = entry.get()
    label.config(text=f"You entered: {text}")

root = tk.Tk()
root.title("Entry Example")

label = tk.Label(root, text="Enter your name:")
label.pack(pady=10)

entry = tk.Entry(root, width=30)
entry.pack(pady=5)

button = tk.Button(root, text="Submit", command=show_input)
button.pack(pady=10)

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

#### Text Widget (Multi-line)
```python
import tkinter as tk

def get_text():
    content = text.get("1.0", "end-1c")
    print(content)

root = tk.Tk()
root.title("Text Widget")

text = tk.Text(root, width=40, height=10)
text.pack(pady=10)

button = tk.Button(root, text="Get Text", command=get_text)
button.pack()

root.mainloop()
```

#### Checkbutton Widget
```python
import tkinter as tk

def show_choices():
    result = []
    if var1.get():
        result.append("Python")
    if var2.get():
        result.append("Java")
    if var3.get():
        result.append("C++")
    
    label.config(text=f"Selected: {', '.join(result)}")

root = tk.Tk()
root.title("Checkbutton Example")

tk.Label(root, text="Select languages:").pack()

var1 = tk.BooleanVar()
var2 = tk.BooleanVar()
var3 = tk.BooleanVar()

tk.Checkbutton(root, text="Python", variable=var1).pack()
tk.Checkbutton(root, text="Java", variable=var2).pack()
tk.Checkbutton(root, text="C++", variable=var3).pack()

tk.Button(root, text="Show Selection", command=show_choices).pack(pady=10)

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

#### Radiobutton Widget
```python
import tkinter as tk

def show_choice():
    label.config(text=f"Selected: {var.get()}")

root = tk.Tk()
root.title("Radiobutton Example")

tk.Label(root, text="Select your favorite:").pack()

var = tk.StringVar()
var.set("Python")  # default value

tk.Radiobutton(root, text="Python", variable=var, value="Python").pack()
tk.Radiobutton(root, text="Java", variable=var, value="Java").pack()
tk.Radiobutton(root, text="C++", variable=var, value="C++").pack()

tk.Button(root, text="Show Selection", command=show_choice).pack(pady=10)

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

#### Listbox Widget
```python
import tkinter as tk

def show_selection():
    selection = listbox.curselection()
    if selection:
        item = listbox.get(selection[0])
        label.config(text=f"Selected: {item}")

root = tk.Tk()
root.title("Listbox Example")

listbox = tk.Listbox(root, height=5)
listbox.pack(pady=10)

items = ["Apple", "Banana", "Cherry", "Date", "Elderberry"]
for item in items:
    listbox.insert(tk.END, item)

tk.Button(root, text="Show Selection", command=show_selection).pack()

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

#### Combobox (Dropdown)
```python
import tkinter as tk
from tkinter import ttk

def show_selection():
    label.config(text=f"Selected: {combo.get()}")

root = tk.Tk()
root.title("Combobox Example")

tk.Label(root, text="Select country:").pack(pady=10)

combo = ttk.Combobox(root, values=["India", "USA", "UK", "Canada"])
combo.pack()
combo.current(0)  # Set default selection

tk.Button(root, text="Show Selection", command=show_selection).pack(pady=10)

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

### Layout Management

#### pack() Method
```python
import tkinter as tk

root = tk.Tk()

tk.Label(root, text="Top", bg="red").pack(side=tk.TOP, fill=tk.X)
tk.Label(root, text="Bottom", bg="green").pack(side=tk.BOTTOM, fill=tk.X)
tk.Label(root, text="Left", bg="yellow").pack(side=tk.LEFT, fill=tk.Y)
tk.Label(root, text="Right", bg="blue").pack(side=tk.RIGHT, fill=tk.Y)

root.mainloop()
```

#### grid() Method
```python
import tkinter as tk

root = tk.Tk()
root.title("Grid Layout")

tk.Label(root, text="Name:").grid(row=0, column=0, padx=10, pady=5)
tk.Entry(root).grid(row=0, column=1, padx=10, pady=5)

tk.Label(root, text="Email:").grid(row=1, column=0, padx=10, pady=5)
tk.Entry(root).grid(row=1, column=1, padx=10, pady=5)

tk.Button(root, text="Submit").grid(row=2, column=0, columnspan=2, pady=10)

root.mainloop()
```

#### place() Method
```python
import tkinter as tk

root = tk.Tk()
root.geometry("400x300")

tk.Label(root, text="Absolute Position", bg="yellow").place(x=50, y=50)
tk.Button(root, text="Button").place(x=150, y=100)

root.mainloop()
```

### Complete GUI Examples

#### Example 1: Simple Calculator
```python
import tkinter as tk

def calculate():
    try:
        result = eval(entry.get())
        label_result.config(text=f"Result: {result}")
    except:
        label_result.config(text="Error: Invalid expression")

root = tk.Tk()
root.title("Simple Calculator")
root.geometry("300x200")

tk.Label(root, text="Enter expression:", font=("Arial", 12)).pack(pady=10)

entry = tk.Entry(root, width=30, font=("Arial", 12))
entry.pack(pady=5)

tk.Button(root, text="Calculate", command=calculate, 
          font=("Arial", 12), bg="green", fg="white").pack(pady=10)

label_result = tk.Label(root, text="", font=("Arial", 12, "bold"))
label_result.pack(pady=10)

root.mainloop()
```

#### Example 2: Temperature Converter
```python
import tkinter as tk

def celsius_to_fahrenheit():
    try:
        celsius = float(entry_celsius.get())
        fahrenheit = (celsius * 9/5) + 32
        entry_fahrenheit.delete(0, tk.END)
        entry_fahrenheit.insert(0, f"{fahrenheit:.2f}")
    except:
        entry_fahrenheit.delete(0, tk.END)
        entry_fahrenheit.insert(0, "Error")

def fahrenheit_to_celsius():
    try:
        fahrenheit = float(entry_fahrenheit.get())
        celsius = (fahrenheit - 32) * 5/9
        entry_celsius.delete(0, tk.END)
        entry_celsius.insert(0, f"{celsius:.2f}")
    except:
        entry_celsius.delete(0, tk.END)
        entry_celsius.insert(0, "Error")

root = tk.Tk()
root.title("Temperature Converter")
root.geometry("300x200")

tk.Label(root, text="Celsius:").grid(row=0, column=0, padx=10, pady=10)
entry_celsius = tk.Entry(root)
entry_celsius.grid(row=0, column=1, padx=10, pady=10)

tk.Label(root, text="Fahrenheit:").grid(row=1, column=0, padx=10, pady=10)
entry_fahrenheit = tk.Entry(root)
entry_fahrenheit.grid(row=1, column=1, padx=10, pady=10)

tk.Button(root, text="C → F", command=celsius_to_fahrenheit).grid(row=2, column=0, pady=10)
tk.Button(root, text="F → C", command=fahrenheit_to_celsius).grid(row=2, column=1, pady=10)

root.mainloop()
```

#### Example 3: Login Form
```python
import tkinter as tk
from tkinter import messagebox

def login():
    username = entry_username.get()
    password = entry_password.get()
    
    if username == "admin" and password == "1234":
        messagebox.showinfo("Success", "Login Successful!")
    else:
        messagebox.showerror("Error", "Invalid credentials!")

root = tk.Tk()
root.title("Login Form")
root.geometry("300x200")

tk.Label(root, text="Username:", font=("Arial", 12)).grid(row=0, column=0, padx=10, pady=10)
entry_username = tk.Entry(root, font=("Arial", 12))
entry_username.grid(row=0, column=1, padx=10, pady=10)

tk.Label(root, text="Password:", font=("Arial", 12)).grid(row=1, column=0, padx=10, pady=10)
entry_password = tk.Entry(root, show="*", font=("Arial", 12))
entry_password.grid(row=1, column=1, padx=10, pady=10)

tk.Button(root, text="Login", command=login, 
          font=("Arial", 12), bg="blue", fg="white").grid(row=2, column=0, columnspan=2, pady=20)

root.mainloop()
```

#### Example 4: To-Do List
```python
import tkinter as tk

def add_task():
    task = entry.get()
    if task:
        listbox.insert(tk.END, task)
        entry.delete(0, tk.END)

def delete_task():
    try:
        selection = listbox.curselection()
        listbox.delete(selection)
    except:
        pass

def clear_all():
    listbox.delete(0, tk.END)

root = tk.Tk()
root.title("To-Do List")
root.geometry("400x400")

tk.Label(root, text="To-Do List", font=("Arial", 16, "bold")).pack(pady=10)

frame_input = tk.Frame(root)
frame_input.pack(pady=10)

entry = tk.Entry(frame_input, width=30, font=("Arial", 12))
entry.pack(side=tk.LEFT, padx=5)

tk.Button(frame_input, text="Add", command=add_task, bg="green", fg="white").pack(side=tk.LEFT)

listbox = tk.Listbox(root, width=40, height=10, font=("Arial", 11))
listbox.pack(pady=10)

frame_buttons = tk.Frame(root)
frame_buttons.pack(pady=10)

tk.Button(frame_buttons, text="Delete Selected", command=delete_task, 
          bg="red", fg="white").pack(side=tk.LEFT, padx=5)
tk.Button(frame_buttons, text="Clear All", command=clear_all, 
          bg="orange", fg="white").pack(side=tk.LEFT, padx=5)

root.mainloop()
```

#### Example 5: Student Registration Form
```python
import tkinter as tk
from tkinter import messagebox

def submit():
    name = entry_name.get()
    roll = entry_roll.get()
    age = entry_age.get()
    gender = var_gender.get()
    course = combo_course.get()
    
    if name and roll and age:
        message = f"Name: {name}\nRoll: {roll}\nAge: {age}\nGender: {gender}\nCourse: {course}"
        messagebox.showinfo("Registration Successful", message)
    else:
        messagebox.showwarning("Warning", "Please fill all fields!")

def clear():
    entry_name.delete(0, tk.END)
    entry_roll.delete(0, tk.END)
    entry_age.delete(0, tk.END)
    var_gender.set("Male")
    combo_course.current(0)

root = tk.Tk()
root.title("Student Registration")
root.geometry("400x400")

tk.Label(root, text="Student Registration Form", 
         font=("Arial", 16, "bold")).grid(row=0, column=0, columnspan=2, pady=20)

tk.Label(root, text="Name:", font=("Arial", 12)).grid(row=1, column=0, padx=10, pady=10, sticky="e")
entry_name = tk.Entry(root, width=25, font=("Arial", 12))
entry_name.grid(row=1, column=1, padx=10, pady=10)

tk.Label(root, text="Roll No:", font=("Arial", 12)).grid(row=2, column=0, padx=10, pady=10, sticky="e")
entry_roll = tk.Entry(root, width=25, font=("Arial", 12))
entry_roll.grid(row=2, column=1, padx=10, pady=10)

tk.Label(root, text="Age:", font=("Arial", 12)).grid(row=3, column=0, padx=10, pady=10, sticky="e")
entry_age = tk.Entry(root, width=25, font=("Arial", 12))
entry_age.grid(row=3, column=1, padx=10, pady=10)

tk.Label(root, text="Gender:", font=("Arial", 12)).grid(row=4, column=0, padx=10, pady=10, sticky="e")
var_gender = tk.StringVar()
var_gender.set("Male")
frame_gender = tk.Frame(root)
frame_gender.grid(row=4, column=1, sticky="w")
tk.Radiobutton(frame_gender, text="Male", variable=var_gender, value="Male").pack(side=tk.LEFT)
tk.Radiobutton(frame_gender, text="Female", variable=var_gender, value="Female").pack(side=tk.LEFT)

tk.Label(root, text="Course:", font=("Arial", 12)).grid(row=5, column=0, padx=10, pady=10, sticky="e")
from tkinter import ttk
combo_course = ttk.Combobox(root, values=["B.Tech", "M.Tech", "BCA", "MCA"], 
                             width=23, font=("Arial", 12))
combo_course.grid(row=5, column=1, padx=10, pady=10)
combo_course.current(0)

frame_buttons = tk.Frame(root)
frame_buttons.grid(row=6, column=0, columnspan=2, pady=20)

tk.Button(frame_buttons, text="Submit", command=submit, 
          width=10, bg="green", fg="white", font=("Arial", 12)).pack(side=tk.LEFT, padx=5)
tk.Button(frame_buttons, text="Clear", command=clear, 
          width=10, bg="red", fg="white", font=("Arial", 12)).pack(side=tk.LEFT, padx=5)

root.mainloop()
```

---

## 7. Working with Python IDEs

### Popular Python IDEs

1. **PyCharm** - Professional IDE by JetBrains
   - Features: Code completion, debugging, version control
   - Community (free) and Professional editions

2. **VS Code** - Lightweight, extensible
   - Python extension required
   - IntelliSense, debugging, Jupyter support

3. **Jupyter Notebook** - Interactive computing
   - Web-based interface
   - Great for data science and visualization

4. **Spyder** - Scientific Python Development
   - Comes with Anaconda
   - Variable explorer, IPython console

5. **IDLE** - Python's built-in IDE
   - Lightweight and simple
   - Good for beginners

### Running Python Programs in IDE

**PyCharm:**
- Right-click file → Run
- Or press Shift+F10

**VS Code:**
- Click Run button (▶)
- Or press F5

**Jupyter Notebook:**
- Click Run cell button
- Or press Shift+Enter

---

## 🚀 Quick Reference Summary

### Package Installation
```bash
pip install numpy pandas matplotlib
```

### NumPy Basics
```python
import numpy as np
arr = np.array([1, 2, 3])
np.mean(arr), np.sum(arr), np.max(arr)
```

### Pandas Basics
```python
import pandas as pd
df = pd.read_csv('file.csv')
df.head(), df.info(), df.describe()
```

### Matplotlib Basics
```python
import matplotlib.pyplot as plt
plt.plot(x, y)
plt.xlabel('X'), plt.ylabel('Y')
plt.title('Title')
plt.show()
```

### Tkinter Basics
```python
import tkinter as tk
root = tk.Tk()
tk.Label(root, text="Hello").pack()
root.mainloop()
```

---

## 📝 Exam Important Questions

1. **Explain** NumPy arrays and their advantages over Python lists.

2. **Write a program** using NumPy to:
   - Create array of 10 random numbers
   - Calculate mean, median, standard deviation
   - Find max and min values

3. **Demonstrate** Pandas DataFrame operations:
   - Creating DataFrame
   - Reading CSV
   - Filtering and sorting data

4. **Create a program** using Matplotlib to visualize student marks with:
   - Bar chart
   - Pie chart
   - Histogram

5. **Explain** different Tkinter widgets with examples.

6. **Create a GUI application** with:
   - Entry fields for name and email
   - Submit button
   - Display entered information

7. **Write a program** to analyze sales data using Pandas and visualize with Matplotlib.

8. **Create a calculator GUI** using Tkinter with all basic operations.

9. **Explain** layout management in Tkinter (pack, grid, place).

10. **Develop a complete application** combining:
    - File operations (read student data from CSV)
    - Pandas (data processing)
    - Matplotlib (data visualization)
    - Tkinter (GUI interface)

---

*End of Unit-5*

*All Python Units Complete! 🎉*
