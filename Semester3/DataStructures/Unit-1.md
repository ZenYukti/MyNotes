# Unit-1: Introduction, Arrays & Linked Lists

---

## 1. Basic Terminology

### Data
- **Data**: Raw facts and figures
- **Information**: Processed data with meaning
- **Data Item**: Single unit of values
  - **Elementary Item**: Cannot be divided (e.g., student ID)
  - **Group Item**: Can be divided into sub-items (e.g., student name)

### Data Structure
- **Definition**: Way of organizing and storing data for efficient access and modification
- **Types**:
  - **Primitive**: Built-in types (int, float, char, etc.)
  - **Non-Primitive**: Derived types (arrays, structures, etc.)

### Classification of Data Structures

```
Data Structures
    |
    |--- Primitive
    |       |--- Integer
    |       |--- Float
    |       |--- Character
    |       |--- Boolean
    |
    |--- Non-Primitive
            |
            |--- Linear
            |       |--- Static (Array)
            |       |--- Dynamic (Linked List, Stack, Queue)
            |
            |--- Non-Linear
                    |--- Trees
                    |--- Graphs
```

### Elementary Data Organization

#### Data Field
- Single piece of information
- Example: Employee Name, Age, Salary

#### Record
- Collection of related data fields
- Example: Employee record = {ID, Name, Age, Salary}

#### File
- Collection of records
- Example: Employee file = Collection of all employee records

#### Database
- Collection of related files
- Example: Company database = {Employee file, Department file, Project file}

---

## 2. Built-in Data Types in C

### Integer Types
```c
char        // 1 byte (-128 to 127 or 0 to 255)
short       // 2 bytes (-32,768 to 32,767)
int         // 4 bytes (-2,147,483,648 to 2,147,483,647)
long        // 4 or 8 bytes
long long   // 8 bytes
```

### Floating-Point Types
```c
float       // 4 bytes (6 decimal places)
double      // 8 bytes (15 decimal places)
long double // 10 bytes (19 decimal places)
```

### Character Type
```c
char        // 1 byte (-128 to 127 or 0 to 255)
```

### Derived Types
- **Array**: Collection of similar data types
- **Pointer**: Stores memory address
- **Structure**: Collection of different data types
- **Union**: Special data type for storing different data types in same memory

---

## 3. Algorithm

### Definition
- **Algorithm**: Step-by-step procedure to solve a problem
- **Characteristics**:
  - **Input**: Zero or more inputs
  - **Output**: At least one output
  - **Definiteness**: Each step clearly defined
  - **Finiteness**: Must terminate after finite steps
  - **Effectiveness**: Each operation must be basic enough to be executed

### Algorithm Representation

#### Example: Find Maximum of Three Numbers
```
Algorithm: FindMax(a, b, c)
Input: Three numbers a, b, c
Output: Maximum of three numbers

1. Start
2. Read a, b, c
3. If (a > b) and (a > c) then
       max = a
   Else if (b > c) then
       max = b
   Else
       max = c
4. Print max
5. Stop
```

---

## 4. Efficiency of an Algorithm

### Performance Factors
- **Time Complexity**: Amount of time taken to run
- **Space Complexity**: Amount of memory space required

### How to Measure Efficiency?

#### Time Complexity
- Measured by counting:
  - Number of comparisons
  - Number of assignments
  - Number of operations
- Expressed as function of input size **n**

#### Space Complexity
- **Fixed Part**: Space for constants, variables, program code
- **Variable Part**: Space for dynamic allocation, recursion stack

---

## 5. Time and Space Complexity

### Time Complexity Analysis

#### Best Case
- Minimum time required
- Represented by **Ω (Omega)**

#### Average Case
- Expected time for random input
- Represented by **Θ (Theta)**

#### Worst Case
- Maximum time required
- Represented by **O (Big Oh)**

### Example: Linear Search
```c
int linearSearch(int arr[], int n, int key) {
    for(int i = 0; i < n; i++) {
        if(arr[i] == key)
            return i;
    }
    return -1;
}
```
- **Best Case**: Ω(1) - Element found at first position
- **Average Case**: Θ(n/2) ≈ Θ(n)
- **Worst Case**: O(n) - Element at last or not present

### Space Complexity

#### Components
- **Instruction Space**: Space for code
- **Data Space**: Space for constants, variables
- **Environment Space**: Space for function calls, recursion

#### Example
```c
int sum(int n) {
    return n * (n + 1) / 2;  // S(n) = O(1)
}

int sumRecursive(int n) {
    if(n == 0) return 0;
    return n + sumRecursive(n-1);  // S(n) = O(n) due to recursion stack
}
```

---

## 6. Asymptotic Notations

### Big Oh (O) - Upper Bound

#### Definition
- **O(g(n))**: Set of functions that grow no faster than g(n)
- f(n) = O(g(n)) if ∃ positive constants c and n₀ such that:
  - **f(n) ≤ c × g(n)** for all n ≥ n₀

#### Example
- f(n) = 3n + 2
- f(n) = O(n) because 3n + 2 ≤ 4n for n ≥ 2

### Big Omega (Ω) - Lower Bound

#### Definition
- **Ω(g(n))**: Set of functions that grow at least as fast as g(n)
- f(n) = Ω(g(n)) if ∃ positive constants c and n₀ such that:
  - **f(n) ≥ c × g(n)** for all n ≥ n₀

#### Example
- f(n) = 3n + 2
- f(n) = Ω(n) because 3n + 2 ≥ 3n for all n ≥ 0

### Big Theta (Θ) - Tight Bound

#### Definition
- **Θ(g(n))**: Set of functions that grow at same rate as g(n)
- f(n) = Θ(g(n)) if f(n) = O(g(n)) and f(n) = Ω(g(n))
- ∃ positive constants c₁, c₂, and n₀ such that:
  - **c₁ × g(n) ≤ f(n) ≤ c₂ × g(n)** for all n ≥ n₀

#### Example
- f(n) = 3n + 2
- f(n) = Θ(n) because 3n ≤ 3n + 2 ≤ 4n for n ≥ 2

### Common Complexity Classes (Increasing Order)
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)

Constant < Logarithmic < Linear < Linearithmic < Quadratic < Cubic < Exponential < Factorial
```

### Properties of Asymptotic Notations

#### Transitivity
- If f(n) = O(g(n)) and g(n) = O(h(n)), then f(n) = O(h(n))

#### Reflexivity
- f(n) = O(f(n))

#### Symmetry (for Θ)
- If f(n) = Θ(g(n)), then g(n) = Θ(f(n))

#### Sum Rule
- O(f(n)) + O(g(n)) = O(max(f(n), g(n)))

#### Product Rule
- O(f(n)) × O(g(n)) = O(f(n) × g(n))

---

## 7. Time-Space Trade-off

### Concept
- **Definition**: Situation where we can reduce time by using more space, or reduce space by using more time
- **Goal**: Find optimal balance based on requirements

### Examples

#### Example 1: Lookup Table vs Computation
**Approach 1: Compute Every Time**
```c
int factorial(int n) {
    if(n <= 1) return 1;
    return n * factorial(n-1);
}
// Time: O(n), Space: O(1)
```

**Approach 2: Precompute and Store**
```c
int fact[100];  // Precomputed factorials
// Time: O(1) lookup, Space: O(n) storage
```

#### Example 2: String Matching
- **Naive Approach**: O(mn) time, O(1) space
- **KMP Algorithm**: O(m+n) time, O(m) space for pattern preprocessing

### When to Use?
- **Time-Critical Applications**: Use more space (caching, memoization)
- **Space-Critical Applications**: Use more time (embedded systems, mobile apps)

---

## 8. Abstract Data Types (ADT)

### Definition
- **ADT**: Mathematical model with set of operations defined on it
- Specifies **WHAT** to do, not **HOW** to do it
- Separates interface from implementation

### Characteristics
- **Data encapsulation**: Hide internal representation
- **Data abstraction**: Define operations independent of implementation
- **Information hiding**: User doesn't need to know implementation details

### Examples of ADT

#### List ADT
**Operations:**
- `insert(x)`: Insert element x
- `delete(x)`: Delete element x
- `search(x)`: Search for element x
- `isEmpty()`: Check if empty
- `size()`: Return number of elements

#### Stack ADT
**Operations:**
- `push(x)`: Insert element at top
- `pop()`: Remove and return top element
- `peek()`: Return top element without removing
- `isEmpty()`: Check if empty

#### Queue ADT
**Operations:**
- `enqueue(x)`: Insert element at rear
- `dequeue()`: Remove and return front element
- `front()`: Return front element
- `isEmpty()`: Check if empty

---

## 9. Arrays: Definition and Types

### Definition
- **Array**: Collection of elements of same data type stored in contiguous memory locations
- **Index**: Position of element in array (0-based in C)
- **Size**: Fixed at compile time (static)

### Characteristics
- **Homogeneous**: All elements of same type
- **Contiguous Memory**: Elements stored in consecutive locations
- **Random Access**: Direct access using index in O(1) time
- **Fixed Size**: Cannot be changed after declaration

### Array Declaration in C
```c
// Single-dimensional array
int arr[10];              // Array of 10 integers
float marks[5];           // Array of 5 floats
char name[20];            // Array of 20 characters

// Initialization
int arr[5] = {1, 2, 3, 4, 5};
int arr[] = {1, 2, 3, 4, 5};  // Size automatically determined
```

### Single-Dimensional Array

#### Structure
```
Array: arr[5] = {10, 20, 30, 40, 50}

Memory Layout:
+----+----+----+----+----+
| 10 | 20 | 30 | 40 | 50 |
+----+----+----+----+----+
  0    1    2    3    4     (Indices)
```

#### Operations
```c
// Access
int value = arr[2];  // value = 30

// Modify
arr[3] = 100;  // arr = {10, 20, 30, 100, 50}

// Traversal
for(int i = 0; i < 5; i++) {
    printf("%d ", arr[i]);
}
```

### Multi-Dimensional Arrays

#### Two-Dimensional Array (Matrix)
```c
// Declaration
int matrix[3][4];  // 3 rows, 4 columns

// Initialization
int matrix[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

**Visual Representation:**
```
matrix[3][3]:
     Col0  Col1  Col2
Row0   1     2     3
Row1   4     5     6
Row2   7     8     9
```

#### Three-Dimensional Array
```c
int arr3D[2][3][4];  // 2 blocks, 3 rows, 4 columns

/*
Visualization:
Block 0:              Block 1:
  [row0: 4 cols]       [row0: 4 cols]
  [row1: 4 cols]       [row1: 4 cols]
  [row2: 4 cols]       [row2: 4 cols]
*/
```

---

## 10. Representation of Arrays

### Row Major Order (RMO)

#### Concept
- Elements stored row-by-row
- Complete first row, then second row, and so on
- **Used by**: C, C++, Pascal

#### Example
```
Matrix A[3][3]:
1  2  3
4  5  6
7  8  9

Row Major Order in Memory:
1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9
```

### Column Major Order (CMO)

#### Concept
- Elements stored column-by-column
- Complete first column, then second column, and so on
- **Used by**: FORTRAN, MATLAB

#### Example
```
Matrix A[3][3]:
1  2  3
4  5  6
7  8  9

Column Major Order in Memory:
1 → 4 → 7 → 2 → 5 → 8 → 3 → 6 → 9
```

---

## 11. Index Formulae for Arrays

### One-Dimensional Array

#### Formula
```
Address(arr[i]) = Base_Address + (i - LB) × Size_of_Element

Where:
- Base_Address: Starting address of array
- i: Index of element
- LB: Lower Bound (usually 0 in C)
- Size_of_Element: Size of one element in bytes
```

#### Example
```
int arr[10];  // Base address = 1000, Size of int = 4 bytes
Address(arr[5]) = 1000 + (5 - 0) × 4 = 1000 + 20 = 1020
```

### Two-Dimensional Array

#### Row Major Order Formula
```
Address(arr[i][j]) = Base + [(i - LB₁) × n + (j - LB₂)] × Size

Where:
- LB₁: Lower bound of rows (0 in C)
- LB₂: Lower bound of columns (0 in C)
- n: Number of columns
```

#### Column Major Order Formula
```
Address(arr[i][j]) = Base + [(j - LB₂) × m + (i - LB₁)] × Size

Where:
- m: Number of rows
```

#### Example (Row Major Order)
```
int matrix[3][4];  // Base = 1000, Size = 4 bytes
Address(matrix[2][3]) = 1000 + [(2-0) × 4 + (3-0)] × 4
                      = 1000 + [8 + 3] × 4
                      = 1000 + 44
                      = 1044
```

### Three-Dimensional Array

#### Row Major Order Formula
```
Address(arr[i][j][k]) = Base + [(i - LB₁) × n × p + (j - LB₂) × p + (k - LB₃)] × Size

Where:
- LB₁, LB₂, LB₃: Lower bounds
- n: Number of rows (2nd dimension)
- p: Number of columns (3rd dimension)
```

#### Example
```
int arr[2][3][4];  // Base = 1000, Size = 4 bytes
Address(arr[1][2][3]) = 1000 + [(1-0)×3×4 + (2-0)×4 + (3-0)] × 4
                      = 1000 + [12 + 8 + 3] × 4
                      = 1000 + 92
                      = 1092
```

### n-Dimensional Array

#### General Formula (Row Major Order)
```
Address(A[i₁][i₂]...[iₙ]) = Base + [
    (i₁ - LB₁) × d₂ × d₃ × ... × dₙ +
    (i₂ - LB₂) × d₃ × d₄ × ... × dₙ +
    ...
    (iₙ₋₁ - LBₙ₋₁) × dₙ +
    (iₙ - LBₙ)
] × Size

Where d₂, d₃, ..., dₙ are dimensions
```

---

## 12. Applications of Arrays

### 1. Implementing Other Data Structures
- Stacks, Queues, Hash Tables
- Matrices, Sparse Matrices
- Heaps, Priority Queues

### 2. Sorting and Searching
- Storing elements for sorting algorithms
- Binary search on sorted arrays
- Finding min/max elements

### 3. Matrix Operations
- Addition, Subtraction, Multiplication
- Transpose, Determinant calculation
- Solving linear equations

### 4. Lookup Tables
- Pre-computed values (factorials, primes)
- Character encoding tables
- Mathematical function values

### 5. Buffers
- I/O buffers for data transfer
- Screen buffers for graphics
- Audio/video streaming buffers

### 6. Dynamic Programming
- Memoization tables
- DP state storage
- Tabulation method

---

## 13. Sparse Matrices

### Definition
- **Sparse Matrix**: Matrix where most elements are zero
- **Criterion**: Number of non-zero elements ≤ (rows × columns) / 3

### Example
```
Standard Matrix (4×5):
0  0  3  0  4
0  0  5  7  0
0  0  0  0  0
0  2  6  0  0

Non-zero elements: 6 out of 20 (30%)
This is a sparse matrix!
```

### Why Sparse Matrix Representation?
- **Memory Efficiency**: Store only non-zero elements
- **Time Efficiency**: Skip operations on zero elements
- **Example**: 1000×1000 matrix with 1% non-zero elements
  - Normal: 1,000,000 elements × 4 bytes = 4 MB
  - Sparse: 10,000 elements × (3 × 4 bytes) = 120 KB

### Sparse Matrix Representations

#### 1. Array (Triplet) Representation

**Structure:**
```
Each non-zero element stored as: (row, column, value)

Array format:
[0] [Number of rows, Number of columns, Number of non-zero elements]
[1] [row₁, col₁, value₁]
[2] [row₂, col₂, value₂]
...
```

**Example:**
```
Original Matrix:
0  0  3  0  4
0  0  5  7  0
0  0  0  0  0
0  2  6  0  0

Triplet Representation:
Row  Col  Value
 4    5     6     // Header: rows, cols, non-zero count
 0    2     3
 0    4     4
 1    2     5
 1    3     7
 3    1     2
 3    2     6
```

**C Structure:**
```c
struct Element {
    int row;
    int col;
    int value;
};

struct SparseMatrix {
    int rows, cols, num;
    struct Element *elements;
};
```

**Advantages:**
- Simple to implement
- Easy to traverse
- Suitable for algorithms processing in row order

**Disadvantages:**
- Random access is O(n) where n = non-zero elements
- Insertion/deletion requires shifting

#### 2. Linked List Representation

**Structure:**
```
Header node → (row, col, value, next) → ... → NULL

For each row, maintain a linked list of non-zero columns
```

**Advantages:**
- Dynamic size
- Easy insertion/deletion
- No shifting required

**Disadvantages:**
- Extra memory for pointers
- Sequential access only

#### 3. Dictionary of Keys (DOK)

**Concept:**
- Use hash table with (row, col) as key and value as data
- Fast access: O(1) average case

**Python Example:**
```python
sparse = {
    (0, 2): 3,
    (0, 4): 4,
    (1, 2): 5,
    (1, 3): 7,
    (3, 1): 2,
    (3, 2): 6
}
```

### Operations on Sparse Matrices

#### Transpose
```
Algorithm: Transpose of Sparse Matrix
Input: Sparse matrix A (triplet form)
Output: Transposed matrix B

1. B[0] = [A[0].cols, A[0].rows, A[0].num]
2. For each element in A (starting from A[1]):
       Swap row and column
       Store in B
3. Sort B by row (and column within row)
```

#### Addition (A + B)
- Traverse both matrices simultaneously
- If same (row, col): Add values
- If different: Copy smaller (row, col) element
- Continue until both exhausted

**Time Complexity**: O(m + n) where m, n are non-zero elements

---

## 14. Linked Lists: Introduction

### Definition
- **Linked List**: Linear data structure where elements are stored in nodes
- Each node contains:
  - **Data**: Actual value
  - **Pointer**: Address of next node

### Advantages over Arrays
- **Dynamic Size**: Can grow/shrink at runtime
- **Efficient Insertion/Deletion**: O(1) if position known
- **No Memory Waste**: Allocate only what's needed

### Disadvantages
- **Extra Memory**: Pointers require additional space
- **No Random Access**: Must traverse from head (O(n))
- **Cache Unfriendly**: Non-contiguous memory locations

### Node Structure
```c
struct Node {
    int data;           // Data field
    struct Node* next;  // Pointer to next node
};
```

---

## 15. Singly Linked List

### Structure
```
[Data|Next] → [Data|Next] → [Data|Next] → NULL

Example:
[10|•] → [20|•] → [30|NULL]
```

### Array Implementation

#### Concept
- Use two arrays: DATA[] and NEXT[]
- DATA[i]: Stores data
- NEXT[i]: Stores index of next node
- Special value (e.g., -1) indicates NULL

#### Example
```
Logical List: 10 → 20 → 30 → NULL
Head = 0

Index:  0   1   2   3   4
DATA:  10  20  30  --  --
NEXT:   1   2  -1  --  --
```

### Pointer Implementation

#### Basic Operations

**1. Create Node**
```c
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if(newNode == NULL) {
        printf("Memory allocation failed\n");
        return NULL;
    }
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}
```

**2. Insert at Beginning**
```c
struct Node* insertAtBeginning(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    return head;
}

// Time Complexity: O(1)
```

**3. Insert at End**
```c
struct Node* insertAtEnd(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    
    if(head == NULL) {
        return newNode;
    }
    
    struct Node* temp = head;
    while(temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
    return head;
}

// Time Complexity: O(n)
```

**4. Insert at Position**
```c
struct Node* insertAtPosition(struct Node* head, int data, int pos) {
    if(pos == 1) {
        return insertAtBeginning(head, data);
    }
    
    struct Node* newNode = createNode(data);
    struct Node* temp = head;
    
    for(int i = 1; i < pos-1 && temp != NULL; i++) {
        temp = temp->next;
    }
    
    if(temp == NULL) {
        printf("Position out of range\n");
        free(newNode);
        return head;
    }
    
    newNode->next = temp->next;
    temp->next = newNode;
    return head;
}

// Time Complexity: O(n)
```

**5. Delete from Beginning**
```c
struct Node* deleteFromBeginning(struct Node* head) {
    if(head == NULL) {
        printf("List is empty\n");
        return NULL;
    }
    
    struct Node* temp = head;
    head = head->next;
    free(temp);
    return head;
}

// Time Complexity: O(1)
```

**6. Delete from End**
```c
struct Node* deleteFromEnd(struct Node* head) {
    if(head == NULL) {
        printf("List is empty\n");
        return NULL;
    }
    
    if(head->next == NULL) {
        free(head);
        return NULL;
    }
    
    struct Node* temp = head;
    while(temp->next->next != NULL) {
        temp = temp->next;
    }
    
    free(temp->next);
    temp->next = NULL;
    return head;
}

// Time Complexity: O(n)
```

**7. Delete by Value**
```c
struct Node* deleteByValue(struct Node* head, int key) {
    if(head == NULL) return NULL;
    
    // If head contains the key
    if(head->data == key) {
        struct Node* temp = head;
        head = head->next;
        free(temp);
        return head;
    }
    
    struct Node* temp = head;
    while(temp->next != NULL && temp->next->data != key) {
        temp = temp->next;
    }
    
    if(temp->next == NULL) {
        printf("Key not found\n");
        return head;
    }
    
    struct Node* toDelete = temp->next;
    temp->next = temp->next->next;
    free(toDelete);
    return head;
}

// Time Complexity: O(n)
```

**8. Search**
```c
int search(struct Node* head, int key) {
    struct Node* temp = head;
    int position = 1;
    
    while(temp != NULL) {
        if(temp->data == key) {
            return position;
        }
        temp = temp->next;
        position++;
    }
    return -1;  // Not found
}

// Time Complexity: O(n)
```

**9. Traverse/Display**
```c
void display(struct Node* head) {
    if(head == NULL) {
        printf("List is empty\n");
        return;
    }
    
    struct Node* temp = head;
    while(temp != NULL) {
        printf("%d → ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

// Time Complexity: O(n)
```

---

## 16. Doubly Linked List

### Definition
- Each node has two pointers:
  - **prev**: Points to previous node
  - **next**: Points to next node
- Allows traversal in both directions

### Structure
```
NULL ← [prev|Data|next] ⇄ [prev|Data|next] ⇄ [prev|Data|next] → NULL

Example:
NULL ← [•|10|•] ⇄ [•|20|•] ⇄ [•|30|NULL]
```

### Node Structure
```c
struct DNode {
    int data;
    struct DNode* prev;
    struct DNode* next;
};
```

### Advantages
- Bidirectional traversal
- Delete node without traversing from head
- Insert before a given node easily

### Disadvantages
- Extra memory for prev pointer
- More complex operations

### Operations

**1. Insert at Beginning**
```c
struct DNode* insertAtBeginning(struct DNode* head, int data) {
    struct DNode* newNode = (struct DNode*)malloc(sizeof(struct DNode));
    newNode->data = data;
    newNode->prev = NULL;
    newNode->next = head;
    
    if(head != NULL) {
        head->prev = newNode;
    }
    
    head = newNode;
    return head;
}

// Time Complexity: O(1)
```

**2. Insert at End**
```c
struct DNode* insertAtEnd(struct DNode* head, int data) {
    struct DNode* newNode = (struct DNode*)malloc(sizeof(struct DNode));
    newNode->data = data;
    newNode->next = NULL;
    
    if(head == NULL) {
        newNode->prev = NULL;
        return newNode;
    }
    
    struct DNode* temp = head;
    while(temp->next != NULL) {
        temp = temp->next;
    }
    
    temp->next = newNode;
    newNode->prev = temp;
    return head;
}

// Time Complexity: O(n)
```

**3. Delete Node**
```c
struct DNode* deleteNode(struct DNode* head, struct DNode* del) {
    if(head == NULL || del == NULL) return head;
    
    // If node to delete is head
    if(head == del) {
        head = del->next;
    }
    
    // Change next only if not last node
    if(del->next != NULL) {
        del->next->prev = del->prev;
    }
    
    // Change prev only if not first node
    if(del->prev != NULL) {
        del->prev->next = del->next;
    }
    
    free(del);
    return head;
}

// Time Complexity: O(1) if node pointer given
```

**4. Reverse Traversal**
```c
void displayReverse(struct DNode* head) {
    if(head == NULL) return;
    
    // Go to last node
    struct DNode* temp = head;
    while(temp->next != NULL) {
        temp = temp->next;
    }
    
    // Traverse backward
    printf("Reverse: ");
    while(temp != NULL) {
        printf("%d ← ", temp->data);
        temp = temp->prev;
    }
    printf("NULL\n");
}
```

---

## 17. Circular Linked List

### Definition
- Last node points back to first node (or head)
- Forms a circular structure
- Can be singly or doubly circular

### Singly Circular Linked List
```
     ┌─────────────────────┐
     ↓                     |
[Data|Next] → [Data|Next] → [Data|Next]
```

### Structure
```c
// Same as singly linked list
struct Node {
    int data;
    struct Node* next;
};

// But last node's next points to head, not NULL
```

### Operations

**1. Insert at Beginning**
```c
struct Node* insertAtBeginning(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    
    if(head == NULL) {
        newNode->next = newNode;  // Points to itself
        return newNode;
    }
    
    // Find last node
    struct Node* temp = head;
    while(temp->next != head) {
        temp = temp->next;
    }
    
    newNode->next = head;
    temp->next = newNode;
    head = newNode;
    return head;
}
```

**2. Insert at End**
```c
struct Node* insertAtEnd(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    
    if(head == NULL) {
        newNode->next = newNode;
        return newNode;
    }
    
    struct Node* temp = head;
    while(temp->next != head) {
        temp = temp->next;
    }
    
    temp->next = newNode;
    newNode->next = head;
    return head;
}
```

**3. Delete Node**
```c
struct Node* deleteNode(struct Node* head, int key) {
    if(head == NULL) return NULL;
    
    // If only one node
    if(head->data == key && head->next == head) {
        free(head);
        return NULL;
    }
    
    // If head is to be deleted
    if(head->data == key) {
        struct Node* temp = head;
        while(temp->next != head) {
            temp = temp->next;
        }
        temp->next = head->next;
        struct Node* toDelete = head;
        head = head->next;
        free(toDelete);
        return head;
    }
    
    // Delete from middle or end
    struct Node* temp = head;
    while(temp->next != head && temp->next->data != key) {
        temp = temp->next;
    }
    
    if(temp->next == head) {
        printf("Key not found\n");
        return head;
    }
    
    struct Node* toDelete = temp->next;
    temp->next = temp->next->next;
    free(toDelete);
    return head;
}
```

**4. Display**
```c
void display(struct Node* head) {
    if(head == NULL) {
        printf("List is empty\n");
        return;
    }
    
    struct Node* temp = head;
    do {
        printf("%d → ", temp->data);
        temp = temp->next;
    } while(temp != head);
    printf("(back to head)\n");
}
```

### Advantages
- Can traverse entire list from any node
- No NULL pointers
- Useful for round-robin scheduling

### Disadvantages
- Infinite loop risk if not careful
- More complex operations

---

## 18. Polynomial Representation

### Polynomial Definition
```
P(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₁x + a₀

Example: P(x) = 5x³ + 4x² + 2x + 1
```

### Representation Using Arrays

#### Method 1: Coefficient Array
```c
// Store only coefficients
float poly[4] = {1, 2, 4, 5};  // Represents 5x³ + 4x² + 2x + 1
// Index represents power of x
```

#### Method 2: Structure Array
```c
struct Term {
    float coeff;
    int exp;
};

struct Term poly[4] = {
    {5, 3},   // 5x³
    {4, 2},   // 4x²
    {2, 1},   // 2x
    {1, 0}    // 1
};
```

### Representation Using Linked List

#### Structure
```c
struct PolyNode {
    float coeff;
    int exp;
    struct PolyNode* next;
};
```

#### Example
```
Polynomial: 5x³ + 4x² + 2x + 1

Linked List:
[5,3|•] → [4,2|•] → [2,1|•] → [1,0|NULL]
```

### Advantages of Linked List
- **Space Efficient**: Store only non-zero terms
- **Dynamic Size**: No fixed limit
- **Easy Manipulation**: Insert/delete terms easily

---

## 19. Polynomial Operations (Single Variable)

### Addition of Polynomials

**Algorithm:**
```
Algorithm: Add Polynomials
Input: Two polynomials P1 and P2
Output: Sum polynomial P3 = P1 + P2

1. Compare exponents of current terms in P1 and P2
2. If exp1 > exp2:
       Add term from P1 to result
       Move to next term in P1
3. Else if exp1 < exp2:
       Add term from P2 to result
       Move to next term in P2
4. Else (exp1 == exp2):
       Add coefficients
       If sum != 0, add to result
       Move to next term in both P1 and P2
5. Repeat until both polynomials exhausted
```

**C Implementation:**
```c
struct PolyNode* addPoly(struct PolyNode* p1, struct PolyNode* p2) {
    struct PolyNode *result = NULL, *tail = NULL;
    
    while(p1 != NULL && p2 != NULL) {
        struct PolyNode* newNode = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        
        if(p1->exp > p2->exp) {
            newNode->coeff = p1->coeff;
            newNode->exp = p1->exp;
            p1 = p1->next;
        }
        else if(p1->exp < p2->exp) {
            newNode->coeff = p2->coeff;
            newNode->exp = p2->exp;
            p2 = p2->next;
        }
        else {  // Equal exponents
            float sum = p1->coeff + p2->coeff;
            if(sum != 0) {
                newNode->coeff = sum;
                newNode->exp = p1->exp;
            } else {
                free(newNode);
                p1 = p1->next;
                p2 = p2->next;
                continue;
            }
            p1 = p1->next;
            p2 = p2->next;
        }
        
        newNode->next = NULL;
        if(result == NULL) {
            result = tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }
    
    // Copy remaining terms
    while(p1 != NULL) {
        struct PolyNode* newNode = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        newNode->coeff = p1->coeff;
        newNode->exp = p1->exp;
        newNode->next = NULL;
        tail->next = newNode;
        tail = newNode;
        p1 = p1->next;
    }
    
    while(p2 != NULL) {
        struct PolyNode* newNode = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        newNode->coeff = p2->coeff;
        newNode->exp = p2->exp;
        newNode->next = NULL;
        tail->next = newNode;
        tail = newNode;
        p2 = p2->next;
    }
    
    return result;
}

// Time Complexity: O(m + n) where m, n are terms in P1, P2
```

**Example:**
```
P1(x) = 5x³ + 4x² + 2
P2(x) = 3x³ + 2x² + 5x + 1

P1 + P2 = (5+3)x³ + (4+2)x² + 5x + (2+1)
        = 8x³ + 6x² + 5x + 3
```

### Subtraction of Polynomials

**Algorithm:**
```
P1 - P2 = P1 + (-P2)

1. Negate all coefficients of P2
2. Add P1 and (-P2)
```

**Implementation:**
```c
struct PolyNode* subtractPoly(struct PolyNode* p1, struct PolyNode* p2) {
    // Create negative of p2
    struct PolyNode* negP2 = NULL;
    struct PolyNode* temp = p2;
    
    while(temp != NULL) {
        struct PolyNode* newNode = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        newNode->coeff = -(temp->coeff);
        newNode->exp = temp->exp;
        newNode->next = negP2;
        negP2 = newNode;
        temp = temp->next;
    }
    
    return addPoly(p1, negP2);
}
```

### Multiplication of Polynomials

**Algorithm:**
```
Algorithm: Multiply Polynomials
Input: Two polynomials P1 and P2
Output: Product polynomial P3 = P1 × P2

1. Initialize result polynomial to 0
2. For each term in P1:
       For each term in P2:
           Multiply coefficients: coeff = coeff1 × coeff2
           Add exponents: exp = exp1 + exp2
           Add this term to result (combine like terms)
3. Return result
```

**Implementation:**
```c
struct PolyNode* multiplyPoly(struct PolyNode* p1, struct PolyNode* p2) {
    if(p1 == NULL || p2 == NULL) return NULL;
    
    struct PolyNode* result = NULL;
    struct PolyNode* temp1 = p1;
    
    while(temp1 != NULL) {
        struct PolyNode* temp2 = p2;
        
        while(temp2 != NULL) {
            // Multiply terms
            float coeff = temp1->coeff * temp2->coeff;
            int exp = temp1->exp + temp2->exp;
            
            // Add to result (need function to add single term)
            result = addTerm(result, coeff, exp);
            
            temp2 = temp2->next;
        }
        temp1 = temp1->next;
    }
    
    return result;
}

// Helper function to add single term
struct PolyNode* addTerm(struct PolyNode* poly, float coeff, int exp) {
    // Search for term with same exponent
    struct PolyNode* temp = poly;
    struct PolyNode* prev = NULL;
    
    while(temp != NULL && temp->exp > exp) {
        prev = temp;
        temp = temp->next;
    }
    
    if(temp != NULL && temp->exp == exp) {
        temp->coeff += coeff;
        if(temp->coeff == 0) {
            // Remove node if coefficient becomes 0
            if(prev == NULL) {
                poly = temp->next;
            } else {
                prev->next = temp->next;
            }
            free(temp);
        }
    } else {
        // Insert new node
        struct PolyNode* newNode = (struct PolyNode*)malloc(sizeof(struct PolyNode));
        newNode->coeff = coeff;
        newNode->exp = exp;
        newNode->next = temp;
        
        if(prev == NULL) {
            poly = newNode;
        } else {
            prev->next = newNode;
        }
    }
    
    return poly;
}

// Time Complexity: O(m × n) where m, n are terms in P1, P2
```

**Example:**
```
P1(x) = 2x² + 3x + 1
P2(x) = x + 2

P1 × P2 = (2x² + 3x + 1)(x + 2)
        = 2x³ + 4x² + 3x² + 6x + x + 2
        = 2x³ + 7x² + 7x + 2
```

---

## 20. Two-Variable Polynomial Operations

### Representation

#### Structure
```c
struct Term2D {
    float coeff;
    int expX;   // Exponent of x
    int expY;   // Exponent of y
    struct Term2D* next;
};
```

### Example
```
P(x,y) = 3x²y³ + 5xy² + 2x + 7

Linked List:
[3,2,3|•] → [5,1,2|•] → [2,1,0|•] → [7,0,0|NULL]
```

### Ordering Terms
- **Primary**: By x exponent (descending)
- **Secondary**: By y exponent (descending) for same x exponent

### Addition Algorithm
```
Algorithm: Add 2D Polynomials
1. Compare (expX1, expY1) with (expX2, expY2)
2. If (expX1, expY1) > (expX2, expY2):
       Add term from P1
3. Else if (expX1, expY1) < (expX2, expY2):
       Add term from P2
4. Else:  // Same exponents
       Add coefficients
5. Continue until both exhausted
```

### Multiplication
```
For each term in P1:
    For each term in P2:
        coeff = coeff1 × coeff2
        expX = expX1 + expX2
        expY = expY1 + expY2
        Add to result
```

**Example:**
```
P1(x,y) = 2xy + 3
P2(x,y) = x + y

P1 × P2 = (2xy + 3)(x + y)
        = 2x²y + 2xy² + 3x + 3y
```

---

## 🚀 Quick Reference Summary

### Time Complexities

| Operation | Array | Singly LL | Doubly LL | Circular LL |
|-----------|-------|-----------|-----------|-------------|
| **Access** | O(1) | O(n) | O(n) | O(n) |
| **Insert at Begin** | O(n) | O(1) | O(1) | O(1) |
| **Insert at End** | O(1) | O(n) | O(n) | O(n) |
| **Delete at Begin** | O(n) | O(1) | O(1) | O(1) |
| **Delete at End** | O(1) | O(n) | O(n) | O(n) |
| **Search** | O(n) | O(n) | O(n) | O(n) |

### Space Complexities

| Data Structure | Space |
|----------------|-------|
| **Array** | O(n) |
| **Singly Linked List** | O(n) + pointer overhead |
| **Doubly Linked List** | O(n) + 2×pointer overhead |
| **Sparse Matrix (Triplet)** | O(k) where k = non-zero elements |

### Key Formulas

**Array Address Calculation:**
- **1D**: `Address(arr[i]) = Base + (i - LB) × Size`
- **2D (Row Major)**: `Address(arr[i][j]) = Base + [(i - LB₁) × n + (j - LB₂)] × Size`
- **2D (Column Major)**: `Address(arr[i][j]) = Base + [(j - LB₂) × m + (i - LB₁)] × Size`

**Asymptotic Notations:**
- **Big O**: f(n) ≤ c × g(n) (Upper Bound)
- **Big Ω**: f(n) ≥ c × g(n) (Lower Bound)
- **Big Θ**: c₁ × g(n) ≤ f(n) ≤ c₂ × g(n) (Tight Bound)

### Common Operations Comparison

| Feature | Array | Linked List |
|---------|-------|-------------|
| **Size** | Fixed | Dynamic |
| **Memory** | Contiguous | Non-contiguous |
| **Access** | Random (O(1)) | Sequential (O(n)) |
| **Insert/Delete** | O(n) | O(1) at known position |
| **Memory Waste** | Pre-allocated | Pointer overhead |
| **Cache** | Friendly | Unfriendly |

---

## 📝 Exam Important Questions

1. **Explain** Big O, Big Omega, and Big Theta notations with examples. Prove that 3n² + 2n + 5 = O(n²).

2. **Derive** address formula for 2D array in Row Major Order and Column Major Order.

3. **Write** algorithm and C code to add two polynomials represented using linked lists.

4. **Compare** Array implementation vs Linked List implementation of linear data structures.

5. **Implement** operations (insert, delete, search) on:
   - Singly Linked List
   - Doubly Linked List
   - Circular Linked List

6. **Explain** sparse matrix representation. Write algorithm for transpose of sparse matrix.

7. **Write** C program to multiply two polynomials using linked list representation.

8. **Analyze** time and space complexity of various linked list operations.

9. **Explain** time-space trade-off with suitable examples.

10. **Implement** a program to convert array representation of linked list to pointer representation.

---

*End of Unit-1*
