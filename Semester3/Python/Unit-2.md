# Unit-2: Python Program Flow Control

---

## 1. Conditional Blocks

### if Statement

**Syntax:**
```python
if condition:
    # code block executes if condition is True
    statement(s)
```

**Example:**
```python
age = 18

if age >= 18:
    print("You are eligible to vote")
    print("Welcome to voting booth")

print("Program continues")
```

**Output:**
```
You are eligible to vote
Welcome to voting booth
Program continues
```

### if-else Statement

**Syntax:**
```python
if condition:
    # executes if condition is True
    statement(s)
else:
    # executes if condition is False
    statement(s)
```

**Example:**
```python
age = 16

if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")
    print(f"Wait for {18 - age} more years")
```

**Output:**
```
You cannot vote yet
Wait for 2 more years
```

### if-elif-else Statement

**Syntax:**
```python
if condition1:
    # executes if condition1 is True
elif condition2:
    # executes if condition2 is True
elif condition3:
    # executes if condition3 is True
else:
    # executes if all conditions are False
```

**Example:**
```python
marks = 75

if marks >= 90:
    grade = 'A'
elif marks >= 80:
    grade = 'B'
elif marks >= 70:
    grade = 'C'
elif marks >= 60:
    grade = 'D'
else:
    grade = 'F'

print(f"Marks: {marks}, Grade: {grade}")
```

**Output:**
```
Marks: 75, Grade: C
```

### Nested if Statements

```python
num = 15

if num > 0:
    print("Positive number")
    if num % 2 == 0:
        print("Even number")
    else:
        print("Odd number")
else:
    print("Non-positive number")
```

**Output:**
```
Positive number
Odd number
```

### Practical Example: Calculator

```python
num1 = 10
num2 = 5
operator = '+'

if operator == '+':
    result = num1 + num2
elif operator == '-':
    result = num1 - num2
elif operator == '*':
    result = num1 * num2
elif operator == '/':
    if num2 != 0:
        result = num1 / num2
    else:
        result = "Error: Division by zero"
else:
    result = "Invalid operator"

print(f"{num1} {operator} {num2} = {result}")
```

**Output:**
```
10 + 5 = 15
```

### Ternary Operator (Conditional Expression)

```python
# Syntax: value_if_true if condition else value_if_false

age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)  # Adult

# Traditional if-else equivalent:
if age >= 18:
    status = "Adult"
else:
    status = "Minor"

# Practical use
a = 10
b = 20
max_value = a if a > b else b
print(f"Maximum: {max_value}")  # Maximum: 20
```

**Output:**
```
Adult
Maximum: 20
```

---

## 2. for Loops in Python

### Simple for Loop

**Syntax:**
```python
for variable in sequence:
    # code block
    statement(s)
```

**Example:**
```python
# Loop through list
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

**Output:**
```
apple
banana
cherry
```

### for Loop with range()

#### range(stop)
```python
# range(5) generates 0, 1, 2, 3, 4
for i in range(5):
    print(i, end=" ")
print()  # newline
```

**Output:**
```
0 1 2 3 4
```

#### range(start, stop)
```python
# range(2, 8) generates 2, 3, 4, 5, 6, 7
for i in range(2, 8):
    print(i, end=" ")
print()
```

**Output:**
```
2 3 4 5 6 7
```

#### range(start, stop, step)
```python
# range(0, 10, 2) generates 0, 2, 4, 6, 8
for i in range(0, 10, 2):
    print(i, end=" ")
print()

# Countdown
for i in range(10, 0, -1):
    print(i, end=" ")
print()
```

**Output:**
```
0 2 4 6 8
10 9 8 7 6 5 4 3 2 1
```

### for Loop with Strings

```python
# Iterate through characters
text = "Python"

for char in text:
    print(char, end="-")
print()

# With index using enumerate()
for index, char in enumerate(text):
    print(f"Index {index}: {char}")
```

**Output:**
```
P-y-t-h-o-n-
Index 0: P
Index 1: y
Index 2: t
Index 3: h
Index 4: o
Index 5: n
```

### for Loop with Lists

```python
numbers = [10, 20, 30, 40, 50]

# Simple iteration
for num in numbers:
    print(num * 2, end=" ")
print()

# With index
for i in range(len(numbers)):
    print(f"Index {i}: {numbers[i]}")

# Using enumerate (better way)
for index, value in enumerate(numbers):
    print(f"numbers[{index}] = {value}")
```

**Output:**
```
20 40 60 80 100
Index 0: 10
Index 1: 20
Index 2: 30
Index 3: 40
Index 4: 50
numbers[0] = 10
numbers[1] = 20
numbers[2] = 30
numbers[3] = 40
numbers[4] = 50
```

### for Loop with Dictionaries

```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

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
Alice
20
A

Key-Value pairs:
name: Alice
age: 20
grade: A
```

### Nested for Loops

```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}", end="  ")
    print()  # newline after inner loop

# Pattern printing
for i in range(1, 6):
    for j in range(i):
        print("*", end="")
    print()
```

**Output:**
```
1 x 1 = 1  1 x 2 = 2  1 x 3 = 3  
2 x 1 = 2  2 x 2 = 4  2 x 3 = 6  
3 x 1 = 3  3 x 2 = 6  3 x 3 = 9  
*
**
***
****
*****
```

---

## 3. while Loops in Python

### Basic while Loop

**Syntax:**
```python
while condition:
    # code block executes while condition is True
    statement(s)
```

**Example:**
```python
count = 1

while count <= 5:
    print(f"Count: {count}")
    count += 1

print("Loop ended")
```

**Output:**
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
Loop ended
```

### while Loop with Input

```python
# Password verification
password = ""

while password != "python123":
    password = input("Enter password: ")
    if password != "python123":
        print("Wrong password. Try again.")

print("Access granted!")
```

**Output:**
```
Enter password: hello
Wrong password. Try again.
Enter password: test
Wrong password. Try again.
Enter password: python123
Access granted!
```

### Infinite while Loop

```python
# Infinite loop (use with caution)
# while True:
#     print("This runs forever")

# Controlled infinite loop with break
count = 0
while True:
    print(count)
    count += 1
    if count >= 5:
        break
```

**Output:**
```
0
1
2
3
4
```

### while vs for Loop

```python
# Using for loop
print("For loop:")
for i in range(5):
    print(i, end=" ")
print()

# Using while loop (same result)
print("While loop:")
i = 0
while i < 5:
    print(i, end=" ")
    i += 1
print()
```

**Output:**
```
For loop:
0 1 2 3 4
While loop:
0 1 2 3 4
```

---

## 4. Loop Manipulation

### pass Statement
- **Empty placeholder**
- Does nothing
- Used when syntax requires a statement but you don't want to execute anything

```python
# pass in loop
for i in range(5):
    pass  # TODO: implement later

# pass in conditional
x = 10
if x > 5:
    pass  # will implement logic later
else:
    print("x is small")

# pass in function
def my_function():
    pass  # empty function

print("Program continues")
```

**Output:**
```
Program continues
```

### continue Statement
- **Skip current iteration**
- Jump to next iteration
- Rest of the loop code is skipped

```python
# Skip even numbers
print("Odd numbers from 1 to 10:")
for i in range(1, 11):
    if i % 2 == 0:
        continue  # skip even numbers
    print(i, end=" ")
print()

# Skip specific values
fruits = ["apple", "banana", "cherry", "date"]
for fruit in fruits:
    if fruit == "banana":
        continue  # skip banana
    print(fruit)
```

**Output:**
```
Odd numbers from 1 to 10:
1 3 5 7 9
apple
cherry
date
```

### break Statement
- **Exit loop immediately**
- No further iterations
- Control moves to statement after loop

```python
# Find first even number
numbers = [1, 3, 5, 8, 9, 10]

for num in numbers:
    if num % 2 == 0:
        print(f"First even number: {num}")
        break
    print(f"Checking {num}")

# Search in list
fruits = ["apple", "banana", "cherry", "date"]
search = "cherry"

for fruit in fruits:
    if fruit == search:
        print(f"Found {search}!")
        break
else:
    print(f"{search} not found")
```

**Output:**
```
Checking 1
Checking 3
Checking 5
First even number: 8
Found cherry!
```

### else with Loops
- **else executes** when loop completes normally
- **else doesn't execute** if loop exits with `break`

```python
# else with for loop
print("Example 1: Loop completes normally")
for i in range(5):
    print(i, end=" ")
else:
    print("\nLoop completed successfully")

# else with break
print("\nExample 2: Loop exits with break")
for i in range(5):
    if i == 3:
        print(f"\nBreaking at {i}")
        break
    print(i, end=" ")
else:
    print("\nThis won't print")

# Practical use: Search
print("\nExample 3: Search")
numbers = [1, 3, 5, 7, 9]
search = 4

for num in numbers:
    if num == search:
        print(f"Found {search}")
        break
else:
    print(f"{search} not found in list")
```

**Output:**
```
Example 1: Loop completes normally
0 1 2 3 4
Loop completed successfully

Example 2: Loop exits with break
0 1 2
Breaking at 3

Example 3: Search
4 not found in list
```

### Combining break, continue, and pass

```python
print("Numbers from 1 to 10:")
for i in range(1, 11):
    if i == 5:
        pass  # placeholder, do nothing
    elif i % 2 == 0:
        continue  # skip even numbers
    elif i == 9:
        break  # stop at 9
    print(i, end=" ")
print()
```

**Output:**
```
Numbers from 1 to 10:
1 3 5 7
```

---

## 5. Programming Examples

### Example 1: Prime Number Check

```python
num = int(input("Enter a number: "))

if num < 2:
    print(f"{num} is not prime")
else:
    is_prime = True
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            is_prime = False
            break
    
    if is_prime:
        print(f"{num} is prime")
    else:
        print(f"{num} is not prime")
```

**Output:**
```
Enter a number: 17
17 is prime
```

### Example 2: Factorial Calculation

```python
# Using for loop
n = 5
factorial = 1

for i in range(1, n + 1):
    factorial *= i

print(f"Factorial of {n} = {factorial}")

# Using while loop
n = 5
factorial = 1
i = 1

while i <= n:
    factorial *= i
    i += 1

print(f"Factorial of {n} = {factorial}")
```

**Output:**
```
Factorial of 5 = 120
Factorial of 5 = 120
```

### Example 3: Fibonacci Series

```python
n = 10  # number of terms
a, b = 0, 1

print("Fibonacci series:")
for i in range(n):
    print(a, end=" ")
    a, b = b, a + b
print()
```

**Output:**
```
Fibonacci series:
0 1 1 2 3 5 8 13 21 34
```

### Example 4: Sum of Digits

```python
num = 12345
sum_digits = 0

while num > 0:
    digit = num % 10
    sum_digits += digit
    num //= 10

print(f"Sum of digits: {sum_digits}")
```

**Output:**
```
Sum of digits: 15
```

### Example 5: Reverse a Number

```python
num = 12345
reverse = 0

while num > 0:
    digit = num % 10
    reverse = reverse * 10 + digit
    num //= 10

print(f"Reversed number: {reverse}")
```

**Output:**
```
Reversed number: 54321
```

### Example 6: Pattern Printing

```python
# Pattern 1: Right triangle
n = 5
for i in range(1, n + 1):
    for j in range(i):
        print("*", end="")
    print()

print()

# Pattern 2: Number pyramid
for i in range(1, n + 1):
    for j in range(1, i + 1):
        print(j, end="")
    print()

print()

# Pattern 3: Inverted triangle
for i in range(n, 0, -1):
    for j in range(i):
        print("*", end="")
    print()
```

**Output:**
```
*
**
***
****
*****

1
12
123
1234
12345

*****
****
***
**
*
```

### Example 7: Menu-Driven Calculator

```python
while True:
    print("\n=== Calculator ===")
    print("1. Addition")
    print("2. Subtraction")
    print("3. Multiplication")
    print("4. Division")
    print("5. Exit")
    
    choice = int(input("Enter choice (1-5): "))
    
    if choice == 5:
        print("Exiting...")
        break
    
    if choice < 1 or choice > 5:
        print("Invalid choice!")
        continue
    
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    
    if choice == 1:
        print(f"Result: {num1 + num2}")
    elif choice == 2:
        print(f"Result: {num1 - num2}")
    elif choice == 3:
        print(f"Result: {num1 * num2}")
    elif choice == 4:
        if num2 != 0:
            print(f"Result: {num1 / num2}")
        else:
            print("Error: Division by zero!")
```

**Output:**
```
=== Calculator ===
1. Addition
2. Subtraction
3. Multiplication
4. Division
5. Exit
Enter choice (1-5): 1
Enter first number: 10
Enter second number: 5
Result: 15.0

=== Calculator ===
...
```

### Example 8: Nested Loop - Multiplication Table

```python
# Multiplication table from 1 to 5
for i in range(1, 6):
    print(f"\nTable of {i}:")
    for j in range(1, 11):
        print(f"{i} x {j} = {i*j}")
```

**Output:**
```
Table of 1:
1 x 1 = 1
1 x 2 = 2
...
1 x 10 = 10

Table of 2:
2 x 1 = 2
2 x 2 = 4
...
```

### Example 9: Finding Maximum in List

```python
numbers = [45, 23, 67, 12, 89, 34]
max_num = numbers[0]

for num in numbers:
    if num > max_num:
        max_num = num

print(f"Maximum number: {max_num}")

# Alternative using enumerate
numbers = [45, 23, 67, 12, 89, 34]
max_num = numbers[0]
max_index = 0

for index, num in enumerate(numbers):
    if num > max_num:
        max_num = num
        max_index = index

print(f"Maximum: {max_num} at index {max_index}")
```

**Output:**
```
Maximum number: 89
Maximum: 89 at index 4
```

### Example 10: Count Vowels and Consonants

```python
text = "Hello World"
vowels = "aeiouAEIOU"
vowel_count = 0
consonant_count = 0

for char in text:
    if char.isalpha():
        if char in vowels:
            vowel_count += 1
        else:
            consonant_count += 1

print(f"Vowels: {vowel_count}")
print(f"Consonants: {consonant_count}")
```

**Output:**
```
Vowels: 3
Consonants: 7
```

---

## 🚀 Quick Reference Summary

### Conditional Statements

| Statement | Description | Example |
|-----------|-------------|---------|
| **if** | Execute if condition is True | `if x > 0: print(x)` |
| **if-else** | Execute different blocks | `if x > 0: ... else: ...` |
| **if-elif-else** | Multiple conditions | `if x > 0: ... elif x == 0: ... else: ...` |
| **Ternary** | Conditional expression | `result = a if condition else b` |

### Loops

| Loop | Description | Use Case |
|------|-------------|----------|
| **for** | Iterate over sequence | Known iterations |
| **while** | Loop while condition is True | Unknown iterations |

### Loop Control

| Statement | Description | Effect |
|-----------|-------------|--------|
| **break** | Exit loop | Terminates loop immediately |
| **continue** | Skip iteration | Jump to next iteration |
| **pass** | Do nothing | Placeholder |
| **else** | Execute after loop | Runs if loop completes normally |

### range() Function

```python
range(stop)              # 0 to stop-1
range(start, stop)       # start to stop-1
range(start, stop, step) # with step increment
```

---

## 📝 Exam Important Questions

1. **Write a program** to check if a number is positive, negative, or zero using if-elif-else.

2. **Explain** the difference between `break` and `continue` with examples.

3. **Write a program** to print all prime numbers between 1 and 50 using for loop.

4. **Demonstrate** the use of else clause with loops.

5. **Write a program** to find factorial of a number using:
   - for loop
   - while loop

6. **Create a pattern** using nested loops:
   ```
   *
   **
   ***
   ****
   *****
   ```

7. **Write a program** to reverse a string using loop.

8. **Explain** range() function with examples of all three forms.

9. **Write a menu-driven program** for:
   - Area of circle
   - Area of rectangle
   - Area of triangle
   - Exit

10. **Write a program** to:
    - Take a number as input
    - Print multiplication table of that number
    - Use while loop

---

*End of Unit-2*
