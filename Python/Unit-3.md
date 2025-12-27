# Unit-3: Python Complex Data Types and Functions

---

## 1. String Data Type

### String Basics

```python
# Creating strings
str1 = "Hello"
str2 = 'Python'
str3 = """Multi-line
string"""
str4 = '''Also
multi-line'''

print(str1)
print(str2)
print(str3)
```

**Output:**
```
Hello
Python
Multi-line
string
```

### String Indexing and Slicing

```python
text = "Python Programming"

# Indexing (0-based)
print(text[0])      # P (first character)
print(text[7])      # P (8th character)
print(text[-1])     # g (last character)
print(text[-2])     # n (second last)

# Slicing: string[start:end:step]
print(text[0:6])    # Python (index 0 to 5)
print(text[7:])     # Programming (from index 7 to end)
print(text[:6])     # Python (start to index 5)
print(text[::2])    # Pto rgamn (every 2nd character)
print(text[::-1])   # gnimmargorP nohtyP (reverse)
```

**Output:**
```
P
P
g
n
Python
Programming
Python
Pto rgamn
gnimmargorP nohtyP
```

### String Operations

```python
# Concatenation
first = "Hello"
last = "World"
full = first + " " + last
print(full)  # Hello World

# Repetition
print("Ha" * 3)  # HaHaHa

# Membership
print("Hello" in full)      # True
print("Python" in full)     # False
print("Python" not in full) # True

# Length
print(len(full))  # 11

# Comparison
print("apple" < "banana")   # True (alphabetical)
print("Apple" == "apple")   # False (case-sensitive)
```

**Output:**
```
Hello World
HaHaHa
True
False
True
11
True
False
```

### String Methods

#### Case Conversion
```python
text = "Python Programming"

print(text.upper())       # PYTHON PROGRAMMING
print(text.lower())       # python programming
print(text.capitalize())  # Python programming
print(text.title())       # Python Programming
print(text.swapcase())    # pYTHON pROGRAMMING
```

**Output:**
```
PYTHON PROGRAMMING
python programming
Python programming
Python Programming
pYTHON pROGRAMMING
```

#### Searching Methods
```python
text = "Python Programming"

print(text.find("Pro"))      # 7 (index of first occurrence)
print(text.find("Java"))     # -1 (not found)
print(text.index("Pro"))     # 7 (raises error if not found)
print(text.count("g"))       # 2 (occurrences)
print(text.startswith("Py")) # True
print(text.endswith("ing"))  # True
```

**Output:**
```
7
-1
7
2
True
True
```

#### Trimming and Alignment
```python
text = "  Python  "

print(text.strip())   # "Python" (remove both ends)
print(text.lstrip())  # "Python  " (remove left)
print(text.rstrip())  # "  Python" (remove right)

# Alignment
print("Python".center(20, '-'))  # -------Python-------
print("Python".ljust(20, '-'))   # Python--------------
print("Python".rjust(20, '-'))   # --------------Python
```

**Output:**
```
Python
Python  
  Python
-------Python-------
Python--------------
--------------Python
```

#### Splitting and Joining
```python
# Split
text = "apple,banana,cherry"
fruits = text.split(',')
print(fruits)  # ['apple', 'banana', 'cherry']

sentence = "Hello World Python"
words = sentence.split()  # default splits by whitespace
print(words)  # ['Hello', 'World', 'Python']

# Join
fruits = ['apple', 'banana', 'cherry']
text = ', '.join(fruits)
print(text)  # apple, banana, cherry

words = ['Hello', 'World']
sentence = ' '.join(words)
print(sentence)  # Hello World
```

**Output:**
```
['apple', 'banana', 'cherry']
['Hello', 'World', 'Python']
apple, banana, cherry
Hello World
```

#### Replacement
```python
text = "Hello World"

print(text.replace("World", "Python"))  # Hello Python
print(text.replace("l", "L"))           # HeLLo WorLd
print(text.replace("l", "L", 2))        # HeLLo World (max 2 replacements)
```

**Output:**
```
Hello Python
HeLLo WorLd
HeLLo World
```

#### Checking Methods
```python
# Check content
print("hello".isalpha())      # True (all alphabetic)
print("hello123".isalpha())   # False
print("12345".isdigit())      # True (all digits)
print("hello123".isalnum())   # True (alphanumeric)
print("   ".isspace())        # True (all whitespace)
print("Hello".islower())      # False
print("HELLO".isupper())      # True
print("Hello World".istitle()) # True
```

**Output:**
```
True
False
True
True
True
False
True
True
```

### String Formatting

#### Old Style (%)
```python
name = "Alice"
age = 25

print("Name: %s, Age: %d" % (name, age))
print("Price: $%.2f" % 19.99)
```

**Output:**
```
Name: Alice, Age: 25
Price: $19.99
```

#### str.format()
```python
name = "Bob"
age = 30

print("Name: {}, Age: {}".format(name, age))
print("Name: {0}, Age: {1}".format(name, age))
print("Name: {n}, Age: {a}".format(n=name, a=age))
print("Price: ${:.2f}".format(19.99))
```

**Output:**
```
Name: Bob, Age: 30
Name: Bob, Age: 30
Name: Bob, Age: 30
Price: $19.99
```

#### f-strings (Python 3.6+)
```python
name = "Charlie"
age = 35
price = 19.99

print(f"Name: {name}, Age: {age}")
print(f"Price: ${price:.2f}")
print(f"Next year: {age + 1}")
print(f"Name in caps: {name.upper()}")
```

**Output:**
```
Name: Charlie, Age: 35
Price: $19.99
Next year: 36
Name in caps: CHARLIE
```

---

## 2. List Data Type

### List Basics

```python
# Creating lists
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
empty = []

print(fruits)
print(type(fruits))  # <class 'list'>
print(len(fruits))   # 3
```

**Output:**
```
['apple', 'banana', 'cherry']
<class 'list'>
3
```

### List Indexing and Slicing

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

# Indexing
print(fruits[0])     # apple
print(fruits[2])     # cherry
print(fruits[-1])    # elderberry
print(fruits[-2])    # date

# Slicing
print(fruits[1:4])   # ['banana', 'cherry', 'date']
print(fruits[:3])    # ['apple', 'banana', 'cherry']
print(fruits[2:])    # ['cherry', 'date', 'elderberry']
print(fruits[::2])   # ['apple', 'cherry', 'elderberry']
print(fruits[::-1])  # reverse list
```

**Output:**
```
apple
cherry
elderberry
date
['banana', 'cherry', 'date']
['apple', 'banana', 'cherry']
['cherry', 'date', 'elderberry']
['apple', 'cherry', 'elderberry']
['elderberry', 'date', 'cherry', 'banana', 'apple']
```

### List Operations

```python
# Concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # [1, 2, 3, 4, 5, 6]

# Repetition
print([1, 2] * 3)  # [1, 2, 1, 2, 1, 2]

# Membership
print(2 in list1)      # True
print(10 in list1)     # False
print(10 not in list1) # True

# Comparison
print([1, 2, 3] == [1, 2, 3])  # True
print([1, 2] < [1, 3])         # True (element-wise)
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
[1, 2, 1, 2, 1, 2]
True
False
True
True
True
```

### List Methods

#### Adding Elements
```python
fruits = ["apple", "banana"]

# append() - add single element at end
fruits.append("cherry")
print(fruits)  # ['apple', 'banana', 'cherry']

# insert() - add at specific position
fruits.insert(1, "blueberry")
print(fruits)  # ['apple', 'blueberry', 'banana', 'cherry']

# extend() - add multiple elements
fruits.extend(["date", "elderberry"])
print(fruits)  # ['apple', 'blueberry', 'banana', 'cherry', 'date', 'elderberry']
```

**Output:**
```
['apple', 'banana', 'cherry']
['apple', 'blueberry', 'banana', 'cherry']
['apple', 'blueberry', 'banana', 'cherry', 'date', 'elderberry']
```

#### Removing Elements
```python
fruits = ["apple", "banana", "cherry", "banana", "date"]

# remove() - remove first occurrence
fruits.remove("banana")
print(fruits)  # ['apple', 'cherry', 'banana', 'date']

# pop() - remove by index (default: last)
last = fruits.pop()
print(last)    # date
print(fruits)  # ['apple', 'cherry', 'banana']

second = fruits.pop(1)
print(second)  # cherry
print(fruits)  # ['apple', 'banana']

# clear() - remove all elements
fruits.clear()
print(fruits)  # []

# del - delete by index or slice
numbers = [1, 2, 3, 4, 5]
del numbers[2]
print(numbers)  # [1, 2, 4, 5]

del numbers[1:3]
print(numbers)  # [1, 5]
```

**Output:**
```
['apple', 'cherry', 'banana', 'date']
date
['apple', 'cherry', 'banana']
cherry
['apple', 'banana']
[]
[1, 2, 4, 5]
[1, 5]
```

#### Sorting and Reversing
```python
numbers = [3, 1, 4, 1, 5, 9, 2]

# sort() - sort in place
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 4, 5, 9]

numbers.sort(reverse=True)
print(numbers)  # [9, 5, 4, 3, 2, 1, 1]

# sorted() - return new sorted list
original = [3, 1, 4, 1, 5]
sorted_list = sorted(original)
print(original)     # [3, 1, 4, 1, 5] (unchanged)
print(sorted_list)  # [1, 1, 3, 4, 5]

# reverse() - reverse in place
numbers = [1, 2, 3, 4, 5]
numbers.reverse()
print(numbers)  # [5, 4, 3, 2, 1]

# reversed() - return iterator
original = [1, 2, 3]
print(list(reversed(original)))  # [3, 2, 1]
```

**Output:**
```
[1, 1, 2, 3, 4, 5, 9]
[9, 5, 4, 3, 2, 1, 1]
[3, 1, 4, 1, 5]
[1, 1, 3, 4, 5]
[5, 4, 3, 2, 1]
[3, 2, 1]
```

#### Other Methods
```python
numbers = [1, 2, 3, 2, 4, 2, 5]

# count() - count occurrences
print(numbers.count(2))  # 3

# index() - find first index
print(numbers.index(3))  # 2

# copy() - shallow copy
original = [1, 2, 3]
copy = original.copy()
copy.append(4)
print(original)  # [1, 2, 3]
print(copy)      # [1, 2, 3, 4]
```

**Output:**
```
3
2
[1, 2, 3]
[1, 2, 3, 4]
```

### List Comprehension

```python
# Basic list comprehension
squares = [x**2 for x in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# With condition
evens = [x for x in range(1, 11) if x % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# With if-else
labels = ["Even" if x % 2 == 0 else "Odd" for x in range(1, 6)]
print(labels)  # ['Odd', 'Even', 'Odd', 'Even', 'Odd']

# Nested loops
matrix = [[i*j for j in range(1, 4)] for i in range(1, 4)]
print(matrix)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

**Output:**
```
[1, 4, 9, 16, 25]
[2, 4, 6, 8, 10]
['Odd', 'Even', 'Odd', 'Even', 'Odd']
[[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

---

## 3. Tuple Data Type

### Tuple Basics

```python
# Creating tuples
fruits = ("apple", "banana", "cherry")
numbers = (1, 2, 3, 4, 5)
mixed = (1, "hello", 3.14, True)
single = (1,)  # Note: comma is required for single element
empty = ()

print(fruits)
print(type(fruits))  # <class 'tuple'>
print(len(fruits))   # 3

# Tuple without parentheses (tuple packing)
point = 10, 20
print(point)  # (10, 20)
```

**Output:**
```
('apple', 'banana', 'cherry')
<class 'tuple'>
3
(10, 20)
```

### Tuple Indexing and Slicing

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")

# Indexing (same as list)
print(fruits[0])     # apple
print(fruits[-1])    # elderberry

# Slicing (same as list)
print(fruits[1:4])   # ('banana', 'cherry', 'date')
print(fruits[:3])    # ('apple', 'banana', 'cherry')
print(fruits[::2])   # ('apple', 'cherry', 'elderberry')
```

**Output:**
```
apple
elderberry
('banana', 'cherry', 'date')
('apple', 'banana', 'cherry')
('apple', 'cherry', 'elderberry')
```

### Tuple Operations

```python
# Concatenation
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)
combined = tuple1 + tuple2
print(combined)  # (1, 2, 3, 4, 5, 6)

# Repetition
print((1, 2) * 3)  # (1, 2, 1, 2, 1, 2)

# Membership
print(2 in tuple1)  # True

# Cannot modify tuples (immutable)
# fruits[0] = "orange"  # TypeError
```

**Output:**
```
(1, 2, 3, 4, 5, 6)
(1, 2, 1, 2, 1, 2)
True
```

### Tuple Methods

```python
numbers = (1, 2, 3, 2, 4, 2, 5)

# count() - count occurrences
print(numbers.count(2))  # 3

# index() - find first index
print(numbers.index(3))  # 2
```

**Output:**
```
3
2
```

### Tuple Unpacking

```python
# Basic unpacking
point = (10, 20)
x, y = point
print(f"x: {x}, y: {y}")  # x: 10, y: 20

# Multiple assignment
a, b, c = (1, 2, 3)
print(a, b, c)  # 1 2 3

# Swapping using tuples
a, b = 5, 10
print(f"Before: a={a}, b={b}")
a, b = b, a  # swap
print(f"After: a={a}, b={b}")

# Unpacking with * (Python 3)
numbers = (1, 2, 3, 4, 5)
first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5
```

**Output:**
```
x: 10, y: 20
1 2 3
Before: a=5, b=10
After: a=10, b=5
1
[2, 3, 4]
5
```

### Tuple vs List

| Feature | Tuple | List |
|---------|-------|------|
| **Syntax** | `(1, 2, 3)` | `[1, 2, 3]` |
| **Mutable** | No | Yes |
| **Speed** | Faster | Slower |
| **Methods** | 2 (count, index) | Many |
| **Use Case** | Fixed data | Dynamic data |

```python
# Tuples are faster
import time

# Tuple
start = time.time()
t = (1, 2, 3, 4, 5) * 1000000
end = time.time()
print(f"Tuple time: {end - start:.5f}")

# List
start = time.time()
l = [1, 2, 3, 4, 5] * 1000000
end = time.time()
print(f"List time: {end - start:.5f}")
```

---

## 4. Dictionary Data Type

### Dictionary Basics

```python
# Creating dictionaries
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

# Different ways to create
dict1 = {"a": 1, "b": 2}
dict2 = dict(a=1, b=2)
dict3 = dict([("a", 1), ("b", 2)])

print(student)
print(type(student))  # <class 'dict'>
print(len(student))   # 3
```

**Output:**
```
{'name': 'Alice', 'age': 20, 'grade': 'A'}
<class 'dict'>
3
```

### Accessing Dictionary Elements

```python
student = {
    "name": "Bob",
    "age": 22,
    "grade": "B"
}

# Access by key
print(student["name"])  # Bob
print(student["age"])   # 22

# Using get() (safer - no error if key doesn't exist)
print(student.get("name"))        # Bob
print(student.get("city"))        # None
print(student.get("city", "NYC")) # NYC (default value)
```

**Output:**
```
Bob
22
Bob
None
NYC
```

### Dictionary Operations

```python
student = {"name": "Charlie", "age": 21}

# Add/Update
student["grade"] = "A"  # add new key
student["age"] = 22     # update existing key
print(student)

# Check key existence
print("name" in student)     # True
print("city" in student)     # False
print("city" not in student) # True

# Get all keys
print(student.keys())    # dict_keys(['name', 'age', 'grade'])

# Get all values
print(student.values())  # dict_values(['Charlie', 22, 'A'])

# Get all items (key-value pairs)
print(student.items())   # dict_items([('name', 'Charlie'), ('age', 22), ('grade', 'A')])
```

**Output:**
```
{'name': 'Charlie', 'age': 22, 'grade': 'A'}
True
False
True
dict_keys(['name', 'age', 'grade'])
dict_values(['Charlie', 22, 'A'])
dict_items([('name', 'Charlie'), ('age', 22), ('grade', 'A')])
```

### Dictionary Methods

```python
student = {"name": "David", "age": 23, "grade": "B"}

# pop() - remove and return value
grade = student.pop("grade")
print(grade)    # B
print(student)  # {'name': 'David', 'age': 23}

# popitem() - remove last inserted item
student = {"name": "Eve", "age": 24, "grade": "A"}
item = student.popitem()
print(item)     # ('grade', 'A')
print(student)  # {'name': 'Eve', 'age': 24}

# update() - merge dictionaries
student = {"name": "Frank", "age": 25}
new_info = {"grade": "A", "city": "NYC"}
student.update(new_info)
print(student)  # {'name': 'Frank', 'age': 25, 'grade': 'A', 'city': 'NYC'}

# clear() - remove all items
student.clear()
print(student)  # {}

# copy() - shallow copy
original = {"a": 1, "b": 2}
copy = original.copy()
copy["c"] = 3
print(original)  # {'a': 1, 'b': 2}
print(copy)      # {'a': 1, 'b': 2, 'c': 3}
```

**Output:**
```
B
{'name': 'David', 'age': 23}
('grade', 'A')
{'name': 'Eve', 'age': 24}
{'name': 'Frank', 'age': 25, 'grade': 'A', 'city': 'NYC'}
{}
{'a': 1, 'b': 2}
{'a': 1, 'b': 2, 'c': 3}
```

### Iterating Through Dictionaries

```python
student = {"name": "Grace", "age": 26, "grade": "A"}

# Iterate through keys
print("Keys:")
for key in student:
    print(key)

# Iterate through values
print("\nValues:")
for value in student.values():
    print(value)

# Iterate through key-value pairs
print("\nKey-Value pairs:")
for key, value in student.items():
    print(f"{key}: {value}")
```

**Output:**
```
Keys:
name
age
grade

Values:
Grace
26
A

Key-Value pairs:
name: Grace
age: 26
grade: A
```

### Dictionary Comprehension

```python
# Basic dictionary comprehension
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# From two lists
keys = ["a", "b", "c"]
values = [1, 2, 3]
dict_from_lists = {k: v for k, v in zip(keys, values)}
print(dict_from_lists)  # {'a': 1, 'b': 2, 'c': 3}

# With condition
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

**Output:**
```
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
{'a': 1, 'b': 2, 'c': 3}
{2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

---

## 5. Python Functions

### Defining Functions

```python
# Basic function
def greet():
    print("Hello, World!")

greet()  # Hello, World!

# Function with parameters
def greet_person(name):
    print(f"Hello, {name}!")

greet_person("Alice")  # Hello, Alice!

# Function with return value
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # 8
```

**Output:**
```
Hello, World!
Hello, Alice!
8
```

### Function Parameters

#### Default Parameters
```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()          # Hello, Guest!
greet("Alice")   # Hello, Alice!

# Multiple default parameters
def power(base, exponent=2):
    return base ** exponent

print(power(5))      # 25 (5^2)
print(power(5, 3))   # 125 (5^3)
```

**Output:**
```
Hello, Guest!
Hello, Alice!
25
125
```

#### Keyword Arguments
```python
def describe_pet(animal, name):
    print(f"I have a {animal} named {name}.")

# Positional arguments
describe_pet("dog", "Buddy")

# Keyword arguments
describe_pet(name="Whiskers", animal="cat")
describe_pet(animal="hamster", name="Harry")
```

**Output:**
```
I have a dog named Buddy.
I have a cat named Whiskers.
I have a hamster named Harry.
```

#### Variable-length Arguments (*args)
```python
def sum_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))        # 6
print(sum_all(1, 2, 3, 4, 5))  # 15

# Example with regular parameter
def greet_all(greeting, *names):
    for name in names:
        print(f"{greeting}, {name}!")

greet_all("Hello", "Alice", "Bob", "Charlie")
```

**Output:**
```
6
15
Hello, Alice!
Hello, Bob!
Hello, Charlie!
```

#### Variable-length Keyword Arguments (**kwargs)
```python
def print_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="NYC")
print()

# Combined parameters
def student_info(name, *subjects, **grades):
    print(f"Name: {name}")
    print(f"Subjects: {subjects}")
    print(f"Grades: {grades}")

student_info("Bob", "Math", "Science", math=90, science=85)
```

**Output:**
```
name: Alice
age: 25
city: NYC

Name: Bob
Subjects: ('Math', 'Science')
Grades: {'math': 90, 'science': 85}
```

### Return Statement

```python
# Single return value
def square(x):
    return x ** 2

print(square(5))  # 25

# Multiple return values (returns tuple)
def min_max(numbers):
    return min(numbers), max(numbers)

minimum, maximum = min_max([1, 5, 3, 9, 2])
print(f"Min: {minimum}, Max: {maximum}")

# Early return
def is_even(num):
    if num % 2 == 0:
        return True
    return False

print(is_even(4))  # True
print(is_even(7))  # False

# No return (returns None)
def print_message(msg):
    print(msg)

result = print_message("Hello")
print(result)  # None
```

**Output:**
```
25
Min: 1, Max: 9
True
False
Hello
None
```

### Lambda Functions (Anonymous Functions)

```python
# Basic lambda
square = lambda x: x ** 2
print(square(5))  # 25

# Lambda with multiple parameters
add = lambda a, b: a + b
print(add(3, 4))  # 7

# Lambda in sorting
students = [
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 20},
    {"name": "Charlie", "age": 23}
]

students.sort(key=lambda s: s["age"])
print(students)

# Lambda with map()
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x**2, numbers))
print(squares)  # [1, 4, 9, 16, 25]

# Lambda with filter()
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4]
```

**Output:**
```
25
7
[{'name': 'Bob', 'age': 20}, {'name': 'Charlie', 'age': 23}, {'name': 'Alice', 'age': 25}]
[1, 4, 9, 16, 25]
[2, 4]
```

### Built-in Functions for Data Types

#### map()
```python
# Apply function to all items
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x**2, numbers))
print(squares)  # [1, 4, 9, 16, 25]

# Multiple iterables
list1 = [1, 2, 3]
list2 = [4, 5, 6]
sums = list(map(lambda x, y: x + y, list1, list2))
print(sums)  # [5, 7, 9]
```

**Output:**
```
[1, 4, 9, 16, 25]
[5, 7, 9]
```

#### filter()
```python
# Filter items based on condition
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# Filter strings
words = ["apple", "banana", "cherry", "date"]
long_words = list(filter(lambda w: len(w) > 5, words))
print(long_words)  # ['banana', 'cherry']
```

**Output:**
```
[2, 4, 6, 8, 10]
['banana', 'cherry']
```

#### reduce()
```python
from functools import reduce

# Reduce to single value
numbers = [1, 2, 3, 4, 5]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 120 (1*2*3*4*5)

# Find maximum
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # 5
```

**Output:**
```
120
5
```

---

## 🚀 Quick Reference Summary

### String Methods

| Method | Description | Example |
|--------|-------------|---------|
| `upper()` | Convert to uppercase | `"hello".upper()` → `"HELLO"` |
| `lower()` | Convert to lowercase | `"HELLO".lower()` → `"hello"` |
| `split()` | Split into list | `"a,b,c".split(',')` → `['a','b','c']` |
| `join()` | Join list to string | `','.join(['a','b'])` → `"a,b"` |
| `replace()` | Replace substring | `"hello".replace('l','L')` → `"heLLo"` |
| `strip()` | Remove whitespace | `" hi ".strip()` → `"hi"` |

### List vs Tuple vs Dictionary

| Feature | List | Tuple | Dictionary |
|---------|------|-------|------------|
| **Syntax** | `[1, 2, 3]` | `(1, 2, 3)` | `{'a': 1}` |
| **Mutable** | Yes | No | Yes |
| **Ordered** | Yes | Yes | Yes (Python 3.7+) |
| **Indexed** | By integer | By integer | By key |
| **Duplicates** | Yes | Yes | Keys: No, Values: Yes |

### Function Types

```python
# Regular function
def func(x):
    return x * 2

# Lambda function
func = lambda x: x * 2

# With *args
def func(*args):
    pass

# With **kwargs
def func(**kwargs):
    pass
```

---

## 📝 Exam Important Questions

1. **Explain** string slicing with examples including negative indices.

2. **Write a program** to count vowels and consonants in a string.

3. **Demonstrate** list methods: append, extend, insert, remove, pop.

4. **Explain** the difference between list and tuple with examples.

5. **Write a program** to sort a list of dictionaries by a specific key.

6. **Create a function** to find factorial using recursion.

7. **Explain** *args and **kwargs with examples.

8. **Write a program** using lambda, map, and filter to process a list.

9. **Demonstrate** dictionary operations: add, update, delete, iterate.

10. **Write a function** to:
    - Accept variable number of arguments
    - Return sum of all even numbers
    - Use list comprehension

---

*End of Unit-3*
