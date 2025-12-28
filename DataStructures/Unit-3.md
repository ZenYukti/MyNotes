# Unit-3: Searching, Hashing & Sorting

---

## 1. Searching: Introduction

### Definition
- **Searching**: Process of finding a particular element in a collection of elements
- **Goal**: Determine if search key exists and locate its position

### Types of Searching
- **Internal Searching**: Data in main memory (arrays, lists)
- **External Searching**: Data in secondary storage (files, databases)

### Performance Metrics
- **Successful Search**: Element found
- **Unsuccessful Search**: Element not found
- **Comparisons**: Number of comparisons needed

---

## 2. Sequential Search (Linear Search)

### Algorithm
```
Algorithm: SequentialSearch
Input: Array arr[n], search key
Output: Index if found, -1 otherwise

1. Start from first element (index 0)
2. Compare each element with key
3. If match found, return index
4. If end reached without match, return -1
```

### Implementation
```c
int sequentialSearch(int arr[], int n, int key) {
    for(int i = 0; i < n; i++) {
        if(arr[i] == key) {
            return i;  // Found at index i
        }
    }
    return -1;  // Not found
}
```

### Example
```
Array: [5, 2, 9, 1, 7, 6]
Search: 7

Comparisons:
arr[0]=5 ≠ 7
arr[1]=2 ≠ 7
arr[2]=9 ≠ 7
arr[3]=1 ≠ 7
arr[4]=7 = 7 ✓ Found at index 4
```

### Analysis
- **Best Case**: O(1) - Element at first position
- **Worst Case**: O(n) - Element at last position or not present
- **Average Case**: O(n/2) ≈ O(n)
- **Space Complexity**: O(1)

### Advantages
- Simple implementation
- Works on unsorted data
- No preprocessing required

### Disadvantages
- Slow for large datasets
- Not efficient for repeated searches

---

## 3. Binary Search

### Prerequisite
- **Array must be sorted** (ascending or descending)

### Algorithm
```
Algorithm: BinarySearch
Input: Sorted array arr[n], search key
Output: Index if found, -1 otherwise

1. Set low = 0, high = n-1
2. While low ≤ high:
   a) mid = (low + high) / 2
   b) If arr[mid] == key:
         return mid
   c) If arr[mid] < key:
         low = mid + 1  (search right half)
   d) Else:
         high = mid - 1  (search left half)
3. Return -1 (not found)
```

### Implementation
```c
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    
    while(low <= high) {
        int mid = low + (high - low) / 2;  // Avoid overflow
        
        if(arr[mid] == key) {
            return mid;
        }
        else if(arr[mid] < key) {
            low = mid + 1;  // Search right
        }
        else {
            high = mid - 1;  // Search left
        }
    }
    
    return -1;
}
```

### Example
```
Array: [1, 3, 5, 7, 9, 11, 13, 15]
Search: 7

Iteration 1: low=0, high=7, mid=3
arr[3]=7 = 7 ✓ Found!

Search: 10

Iteration 1: low=0, high=7, mid=3
arr[3]=7 < 10 → low=4

Iteration 2: low=4, high=7, mid=5
arr[5]=11 > 10 → high=4

Iteration 3: low=4, high=4, mid=4
arr[4]=9 < 10 → low=5

low > high → Not found
```

### Recursive Implementation
```c
int binarySearchRecursive(int arr[], int low, int high, int key) {
    if(low > high) {
        return -1;
    }
    
    int mid = low + (high - low) / 2;
    
    if(arr[mid] == key) {
        return mid;
    }
    else if(arr[mid] < key) {
        return binarySearchRecursive(arr, mid + 1, high, key);
    }
    else {
        return binarySearchRecursive(arr, low, mid - 1, key);
    }
}
```

### Analysis
- **Best Case**: O(1) - Element at middle
- **Worst Case**: O(log n)
- **Average Case**: O(log n)
- **Space Complexity**: 
  - Iterative: O(1)
  - Recursive: O(log n) - recursion stack

### Comparison: Linear vs Binary

| Aspect | Linear Search | Binary Search |
|--------|---------------|---------------|
| **Requirement** | None | Sorted array |
| **Time (Worst)** | O(n) | O(log n) |
| **Best for** | Small/unsorted data | Large sorted data |
| **Implementation** | Simple | Moderate |

---

## 4. Index Sequential Search

### Concept
- **Hybrid approach**: Combine indexing with sequential search
- Divide sorted array into blocks
- Create index table for block starting positions
- Search index, then search within block

### Structure
```
Index Table:
Block 0: 10 (starts at position 0)
Block 1: 40 (starts at position 3)
Block 2: 70 (starts at position 6)

Array: [10, 20, 30 | 40, 50, 60 | 70, 80, 90]
        Block 0    | Block 1    | Block 2
```

### Algorithm
```
Algorithm: IndexSequentialSearch
Input: Sorted array with index, search key
Output: Index if found, -1 otherwise

1. Search index table to find appropriate block
2. Perform sequential search within that block
3. Return index if found, -1 otherwise
```

### Example
```
Search: 50

Step 1: Check index
10 ≤ 50? Yes
40 ≤ 50? Yes
70 ≤ 50? No → Search Block 1

Step 2: Sequential search in Block 1
arr[3]=40 ≠ 50
arr[4]=50 = 50 ✓ Found at index 4
```

### Analysis
- **Time Complexity**: O(√n) - if blocks of size √n
- **Better than**: Sequential search O(n)
- **Worse than**: Binary search O(log n)
- **Advantage**: Works well for disk-based storage

---

## 5. Hashing: Introduction

### Definition
- **Hash Table**: Data structure for fast key-value storage/retrieval
- **Hash Function**: h(key) → index in hash table
- **Goal**: O(1) average time for search, insert, delete

### Hash Function
```
h(key) = key % table_size

Example:
key = 25, table_size = 10
h(25) = 25 % 10 = 5
Store at index 5
```

### Ideal Hash Function Properties
- **Uniform Distribution**: Keys spread evenly
- **Minimal Collisions**: Few keys map to same index
- **Fast Computation**: Quick to calculate
- **Deterministic**: Same key → same hash always

### Common Hash Functions

#### 1. Division Method
```c
int hash(int key, int size) {
    return key % size;
}
// Best: size = prime number
```

#### 2. Multiplication Method
```c
int hash(int key, int size) {
    double A = 0.6180339887;  // (√5 - 1) / 2
    return (int)(size * (key * A - (int)(key * A)));
}
```

#### 3. Mid-Square Method
```
key = 123
key² = 15129
Extract middle digits: 51
h(123) = 51 % table_size
```

#### 4. Folding Method
```
key = 12345678
Split: 123 | 456 | 78
Sum: 123 + 456 + 78 = 657
h(key) = 657 % table_size
```

---

## 6. Collision in Hashing

### Definition
- **Collision**: Two keys hash to same index
- **Example**: h(25) = 5 and h(15) = 5 (when table_size = 10)

### Load Factor
```
Load Factor (α) = n / m

Where:
n = number of keys
m = table size

α < 0.7 → Good performance
α > 0.9 → Many collisions
```

---

## 7. Collision Resolution Techniques

### A. Open Addressing (Closed Hashing)

All elements stored in hash table itself. When collision occurs, probe for next empty slot.

#### 1. Linear Probing
```
h(key, i) = [h(key) + i] % m

Where:
i = 0, 1, 2, 3, ... (probe sequence)
m = table size
```

**Example:**
```
Table size = 10
Insert: 25, 15, 35, 5

h(25) = 25 % 10 = 5
Table[5] = 25

h(15) = 15 % 10 = 5 (collision!)
Try (5+1) % 10 = 6
Table[6] = 15

h(35) = 35 % 10 = 5 (collision!)
Try (5+1) % 10 = 6 (occupied)
Try (5+2) % 10 = 7
Table[7] = 35

Result:
Index: 0  1  2  3  4  5   6   7   8  9
Value: -  -  -  -  -  25  15  35  -  -
```

**Advantages:**
- Simple implementation
- Good cache performance

**Disadvantages:**
- **Primary Clustering**: Consecutive occupied cells
- Performance degrades as table fills

#### 2. Quadratic Probing
```
h(key, i) = [h(key) + c₁·i + c₂·i²] % m

Common: c₁ = c₂ = 1
h(key, i) = [h(key) + i²] % m
```

**Example:**
```
Table size = 10
Insert: 25, 15, 35

h(25) = 5
Table[5] = 25

h(15) = 5 (collision!)
Try (5 + 1²) % 10 = 6
Table[6] = 15

h(35) = 5 (collision!)
Try (5 + 1²) % 10 = 6 (occupied)
Try (5 + 2²) % 10 = 9
Table[9] = 35

Result:
Index: 0  1  2  3  4  5   6   7  8  9
Value: -  -  -  -  -  25  15  -  -  35
```

**Advantages:**
- Reduces primary clustering
- Better distribution

**Disadvantages:**
- **Secondary Clustering**: Keys with same hash follow same probe sequence
- May not probe all positions

#### 3. Double Hashing
```
h(key, i) = [h₁(key) + i·h₂(key)] % m

Where:
h₁(key) = key % m (primary hash)
h₂(key) = 1 + (key % (m-1)) (secondary hash)
```

**Example:**
```
Table size = 10
h₁(key) = key % 10
h₂(key) = 1 + (key % 9)

Insert: 25, 15

h(25) = 25 % 10 = 5
Table[5] = 25

h(15) = 15 % 10 = 5 (collision!)
h₂(15) = 1 + (15 % 9) = 1 + 6 = 7
Try (5 + 1·7) % 10 = 12 % 10 = 2
Table[2] = 15
```

**Advantages:**
- Best open addressing method
- Minimal clustering
- Better distribution

**Disadvantages:**
- More complex
- Two hash functions needed

### B. Chaining (Open Hashing)

Each table slot contains linked list of all keys that hash to that index.

**Structure:**
```
Table[0] → NULL
Table[1] → [11] → [21] → NULL
Table[2] → [2] → NULL
Table[3] → NULL
Table[4] → [14] → [24] → NULL
...
```

**Implementation:**
```c
struct Node {
    int key;
    int value;
    struct Node* next;
};

struct HashTable {
    struct Node** table;
    int size;
};

void insert(struct HashTable* ht, int key, int value) {
    int index = key % ht->size;
    
    // Create new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->key = key;
    newNode->value = value;
    newNode->next = ht->table[index];
    
    // Insert at beginning
    ht->table[index] = newNode;
}

int search(struct HashTable* ht, int key) {
    int index = key % ht->size;
    struct Node* temp = ht->table[index];
    
    while(temp != NULL) {
        if(temp->key == key) {
            return temp->value;
        }
        temp = temp->next;
    }
    
    return -1;  // Not found
}
```

**Example:**
```
Table size = 5
Insert: 10, 22, 31, 4, 15, 28, 17, 88, 59

h(10) = 10 % 5 = 0
h(22) = 22 % 5 = 2
h(31) = 31 % 5 = 1
h(4)  = 4 % 5  = 4
h(15) = 15 % 5 = 0 (collision with 10)
h(28) = 28 % 5 = 3
h(17) = 17 % 5 = 2 (collision with 22)
h(88) = 88 % 5 = 3 (collision with 28)
h(59) = 59 % 5 = 4 (collision with 4)

Result:
Table[0] → [15] → [10] → NULL
Table[1] → [31] → NULL
Table[2] → [17] → [22] → NULL
Table[3] → [88] → [28] → NULL
Table[4] → [59] → [4] → NULL
```

**Advantages:**
- Simple implementation
- No clustering
- Table never "fills up"
- Easy deletion

**Disadvantages:**
- Extra memory for pointers
- Poor cache performance
- Linked list traversal overhead

### Comparison: Open Addressing vs Chaining

| Aspect | Open Addressing | Chaining |
|--------|-----------------|----------|
| **Storage** | All in table | Table + linked lists |
| **Memory** | Fixed | Dynamic |
| **Cache** | Better | Worse |
| **Load Factor** | Must keep < 1 | Can exceed 1 |
| **Deletion** | Complex | Simple |
| **Best for** | Low load factor | High load factor |

---

## 8. Sorting: Introduction

### Definition
- **Sorting**: Arranging elements in specific order (ascending/descending)

### Types of Sorting

#### By Method
- **Comparison-based**: Compare elements (Bubble, Quick, Merge)
- **Non-comparison**: Use key properties (Radix, Counting)

#### By Stability
- **Stable**: Maintains relative order of equal elements
- **Unstable**: May change relative order

#### By Memory
- **In-place**: O(1) extra space
- **Out-of-place**: Requires extra space

### Sorting Algorithm Comparison

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| **Bubble** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Selection** | O(n²) | O(n²) | O(n²) | O(1) | No |
| **Insertion** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| **Radix** | O(d·n) | O(d·n) | O(d·n) | O(n+k) | Yes |

---

## 9. Bubble Sort

### Algorithm
```
Algorithm: BubbleSort
Input: Array arr[n]
Output: Sorted array

1. For i = 0 to n-1:
   a) For j = 0 to n-i-1:
      - If arr[j] > arr[j+1]:
           Swap arr[j] and arr[j+1]
```

### Implementation
```c
void bubbleSort(int arr[], int n) {
    for(int i = 0; i < n-1; i++) {
        int swapped = 0;
        
        for(int j = 0; j < n-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                // Swap
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                swapped = 1;
            }
        }
        
        // If no swap, already sorted
        if(swapped == 0) {
            break;
        }
    }
}
```

### Example
```
Array: [5, 2, 8, 1, 9]

Pass 1: [2, 5, 1, 8, 9] (9 bubbles to end)
Pass 2: [2, 1, 5, 8, 9] (8 in place)
Pass 3: [1, 2, 5, 8, 9] (5 in place)
Pass 4: [1, 2, 5, 8, 9] (no swap, done)

Sorted: [1, 2, 5, 8, 9]
```

### Analysis
- **Best Case**: O(n) - Already sorted (with optimization)
- **Worst Case**: O(n²) - Reverse sorted
- **Space**: O(1) - In-place
- **Stable**: Yes

---

## 10. Selection Sort

### Algorithm
```
Algorithm: SelectionSort
Input: Array arr[n]
Output: Sorted array

1. For i = 0 to n-1:
   a) Find minimum element in arr[i...n-1]
   b) Swap with arr[i]
```

### Implementation
```c
void selectionSort(int arr[], int n) {
    for(int i = 0; i < n-1; i++) {
        int minIdx = i;
        
        // Find minimum in unsorted part
        for(int j = i+1; j < n; j++) {
            if(arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        
        // Swap minimum with first unsorted element
        if(minIdx != i) {
            int temp = arr[i];
            arr[i] = arr[minIdx];
            arr[minIdx] = temp;
        }
    }
}
```

### Example
```
Array: [5, 2, 8, 1, 9]

Pass 1: min=1, swap → [1, 2, 8, 5, 9]
Pass 2: min=2, no swap → [1, 2, 8, 5, 9]
Pass 3: min=5, swap → [1, 2, 5, 8, 9]
Pass 4: min=8, no swap → [1, 2, 5, 8, 9]

Sorted: [1, 2, 5, 8, 9]
```

### Analysis
- **All Cases**: O(n²)
- **Space**: O(1)
- **Stable**: No
- **Min Swaps**: O(n)

---

## 11. Insertion Sort

### Algorithm
```
Algorithm: InsertionSort
Input: Array arr[n]
Output: Sorted array

1. For i = 1 to n-1:
   a) key = arr[i]
   b) j = i - 1
   c) While j ≥ 0 and arr[j] > key:
      - arr[j+1] = arr[j]
      - j = j - 1
   d) arr[j+1] = key
```

### Implementation
```c
void insertionSort(int arr[], int n) {
    for(int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        // Shift elements greater than key
        while(j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        
        // Insert key
        arr[j+1] = key;
    }
}
```

### Example
```
Array: [5, 2, 8, 1, 9]

Pass 1: key=2, insert → [2, 5, 8, 1, 9]
Pass 2: key=8, no shift → [2, 5, 8, 1, 9]
Pass 3: key=1, insert → [1, 2, 5, 8, 9]
Pass 4: key=9, no shift → [1, 2, 5, 8, 9]

Sorted: [1, 2, 5, 8, 9]
```

### Analysis
- **Best Case**: O(n) - Already sorted
- **Worst Case**: O(n²) - Reverse sorted
- **Space**: O(1)
- **Stable**: Yes
- **Good for**: Small datasets, nearly sorted data

---

## 12. Quick Sort

### Algorithm
```
Algorithm: QuickSort
Input: Array arr[low...high]
Output: Sorted array

1. If low < high:
   a) pivot_index = partition(arr, low, high)
   b) QuickSort(arr, low, pivot_index - 1)
   c) QuickSort(arr, pivot_index + 1, high)

partition(arr, low, high):
1. pivot = arr[high]
2. i = low - 1
3. For j = low to high-1:
   a) If arr[j] ≤ pivot:
      - i++
      - Swap arr[i] and arr[j]
4. Swap arr[i+1] and arr[high]
5. Return i+1
```

### Implementation
```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    
    for(int j = low; j < high; j++) {
        if(arr[j] <= pivot) {
            i++;
            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    
    // Place pivot in correct position
    int temp = arr[i+1];
    arr[i+1] = arr[high];
    arr[high] = temp;
    
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if(low < high) {
        int pi = partition(arr, low, high);
        
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

### Example
```
Array: [5, 2, 8, 1, 9], pivot = 9

Partition: [5, 2, 8, 1] | 9 | []
           ↓
          [2, 1] | 5 | [8] | 9
           ↓
          [1] | 2 | [5, 8] | 9
                    ↓
          [1, 2, 5] | 8 | [9]

Sorted: [1, 2, 5, 8, 9]
```

### Analysis
- **Best Case**: O(n log n) - Balanced partitions
- **Worst Case**: O(n²) - Already sorted with bad pivot
- **Average**: O(n log n)
- **Space**: O(log n) - Recursion stack
- **Stable**: No
- **In-place**: Yes

---

## 13. Merge Sort

### Algorithm
```
Algorithm: MergeSort
Input: Array arr[left...right]
Output: Sorted array

1. If left < right:
   a) mid = (left + right) / 2
   b) MergeSort(arr, left, mid)
   c) MergeSort(arr, mid+1, right)
   d) Merge(arr, left, mid, right)

Merge(arr, left, mid, right):
1. Create temp arrays L[left...mid], R[mid+1...right]
2. Merge L and R back into arr[left...right]
```

### Implementation
```c
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    // Create temp arrays
    int L[n1], R[n2];
    
    for(int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for(int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    // Merge
    int i = 0, j = 0, k = left;
    while(i < n1 && j < n2) {
        if(L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }
    
    // Copy remaining
    while(i < n1) arr[k++] = L[i++];
    while(j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int left, int right) {
    if(left < right) {
        int mid = left + (right - left) / 2;
        
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```

### Example
```
Array: [5, 2, 8, 1, 9]

Divide:
[5, 2, 8, 1, 9]
   ↓
[5, 2] [8, 1, 9]
  ↓       ↓
[5][2] [8][1, 9]
           ↓
        [8][1][9]

Merge:
[2, 5] [1, 8, 9]
   ↓
[1, 2, 5, 8, 9]
```

### Analysis
- **All Cases**: O(n log n)
- **Space**: O(n)
- **Stable**: Yes
- **Not in-place**

---

## 14. Heap Sort

### Concept
- Uses binary heap data structure
- **Max Heap**: Parent ≥ children
- **Min Heap**: Parent ≤ children

### Algorithm
```
Algorithm: HeapSort
Input: Array arr[n]
Output: Sorted array

1. Build max heap from array
2. For i = n-1 to 1:
   a) Swap arr[0] with arr[i] (move max to end)
   b) Heapify arr[0...i-1]
```

### Implementation
```c
void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;
    
    if(left < n && arr[left] > arr[largest])
        largest = left;
    
    if(right < n && arr[right] > arr[largest])
        largest = right;
    
    if(largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    // Build max heap
    for(int i = n/2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    
    // Extract elements
    for(int i = n-1; i > 0; i--) {
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        
        heapify(arr, i, 0);
    }
}
```

### Analysis
- **All Cases**: O(n log n)
- **Space**: O(1)
- **Stable**: No
- **In-place**: Yes

---

## 15. Radix Sort

### Concept
- Non-comparison sort
- Process digits from least to most significant
- Uses counting sort as subroutine

### Algorithm
```
Algorithm: RadixSort
Input: Array arr[n]
Output: Sorted array

1. Find maximum number to know digit count
2. For each digit position (1, 10, 100, ...):
   a) Use counting sort on current digit
```

### Implementation
```c
int getMax(int arr[], int n) {
    int max = arr[0];
    for(int i = 1; i < n; i++)
        if(arr[i] > max)
            max = arr[i];
    return max;
}

void countSort(int arr[], int n, int exp) {
    int output[n];
    int count[10] = {0};
    
    // Count occurrences
    for(int i = 0; i < n; i++)
        count[(arr[i]/exp) % 10]++;
    
    // Cumulative count
    for(int i = 1; i < 10; i++)
        count[i] += count[i-1];
    
    // Build output
    for(int i = n-1; i >= 0; i--) {
        output[count[(arr[i]/exp) % 10] - 1] = arr[i];
        count[(arr[i]/exp) % 10]--;
    }
    
    // Copy to original
    for(int i = 0; i < n; i++)
        arr[i] = output[i];
}

void radixSort(int arr[], int n) {
    int max = getMax(arr, n);
    
    for(int exp = 1; max/exp > 0; exp *= 10) {
        countSort(arr, n, exp);
    }
}
```

### Example
```
Array: [170, 45, 75, 90, 802, 24, 2, 66]

Pass 1 (1s place): [170, 90, 802, 2, 24, 45, 75, 66]
Pass 2 (10s place): [802, 2, 24, 45, 66, 170, 75, 90]
Pass 3 (100s place): [2, 24, 45, 66, 75, 90, 170, 802]

Sorted: [2, 24, 45, 66, 75, 90, 170, 802]
```

### Analysis
- **Time**: O(d·(n+k)) where d=digits, k=range
- **Space**: O(n+k)
- **Stable**: Yes
- **Best for**: Integers with fixed digits

---

## 🚀 Quick Reference Summary

### Search Complexity

| Algorithm | Best | Average | Worst | Requirement |
|-----------|------|---------|-------|-------------|
| **Linear** | O(1) | O(n) | O(n) | None |
| **Binary** | O(1) | O(log n) | O(log n) | Sorted |
| **Hashing** | O(1) | O(1) | O(n) | Hash table |

### Sort Selection Guide

**Small Data (n < 50):**
- Insertion Sort

**Nearly Sorted:**
- Insertion Sort, Bubble Sort

**Large Data, Memory Limited:**
- Heap Sort, Quick Sort

**Large Data, Stable Required:**
- Merge Sort

**Integer Data with Fixed Digits:**
- Radix Sort

**General Purpose:**
- Quick Sort (average), Merge Sort (guaranteed)

---

## 📝 Exam Important Questions

1. **Compare** linear search and binary search with example.

2. **Explain** collision resolution techniques: Linear Probing, Quadratic Probing, Double Hashing, and Chaining.

3. **Write** algorithm and C code for Quick Sort. Trace for array [5, 2, 8, 1, 9].

4. **Explain** Merge Sort with example. Why is it better than Quick Sort in worst case?

5. **Differentiate** between stable and unstable sorting. Give examples.

6. **Implement** hash table using chaining. Show insertion and search operations.

7. **Explain** Heap Sort. Build max heap for [4, 10, 3, 5, 1] and sort.

8. **Compare** all sorting algorithms with time/space complexity table.

9. **Explain** Radix Sort with example for [170, 45, 75, 90, 802, 24].

10. **Analyze** best, average, and worst case for Insertion Sort.

---

*End of Unit-3*
