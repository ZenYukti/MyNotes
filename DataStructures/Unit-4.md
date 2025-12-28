# Unit-4: Trees

---

## 1. Tree: Basic Terminology

### Definition
- **Tree**: Hierarchical non-linear data structure
- **Root**: Topmost node (no parent)
- **Node**: Contains data and references to children
- **Edge**: Connection between two nodes

### Tree Structure
```
       A (Root)
      /|\
     / | \
    B  C  D
   /\    /|\
  E  F  G H I (Leaves)
```

### Key Terms

#### Node Properties
- **Parent**: Node directly above
- **Child**: Node directly below
- **Siblings**: Nodes with same parent
- **Leaf/Terminal**: Node with no children
- **Internal**: Node with at least one child

#### Tree Properties
- **Degree**: Maximum number of children any node has
- **Level**: Distance from root (root = level 0)
- **Height**: Maximum level in tree
- **Depth of Node**: Length of path from root to node
- **Path**: Sequence of nodes connected by edges

#### Subtree
- **Subtree**: Tree formed by node and its descendants

### Example
```
       A          Level 0 (Root)
      /|\
     B C D        Level 1
    /\   /|\
   E  F G H I     Level 2 (Leaves)

- Root: A
- Parent of E: B
- Children of A: B, C, D
- Siblings of B: C, D
- Leaves: E, F, G, H, I
- Degree of tree: 3 (node D)
- Height: 2
- Depth of E: 2
```

---

## 2. Binary Tree

### Definition
- **Binary Tree**: Tree where each node has **at most 2 children**
- **Left Child** and **Right Child**

### Structure
```
       10
      /  \
     5    15
    / \     \
   3   7    20
```

### Types of Binary Trees

#### 1. Strictly Binary Tree
- Every node has **exactly 0 or 2 children**
- No node with only one child

```
       A
      / \
     B   C
    / \
   D   E

✓ Strictly Binary (all nodes have 0 or 2 children)
```

#### 2. Complete Binary Tree
- All levels **completely filled** except possibly last
- Last level filled **left to right**

```
       1
      / \
     2   3
    / \  /
   4  5 6

✓ Complete Binary Tree
```

```
       1
      / \
     2   3
    /   / \
   4   5   6

✗ NOT Complete (level 2 not filled left to right)
```

#### 3. Full Binary Tree
- All internal nodes have **exactly 2 children**
- All leaves at **same level**

```
       1
      / \
     2   3
    /\  /\
   4 5 6 7

✓ Full Binary Tree
```

#### 4. Perfect Binary Tree
- All internal nodes have 2 children
- All leaves at same level
- Number of nodes = 2^(h+1) - 1

```
       1
      / \
     2   3
    /\  /\
   4 5 6 7

✓ Perfect Binary Tree (height=2, nodes=7=2³-1)
```

### Properties of Binary Trees

**If height = h:**
- **Min nodes**: h + 1 (skewed tree)
- **Max nodes**: 2^(h+1) - 1 (perfect tree)
- **Max nodes at level i**: 2^i

**If n = total nodes:**
- **Min height**: ⌈log₂(n+1)⌉ - 1
- **Max height**: n - 1 (skewed)

**For Complete Binary Tree:**
- If n nodes, height = ⌊log₂n⌋

---

## 3. Binary Tree Representation

### A. Array Representation

#### Rules
- Root at index 0 (or 1)
- For node at index i:
  - **Left child**: 2i + 1 (or 2i if 1-indexed)
  - **Right child**: 2i + 2 (or 2i+1 if 1-indexed)
  - **Parent**: ⌊(i-1)/2⌋ (or ⌊i/2⌋ if 1-indexed)

#### Example
```
Tree:
       A(0)
      /    \
    B(1)   C(2)
   /  \    /
 D(3) E(4) F(5)

Array (0-indexed):
Index: 0  1  2  3  4  5
Value: A  B  C  D  E  F

Relations:
- Parent of E(4): ⌊(4-1)/2⌋ = 1 (B)
- Left child of B(1): 2(1)+1 = 3 (D)
- Right child of B(1): 2(1)+2 = 4 (E)
```

#### Advantages
- Simple implementation
- Fast access to parent/children
- No extra space for pointers

#### Disadvantages
- **Space wastage** for skewed trees
- **Fixed size**
- Insertion/deletion difficult

### B. Linked List Representation

#### Node Structure
```c
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};
```

#### Example
```
Tree:
       10
      /  \
     5    15
    / \
   3   7

Memory:
Node(10): data=10, left=&Node(5), right=&Node(15)
Node(5):  data=5, left=&Node(3), right=&Node(7)
Node(15): data=15, left=NULL, right=NULL
Node(3):  data=3, left=NULL, right=NULL
Node(7):  data=7, left=NULL, right=NULL
```

#### Advantages
- Dynamic size
- No space wastage
- Easy insertion/deletion

#### Disadvantages
- Extra memory for pointers
- No direct parent access

---

## 4. Tree Traversal Algorithms

### Traversal Types

#### 1. Inorder Traversal (LNR)
```
Algorithm:
1. Traverse left subtree
2. Visit node
3. Traverse right subtree
```

**Implementation:**
```c
void inorder(struct Node* root) {
    if(root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}
```

**Dry Run: Inorder Traversal**
```
Tree:
       1
      / \
     2   3
    / \
   4   5

Recursive Calls:
─────────────────
inorder(1):
  │
  ├─ inorder(2):           [Visit Left]
  │    │
  │    ├─ inorder(4):      [Visit Left]
  │    │    ├─ inorder(NULL)
  │    │    ├─ print(4)    ← Output: 4
  │    │    └─ inorder(NULL)
  │    │
  │    ├─ print(2)         ← Output: 2
  │    │
  │    └─ inorder(5):      [Visit Right]
  │         ├─ inorder(NULL)
  │         ├─ print(5)    ← Output: 5
  │         └─ inorder(NULL)
  │
  ├─ print(1)              ← Output: 1
  │
  └─ inorder(3):           [Visit Right]
       ├─ inorder(NULL)
       ├─ print(3)         ← Output: 3
       └─ inorder(NULL)

Output Sequence: 4 2 5 1 3

Stack Visualization:
────────────────────
|  1  |     |  1  |     |  1  |     |  1  |     |  1  |
|  2  | →   |  2  | →   |  2  | →   |  2  | →   |     |
|  4  |     |     |     |  5  |     |     |     |  3  |
  ↓           ↓           ↓           ↓           ↓
Print 4    Print 2    Print 5    Print 1    Print 3
```

#### 2. Preorder Traversal (NLR)
```
Algorithm:
1. Visit node
2. Traverse left subtree
3. Traverse right subtree
```

**Implementation:**
```c
void preorder(struct Node* root) {
    if(root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}
```

**Dry Run: Preorder Traversal**
```
Tree:
       1
      / \
     2   3
    / \
   4   5

Recursive Calls:
─────────────────
preorder(1):
  │
  ├─ print(1)              ← Output: 1
  │
  ├─ preorder(2):          [Visit Left]
  │    │
  │    ├─ print(2)         ← Output: 2
  │    │
  │    ├─ preorder(4):     [Visit Left]
  │    │    ├─ print(4)   ← Output: 4
  │    │    ├─ preorder(NULL)
  │    │    └─ preorder(NULL)
  │    │
  │    └─ preorder(5):     [Visit Right]
  │         ├─ print(5)    ← Output: 5
  │         ├─ preorder(NULL)
  │         └─ preorder(NULL)
  │
  └─ preorder(3):          [Visit Right]
       ├─ print(3)         ← Output: 3
       ├─ preorder(NULL)
       └─ preorder(NULL)

Output Sequence: 1 2 4 5 3

Execution Order:
────────────────
Visit Order: Root → Left → Right

    1 ← Start (print immediately)
   ↙ ↘
  2   3
 ↙ ↘
4   5

Sequence:
1. Visit 1 → Print 1
2. Go left to 2 → Print 2
3. Go left to 4 → Print 4
4. Back to 2, go right to 5 → Print 5
5. Back to 1, go right to 3 → Print 3

Result: 1 2 4 5 3
```

#### 3. Postorder Traversal (LRN)
```
Algorithm:
1. Traverse left subtree
2. Traverse right subtree
3. Visit node
```

**Implementation:**
```c
void postorder(struct Node* root) {
    if(root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}
```

**Dry Run: Postorder Traversal**
```
Tree:
       1
      / \
     2   3
    / \
   4   5

Recursive Calls:
─────────────────
postorder(1):
  │
  ├─ postorder(2):         [Visit Left]
  │    │
  │    ├─ postorder(4):    [Visit Left]
  │    │    ├─ postorder(NULL)
  │    │    ├─ postorder(NULL)
  │    │    └─ print(4)    ← Output: 4
  │    │
  │    ├─ postorder(5):    [Visit Right]
  │    │    ├─ postorder(NULL)
  │    │    ├─ postorder(NULL)
  │    │    └─ print(5)    ← Output: 5
  │    │
  │    └─ print(2)         ← Output: 2
  │
  ├─ postorder(3):         [Visit Right]
  │    ├─ postorder(NULL)
  │    ├─ postorder(NULL)
  │    └─ print(3)         ← Output: 3
  │
  └─ print(1)              ← Output: 1

Output Sequence: 4 5 2 3 1

Execution Order:
────────────────
Visit Order: Left → Right → Root

    1 ← Last (print at end)
   ↙ ↘
  2   3
 ↙ ↘
4   5

Sequence:
1. Go left to 2, then left to 4 → Print 4 (leaf)
2. Back to 2, go right to 5 → Print 5 (leaf)
3. Both children of 2 done → Print 2
4. Back to 1, go right to 3 → Print 3 (leaf)
5. Both children of 1 done → Print 1 (root)

Result: 4 5 2 3 1 (Children before parent)
```

### Traversal Applications

| Traversal | Use Case |
|-----------|----------|
| **Inorder** | Get sorted sequence in BST |
| **Preorder** | Create copy of tree, prefix expression |
| **Postorder** | Delete tree, postfix expression |

---

## 5. Constructing Binary Tree from Traversals

### Rules
- **Inorder + Preorder** → Unique tree
- **Inorder + Postorder** → Unique tree
- **Preorder + Postorder** → Not always unique

### From Inorder and Preorder

**Algorithm:**
```
1. First element of Preorder is root
2. Find root in Inorder
3. Elements left of root in Inorder = left subtree
4. Elements right of root in Inorder = right subtree
5. Recursively build left and right subtrees
```

**Dry Run: Tree Construction from Traversals**
```
Given:
Inorder:   D B E A F C
Preorder:  A B D E C F

┌─────────────────────────────────────────┐
│ Step 1: Find Root                       │
└─────────────────────────────────────────┘
Preorder[0] = A → Root = A

       A

┌─────────────────────────────────────────┐
│ Step 2: Split Inorder at Root 'A'      │
└─────────────────────────────────────────┘
Inorder: [D B E] | A | [F C]
         ───────   ↑   ─────
         Left      Root Right

Preorder remaining: B D E C F

┌─────────────────────────────────────────┐
│ Step 3: Build Left Subtree [D B E]     │
└─────────────────────────────────────────┘
Next in Preorder = B → Left child of A

Inorder: [D] | B | [E]
          ↓    ↑    ↓
        Left  Root Right

       A
      /
     B

┌─────────────────────────────────────────┐
│ Step 4: Build B's children              │
└─────────────────────────────────────────┘
Next in Preorder = D → Left child of B
Next in Preorder = E → Right child of B

       A
      /
     B
    / \
   D   E

┌─────────────────────────────────────────┐
│ Step 5: Build Right Subtree [F C]      │
└─────────────────────────────────────────┘
Next in Preorder = C → Right child of A

Inorder: [F] | C |
          ↓    ↑
        Left  Root

       A
      / \
     B   C
    / \  /
   D  E F

┌─────────────────────────────────────────┐
│ Final Tree                              │
└─────────────────────────────────────────┘
       A
      / \
     B   C
    / \  /
   D  E F

Verification:
─────────────
Inorder:   D B E A F C ✓
Preorder:  A B D E C F ✓
Postorder: D E B F C A
```

---

## 6. Binary Search Tree (BST)

### Definition
- Binary tree with property:
  - **Left subtree** contains values **< root**
  - **Right subtree** contains values **> root**
  - Both subtrees are also BSTs

### Example
```
Valid BST:
       50
      /  \
    30    70
   / \   / \
  20 40 60 80

Invalid (40 > 30 but < 50, wrong position):
       50
      /  \
    30    70
   / \
  20 40
      \
      35
```

### Operations on BST

#### 1. Search
```c
struct Node* search(struct Node* root, int key) {
    if(root == NULL || root->data == key) {
        return root;
    }
    
    if(key < root->data) {
        return search(root->left, key);
    }
    
    return search(root->right, key);
}

// Time: O(h) where h = height
// Best: O(log n), Worst: O(n) for skewed
```

#### 2. Insertion
```c
struct Node* insert(struct Node* root, int key) {
    if(root == NULL) {
        struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
        newNode->data = key;
        newNode->left = newNode->right = NULL;
        return newNode;
    }
    
    if(key < root->data) {
        root->left = insert(root->left, key);
    }
    else if(key > root->data) {
        root->right = insert(root->right, key);
    }
    
    return root;
}

// Time: O(h)
```

**Dry Run: BST Insertion**
```
Insert sequence: 50, 30, 70, 20, 40, 25

Step 1: Insert 50
       50 (root)

Step 2: Insert 30
       30 < 50, go left
       
       50
      /
    30

Step 3: Insert 70
       70 > 50, go right
       
       50
      /  \
    30    70

Step 4: Insert 20
       20 < 50, go left
       20 < 30, go left
       
       50
      /  \
    30    70
   /
  20

Step 5: Insert 40
       40 < 50, go left
       40 > 30, go right
       
       50
      /  \
    30    70
   / \
  20 40

Step 6: Insert 25
       25 < 50, go left
       25 < 30, go left
       25 > 20, go right
       
       50
      /  \
    30    70
   / \
  20 40
    \
    25

Final BST - Inorder: 20 25 30 40 50 70 ✓
```

#### 3. Deletion

**Cases:**
1. **Node is leaf**: Simply remove
2. **Node has one child**: Replace with child
3. **Node has two children**: Replace with inorder successor/predecessor

**Dry Run: BST Deletion**
```
Initial BST:
       50
      /  \
    30    70
   / \   / \
  20 40 60 80

Case 1: Delete 20 (Leaf node)
───────────────────────────────
       50
      /  \
    30    70
     \   / \
     40 60 80

Case 2: Delete 30 (One child: 40)
──────────────────────────────────
       50
      /  \
    40    70
         / \
        60 80

Case 3: Delete 50 (Two children)
─────────────────────────────────
Find inorder successor of 50:
- Go right: 70
- Go leftmost: 60

Step 1: Replace 50 with 60
       60
      /  \
    40    70
           \
           80

Step 2: Delete original 60 node
       60
      /  \
    40    70
           \
           80

Alternative: Delete 70 (Two children)
──────────────────────────────────────
Original:
       50
      /  \
    30    70
   / \   / \
  20 40 60 80

Inorder successor of 70 = 80

       50
      /  \
    30    80
   / \   /
  20 40 60

Verify inorder: 20 30 40 50 60 80 ✓
```

```c
struct Node* findMin(struct Node* root) {
    while(root->left != NULL) {
        root = root->left;
    }
    return root;
}

struct Node* deleteNode(struct Node* root, int key) {
    if(root == NULL) return root;
    
    if(key < root->data) {
        root->left = deleteNode(root->left, key);
    }
    else if(key > root->data) {
        root->right = deleteNode(root->right, key);
    }
    else {
        // Node found
        
        // Case 1: Leaf node
        if(root->left == NULL && root->right == NULL) {
            free(root);
            return NULL;
        }
        
        // Case 2: One child
        if(root->left == NULL) {
            struct Node* temp = root->right;
            free(root);
            return temp;
        }
        if(root->right == NULL) {
            struct Node* temp = root->left;
            free(root);
            return temp;
        }
        
        // Case 3: Two children
        struct Node* temp = findMin(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    
    return root;
}
```

---

## 7. Extended Binary Tree

### Definition
- Binary tree where all empty subtrees replaced with **external nodes** (⊡)
- Original nodes called **internal nodes** (○)

### Example
```
Original Tree:
       A
      / \
     B   C
    /
   D

Extended Tree:
       A
      / \
     B   C
    /\  /\
   D ⊡ ⊡ ⊡
  /\
 ⊡ ⊡

Internal nodes (○): A, B, C, D
External nodes (⊡): 5 nodes
```

### Properties
- If n = internal nodes, external nodes = n + 1
- Used in expression trees, Huffman coding

---

## 8. Threaded Binary Tree

### Concept
- Utilize NULL pointers in binary tree
- **Right NULL** → Points to inorder successor
- **Left NULL** → Points to inorder predecessor

### Types

#### 1. Single Threaded
- Only right NULL pointers threaded

#### 2. Double Threaded
- Both left and right NULL pointers threaded

### Node Structure
```c
struct ThreadedNode {
    int data;
    struct ThreadedNode* left;
    struct ThreadedNode* right;
    int leftThread;   // 1 if left is thread
    int rightThread;  // 1 if right is thread
};
```

### Example
```
Regular Tree:
       A
      / \
     B   C
    /
   D

Threaded Tree (right threaded):
       A
      / \
     B   C
    /↗
   D

Threads:
- D.right → B (inorder successor)
- B.right → A (inorder successor)
- C.right → NULL (no successor)
```

### Advantages
- **Faster traversal** - No recursion/stack needed
- **Efficient** - Utilizes NULL pointers
- **Space efficient** - No extra space for stack

### Inorder Traversal (Threaded)
```c
void inorderThreaded(struct ThreadedNode* root) {
    struct ThreadedNode* curr = leftmost(root);
    
    while(curr != NULL) {
        printf("%d ", curr->data);
        
        if(curr->rightThread) {
            curr = curr->right;
        }
        else {
            curr = leftmost(curr->right);
        }
    }
}

struct ThreadedNode* leftmost(struct ThreadedNode* node) {
    if(node == NULL) return NULL;
    
    while(node->left != NULL && !node->leftThread) {
        node = node->left;
    }
    return node;
}
```

### Dry Run: Threaded Tree Traversal
```
Threaded Tree:
       20
      /  \
    10    30
   /  ↗  ↗  \
  5        40

Threads:
5.right → 10
10.right → 20
30.right → 40

Step 1: curr = leftmost(20) = 5
        Print: 5
        5.rightThread = true, curr = 5.right = 10

Step 2: Print: 10
        10.rightThread = true, curr = 10.right = 20

Step 3: Print: 20
        20.rightThread = false
        curr = leftmost(20.right) = leftmost(30) = 30

Step 4: Print: 30
        30.rightThread = true, curr = 30.right = 40

Step 5: Print: 40
        40.right = NULL, curr = NULL

Output: 5 10 20 30 40
```

---

## 9. Huffman Coding

### Concept
- **Data compression** technique
- **Variable-length codes** for characters
- Frequent characters get **shorter codes**

### Algorithm
```
Algorithm: HuffmanCoding
Input: Characters with frequencies
Output: Huffman tree

1. Create leaf node for each character
2. Build min heap of all nodes
3. While heap has more than one node:
   a) Extract two minimum frequency nodes
   b) Create new internal node with frequency = sum
   c) Left child = first min, Right child = second min
   d) Insert new node into heap
4. Remaining node is root
```

### Dry Run: Huffman Coding Algorithm
```
Input:
Characters: A    B    C    D    E
Frequency:  5    9    12   13   16

┌────────────────────────────────────────────┐
│ Step 1: Create leaf nodes                  │
└────────────────────────────────────────────┘
Min Heap: [A:5] [B:9] [C:12] [D:13] [E:16]
          ─────────────────────────────────
           Sort by frequency (min heap)

┌────────────────────────────────────────────┐
│ Iteration 1: Extract 2 minimum             │
└────────────────────────────────────────────┘
Extract: A(5), B(9)
Combine: New node = 5 + 9 = 14

    (14)
    / \
   A:5 B:9

Heap: [C:12] [D:13] [(AB):14] [E:16]

┌────────────────────────────────────────────┐
│ Iteration 2: Extract 2 minimum             │
└────────────────────────────────────────────┘
Extract: C(12), D(13)
Combine: New node = 12 + 13 = 25

    (25)
    / \
  C:12 D:13

Heap: [(AB):14] [E:16] [(CD):25]

┌────────────────────────────────────────────┐
│ Iteration 3: Extract 2 minimum             │
└────────────────────────────────────────────┘
Extract: (AB):14, E:16
Combine: New node = 14 + 16 = 30

      (30)
      / \
   (14)  E:16
   / \
  A:5 B:9

Heap: [(CD):25] [(ABE):30]

┌────────────────────────────────────────────┐
│ Iteration 4: Extract 2 minimum (Final)     │
└────────────────────────────────────────────┘
Extract: (CD):25, (ABE):30
Combine: Root = 25 + 30 = 55

         (55)
        /    \
     (25)    (30)
     / \     / \
   C:12 D:13 (14) E:16
            / \
          A:5 B:9

Heap: [Root:55] ← Done!

┌────────────────────────────────────────────┐
│ Assign Codes (Left=0, Right=1)            │
└────────────────────────────────────────────┘
         (55)
        /    \
      0/      \1
     (25)    (30)
     / \     / \
   0/  1\  0/  1\
   C   D  (14)  E
          / \
        0/  1\
        A    B

Huffman Codes:
──────────────
C: 00      (Path: root→left→left)
D: 01      (Path: root→left→right)
A: 100     (Path: root→right→left→left)
B: 101     (Path: root→right→left→right)
E: 11      (Path: root→right→right)

┌────────────────────────────────────────────┐
│ Encoding Example                           │
└────────────────────────────────────────────┘
Text: "ABCDE"
Encoded: 100 101 00 01 11
Total bits: 13 bits

Fixed-length: 3 bits/char × 5 = 15 bits
Compression: 13/15 = 86.7%

Decoding: 10010100 0111
          100 101 00 01 11
          A   B   C  D  E  ✓
```

### Implementation
```c
struct MinHeapNode {
    char data;
    int freq;
    struct MinHeapNode *left, *right;
};

struct MinHeapNode* buildHuffmanTree(char data[], int freq[], int size) {
    struct MinHeapNode *left, *right, *top;
    struct MinHeap* minHeap = createAndBuildMinHeap(data, freq, size);
    
    while(!isSizeOne(minHeap)) {
        left = extractMin(minHeap);
        right = extractMin(minHeap);
        
        top = newNode('$', left->freq + right->freq);
        top->left = left;
        top->right = right;
        
        insertMinHeap(minHeap, top);
    }
    
    return extractMin(minHeap);
}
```

### Advantages
- Optimal prefix code
- No ambiguity in decoding
- Good compression ratio

---

## 10. AVL Tree

### Definition
- **Self-balancing** Binary Search Tree
- **Balance Factor** = height(left) - height(right)
- Balance factor must be **-1, 0, or +1** for all nodes

### Example
```
Valid AVL Tree:
       30 (BF=0)
      /  \
    20   40 (BF=-1, 0, +1 only)
   /    / \
  10   35 50

Invalid (node 30 has BF=2):
       30
      /
    20
   /
  10
```

### Rotations

#### Dry Run: AVL Tree Rotations

**1. Right Rotation (LL Case)**
```
Scenario: Insert 10, 20, 30 (causes right rotation)

Step 1: Insert 30
   30 (BF=0)

Step 2: Insert 20
   30 (BF=1)  ← Left heavy
   /
  20 (BF=0)

Step 3: Insert 10
   30 (BF=2)  ← IMBALANCE! (BF > 1)
   /
  20 (BF=1)
  /
 10 (BF=0)

LL Case Detected → Right Rotation

Rotation Process:
─────────────────
    30            20
    /      →     /  \
   20          10    30
   /
  10

After Rotation:
      20 (BF=0)
     /  \
   10    30
  (BF=0)(BF=0)

All nodes balanced! ✓
```

**2. Left Rotation (RR Case)**
```
Scenario: Insert 10, 20, 30

Step 1: Insert 10
   10 (BF=0)

Step 2: Insert 20
   10 (BF=-1)  ← Right heavy
    \
    20 (BF=0)

Step 3: Insert 30
   10 (BF=-2)  ← IMBALANCE! (BF < -1)
    \
    20 (BF=-1)
     \
     30 (BF=0)

RR Case Detected → Left Rotation

Rotation Process:
─────────────────
  10              20
   \      →      /  \
   20          10    30
    \
    30

After Rotation:
      20 (BF=0)
     /  \
   10    30
  (BF=0)(BF=0)

All nodes balanced! ✓
```

**3. Left-Right Rotation (LR Case)**
```
Scenario: Insert 30, 10, 20

Step 1: Insert 30
   30 (BF=0)

Step 2: Insert 10
   30 (BF=1)
   /
  10 (BF=0)

Step 3: Insert 20
   30 (BF=2)  ← IMBALANCE!
   /
  10 (BF=-1) ← Right heavy child
   \
   20 (BF=0)

LR Case: Left child is right heavy

Two Rotations Required:
───────────────────────

Rotation 1: Left rotate on 10
   30              30
   /               /
  10       →     20
   \             /
   20          10

Rotation 2: Right rotate on 30
   30              20
   /       →      /  \
  20            10    30
  /
 10

Final Tree:
      20 (BF=0)
     /  \
   10    30
  (BF=0)(BF=0)

All nodes balanced! ✓
```

**4. Right-Left Rotation (RL Case)**
```
Scenario: Insert 10, 30, 20

Step 1: Insert 10
   10 (BF=0)

Step 2: Insert 30
   10 (BF=-1)
    \
    30 (BF=0)

Step 3: Insert 20
   10 (BF=-2)  ← IMBALANCE!
    \
    30 (BF=1)  ← Left heavy child
    /
   20 (BF=0)

RL Case: Right child is left heavy

Two Rotations Required:
───────────────────────

Rotation 1: Right rotate on 30
  10              10
   \               \
   30      →       20
   /                 \
  20                 30

Rotation 2: Left rotate on 10
  10              20
   \       →     /  \
   20          10    30
    \
    30

Final Tree:
      20 (BF=0)
     /  \
   10    30
  (BF=0)(BF=0)

All nodes balanced! ✓
```

**Complete AVL Insertion Example**
```
Insert sequence: 50, 25, 75, 10, 30, 60, 80, 5, 15, 27, 35

Step 1-3: Insert 50, 25, 75
      50
     /  \
   25    75

Step 4-5: Insert 10, 30
      50
     /  \
   25    75
   / \
  10 30
**Dry Run: Max Heap Insertion**
```
Insert sequence: 50, 30, 40, 10, 20, 60

Step 1: Insert 50
───────────────────
Array: [50]
Tree:   50

Step 2: Insert 30
───────────────────
Array: [50, 30]

Tree:   50
       /
      30

Check: 30 < 50 ✓ (No swap needed)
**Dry Run: Extract Max from Heap**
```
Initial Max Heap:
       90
       /  \
      80  70
     / \  / \
    50 40 30 60

Array: [90, 80, 70, 50, 40, 30, 60]
Index:   0   1   2   3   4   5   6

┌────────────────────────────────────────┐
│ Extract Max Operation                  │
└────────────────────────────────────────┘

Step 1: Save root value
───────────────────────
max = 90

Step 2: Replace root with last element
───────────────────────────────────────
Array: [60, 80, 70, 50, 40, 30]
                 ↑
           Last element moved to root

Tree:  60
       /  \
      80  70
     / \  /
    50 40 30

⚠️ Heap property violated! (60 < 80)

Step 3: Heapify Down
────────────────────

Iteration 1:
───────────
i = 0 (60)
left = 2*0+1 = 1 (80)
right = 2*0+2 = 2 (70)

Compare:
60 vs 80 vs 70
Largest = 80 (left child)

Swap 60 ↔ 80:

Array: [80, 60, 70, 50, 40, 30]

Tree:  80
       /  \
      60  70
     / \  /
    50 40 30

Iteration 2:
───────────
i = 1 (60)
left = 2*1+1 = 3 (50)
right = 2*1+2 = 4 (40)

Compare:
60 vs 50 vs 40
Largest = 60 (parent)

✓ Heap property satisfied!
Stop heapify.

Final Heap:
       80
       /  \
      60  70
     / \  /
    50 40 30

Array: [80, 60, 70, 50, 40, 30]

Return: 90 (extracted max)

┌────────────────────────────────────────┐
│ Extract Max Again                      │
└────────────────────────────────────────┘

Step 1: max = 80

Step 2: Replace root with last (30)
Array: [30, 60, 70, 50, 40]

Tree:  30
       /  \
      60  70
     / \
    50 40

Step 3: Heapify Down

Iteration 1:
Compare: 30 vs 60 vs 70
Largest = 70
Swap 30 ↔ 70

Tree:  70
       /  \
      60  30
     / \
    50 40

Iteration 2:
Compare: 30 vs NULL vs NULL
No children, stop.

Final: [70, 60, 30, 50, 40]

Tree:  70
       /  \
      60  30
     / \
    50 40

Return: 80
```


Step 3: Insert 40
───────────────────
Array: [50, 30, 40]

Tree:   50
       /  \
      30  40

Check: 40 < 50 ✓ (No swap needed)

Step 4: Insert 10
───────────────────
Array: [50, 30, 40, 10]

Tree:   50
       /  \
      30  40
     /
    10

Check: 10 < 30 ✓ (No swap needed)

Step 5: Insert 20
───────────────────
Array: [50, 30, 40, 10, 20]

Tree:   50
       /  \
      30  40
     / \
    10 20

Check: 20 < 30 ✓ (No swap needed)

Step 6: Insert 60
───────────────────
Array: [50, 30, 40, 10, 20, 60]

Tree:   50
       /  \
      30  40
     / \  /
    10 20 60

Heapify Up Process:
──────────────────
Position: i = 5 (60)
Parent: ⌊(5-1)/2⌋ = 2 (40)

Compare: 60 > 40 → Swap!

Array: [50, 30, 60, 10, 20, 40]
Tree:   50
       /  \
      30  60  ← Swapped
     / \  /
    10 20 40

Position: i = 2 (60)
Parent: ⌊(2-1)/2⌋ = 0 (50)

Compare: 60 > 50 → Swap!

Array: [60, 30, 50, 10, 20, 40]
Final Tree:
       60   ← Root (max element)
       /  \
      30  50
     / \  /
    10 20 40

Position: i = 0 (root) → Stop

Max Heap Property Satisfied! ✓
Parent ≥ Children for all nodes
```


Step 6-7: Insert 60, 80
      50
     /  \
   25    75
   / \   / \
  10 30 60 80

Step 8: Insert 5
      50
     /  \
   25    75
   / \   / \
  10 30 60 80
  /
 5
(Balanced, BF ≤ 1)

Step 9: Insert 15
      50 (BF=1)
     /  \
   25    75
   / \   / \
  10 30 60 80
  / \
 5  15

Step 10: Insert 27 (Causes LR imbalance at 25)
      50 (BF=2)  ← Imbalance!
     /  \
   25    75
   / \   / \
  10 30 60 80
  / \  /
 5 15 27

Perform LR rotation on subtree rooted at 25:
After rotation:
      50
     /  \
   25    75
   / \   / \
  10 27 60 80
  / \ \
 5 15 30

(Continue building tree...)

Final Balanced AVL Tree maintained throughout!
```

### Insertion
```c
struct AVLNode* insert(struct AVLNode* node, int key) {
    // Standard BST insertion
    if(node == NULL)
        return newNode(key);
    
    if(key < node->data)
        node->left = insert(node->left, key);
    else if(key > node->data)
        node->right = insert(node->right, key);
    else
        return node;
    
    // Update height
    node->height = 1 + max(height(node->left), height(node->right));
    
    // Get balance factor
    int balance = getBalance(node);
    
    // LL Case
    if(balance > 1 && key < node->left->data)
        return rightRotate(node);
    
    // RR Case
    if(balance < -1 && key > node->right->data)
        return leftRotate(node);
    
    // LR Case
    if(balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }
    
    // RL Case
    if(balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }
    
    return node;
}
```

### Analysis
- **Search**: O(log n)
- **Insert**: O(log n)
- **Delete**: O(log n)
- **Space**: O(n)

---

## 11. B-Tree

### Definition
- Self-balancing search tree
- **Multi-way** tree (more than 2 children)
- Optimized for systems that read/write large blocks of data (databases, file systems)

### Properties (B-Tree of order m)
1. Every node has at most **m children**
2. Every non-leaf node (except root) has at least **⌈m/2⌉ children**
3. Root has at least **2 children** (if not leaf)
4. All leaves at **same level**
5. Non-leaf node with k children contains **k-1 keys**

### Example (B-Tree of order 3)
```
        [20]
       /    \
   [10]      [30, 40]
   /  \      /   |   \
 [5] [15]  [25] [35] [45]

Properties:
- Max children per node: 3
- Min children (non-root): ⌈3/2⌉ = 2
- Max keys per node: 2
- Min keys per node: 1
```

### Operations

#### Search
- Similar to BST but with multiple keys per node
- Search within node, then follow child pointer

#### Insertion
1. Find appropriate leaf node
2. If leaf not full, insert key
3. If leaf full, **split** into two nodes
4. Promote middle key to parent
5. Recursively split parent if needed

### Advantages
- **Reduces disk I/O** - Store multiple keys per node
- **Balanced** - All leaves at same level
- **Good for databases** - Minimizes disk accesses

---

## 12. Binary Heap

### Definition
- **Complete binary tree** satisfying heap property
- **Max Heap**: Parent ≥ children
- **Min Heap**: Parent ≤ children

### Max Heap Example
```
       90
      /  \
    80    70
   / \    /
  50 40  30

Array: [90, 80, 70, 50, 40, 30]
```

### Array Representation
```
For node at index i:
- Parent: ⌊(i-1)/2⌋
- Left child: 2i + 1
- Right child: 2i + 2
```

### Operations

#### 1. Insert
```c
void insert(int heap[], int* n, int value) {
    // Insert at end
    (*n)++;
    int i = *n - 1;
    heap[i] = value;
    
    // Heapify up
    while(i > 0 && heap[parent(i)] < heap[i]) {
        swap(&heap[i], &heap[parent(i)]);
        i = parent(i);
    }
}

// Time: O(log n)
```

#### 2. Extract Max (Delete Root)
```c
int extractMax(int heap[], int* n) {
    if(*n <= 0) return -1;
    
    int root = heap[0];
    heap[0] = heap[*n - 1];
    (*n)--;
    
    // Heapify down
    heapify(heap, *n, 0);
    
    return root;
}

// Time: O(log n)
```

#### 3. Heapify
```c
void heapify(int heap[], int n, int i) {
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;
    
    if(left < n && heap[left] > heap[largest])
        largest = left;
    
    if(right < n && heap[right] > heap[largest])
        largest = right;
    
    if(largest != i) {
        swap(&heap[i], &heap[largest]);
        heapify(heap, n, largest);
    }
}
```

### Applications
- **Priority Queue** implementation
- **Heap Sort**
- **Graph algorithms** (Dijkstra, Prim)
- **Finding k largest/smallest** elements

---

## 🚀 Quick Reference Summary

### Tree Types

| Tree Type | Property | Application |
|-----------|----------|-------------|
| **Binary Tree** | ≤2 children | General hierarchy |
| **BST** | Left<Root<Right | Searching |
| **AVL** | Self-balancing BST | Fast search |
| **B-Tree** | Multi-way, balanced | Databases |
| **Heap** | Complete + heap property | Priority queue |
| **Threaded** | NULL→successor/predecessor | Fast traversal |

### Traversal Complexity
All traversals: **O(n)** time, **O(h)** space (recursion stack)

### BST Operations
- Search: O(h) - Best O(log n), Worst O(n)
- Insert: O(h)
- Delete: O(h)

### AVL Tree
- All operations: **O(log n)** guaranteed

### Heap Operations
- Insert: O(log n)
- Extract: O(log n)
- Heapify: O(log n)
- Build: O(n)

---

## 📝 Exam Important Questions

1. **Explain** types of binary trees with examples and properties.

2. **Construct** binary tree from:
   - Inorder: D B E A F C
   - Preorder: A B D E C F

3. **Implement** BST operations: insert, delete, search with C code.

4. **Explain** threaded binary tree. Write algorithm for inorder traversal.

5. **Describe** Huffman coding algorithm with example for:
   - Characters: A B C D E
   - Frequency: 5 9 12 13 16

6. **Explain** AVL tree rotations (LL, RR, LR, RL) with diagrams.

7. **Compare** BST vs AVL tree vs B-tree.

8. **Implement** max heap insertion and deletion.

9. **Explain** complete binary tree vs full binary tree vs perfect binary tree.

10. **Trace** all three traversals (inorder, preorder, postorder) for given tree.

---

*End of Unit-4*
