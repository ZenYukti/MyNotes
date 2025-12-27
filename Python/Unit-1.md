# Unit-1: Introduction to Python

---

## 1. Introduction to Python

### What is Python?
- **High-level**, **interpreted** programming language
- Created by **Guido van Rossum** (1991)
- **Easy to learn** - Simple, readable syntax
- **Versatile** - Web development, data science, AI, automation

### Features
- **Interpreted** - No compilation needed
- **Dynamically Typed** - No need to declare variable types
- **Object-Oriented** - Supports OOP concepts
- **Extensive Libraries** - Large standard library
- **Cross-platform** - Works on Windows, Linux, Mac

### Python Syntax Basics
```python
# This is a comment
print("Hello, World!")  # Output to console

# Indentation is important (not braces)
if True:
    print("Indented block")
```

**Output:**
```
Hello, World!
Indented block
```

---

## 2. Python Variables

### Definition
- **Variable**: Container to store data
- **No declaration needed** - Dynamic typing
- **Case-sensitive** - `name` ≠ `Name`

### Variable Assignment
```python
# Simple assignment
x = 10
name = "Python"
pi = 3.14
is_valid = True

print(x)        # 10
print(name)     # Python
print(pi)       # 3.14
print(is_valid) # True
```

**Output:**
```
10
Python
3.14
True
```

### Multiple Assignment
```python
# Assign same value to multiple variables
a = b = c = 100
print(a, b, c)  # 100 100 100

# Assign multiple values
x, y, z = 10, 20, 30
print(x, y, z)  # 10 20 30

# Swap variables
a, b = 5, 10
a, b = b, a  # Swap
print(a, b)  # 10 5
```

**Output:**
```
100 100 100
10 20 30
10 5
```

### Variable Naming Rules

| Rule | Example | Valid? |
|------|---------|--------|
| Start with letter or _ | `name`, `_value` | ✓ |
| Can contain letters, digits, _ | `var1`, `my_var` | ✓ |
| Cannot start with digit | `1var` | ✗ |
| Cannot use keywords | `if`, `for` | ✗ |
| Case-sensitive | `Name` ≠ `name` | ✓ |

```python
# Valid variable names
age = 25
_count = 10
firstName = "John"
my_variable_1 = 100

# Invalid variable names
# 1name = 10      # SyntaxError
# my-var = 20     # SyntaxError
# for = 5         # SyntaxError (keyword)
```

### Variable Types (Dynamic Typing)
```python
# Variable type changes automatically
x = 10          # int
print(type(x))  # <class 'int'>

x = "Hello"     # now string
print(type(x))  # <class 'str'>

x = 3.14        # now float
print(type(x))  # <class 'float'>
```

**Output:**
```
<class 'int'>
<class 'str'>
<class 'float'>
```

---

## 3. Python Basic Operators

### 1. Arithmetic Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division (float) | `5 / 2` | `2.5` |
| `//` | Floor Division | `5 // 2` | `2` |
| `%` | Modulus (remainder) | `5 % 2` | `1` |
| `**` | Exponentiation | `5 ** 2` | `25` |

```python
a = 10
b = 3

print("Addition:", a + b)         # 13
print("Subtraction:", a - b)      # 7
print("Multiplication:", a * b)   # 30
print("Division:", a / b)         # 3.333...
print("Floor Division:", a // b)  # 3
print("Modulus:", a % b)          # 1
print("Exponentiation:", a ** b)  # 1000
```

**Output:**
```
Addition: 13
Subtraction: 7
Multiplication: 30
Division: 3.3333333333333335
Floor Division: 3
Modulus: 1
Exponentiation: 1000
```

### 2. Comparison Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `5 <= 3` | `False` |

```python
x = 10
y = 20

print(x == y)   # False
print(x != y)   # True
print(x > y)    # False
print(x < y)    # True
print(x >= 10)  # True
print(x <= 5)   # False
```

**Output:**
```
False
True
False
True
True
False
```

### 3. Logical Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `and` | Both conditions True | `True and False` | `False` |
| `or` | At least one True | `True or False` | `True` |
| `not` | Negation | `not True` | `False` |

```python
a = True
b = False

print(a and b)  # False
print(a or b)   # True
print(not a)    # False
print(not b)    # True

# Practical example
age = 25
has_license = True

can_drive = age >= 18 and has_license
print("Can drive:", can_drive)  # True
```

**Output:**
```
False
True
False
True
Can drive: True
```

### 4. Assignment Operators

| Operator | Example | Equivalent |
|----------|---------|------------|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |
| `//=` | `x //= 3` | `x = x // 3` |
| `%=` | `x %= 3` | `x = x % 3` |
| `**=` | `x **= 3` | `x = x ** 3` |

```python
x = 10

x += 5   # x = x + 5
print(x)  # 15

x -= 3   # x = x - 3
print(x)  # 12

x *= 2   # x = x * 2
print(x)  # 24

x //= 5  # x = x // 5
print(x)  # 4
```

**Output:**
```
15
12
24
4
```

### 5. Identity Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `is` | Same object | `x is y` |
| `is not` | Different objects | `x is not y` |

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)      # True (same values)
print(a is b)      # False (different objects)
print(a is c)      # True (same object)
print(a is not b)  # True
```

**Output:**
```
True
False
True
True
```

### 6. Membership Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `in` | Element exists | `'a' in 'apple'` |
| `not in` | Element doesn't exist | `'x' not in 'apple'` |

```python
fruits = ["apple", "banana", "cherry"]

print("apple" in fruits)      # True
print("grape" in fruits)      # False
print("grape" not in fruits)  # True

text = "Hello World"
print("Hello" in text)        # True
print("hello" in text)        # False (case-sensitive)
```

**Output:**
```
True
False
True
True
False
```

### Operator Precedence

**Highest to Lowest:**
1. `**` (Exponentiation)
2. `*, /, //, %` (Multiplication, Division)
3. `+, -` (Addition, Subtraction)
4. `==, !=, >, <, >=, <=` (Comparison)
5. `not` (Logical NOT)
6. `and` (Logical AND)
7. `or` (Logical OR)

```python
result = 10 + 5 * 2
print(result)  # 20 (not 30, because * has higher precedence)

result = (10 + 5) * 2
print(result)  # 30 (parentheses first)

result = 10 > 5 and 20 < 30
print(result)  # True
```

**Output:**
```
20
30
True
```

---

## 4. Understanding Python Blocks

### Indentation
- Python uses **indentation** (spaces/tabs) to define blocks
- **No braces** `{}` like C/Java
- **Consistent indentation** required (usually 4 spaces)

```python
# Correct indentation
if True:
    print("Inside if block")
    print("Still inside")
print("Outside if block")
```

**Output:**
```
Inside if block
Still inside
Outside if block
```

### Indentation Error Example
```python
# Wrong indentation - IndentationError
if True:
print("Error!")  # IndentationError: expected an indented block

# Inconsistent indentation - IndentationError
if True:
    print("Line 1")
      print("Line 2")  # IndentationError: unexpected indent
```

### Nested Blocks
```python
x = 10

if x > 5:
    print("x is greater than 5")
    if x > 8:
        print("x is also greater than 8")
    print("Back to first if block")
print("Outside all blocks")
```

**Output:**
```
x is greater than 5
x is also greater than 8
Back to first if block
Outside all blocks
```

### Block Examples
```python
# Function block
def greet():
    print("Hello!")
    print("Welcome!")

greet()

# Loop block
for i in range(3):
    print(f"Iteration {i}")
    print("Inside loop")
print("Outside loop")
```

**Output:**
```
Hello!
Welcome!
Iteration 0
Inside loop
Iteration 1
Inside loop
Iteration 2
Inside loop
Outside loop
```

---

## 5. Python Data Types

### Overview

| Category | Data Types | Example |
|----------|------------|---------|
| **Numeric** | int, float, complex | `10`, `3.14`, `2+3j` |
| **Sequence** | str, list, tuple | `"hello"`, `[1,2,3]`, `(1,2,3)` |
| **Boolean** | bool | `True`, `False` |
| **Set** | set, frozenset | `{1,2,3}` |
| **Mapping** | dict | `{"key": "value"}` |
| **None** | NoneType | `None` |

### Type Checking
```python
x = 10
print(type(x))  # <class 'int'>

y = "Hello"
print(type(y))  # <class 'str'>

z = [1, 2, 3]
print(type(z))  # <class 'list'>
```

**Output:**
```
<class 'int'>
<class 'str'>
<class 'list'>
```

---

## 6. Numeric Data Types

### 1. Integer (int)
- **Whole numbers** (positive, negative, zero)
- **Unlimited precision** in Python 3

```python
# Integer examples
age = 25
temperature = -10
large_number = 999999999999999999999

print(age)            # 25
print(type(age))      # <class 'int'>
print(large_number)   # 999999999999999999999
```

**Output:**
```
25
<class 'int'>
999999999999999999999
```

### 2. Float (float)
- **Decimal numbers**
- **Finite precision** (about 15-17 decimal places)

```python
# Float examples
pi = 3.14159
price = 99.99
scientific = 2.5e-3  # 0.0025

print(pi)              # 3.14159
print(type(pi))        # <class 'float'>
print(scientific)      # 0.0025

# Float operations
a = 10.5
b = 2.5
print(a + b)           # 13.0
print(a / b)           # 4.2
```

**Output:**
```
3.14159
<class 'float'>
0.0025
13.0
4.2
```

### 3. Complex (complex)
- **Complex numbers**: `a + bj`
- `a` = real part, `b` = imaginary part

```python
# Complex number
c = 2 + 3j

print(c)              # (2+3j)
print(type(c))        # <class 'complex'>
print(c.real)         # 2.0
print(c.imag)         # 3.0

# Complex operations
c1 = 1 + 2j
c2 = 3 + 4j
print(c1 + c2)        # (4+6j)
print(c1 * c2)        # (-5+10j)
```

**Output:**
```
(2+3j)
<class 'complex'>
2.0
3.0
(4+6j)
(-5+10j)
```

### Type Conversion

```python
# int to float
x = 10
y = float(x)
print(y)              # 10.0
print(type(y))        # <class 'float'>

# float to int (truncates decimal)
a = 3.99
b = int(a)
print(b)              # 3

# string to int/float
s1 = "100"
s2 = "3.14"
num1 = int(s1)
num2 = float(s2)
print(num1, num2)     # 100 3.14

# int to string
age = 25
age_str = str(age)
print("Age: " + age_str)  # Age: 25
```

**Output:**
```
10.0
<class 'float'>
3
100 3.14
Age: 25
```

### Numeric Operations

```python
# Mixed type operations
a = 10      # int
b = 3.5     # float

print(a + b)    # 13.5 (result is float)
print(a * b)    # 35.0
print(a / b)    # 2.857142857142857

# Math operations
import math

print(abs(-10))         # 10 (absolute value)
print(pow(2, 3))        # 8 (2^3)
print(round(3.7))       # 4 (round to nearest)
print(round(3.14159, 2))  # 3.14 (round to 2 decimals)

print(math.sqrt(16))    # 4.0 (square root)
print(math.ceil(3.2))   # 4 (ceiling)
print(math.floor(3.9))  # 3 (floor)
```

**Output:**
```
13.5
35.0
2.857142857142857
10
8
4
3.14
4.0
4
3
```

### Input and Type Conversion

```python
# Taking numeric input
age = int(input("Enter age: "))        # Convert input to int
height = float(input("Enter height: "))  # Convert input to float

print(f"Age: {age}, Height: {height}")
print(f"Types: {type(age)}, {type(height)}")

# Example run:
# Input: 25
# Input: 5.8
```

**Output:**
```
Enter age: 25
Enter height: 5.8
Age: 25, Height: 5.8
Types: <class 'int'>, <class 'float'>
```

---

## 🚀 Quick Reference Summary

### Variables
- No declaration needed: `x = 10`
- Multiple assignment: `a, b, c = 1, 2, 3`
- Dynamic typing: type changes automatically

### Operators Priority
1. `**` (Exponentiation)
2. `*, /, //, %`
3. `+, -`
4. Comparison (`==, !=, >, <, >=, <=`)
5. `not`, `and`, `or`

### Data Types

| Type | Description | Example |
|------|-------------|---------|
| **int** | Whole numbers | `42`, `-10` |
| **float** | Decimals | `3.14`, `2.5e-3` |
| **complex** | Complex numbers | `2+3j` |
| **str** | Strings | `"Hello"` |
| **bool** | Boolean | `True`, `False` |

### Type Conversion
```python
int()     # Convert to integer
float()   # Convert to float
str()     # Convert to string
bool()    # Convert to boolean
```

### Python Blocks
- Use **indentation** (4 spaces standard)
- No braces needed
- Consistent indentation required

---

## 📝 Exam Important Questions

1. **Explain** Python features and advantages.

2. **Demonstrate** variable assignment and naming rules with examples.

3. **Write a program** using all arithmetic operators.

4. **Explain** operator precedence with example:
   ```python
   result = 10 + 5 * 2 ** 3 - 4
   ```

5. **Differentiate** between `==` and `is` operators.

6. **Explain** Python indentation with examples of correct and incorrect code.

7. **Write a program** to perform type conversions between int, float, and string.

8. **Demonstrate** the difference between `/` and `//` operators.

9. **Explain** logical operators (`and`, `or`, `not`) with truth table.

10. **Write a program** to:
    - Take two numbers as input
    - Perform all arithmetic operations
    - Display results with proper formatting

---

*End of Unit-1*
