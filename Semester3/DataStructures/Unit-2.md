# Unit-2: Stacks & Queues

---

## 1. Stack: Abstract Data Type

### Definition
- **Stack**: Linear data structure following LIFO (Last In First Out) principle
- **Real-life analogy**: Stack of plates, stack of books

### Characteristics
- Elements added and removed from same end (TOP)
- Only TOP element is accessible
- All operations at one end only

### Stack Terminology
- **Push**: Insert element at top
- **Pop**: Remove element from top
- **Top/Peek**: View top element without removing
- **Overflow**: Pushing when stack is full
- **Underflow**: Popping when stack is empty

### Visual Representation
```
        TOP →  |  30  |  ← Push/Pop happens here
               |  20  |
               |  10  |
               +------+
               Bottom
```

---

## 2. Primitive Stack Operations

### Core Operations

#### 1. Push (Insert)
```
Operation: Add element to top of stack
Precondition: Stack should not be full
Postcondition: Element added at top, top pointer incremented
```

#### 2. Pop (Delete)
```
Operation: Remove and return top element
Precondition: Stack should not be empty
Postcondition: Top element removed, top pointer decremented
```

#### 3. Peek/Top
```
Operation: Return top element without removing
Precondition: Stack should not be empty
Postcondition: Stack unchanged, top element returned
```

#### 4. isEmpty
```
Operation: Check if stack is empty
Return: True if empty, False otherwise
```

#### 5. isFull
```
Operation: Check if stack is full (for array implementation)
Return: True if full, False otherwise
```

### Stack Operations Summary

| Operation | Description | Time Complexity |
|-----------|-------------|-----------------|
| **push(x)** | Insert x at top | O(1) |
| **pop()** | Remove and return top | O(1) |
| **peek()** | Return top without removing | O(1) |
| **isEmpty()** | Check if empty | O(1) |
| **isFull()** | Check if full | O(1) |

---

## 3. Array Implementation of Stack

### Structure
```c
#define MAX 100

struct Stack {
    int data[MAX];
    int top;
};
```

### Initialization
```c
void initStack(struct Stack* s) {
    s->top = -1;  // Empty stack
}
```

### Operations Implementation

#### 1. Push Operation
```c
void push(struct Stack* s, int value) {
    // Check overflow
    if(s->top == MAX - 1) {
        printf("Stack Overflow!\n");
        return;
    }
    
    // Increment top and insert
    s->top++;
    s->data[s->top] = value;
    
    // Or: s->data[++s->top] = value;
}

// Time Complexity: O(1)
// Space Complexity: O(1)
```

**Visualization:**
```
Before push(40):          After push(40):
   top → 2 |  30  |           top → 3 |  40  | ← New element
         1 |  20  |                  2 |  30  |
         0 |  10  |                  1 |  20  |
           +------+                  0 |  10  |
                                       +------+
```

#### 2. Pop Operation
```c
int pop(struct Stack* s) {
    // Check underflow
    if(s->top == -1) {
        printf("Stack Underflow!\n");
        return -1;  // Or use error code
    }
    
    // Return and decrement top
    int value = s->data[s->top];
    s->top--;
    return value;
    
    // Or: return s->data[s->top--];
}

// Time Complexity: O(1)
// Space Complexity: O(1)
```

#### 3. Peek Operation
```c
int peek(struct Stack* s) {
    if(s->top == -1) {
        printf("Stack is empty!\n");
        return -1;
    }
    
    return s->data[s->top];
}

// Time Complexity: O(1)
```

#### 4. isEmpty and isFull
```c
int isEmpty(struct Stack* s) {
    return (s->top == -1);
}

int isFull(struct Stack* s) {
    return (s->top == MAX - 1);
}

// Time Complexity: O(1) for both
```

#### 5. Display Stack
```c
void display(struct Stack* s) {
    if(isEmpty(s)) {
        printf("Stack is empty!\n");
        return;
    }
    
    printf("Stack elements (top to bottom):\n");
    for(int i = s->top; i >= 0; i--) {
        printf("| %d |\n", s->data[i]);
    }
    printf("+---+\n");
}
```

### Advantages of Array Implementation
- Simple to implement
- Fast operations (O(1))
- No extra memory for pointers

### Disadvantages
- Fixed size (wastage or overflow)
- Cannot grow dynamically
- Memory allocated upfront

---

## 4. Linked List Implementation of Stack

### Node Structure
```c
struct Node {
    int data;
    struct Node* next;
};

struct Stack {
    struct Node* top;
};
```

### Initialization
```c
void initStack(struct Stack* s) {
    s->top = NULL;  // Empty stack
}
```

### Operations Implementation

#### 1. Push Operation
```c
void push(struct Stack* s, int value) {
    // Create new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    
    if(newNode == NULL) {
        printf("Heap Overflow! Cannot allocate memory.\n");
        return;
    }
    
    // Set data and link
    newNode->data = value;
    newNode->next = s->top;
    
    // Update top
    s->top = newNode;
}

// Time Complexity: O(1)
// Space Complexity: O(1) per push
```

**Visualization:**
```
Before push(40):              After push(40):
top → [30|•] → [20|•] → [10|NULL]    top → [40|•] → [30|•] → [20|•] → [10|NULL]
```

#### 2. Pop Operation
```c
int pop(struct Stack* s) {
    // Check underflow
    if(s->top == NULL) {
        printf("Stack Underflow!\n");
        return -1;
    }
    
    // Save top node and data
    struct Node* temp = s->top;
    int value = temp->data;
    
    // Update top
    s->top = temp->next;
    
    // Free memory
    free(temp);
    
    return value;
}

// Time Complexity: O(1)
// Space Complexity: O(1)
```

#### 3. Peek Operation
```c
int peek(struct Stack* s) {
    if(s->top == NULL) {
        printf("Stack is empty!\n");
        return -1;
    }
    
    return s->top->data;
}

// Time Complexity: O(1)
```

#### 4. isEmpty
```c
int isEmpty(struct Stack* s) {
    return (s->top == NULL);
}

// Time Complexity: O(1)
```

#### 5. Display Stack
```c
void display(struct Stack* s) {
    if(isEmpty(s)) {
        printf("Stack is empty!\n");
        return;
    }
    
    printf("Stack (top to bottom): ");
    struct Node* temp = s->top;
    while(temp != NULL) {
        printf("[%d] → ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
```

### Advantages of Linked List Implementation
- Dynamic size (grows/shrinks as needed)
- No overflow condition (only system memory limit)
- Efficient memory utilization

### Disadvantages
- Extra memory for pointers
- Slightly more complex
- No random access

---

## 5. Application: Infix, Prefix, and Postfix Expressions

### Expression Types

#### Infix Notation
- **Definition**: Operator between operands
- **Example**: `A + B`, `(A + B) * C`
- **Used by**: Humans (natural)
- **Problem**: Requires parentheses and precedence rules

#### Prefix Notation (Polish Notation)
- **Definition**: Operator before operands
- **Example**: `+ A B`, `* + A B C`
- **Advantage**: No parentheses needed, unambiguous
- **Evaluation**: Right to left

#### Postfix Notation (Reverse Polish Notation)
- **Definition**: Operator after operands
- **Example**: `A B +`, `A B + C *`
- **Advantage**: No parentheses, easy to evaluate
- **Evaluation**: Left to right

### Conversion Examples

| Infix | Prefix | Postfix |
|-------|--------|---------|
| `A + B` | `+ A B` | `A B +` |
| `A + B * C` | `+ A * B C` | `A B C * +` |
| `(A + B) * C` | `* + A B C` | `A B + C *` |
| `A * B + C / D` | `+ * A B / C D` | `A B * C D / +` |
| `(A + B) * (C - D)` | `* + A B - C D` | `A B + C D - *` |

### Operator Precedence and Associativity

| Operator | Precedence | Associativity |
|----------|------------|---------------|
| `^` (Power) | 3 (Highest) | Right to Left |
| `*`, `/`, `%` | 2 | Left to Right |
| `+`, `-` | 1 (Lowest) | Left to Right |
| `(` `)` | - | - |

---

## 6. Infix to Postfix Conversion

### Algorithm
```
Algorithm: InfixToPostfix
Input: Infix expression
Output: Postfix expression

1. Initialize empty stack for operators
2. Initialize empty output string
3. Scan infix expression left to right:
   
   a) If operand: Add to output
   
   b) If '(': Push to stack
   
   c) If ')':
      - Pop from stack and add to output
      - Until '(' is encountered
      - Discard '('
   
   d) If operator:
      - While (stack not empty AND
              top has higher/equal precedence AND
              top is not '('):
          Pop from stack and add to output
      - Push current operator to stack

4. Pop all remaining operators from stack and add to output
5. Return output
```

### Implementation
```c
int precedence(char op) {
    switch(op) {
        case '^': return 3;
        case '*':
        case '/':
        case '%': return 2;
        case '+':
        case '-': return 1;
        default: return 0;
    }
}

int isOperator(char ch) {
    return (ch == '+' || ch == '-' || ch == '*' || 
            ch == '/' || ch == '^' || ch == '%');
}

void infixToPostfix(char* infix, char* postfix) {
    struct Stack stack;
    initStack(&stack);
    
    int i = 0, j = 0;
    
    while(infix[i] != '\0') {
        char ch = infix[i];
        
        // If operand, add to output
        if(isalnum(ch)) {
            postfix[j++] = ch;
        }
        // If '(', push to stack
        else if(ch == '(') {
            push(&stack, ch);
        }
        // If ')', pop until '('
        else if(ch == ')') {
            while(!isEmpty(&stack) && peek(&stack) != '(') {
                postfix[j++] = pop(&stack);
            }
            pop(&stack);  // Remove '('
        }
        // If operator
        else if(isOperator(ch)) {
            while(!isEmpty(&stack) && 
                  precedence(peek(&stack)) >= precedence(ch) &&
                  peek(&stack) != '(') {
                postfix[j++] = pop(&stack);
            }
            push(&stack, ch);
        }
        
        i++;
    }
    
    // Pop remaining operators
    while(!isEmpty(&stack)) {
        postfix[j++] = pop(&stack);
    }
    
    postfix[j] = '\0';
}

// Time Complexity: O(n) where n = length of expression
// Space Complexity: O(n) for stack
```

### Example Trace
```
Infix: A + B * C

Step | Symbol | Stack | Output
-----|--------|-------|--------
  1  |   A    |       |   A
  2  |   +    |   +   |   A
  3  |   B    |   +   |   AB
  4  |   *    |  +*   |   AB
  5  |   C    |  +*   |   ABC
  6  |  END   |       |   ABC*+

Postfix: ABC*+
```

### Complex Example
```
Infix: (A + B) * C - D / E

Step | Symbol | Stack | Output
-----|--------|-------|--------
  1  |   (    |   (   |
  2  |   A    |   (   |   A
  3  |   +    |  (+   |   A
  4  |   B    |  (+   |   AB
  5  |   )    |       |   AB+
  6  |   *    |   *   |   AB+
  7  |   C    |   *   |   AB+C
  8  |   -    |   -   |   AB+C*
  9  |   D    |   -   |   AB+C*D
 10  |   /    |  -/   |   AB+C*D
 11  |   E    |  -/   |   AB+C*DE
 12  |  END   |       |   AB+C*DE/-

Postfix: AB+C*DE/-
```

---

## 7. Evaluation of Postfix Expression

### Algorithm
```
Algorithm: EvaluatePostfix
Input: Postfix expression
Output: Result value

1. Initialize empty stack
2. Scan postfix expression left to right:
   
   a) If operand:
      - Push to stack
   
   b) If operator:
      - Pop two operands (op2 = pop, op1 = pop)
      - Compute: result = op1 operator op2
      - Push result back to stack

3. Final stack top is the result
4. Return result
```

### Implementation
```c
int evaluatePostfix(char* postfix) {
    struct Stack stack;
    initStack(&stack);
    
    int i = 0;
    while(postfix[i] != '\0') {
        char ch = postfix[i];
        
        // If operand (digit), push to stack
        if(isdigit(ch)) {
            push(&stack, ch - '0');  // Convert char to int
        }
        // If operator, pop two operands and compute
        else if(isOperator(ch)) {
            int op2 = pop(&stack);
            int op1 = pop(&stack);
            int result;
            
            switch(ch) {
                case '+': result = op1 + op2; break;
                case '-': result = op1 - op2; break;
                case '*': result = op1 * op2; break;
                case '/': result = op1 / op2; break;
                case '^': result = pow(op1, op2); break;
                case '%': result = op1 % op2; break;
            }
            
            push(&stack, result);
        }
        
        i++;
    }
    
    // Final result
    return pop(&stack);
}

// Time Complexity: O(n)
// Space Complexity: O(n)
```

### Example Trace
```
Postfix: 5 3 + 8 2 / *

Step | Symbol | Stack | Operation
-----|--------|-------|------------
  1  |   5    |   5   | Push 5
  2  |   3    |  5,3  | Push 3
  3  |   +    |   8   | 5+3=8, Push 8
  4  |   8    |  8,8  | Push 8
  5  |   2    | 8,8,2 | Push 2
  6  |   /    |  8,4  | 8/2=4, Push 4
  7  |   *    |   32  | 8*4=32, Push 32
  8  |  END   |   32  | Result = 32

Answer: 32
```

### Another Example
```
Postfix: 2 3 1 * + 9 -

Step | Symbol | Stack | Operation
-----|--------|-------|------------
  1  |   2    |   2   | Push 2
  2  |   3    |  2,3  | Push 3
  3  |   1    | 2,3,1 | Push 1
  4  |   *    |  2,3  | 3*1=3, Push 3
  5  |   +    |   5   | 2+3=5, Push 5
  6  |   9    |  5,9  | Push 9
  7  |   -    |  -4   | 5-9=-4, Push -4
  8  |  END   |  -4   | Result = -4

Answer: -4
```

---

## 8. Recursion: Principles

### Definition
- **Recursion**: Function calling itself
- **Base Case**: Condition to stop recursion
- **Recursive Case**: Function calls itself with modified parameters

### Components of Recursion

#### 1. Base Case
- Termination condition
- Prevents infinite recursion
- Returns without further recursive calls

#### 2. Recursive Case
- Function calls itself
- Problem size reduced
- Moves towards base case

### General Structure
```c
returnType recursiveFunction(parameters) {
    // Base case
    if(base_condition) {
        return base_value;
    }
    
    // Recursive case
    return recursiveFunction(modified_parameters);
}
```

### Example: Factorial
```c
int factorial(int n) {
    // Base case
    if(n == 0 || n == 1) {
        return 1;
    }
    
    // Recursive case
    return n * factorial(n - 1);
}

/*
Trace for factorial(4):
factorial(4) = 4 * factorial(3)
             = 4 * 3 * factorial(2)
             = 4 * 3 * 2 * factorial(1)
             = 4 * 3 * 2 * 1
             = 24
*/
```

### Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Definition** | Function calls itself | Loops repeat statements |
| **Termination** | Base case | Loop condition |
| **Memory** | Uses stack (more) | Uses less memory |
| **Speed** | Slower (function call overhead) | Faster |
| **Code** | Often shorter, elegant | May be longer |
| **Readability** | More intuitive for some problems | Sometimes complex |

---

## 9. Tail Recursion

### Definition
- **Tail Recursion**: Recursive call is the last operation in function
- No computation after recursive call returns
- Can be optimized by compiler to iteration

### Tail Recursive Example
```c
// Tail recursive factorial
int factorialTail(int n, int accumulator) {
    // Base case
    if(n == 0 || n == 1) {
        return accumulator;
    }
    
    // Recursive call is last operation
    return factorialTail(n - 1, n * accumulator);
}

int factorial(int n) {
    return factorialTail(n, 1);
}

// Time: O(n), Space: O(1) with optimization
```

### Non-Tail Recursive Example
```c
// Non-tail recursive factorial
int factorial(int n) {
    if(n == 0 || n == 1) {
        return 1;
    }
    
    // Multiplication happens AFTER recursive call returns
    return n * factorial(n - 1);  // NOT tail recursive
}

// Space: O(n) for recursion stack
```

### Why Tail Recursion is Better?
- **Compiler Optimization**: Can be converted to loop
- **Space Efficient**: O(1) space instead of O(n)
- **No Stack Overflow**: For large inputs

### Converting to Tail Recursion
**Original (Non-tail):**
```c
int sum(int n) {
    if(n == 0) return 0;
    return n + sum(n - 1);
}
```

**Tail Recursive Version:**
```c
int sumTail(int n, int acc) {
    if(n == 0) return acc;
    return sumTail(n - 1, acc + n);
}

int sum(int n) {
    return sumTail(n, 0);
}
```

---

## 10. Removal of Recursion

### Converting Recursion to Iteration

#### Method 1: Using Loop (for Tail Recursion)
```c
// Recursive
int factorial(int n) {
    if(n <= 1) return 1;
    return n * factorial(n - 1);
}

// Iterative
int factorialIterative(int n) {
    int result = 1;
    for(int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

#### Method 2: Using Stack (for Non-tail Recursion)
```c
// Simulate recursion using explicit stack

int factorialStack(int n) {
    struct Stack stack;
    initStack(&stack);
    int result = 1;
    
    // Push all numbers to stack
    while(n > 1) {
        push(&stack, n);
        n--;
    }
    
    // Pop and multiply
    while(!isEmpty(&stack)) {
        result *= pop(&stack);
    }
    
    return result;
}
```

---

## 11. Problem Solving: Binary Search

### Recursive Implementation
```c
int binarySearchRecursive(int arr[], int left, int right, int key) {
    // Base case: element not found
    if(left > right) {
        return -1;
    }
    
    // Calculate mid
    int mid = left + (right - left) / 2;
    
    // Base case: element found
    if(arr[mid] == key) {
        return mid;
    }
    
    // Recursive cases
    if(arr[mid] > key) {
        return binarySearchRecursive(arr, left, mid - 1, key);
    } else {
        return binarySearchRecursive(arr, mid + 1, right, key);
    }
}

// Time: O(log n), Space: O(log n) due to recursion stack
```

### Iterative Implementation
```c
int binarySearchIterative(int arr[], int n, int key) {
    int left = 0, right = n - 1;
    
    while(left <= right) {
        int mid = left + (right - left) / 2;
        
        if(arr[mid] == key) {
            return mid;
        }
        
        if(arr[mid] > key) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    
    return -1;  // Not found
}

// Time: O(log n), Space: O(1)
```

### Trade-off Analysis
- **Recursive**: Elegant code, uses O(log n) space
- **Iterative**: More efficient space O(1), slightly faster

---

## 12. Problem Solving: Fibonacci Numbers

### Recursive Implementation (Naive)
```c
int fibonacciRecursive(int n) {
    // Base cases
    if(n == 0) return 0;
    if(n == 1) return 1;
    
    // Recursive case
    return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}

// Time: O(2^n) - Exponential!
// Space: O(n) - Recursion depth
```

**Problem:** Redundant calculations
```
fib(5) calls fib(4) and fib(3)
fib(4) calls fib(3) and fib(2)
fib(3) is calculated multiple times!
```

### Iterative Implementation
```c
int fibonacciIterative(int n) {
    if(n == 0) return 0;
    if(n == 1) return 1;
    
    int prev2 = 0, prev1 = 1;
    int current;
    
    for(int i = 2; i <= n; i++) {
        current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }
    
    return current;
}

// Time: O(n)
// Space: O(1)
```

### Memoization (Dynamic Programming)
```c
int fib[100];  // Memoization array

int fibonacciMemo(int n) {
    // Base cases
    if(n == 0) return 0;
    if(n == 1) return 1;
    
    // Check if already calculated
    if(fib[n] != -1) {
        return fib[n];
    }
    
    // Calculate and store
    fib[n] = fibonacciMemo(n - 1) + fibonacciMemo(n - 2);
    return fib[n];
}

// Initialize array with -1 before calling
// Time: O(n), Space: O(n)
```

### Trade-off Analysis

| Approach | Time | Space | Pros | Cons |
|----------|------|-------|------|------|
| **Naive Recursive** | O(2ⁿ) | O(n) | Simple, elegant | Extremely slow for large n |
| **Memoization** | O(n) | O(n) | Fast, still recursive | Uses extra space |
| **Iterative** | O(n) | O(1) | Fast, space-efficient | Less intuitive |

---

## 13. Problem Solving: Tower of Hanoi

### Problem Statement
- **Given**: 3 pegs (A, B, C) and n disks
- **Goal**: Move all disks from peg A to peg C
- **Rules**:
  1. Move only one disk at a time
  2. Larger disk cannot be on smaller disk
  3. Use peg B as auxiliary

### Visualization
```
Initial State:              Goal State:
Peg A    Peg B    Peg C     Peg A    Peg B    Peg C
 |         |        |         |         |        |
===        |        |         |         |       ===
====       |        |         |         |      ====
=====      |        |         |         |     =====
```

### Recursive Solution
```c
void towerOfHanoi(int n, char source, char dest, char aux) {
    // Base case: 1 disk
    if(n == 1) {
        printf("Move disk 1 from %c to %c\n", source, dest);
        return;
    }
    
    // Step 1: Move n-1 disks from source to auxiliary (using dest)
    towerOfHanoi(n - 1, source, aux, dest);
    
    // Step 2: Move nth disk from source to destination
    printf("Move disk %d from %c to %c\n", n, source, dest);
    
    // Step 3: Move n-1 disks from auxiliary to destination (using source)
    towerOfHanoi(n - 1, aux, dest, source);
}

// Call: towerOfHanoi(3, 'A', 'C', 'B');
```

### Example Trace (n=3)
```
Step | Action
-----|--------
  1  | Move disk 1 from A to C
  2  | Move disk 2 from A to B
  3  | Move disk 1 from C to B
  4  | Move disk 3 from A to C
  5  | Move disk 1 from B to A
  6  | Move disk 2 from B to C
  7  | Move disk 1 from A to C
```

### Analysis
- **Number of moves**: 2ⁿ - 1
- **Time Complexity**: O(2ⁿ)
- **Space Complexity**: O(n) - Recursion stack
- **Cannot be solved iteratively easily** (recursion is natural solution)

---

## 14. Queue: Abstract Data Type

### Definition
- **Queue**: Linear data structure following FIFO (First In First Out) principle
- **Real-life analogy**: Queue at ticket counter, printer queue

### Characteristics
- Elements inserted at REAR (enqueue)
- Elements removed from FRONT (dequeue)
- Two ends: FRONT and REAR

### Visual Representation
```
FRONT                                      REAR
  ↓                                          ↓
[10] [20] [30] [40] [50]
  ↑                    ↑
Dequeue              Enqueue
(Delete)             (Insert)
```

### Queue Terminology
- **Enqueue**: Insert element at rear
- **Dequeue**: Remove element from front
- **Front**: First element in queue
- **Rear**: Last element in queue
- **Overflow**: Enqueue when queue is full
- **Underflow**: Dequeue when queue is empty

---

## 15. Operations on Queue

### Core Operations

#### 1. Enqueue (Insert)
```
Operation: Add element at rear
Precondition: Queue should not be full
Postcondition: Element added at rear, rear pointer incremented
```

#### 2. Dequeue (Delete)
```
Operation: Remove and return front element
Precondition: Queue should not be empty
Postcondition: Front element removed, front pointer incremented
```

#### 3. Front/Peek
```
Operation: Return front element without removing
Precondition: Queue should not be empty
Postcondition: Queue unchanged
```

#### 4. isEmpty
```
Operation: Check if queue is empty
Return: True if empty, False otherwise
```

#### 5. isFull
```
Operation: Check if queue is full (for array implementation)
Return: True if full, False otherwise
```

### Queue Operations Summary

| Operation | Description | Time Complexity |
|-----------|-------------|-----------------|
| **enqueue(x)** | Insert x at rear | O(1) |
| **dequeue()** | Remove from front | O(1) |
| **front()** | Return front element | O(1) |
| **isEmpty()** | Check if empty | O(1) |
| **isFull()** | Check if full | O(1) |

---

## 16. Array Implementation of Queue

### Structure
```c
#define MAX 100

struct Queue {
    int data[MAX];
    int front;
    int rear;
};
```

### Initialization
```c
void initQueue(struct Queue* q) {
    q->front = -1;
    q->rear = -1;
}
```

### Problem with Simple Implementation
```
After several enqueue/dequeue operations:

[X] [X] [X] [40] [50]
           front  rear

Queue appears half-full but front part is wasted!
Solution: Use Circular Queue
```

### Operations (Simple Queue)

#### 1. Enqueue
```c
void enqueue(struct Queue* q, int value) {
    // Check overflow
    if(q->rear == MAX - 1) {
        printf("Queue Overflow!\n");
        return;
    }
    
    // If first element
    if(q->front == -1) {
        q->front = 0;
    }
    
    // Increment rear and insert
    q->rear++;
    q->data[q->rear] = value;
}

// Time Complexity: O(1)
```

#### 2. Dequeue
```c
int dequeue(struct Queue* q) {
    // Check underflow
    if(q->front == -1 || q->front > q->rear) {
        printf("Queue Underflow!\n");
        return -1;
    }
    
    // Remove and increment front
    int value = q->data[q->front];
    q->front++;
    
    // Reset queue if empty
    if(q->front > q->rear) {
        q->front = q->rear = -1;
    }
    
    return value;
}

// Time Complexity: O(1)
```

---

## 17. Circular Queue

### Concept
- Connect rear end to front end (logically)
- Reuse empty spaces at beginning
- Efficient use of array

### Structure
```c
#define MAX 5

struct CircularQueue {
    int data[MAX];
    int front;
    int rear;
};
```

### Initialization
```c
void initQueue(struct CircularQueue* q) {
    q->front = -1;
    q->rear = -1;
}
```

### Visualization
```
Circular Queue (MAX = 5):

     [0]
    /   \
[4]       [1]
   \     /
    [3] [2]

Indices wrap around: 0→1→2→3→4→0→1...
```

### Operations

#### 1. Enqueue
```c
void enqueue(struct CircularQueue* q, int value) {
    // Check if full
    if((q->rear + 1) % MAX == q->front) {
        printf("Queue is Full!\n");
        return;
    }
    
    // If first element
    if(q->front == -1) {
        q->front = 0;
    }
    
    // Circular increment
    q->rear = (q->rear + 1) % MAX;
    q->data[q->rear] = value;
}

// Time Complexity: O(1)
```

#### 2. Dequeue
```c
int dequeue(struct CircularQueue* q) {
    // Check if empty
    if(q->front == -1) {
        printf("Queue is Empty!\n");
        return -1;
    }
    
    int value = q->data[q->front];
    
    // If only one element
    if(q->front == q->rear) {
        q->front = q->rear = -1;
    } else {
        // Circular increment
        q->front = (q->front + 1) % MAX;
    }
    
    return value;
}

// Time Complexity: O(1)
```

#### 3. Display
```c
void display(struct CircularQueue* q) {
    if(q->front == -1) {
        printf("Queue is empty!\n");
        return;
    }
    
    printf("Queue elements: ");
    int i = q->front;
    
    if(q->front <= q->rear) {
        while(i <= q->rear) {
            printf("%d ", q->data[i]);
            i++;
        }
    } else {
        // Wrapped around case
        while(i < MAX) {
            printf("%d ", q->data[i]);
            i++;
        }
        i = 0;
        while(i <= q->rear) {
            printf("%d ", q->data[i]);
            i++;
        }
    }
    printf("\n");
}
```

### Full vs Empty Condition
- **Empty**: `front == -1`
- **Full**: `(rear + 1) % MAX == front`

---

## 18. Linked List Implementation of Queue

### Node Structure
```c
struct Node {
    int data;
    struct Node* next;
};

struct Queue {
    struct Node* front;
    struct Node* rear;
};
```

### Initialization
```c
void initQueue(struct Queue* q) {
    q->front = NULL;
    q->rear = NULL;
}
```

### Operations

#### 1. Enqueue
```c
void enqueue(struct Queue* q, int value) {
    // Create new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    
    if(newNode == NULL) {
        printf("Memory allocation failed!\n");
        return;
    }
    
    newNode->data = value;
    newNode->next = NULL;
    
    // If queue empty
    if(q->rear == NULL) {
        q->front = q->rear = newNode;
        return;
    }
    
    // Add to rear
    q->rear->next = newNode;
    q->rear = newNode;
}

// Time Complexity: O(1)
```

**Visualization:**
```
Before enqueue(40):
front → [10|•] → [20|•] → [30|NULL] ← rear

After enqueue(40):
front → [10|•] → [20|•] → [30|•] → [40|NULL] ← rear
```

#### 2. Dequeue
```c
int dequeue(struct Queue* q) {
    // Check if empty
    if(q->front == NULL) {
        printf("Queue is empty!\n");
        return -1;
    }
    
    // Save front node
    struct Node* temp = q->front;
    int value = temp->data;
    
    // Move front
    q->front = q->front->next;
    
    // If queue becomes empty
    if(q->front == NULL) {
        q->rear = NULL;
    }
    
    free(temp);
    return value;
}

// Time Complexity: O(1)
```

---

## 19. Dequeue (Double-Ended Queue)

### Definition
- **Dequeue**: Queue where insertion and deletion possible at both ends
- **Types**:
  - **Input-Restricted Dequeue**: Insert only at one end, delete from both
  - **Output-Restricted Dequeue**: Delete only from one end, insert at both

### Operations
- `insertFront(x)`: Insert at front
- `insertRear(x)`: Insert at rear
- `deleteFront()`: Delete from front
- `deleteRear()`: Delete from rear

### Array Implementation
```c
#define MAX 100

struct Dequeue {
    int data[MAX];
    int front;
    int rear;
};

void initDequeue(struct Dequeue* dq) {
    dq->front = -1;
    dq->rear = -1;
}

// Insert at rear (similar to queue enqueue)
void insertRear(struct Dequeue* dq, int value) {
    if(dq->rear == MAX - 1) {
        printf("Dequeue Full at rear!\n");
        return;
    }
    
    if(dq->front == -1) {
        dq->front = 0;
    }
    
    dq->rear++;
    dq->data[dq->rear] = value;
}

// Insert at front
void insertFront(struct Dequeue* dq, int value) {
    if(dq->front == 0 || dq->front == -1) {
        printf("Cannot insert at front!\n");
        return;
    }
    
    dq->front--;
    dq->data[dq->front] = value;
}

// Delete from front (similar to queue dequeue)
int deleteFront(struct Dequeue* dq) {
    if(dq->front == -1 || dq->front > dq->rear) {
        printf("Dequeue Empty!\n");
        return -1;
    }
    
    int value = dq->data[dq->front];
    dq->front++;
    
    if(dq->front > dq->rear) {
        dq->front = dq->rear = -1;
    }
    
    return value;
}

// Delete from rear
int deleteRear(struct Dequeue* dq) {
    if(dq->front == -1 || dq->front > dq->rear) {
        printf("Dequeue Empty!\n");
        return -1;
    }
    
    int value = dq->data[dq->rear];
    dq->rear--;
    
    if(dq->rear < dq->front) {
        dq->front = dq->rear = -1;
    }
    
    return value;
}
```

---

## 20. Priority Queue

### Definition
- **Priority Queue**: Queue where each element has priority
- Higher priority elements served first
- FIFO for equal priority elements

### Types
- **Ascending Priority Queue**: Smallest priority served first
- **Descending Priority Queue**: Largest priority served first

### Applications
- CPU Scheduling
- Dijkstra's Algorithm
- Huffman Coding
- Event-driven simulation

### Implementation Methods

#### Method 1: Unordered Array
```c
struct PriorityQueue {
    int data[MAX];
    int priority[MAX];
    int size;
};

void enqueue(struct PriorityQueue* pq, int value, int priority) {
    if(pq->size == MAX) {
        printf("Queue Full!\n");
        return;
    }
    
    pq->data[pq->size] = value;
    pq->priority[pq->size] = priority;
    pq->size++;
}

int dequeue(struct PriorityQueue* pq) {
    if(pq->size == 0) {
        printf("Queue Empty!\n");
        return -1;
    }
    
    // Find highest priority
    int maxPriority = pq->priority[0];
    int maxIndex = 0;
    
    for(int i = 1; i < pq->size; i++) {
        if(pq->priority[i] > maxPriority) {
            maxPriority = pq->priority[i];
            maxIndex = i;
        }
    }
    
    int value = pq->data[maxIndex];
    
    // Shift elements
    for(int i = maxIndex; i < pq->size - 1; i++) {
        pq->data[i] = pq->data[i + 1];
        pq->priority[i] = pq->priority[i + 1];
    }
    
    pq->size--;
    return value;
}

// Enqueue: O(1), Dequeue: O(n)
```

#### Method 2: Ordered Array (by priority)
```c
void enqueue(struct PriorityQueue* pq, int value, int priority) {
    if(pq->size == MAX) {
        printf("Queue Full!\n");
        return;
    }
    
    // Find position to insert
    int i = pq->size - 1;
    while(i >= 0 && pq->priority[i] < priority) {
        pq->data[i + 1] = pq->data[i];
        pq->priority[i + 1] = pq->priority[i];
        i--;
    }
    
    pq->data[i + 1] = value;
    pq->priority[i + 1] = priority;
    pq->size++;
}

int dequeue(struct PriorityQueue* pq) {
    if(pq->size == 0) {
        printf("Queue Empty!\n");
        return -1;
    }
    
    int value = pq->data[pq->size - 1];
    pq->size--;
    return value;
}

// Enqueue: O(n), Dequeue: O(1)
```

#### Method 3: Binary Heap (Most Efficient)
- **Best implementation**: Use binary heap
- **Enqueue**: O(log n)
- **Dequeue**: O(log n)
- **Covered in**: Unit-4 (Trees)

---

## 🚀 Quick Reference Summary

### Stack vs Queue Comparison

| Aspect | Stack | Queue |
|--------|-------|-------|
| **Principle** | LIFO | FIFO |
| **Operations** | Push, Pop | Enqueue, Dequeue |
| **Access Point** | One end (TOP) | Two ends (FRONT, REAR) |
| **Applications** | Recursion, Expression evaluation | Scheduling, BFS |

### Time Complexities

| Data Structure | Insert | Delete | Search | Access |
|----------------|--------|--------|--------|--------|
| **Stack (Array)** | O(1) | O(1) | O(n) | O(n) |
| **Stack (Linked List)** | O(1) | O(1) | O(n) | O(n) |
| **Queue (Array)** | O(1) | O(1) | O(n) | O(n) |
| **Queue (Linked List)** | O(1) | O(1) | O(n) | O(n) |
| **Circular Queue** | O(1) | O(1) | O(n) | O(n) |
| **Priority Queue (Unordered)** | O(1) | O(n) | O(n) | O(n) |
| **Priority Queue (Heap)** | O(log n) | O(log n) | O(n) | O(1) |

### Recursion vs Iteration Trade-offs

| Factor | Recursion | Iteration |
|--------|-----------|-----------|
| **Memory** | More (stack frames) | Less |
| **Speed** | Slower (overhead) | Faster |
| **Code Size** | Shorter | May be longer |
| **Natural Problems** | Tree traversal, Divide & Conquer | Loops, Sequential |
| **Risk** | Stack overflow | Infinite loop |

---

## 📝 Exam Important Questions

1. **Implement** stack using array and linked list. Compare both implementations.

2. **Convert** infix expression `A + B * C - D / E` to postfix. Show step-by-step trace.

3. **Evaluate** postfix expression `5 3 + 8 2 / *`. Show complete trace.

4. **Write** recursive and iterative functions for:
   - Factorial
   - Fibonacci
   - Binary Search
   Compare time and space complexities.

5. **Explain** Tower of Hanoi problem. Write recursive solution and trace for n=3.

6. **Implement** circular queue operations. Explain how it overcomes limitations of simple queue.

7. **Differentiate** between:
   - Stack vs Queue
   - Simple Queue vs Circular Queue
   - Queue vs Dequeue vs Priority Queue

8. **Write** algorithm to implement two stacks in single array efficiently.

9. **Explain** tail recursion. Convert non-tail recursive factorial to tail recursive version.

10. **Implement** priority queue using:
    - Unordered array
    - Ordered array
    Compare time complexities.

---

*End of Unit-2*
