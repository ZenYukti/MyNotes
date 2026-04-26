# Unit-5: Graphs

---

## 1. Graph: Basic Terminology

### Definition
- **Graph**: Collection of vertices (nodes) and edges connecting them
- **G = (V, E)** where V = vertices, E = edges

### Example
```
Graph G:
    A ─── B
    │     │
    │     │
    D ─── C

V = {A, B, C, D}
E = {(A,B), (B,C), (C,D), (D,A)}
```

### Types of Graphs

#### 1. Directed Graph (Digraph)
- Edges have **direction**
- Edge (u, v) ≠ (v, u)

```
    A → B
    ↑   ↓
    D ← C
```

#### 2. Undirected Graph
- Edges have **no direction**
- Edge (u, v) = (v, u)

```
    A ─ B
    │   │
    D ─ C
```

#### 3. Weighted Graph
- Edges have **weights/costs**

```
       5
    A ─── B
    │3    │2
    D ─── C
       4
```

#### 4. Unweighted Graph
- All edges have **equal weight** (or no weight)

### Graph Terminology

| Term | Definition |
|------|------------|
| **Vertex/Node** | Point in graph |
| **Edge** | Connection between vertices |
| **Adjacent** | Two vertices connected by edge |
| **Degree** | Number of edges incident to vertex |
| **In-degree** | Number of incoming edges (directed) |
| **Out-degree** | Number of outgoing edges (directed) |
| **Path** | Sequence of vertices connected by edges |
| **Cycle** | Path that starts and ends at same vertex |
| **Connected Graph** | Path exists between every pair of vertices |
| **Complete Graph** | Every vertex connected to every other vertex |
| **Subgraph** | Subset of vertices and edges |

### Example: Degree Calculation
```
Graph:
    A ─── B ─── C
    │           │
    D ─────────┘

Degrees:
- deg(A) = 2 (connected to B, D)
- deg(B) = 2 (connected to A, C)
- deg(C) = 2 (connected to B, D)
- deg(D) = 2 (connected to A, C)

Total edges = Σ deg(v) / 2 = 8/2 = 4 ✓
```

---

## 2. Graph Representation

### A. Adjacency Matrix

#### Definition
- **2D array** of size V × V
- **Matrix[i][j] = 1** if edge exists from i to j
- **Matrix[i][j] = 0** if no edge

#### Undirected Graph Example
```
Graph:
    0 ─── 1
    │     │
    3 ─── 2

Adjacency Matrix:
    0  1  2  3
0 [ 0  1  0  1 ]
1 [ 1  0  1  0 ]
2 [ 0  1  0  1 ]
3 [ 1  0  1  0 ]

Symmetric matrix (Matrix[i][j] = Matrix[j][i])
```

#### Directed Graph Example
```
Graph:
    0 → 1
    ↑   ↓
    3 ← 2

Adjacency Matrix:
    0  1  2  3
0 [ 0  1  0  0 ]
1 [ 0  0  1  0 ]
2 [ 0  0  0  1 ]
3 [ 1  0  0  0 ]

Not symmetric (directed edges)
```

#### Weighted Graph Example
```
Graph:
       5
    0 ─── 1
    │3    │2
    3 ─── 2
       4

Adjacency Matrix:
    0  1  2  3
0 [ 0  5  0  3 ]
1 [ 5  0  2  0 ]
2 [ 0  2  0  4 ]
3 [ 3  0  4  0 ]

Matrix[i][j] = weight of edge
```

#### Advantages
- **Fast edge lookup**: O(1)
- **Simple implementation**
- **Easy to check if edge exists**

#### Disadvantages
- **Space**: O(V²) - wasteful for sparse graphs
- **Adding vertex**: Expensive (resize matrix)

### B. Adjacency List

#### Definition
- **Array of lists**
- **List[i]** contains all vertices adjacent to vertex i

#### Undirected Graph Example
```
Graph:
    0 ─── 1
    │     │
    3 ─── 2

Adjacency List:
0 → [1, 3]
1 → [0, 2]
2 → [1, 3]
3 → [0, 2]
```

#### Directed Graph Example
```
Graph:
    0 → 1
    ↑   ↓
    3 ← 2

Adjacency List:
0 → [1]
1 → [2]
2 → [3]
3 → [0]
```

#### Weighted Graph Example
```
Graph:
       5
    0 ─── 1
    │3    │2
    3 ─── 2
       4

Adjacency List:
0 → [(1,5), (3,3)]
1 → [(0,5), (2,2)]
2 → [(1,2), (3,4)]
3 → [(0,3), (2,4)]

Each entry: (vertex, weight)
```

#### Implementation
```c
struct Node {
    int vertex;
    int weight;
    struct Node* next;
};

struct Graph {
    int V;  // Number of vertices
    struct Node** array;  // Array of adjacency lists
};

struct Graph* createGraph(int V) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->array = (struct Node**)malloc(V * sizeof(struct Node*));
    
    for(int i = 0; i < V; i++) {
        graph->array[i] = NULL;
    }
    
    return graph;
}

void addEdge(struct Graph* graph, int src, int dest, int weight) {
    // Add edge from src to dest
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = dest;
    newNode->weight = weight;
    newNode->next = graph->array[src];
    graph->array[src] = newNode;
    
    // For undirected graph, add reverse edge
    newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = src;
    newNode->weight = weight;
    newNode->next = graph->array[dest];
    graph->array[dest] = newNode;
}
```

#### Advantages
- **Space efficient**: O(V + E) for sparse graphs
- **Easy to iterate** over neighbors
- **Fast to add vertex**

#### Disadvantages
- **Edge lookup**: O(deg(v)) - slower than matrix
- **More complex** implementation

### Comparison

| Operation | Adjacency Matrix | Adjacency List |
|-----------|-----------------|----------------|
| **Space** | O(V²) | O(V + E) |
| **Add vertex** | O(V²) | O(1) |
| **Add edge** | O(1) | O(1) |
| **Remove edge** | O(1) | O(V) |
| **Check edge** | O(1) | O(deg(v)) |
| **Find neighbors** | O(V) | O(deg(v)) |

---

## 3. Depth First Search (DFS)

### Concept
- **Explore as far as possible** along each branch before backtracking
- Uses **stack** (or recursion)
- **Traversal order**: Deep before wide

### Algorithm
```
DFS(G, start):
1. Mark start as visited
2. Process start
3. For each unvisited neighbor of start:
   a) Recursively call DFS(neighbor)
```

### Implementation
```c
void DFS(int graph[][MAX], int visited[], int vertex, int V) {
    printf("%d ", vertex);
    visited[vertex] = 1;
    
    for(int i = 0; i < V; i++) {
        if(graph[vertex][i] == 1 && !visited[i]) {
            DFS(graph, visited, i, V);
        }
    }
}

// Main function
void DFSTraversal(int graph[][MAX], int V, int start) {
    int visited[MAX] = {0};
    DFS(graph, visited, start, V);
}
```

### Dry Run: DFS
```
Graph:
        0
       / \
      1   2
     /     \
    3       4

Adjacency Matrix:
    0  1  2  3  4
0 [ 0  1  1  0  0 ]
1 [ 1  0  0  1  0 ]
2 [ 1  0  0  0  1 ]
3 [ 0  1  0  0  0 ]
4 [ 0  0  1  0  0 ]

Start: vertex 0

┌────────────────────────────────────────────┐
│ DFS Execution Trace                        │
└────────────────────────────────────────────┘

Call Stack & Visited Array:

Step 1: DFS(0)
───────────────
Visited: [1, 0, 0, 0, 0]
Print: 0
Stack: [DFS(0)]

Neighbors of 0: [1, 2]
Go to unvisited neighbor 1

Step 2: DFS(1)
───────────────
Visited: [1, 1, 0, 0, 0]
Print: 1
Stack: [DFS(0), DFS(1)]

Neighbors of 1: [0, 3]
- 0 already visited
Go to unvisited neighbor 3

Step 3: DFS(3)
───────────────
Visited: [1, 1, 0, 1, 0]
Print: 3
Stack: [DFS(0), DFS(1), DFS(3)]

Neighbors of 3: [1]
- 1 already visited
No unvisited neighbors → Backtrack

Step 4: Return to DFS(1)
─────────────────────────
Stack: [DFS(0), DFS(1)]
No more unvisited neighbors → Backtrack

Step 5: Return to DFS(0)
─────────────────────────
Stack: [DFS(0)]
Neighbors of 0: [1, 2]
- 1 already visited
Go to unvisited neighbor 2

Step 6: DFS(2)
───────────────
Visited: [1, 1, 1, 1, 0]
Print: 2
Stack: [DFS(0), DFS(2)]

Neighbors of 2: [0, 4]
- 0 already visited
Go to unvisited neighbor 4

Step 7: DFS(4)
───────────────
Visited: [1, 1, 1, 1, 1]
Print: 4
Stack: [DFS(0), DFS(2), DFS(4)]

Neighbors of 4: [2]
- 2 already visited
No unvisited neighbors → Backtrack

Step 8: All vertices visited
──────────────────────────────
Stack: []
DFS Complete!

Output: 0 1 3 2 4

Visual Traversal Order:
───────────────────────
    0 (1st)
   / \
(2nd) (4th)
  1   2
 /     \
3       4
(3rd)   (5th)

Path: 0 → 1 → 3 (backtrack) → 2 → 4
```

### Time Complexity
- **Adjacency Matrix**: O(V²)
- **Adjacency List**: O(V + E)

### Space Complexity
- **O(V)** for visited array and recursion stack

---

## 4. Breadth First Search (BFS)

### Concept
- **Explore all neighbors** at current depth before moving to next level
- Uses **queue**
- **Traversal order**: Wide before deep

### Algorithm
```
BFS(G, start):
1. Mark start as visited
2. Enqueue start
3. While queue not empty:
   a) Dequeue vertex v
   b) Process v
   c) For each unvisited neighbor of v:
      - Mark neighbor as visited
      - Enqueue neighbor
```

### Implementation
```c
void BFS(int graph[][MAX], int V, int start) {
    int visited[MAX] = {0};
    int queue[MAX], front = 0, rear = 0;
    
    visited[start] = 1;
    queue[rear++] = start;
    
    while(front < rear) {
        int vertex = queue[front++];
        printf("%d ", vertex);
        
        for(int i = 0; i < V; i++) {
            if(graph[vertex][i] == 1 && !visited[i]) {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
}
```

### Dry Run: BFS
```
Graph:
        0
       / \
      1   2
     /     \
    3       4

Start: vertex 0

┌────────────────────────────────────────────┐
│ BFS Execution Trace                        │
└────────────────────────────────────────────┘

Queue & Visited Array:

Step 1: Initialize
───────────────────
Visited: [1, 0, 0, 0, 0]
Queue: [0]
        ↑
      front

Step 2: Process 0
──────────────────
Dequeue: 0
Print: 0
Visited: [1, 0, 0, 0, 0]

Neighbors of 0: [1, 2]
Mark 1 and 2 as visited, enqueue them

Visited: [1, 1, 1, 0, 0]
Queue: [1, 2]
           ↑
         front

Step 3: Process 1
──────────────────
Dequeue: 1
Print: 1
Visited: [1, 1, 1, 0, 0]

Neighbors of 1: [0, 3]
- 0 already visited
Mark 3 as visited, enqueue it

Visited: [1, 1, 1, 1, 0]
Queue: [2, 3]
           ↑
         front

Step 4: Process 2
──────────────────
Dequeue: 2
Print: 2
Visited: [1, 1, 1, 1, 0]

Neighbors of 2: [0, 4]
- 0 already visited
Mark 4 as visited, enqueue it

Visited: [1, 1, 1, 1, 1]
Queue: [3, 4]
           ↑
         front

Step 5: Process 3
──────────────────
Dequeue: 3
Print: 3
Visited: [1, 1, 1, 1, 1]

Neighbors of 3: [1]
- 1 already visited
No unvisited neighbors

Queue: [4]
        ↑
      front

Step 6: Process 4
──────────────────
Dequeue: 4
Print: 4
Visited: [1, 1, 1, 1, 1]

Neighbors of 4: [2]
- 2 already visited
No unvisited neighbors

Queue: []
Queue empty → BFS Complete!

Output: 0 1 2 3 4

Visual Traversal (Level by Level):
───────────────────────────────────

Level 0:    0 (1st)
           / \
Level 1:  1   2 (2nd, 3rd)
         /     \
Level 2: 3     4 (4th, 5th)

Order: Level 0 → Level 1 → Level 2
       0 → (1, 2) → (3, 4)
```

### Time Complexity
- **Adjacency Matrix**: O(V²)
- **Adjacency List**: O(V + E)

### Space Complexity
- **O(V)** for visited array and queue

### DFS vs BFS Comparison

| Aspect | DFS | BFS |
|--------|-----|-----|
| **Data Structure** | Stack (recursion) | Queue |
| **Traversal** | Deep first | Wide first |
| **Memory** | O(h) height | O(w) width |
| **Path** | Not shortest | Shortest (unweighted) |
| **Use Case** | Topological sort, cycle detection | Shortest path, level order |

---

## 5. Connected Components

### Definition
- **Connected Component**: Maximal set of vertices where path exists between every pair
- **Disconnected Graph**: Graph with multiple connected components

### Example
```
Graph with 3 components:

Component 1:    Component 2:    Component 3:
    0 ─ 1          3 ─ 4             6
    │   │              │
    2 ─┘              5

Total vertices: 7
Components: 3
```

### Algorithm
```c
void findConnectedComponents(int graph[][MAX], int V) {
    int visited[MAX] = {0};
    int component = 0;
    
    for(int i = 0; i < V; i++) {
        if(!visited[i]) {
            component++;
            printf("Component %d: ", component);
            DFS(graph, visited, i, V);
            printf("\n");
        }
    }
    
    printf("Total components: %d\n", component);
}
```

---

## 6. Spanning Tree

### Definition
- **Spanning Tree**: Subgraph that connects **all vertices** with **minimum edges**
- **Properties**:
  - Contains **V-1 edges** (V = number of vertices)
  - **No cycles**
  - **Connected**

### Example
```
Graph:
    0 ─── 1 ─── 2
    │     │     │
    3 ─── 4 ─── 5

Edges: 7
Vertices: 6

One Possible Spanning Tree:
    0 ─── 1 ─── 2
    │     │      
    3     4     5

Edges: 5 = V-1 ✓
No cycles ✓
Connected ✓
```

---

## 7. Minimum Spanning Tree (MST)

### Definition
- **MST**: Spanning tree with **minimum total edge weight**
- **Applications**: Network design, clustering, circuit design

### Algorithms
1. **Prim's Algorithm** - Grows tree from single vertex
2. **Kruskal's Algorithm** - Adds edges in increasing weight order

---

## 8. Prim's Algorithm

### Concept
- Start from **arbitrary vertex**
- Repeatedly add **minimum weight edge** connecting tree to non-tree vertex
- **Greedy approach**

### Algorithm
```
Prim(G, start):
1. Initialize: Mark start, key[start]=0, key[others]=∞
2. While not all vertices in MST:
   a) Pick vertex u with minimum key not in MST
   b) Add u to MST
   c) For each neighbor v of u:
      If v not in MST and weight(u,v) < key[v]:
         key[v] = weight(u,v)
         parent[v] = u
```

### Implementation
```c
#define INF 99999

void prims(int graph[][MAX], int V) {
    int parent[MAX];
    int key[MAX];
    int mstSet[MAX];
    
    // Initialize
    for(int i = 0; i < V; i++) {
        key[i] = INF;
        mstSet[i] = 0;
    }
    
    key[0] = 0;
    parent[0] = -1;
    
    for(int count = 0; count < V - 1; count++) {
        // Find minimum key vertex not in MST
        int min = INF, minIndex;
        for(int v = 0; v < V; v++) {
            if(mstSet[v] == 0 && key[v] < min) {
                min = key[v];
                minIndex = v;
            }
        }
        
        int u = minIndex;
        mstSet[u] = 1;
        
        // Update keys of adjacent vertices
        for(int v = 0; v < V; v++) {
            if(graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph[u][v];
            }
        }
    }
    
    // Print MST
    printf("Edge \tWeight\n");
    int totalWeight = 0;
    for(int i = 1; i < V; i++) {
        printf("%d - %d \t%d\n", parent[i], i, graph[i][parent[i]]);
        totalWeight += graph[i][parent[i]];
    }
    printf("Total MST weight: %d\n", totalWeight);
}
```

### Dry Run: Prim's Algorithm
```
Graph (Weighted):
       2        3
    0 ─── 1 ─── 2
    │     │     │
   6│    8│    7│
    │     │     │
    3 ─── 4 ─── 5
       9    5

Adjacency Matrix (weights):
    0  1  2  3  4  5
0 [ 0  2  0  6  0  0 ]
1 [ 2  0  3  8  5  0 ]
2 [ 0  3  0  0  7  0 ]
3 [ 6  8  0  0  9  0 ]
4 [ 0  5  7  9  0  5 ]
5 [ 0  0  0  0  5  0 ]

Start: vertex 0

┌────────────────────────────────────────────┐
│ Prim's Algorithm Step-by-Step             │
└────────────────────────────────────────────┘

Initialize:
key:    [ 0,  ∞,  ∞,  ∞,  ∞,  ∞]
parent: [-1, -1, -1, -1, -1, -1]
mstSet: [ 0,  0,  0,  0,  0,  0]

┌────────────────────────────────────────────┐
│ Iteration 1                                │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 0 (key=0)
Add 0 to MST

mstSet: [1, 0, 0, 0, 0, 0]

Update neighbors of 0:
- Edge 0→1 (weight=2): key[1]=2, parent[1]=0
- Edge 0→3 (weight=6): key[3]=6, parent[3]=0

key:    [0, 2, ∞, 6, ∞, ∞]
parent: [-1, 0, -1, 0, -1, -1]

MST Edges: None yet
Current Tree: {0}

┌────────────────────────────────────────────┐
│ Iteration 2                                │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 1 (key=2)
Add 1 to MST

mstSet: [1, 1, 0, 0, 0, 0]

Update neighbors of 1:
- Edge 1→0 (weight=2): 0 already in MST
- Edge 1→2 (weight=3): key[2]=3, parent[2]=1
- Edge 1→3 (weight=8): 8 > key[3]=6, no update
- Edge 1→4 (weight=5): key[4]=5, parent[4]=1

key:    [0, 2, 3, 6, 5, ∞]
parent: [-1, 0, 1, 0, 1, -1]

MST Edges: 0-1 (weight=2)
Current Tree: {0, 1}

┌────────────────────────────────────────────┐
│ Iteration 3                                │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 2 (key=3)
Add 2 to MST

mstSet: [1, 1, 1, 0, 0, 0]

Update neighbors of 2:
- Edge 2→1 (weight=3): 1 already in MST
- Edge 2→4 (weight=7): 7 > key[4]=5, no update

key:    [0, 2, 3, 6, 5, ∞]
parent: [-1, 0, 1, 0, 1, -1]

MST Edges: 0-1 (2), 1-2 (3)
Current Tree: {0, 1, 2}

┌────────────────────────────────────────────┐
│ Iteration 4                                │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 4 (key=5)
Add 4 to MST

mstSet: [1, 1, 1, 0, 1, 0]

Update neighbors of 4:
- Edge 4→1 (weight=5): 1 already in MST
- Edge 4→2 (weight=7): 2 already in MST
- Edge 4→3 (weight=9): 9 > key[3]=6, no update
- Edge 4→5 (weight=5): key[5]=5, parent[5]=4

key:    [0, 2, 3, 6, 5, 5]
parent: [-1, 0, 1, 0, 1, 4]

MST Edges: 0-1 (2), 1-2 (3), 1-4 (5)
Current Tree: {0, 1, 2, 4}

┌────────────────────────────────────────────┐
│ Iteration 5                                │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 5 (key=5)
Add 5 to MST

mstSet: [1, 1, 1, 0, 1, 1]

Update neighbors of 5:
- Edge 5→4 (weight=5): 4 already in MST

key:    [0, 2, 3, 6, 5, 5]
parent: [-1, 0, 1, 0, 1, 4]

MST Edges: 0-1 (2), 1-2 (3), 1-4 (5), 4-5 (5)
Current Tree: {0, 1, 2, 4, 5}

┌────────────────────────────────────────────┐
│ Iteration 6 (Last)                         │
└────────────────────────────────────────────┘

Pick vertex with min key not in MST: u = 3 (key=6)
Add 3 to MST

mstSet: [1, 1, 1, 1, 1, 1]

MST Edges: 0-1 (2), 1-2 (3), 1-4 (5), 4-5 (5), 0-3 (6)
All vertices in MST!

┌────────────────────────────────────────────┐
│ Final MST                                  │
└────────────────────────────────────────────┘

MST Edges and Weights:
0 - 1   weight: 2
1 - 2   weight: 3
0 - 3   weight: 6
1 - 4   weight: 5
4 - 5   weight: 5

Total MST Weight: 2 + 3 + 6 + 5 + 5 = 21

Visual MST:
       2        3
    0 ─── 1 ─── 2
    │     │      
   6│    5│     
    │     │      
    3     4 ─── 5
              5

Edges: 5 = V-1 ✓
Total Weight: 21 (minimum)
```

### Time Complexity
- **Simple Implementation**: O(V²)
- **With Min Heap**: O(E log V)

### Space Complexity
- **O(V)** for arrays

---

## 9. Kruskal's Algorithm

### Concept
- Sort all edges by **weight**
- Add edges in **increasing order**
- Skip edge if it creates **cycle** (use Union-Find)
- **Greedy approach**

### Algorithm
```
Kruskal(G):
1. Sort all edges by weight
2. Initialize MST as empty
3. For each edge (u,v) in sorted order:
   a) If adding (u,v) doesn't create cycle:
      - Add (u,v) to MST
   b) If MST has V-1 edges:
      - Stop
```

### Union-Find (Disjoint Set)
```c
int find(int parent[], int i) {
    if(parent[i] == i)
        return i;
    return find(parent, parent[i]);
}

void unionSet(int parent[], int rank[], int x, int y) {
    int xroot = find(parent, x);
    int yroot = find(parent, y);
    
    if(rank[xroot] < rank[yroot])
        parent[xroot] = yroot;
    else if(rank[xroot] > rank[yroot])
        parent[yroot] = xroot;
    else {
        parent[yroot] = xroot;
        rank[xroot]++;
    }
}
```

### Implementation
```c
struct Edge {
    int src, dest, weight;
};

int compare(const void* a, const void* b) {
    return ((struct Edge*)a)->weight - ((struct Edge*)b)->weight;
}

void kruskal(struct Edge edges[], int V, int E) {
    // Sort edges
    qsort(edges, E, sizeof(edges[0]), compare);
    
    int parent[MAX], rank[MAX];
    for(int i = 0; i < V; i++) {
        parent[i] = i;
        rank[i] = 0;
    }
    
    printf("MST Edges:\n");
    int mstWeight = 0, edgeCount = 0;
    
    for(int i = 0; i < E && edgeCount < V - 1; i++) {
        int u = edges[i].src;
        int v = edges[i].dest;
        int weight = edges[i].weight;
        
        int setU = find(parent, u);
        int setV = find(parent, v);
        
        if(setU != setV) {
            printf("%d - %d: %d\n", u, v, weight);
            mstWeight += weight;
            edgeCount++;
            unionSet(parent, rank, setU, setV);
        }
    }
    
    printf("Total MST weight: %d\n", mstWeight);
}
```

### Dry Run: Kruskal's Algorithm
```
Graph (Same as Prim's example):
       2        3
    0 ─── 1 ─── 2
    │     │     │
   6│    8│    7│
    │     │     │
    3 ─── 4 ─── 5
       9    5

Vertices: 6 (0-5)

Edges:
(0,1,2), (1,2,3), (0,3,6), (1,3,8), (1,4,5), 
(2,4,7), (3,4,9), (4,5,5)

┌────────────────────────────────────────────┐
│ Step 1: Sort Edges by Weight              │
└────────────────────────────────────────────┘

Sorted Edges:
1. (0,1): 2
2. (1,2): 3
3. (1,4): 5
4. (4,5): 5
5. (0,3): 6
6. (2,4): 7
7. (1,3): 8
8. (3,4): 9

┌────────────────────────────────────────────┐
│ Step 2: Initialize Union-Find             │
└────────────────────────────────────────────┘

parent: [0, 1, 2, 3, 4, 5]
rank:   [0, 0, 0, 0, 0, 0]

Each vertex is its own parent (separate sets)

┌────────────────────────────────────────────┐
│ Edge Processing                            │
└────────────────────────────────────────────┘

Edge 1: (0,1) weight=2
───────────────────────
find(0) = 0
find(1) = 1
Different sets → Add to MST

Union(0, 1):
parent: [0, 0, 2, 3, 4, 5]
         ↑  ↑
        0 ← 1

MST: [(0,1,2)]
Weight: 2

Edge 2: (1,2) weight=3
───────────────────────
find(1) = find(0) = 0
find(2) = 2
Different sets → Add to MST

Union(0, 2):
parent: [0, 0, 0, 3, 4, 5]
         ↑  ↑  ↑
        Set {0,1,2}

MST: [(0,1,2), (1,2,3)]
Weight: 5

Edge 3: (1,4) weight=5
───────────────────────
find(1) = 0
find(4) = 4
Different sets → Add to MST

Union(0, 4):
parent: [0, 0, 0, 3, 0, 5]
         ↑  ↑  ↑     ↑
        Set {0,1,2,4}

MST: [(0,1,2), (1,2,3), (1,4,5)]
Weight: 10

Edge 4: (4,5) weight=5
───────────────────────
find(4) = 0
find(5) = 5
Different sets → Add to MST

Union(0, 5):
parent: [0, 0, 0, 3, 0, 0]
         ↑  ↑  ↑     ↑  ↑
        Set {0,1,2,4,5}

MST: [(0,1,2), (1,2,3), (1,4,5), (4,5,5)]
Weight: 15

Edge 5: (0,3) weight=6
───────────────────────
find(0) = 0
find(3) = 3
Different sets → Add to MST

Union(0, 3):
parent: [0, 0, 0, 0, 0, 0]
         ↑  ↑  ↑  ↑  ↑  ↑
        All in same set

MST: [(0,1,2), (1,2,3), (1,4,5), (4,5,5), (0,3,6)]
Weight: 21
Edges: 5 = V-1 → STOP!

Edge 6-8: Skipped (MST complete)

┌────────────────────────────────────────────┐
│ Final MST                                  │
└────────────────────────────────────────────┘

MST Edges:
0 - 1: 2
1 - 2: 3
1 - 4: 5
4 - 5: 5
0 - 3: 6

Total Weight: 21

Visual MST:
       2        3
    0 ─── 1 ─── 2
    │     │      
   6│    5│     
    │     │      
    3     4 ─── 5
              5

Same MST as Prim's! ✓
```

### Time Complexity
- **Sorting**: O(E log E)
- **Union-Find**: O(E α(V)) ≈ O(E)
- **Total**: O(E log E) or O(E log V)

### Space Complexity
- **O(V)** for parent and rank arrays

---

## 10. Warshall's Algorithm

### Concept
- Find **transitive closure** of graph
- Determines if path exists between **every pair** of vertices
- **Dynamic Programming** approach

### Transitive Closure
```
If path exists from i to j: TC[i][j] = 1
Otherwise: TC[i][j] = 0
```

### Algorithm
```
Warshall(graph):
1. Initialize TC = adjacency matrix
2. For k = 0 to V-1:
   For i = 0 to V-1:
      For j = 0 to V-1:
         TC[i][j] = TC[i][j] OR (TC[i][k] AND TC[k][j])
```

### Implementation
```c
void warshall(int graph[][MAX], int V) {
    int reach[][MAX];
    
    // Initialize reach matrix
    for(int i = 0; i < V; i++) {
        for(int j = 0; j < V; j++) {
            reach[i][j] = graph[i][j];
        }
    }
    
    // Warshall's algorithm
    for(int k = 0; k < V; k++) {
        for(int i = 0; i < V; i++) {
            for(int j = 0; j < V; j++) {
                reach[i][j] = reach[i][j] || 
                             (reach[i][k] && reach[k][j]);
            }
        }
    }
    
    // Print transitive closure
    printf("Transitive Closure:\n");
    for(int i = 0; i < V; i++) {
        for(int j = 0; j < V; j++) {
            printf("%d ", reach[i][j]);
        }
        printf("\n");
    }
}
```

### Dry Run: Warshall's Algorithm
```
Graph (Directed):
    0 → 1 → 3
    ↓       ↑
    2 ──────┘

Adjacency Matrix:
    0  1  2  3
0 [ 0  1  1  0 ]
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

Paths:
0→1: Yes (direct)
0→2: Yes (direct)
0→3: Yes (0→1→3 or 0→2→3)
1→3: Yes (direct)
2→3: Yes (direct)

┌────────────────────────────────────────────┐
│ Initialize TC Matrix                       │
└────────────────────────────────────────────┘

TC = Adjacency Matrix
    0  1  2  3
0 [ 0  1  1  0 ]
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

┌────────────────────────────────────────────┐
│ k = 0 (Intermediate vertex 0)              │
└────────────────────────────────────────────┘

Check all pairs (i,j) via vertex 0:

TC[i][j] = TC[i][j] OR (TC[i][0] AND TC[0][j])

i=0, j=0: TC[0][0] = 0 OR (0 AND 0) = 0
i=0, j=1: TC[0][1] = 1 OR (0 AND 1) = 1
i=0, j=2: TC[0][2] = 1 OR (0 AND 1) = 1
i=0, j=3: TC[0][3] = 0 OR (0 AND 0) = 0

i=1, j=0: TC[1][0] = 0 OR (0 AND 0) = 0
i=1, j=1: TC[1][1] = 0 OR (0 AND 1) = 0
i=1, j=2: TC[1][2] = 0 OR (0 AND 1) = 0
i=1, j=3: TC[1][3] = 1 OR (0 AND 0) = 1

i=2, j=0: TC[2][0] = 0 OR (0 AND 0) = 0
i=2, j=1: TC[2][1] = 0 OR (0 AND 1) = 0
i=2, j=2: TC[2][2] = 0 OR (0 AND 1) = 0
i=2, j=3: TC[2][3] = 1 OR (0 AND 0) = 1

i=3, j=0-3: All remain 0

After k=0:
    0  1  2  3
0 [ 0  1  1  0 ]
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

No change (vertex 0 has no incoming edges)

┌────────────────────────────────────────────┐
│ k = 1 (Intermediate vertex 1)              │
└────────────────────────────────────────────┘

Check all pairs (i,j) via vertex 1:

TC[i][j] = TC[i][j] OR (TC[i][1] AND TC[1][j])

Key changes:
i=0, j=3: TC[0][3] = 0 OR (1 AND 1) = 1 ✓
         (Path 0→1→3 found!)

After k=1:
    0  1  2  3
0 [ 0  1  1  1 ] ← Changed!
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

┌────────────────────────────────────────────┐
│ k = 2 (Intermediate vertex 2)              │
└────────────────────────────────────────────┘

Check all pairs (i,j) via vertex 2:

TC[i][j] = TC[i][j] OR (TC[i][2] AND TC[2][j])

Key changes:
i=0, j=3: TC[0][3] = 1 OR (1 AND 1) = 1
         (Already found via k=1)

After k=2:
    0  1  2  3
0 [ 0  1  1  1 ]
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

No new paths

┌────────────────────────────────────────────┐
│ k = 3 (Intermediate vertex 3)              │
└────────────────────────────────────────────┘

Check all pairs (i,j) via vertex 3:

Vertex 3 has no outgoing edges → No new paths

After k=3:
    0  1  2  3
0 [ 0  1  1  1 ]
1 [ 0  0  0  1 ]
2 [ 0  0  0  1 ]
3 [ 0  0  0  0 ]

┌────────────────────────────────────────────┐
│ Final Transitive Closure                   │
└────────────────────────────────────────────┘

    0  1  2  3
0 [ 0  1  1  1 ]  ← 0 can reach 1, 2, 3
1 [ 0  0  0  1 ]  ← 1 can reach 3
2 [ 0  0  0  1 ]  ← 2 can reach 3
3 [ 0  0  0  0 ]  ← 3 can't reach anyone

Interpretation:
- From 0: Can reach {1, 2, 3}
- From 1: Can reach {3}
- From 2: Can reach {3}
- From 3: Can't reach any vertex
```

### Time Complexity
- **O(V³)** - Three nested loops

### Space Complexity
- **O(V²)** for reach matrix

---

## 11. Dijkstra's Algorithm

### Concept
- Find **shortest path** from source to all vertices
- Works with **non-negative weights**
- **Greedy approach** - similar to Prim's

### Algorithm
```
Dijkstra(G, source):
1. Initialize: dist[source]=0, dist[others]=∞
2. Mark all vertices as unvisited
3. While unvisited vertices exist:
   a) Pick unvisited vertex u with minimum dist
   b) Mark u as visited
   c) For each unvisited neighbor v of u:
      If dist[u] + weight(u,v) < dist[v]:
         dist[v] = dist[u] + weight(u,v)
         parent[v] = u
```

### Implementation
```c
#define INF 99999

void dijkstra(int graph[][MAX], int V, int source) {
    int dist[MAX];
    int visited[MAX];
    int parent[MAX];
    
    // Initialize
    for(int i = 0; i < V; i++) {
        dist[i] = INF;
        visited[i] = 0;
        parent[i] = -1;
    }
    dist[source] = 0;
    
    for(int count = 0; count < V; count++) {
        // Find minimum distance vertex
        int min = INF, minIndex;
        for(int v = 0; v < V; v++) {
            if(!visited[v] && dist[v] < min) {
                min = dist[v];
                minIndex = v;
            }
        }
        
        int u = minIndex;
        visited[u] = 1;
        
        // Update distances
        for(int v = 0; v < V; v++) {
            if(!visited[v] && graph[u][v] && 
               dist[u] != INF &&
               dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
                parent[v] = u;
            }
        }
    }
    
    // Print shortest paths
    printf("Vertex\tDistance\tPath\n");
    for(int i = 0; i < V; i++) {
        printf("%d\t%d\t\t", i, dist[i]);
        printPath(parent, i);
        printf("\n");
    }
}
```

### Dry Run: Dijkstra's Algorithm
```
Graph (Weighted):
       4        2
    0 ─── 1 ─── 2
    │     │     │
   1│    3│    1│
    │     │     │
    3 ─── 4 ─── 5
       2    3

Adjacency Matrix (weights):
    0  1  2  3  4  5
0 [ 0  4  0  1  0  0 ]
1 [ 4  0  2  0  3  0 ]
2 [ 0  2  0  0  0  1 ]
3 [ 1  0  0  0  2  0 ]
4 [ 0  3  0  2  0  3 ]
5 [ 0  0  1  0  3  0 ]

Source: vertex 0

┌────────────────────────────────────────────┐
│ Initialize                                 │
└────────────────────────────────────────────┘

dist:    [ 0,  ∞,  ∞,  ∞,  ∞,  ∞]
visited: [ 0,  0,  0,  0,  0,  0]
parent:  [-1, -1, -1, -1, -1, -1]

┌────────────────────────────────────────────┐
│ Iteration 1                                │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 0 (dist=0)
Mark 0 as visited

visited: [1, 0, 0, 0, 0, 0]

Update neighbors of 0:
- 0→1 (weight=4): dist[1] = 0+4 = 4, parent[1]=0
- 0→3 (weight=1): dist[3] = 0+1 = 1, parent[3]=0

dist:    [0, 4, ∞, 1, ∞, ∞]
parent:  [-1, 0, -1, 0, -1, -1]

Shortest paths so far:
0→1: 4 (via 0)
0→3: 1 (via 0)

┌────────────────────────────────────────────┐
│ Iteration 2                                │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 3 (dist=1)
Mark 3 as visited

visited: [1, 0, 0, 1, 0, 0]

Update neighbors of 3:
- 3→0 (weight=1): 0 already visited
- 3→4 (weight=2): dist[4] = 1+2 = 3, parent[4]=3

dist:    [0, 4, ∞, 1, 3, ∞]
parent:  [-1, 0, -1, 0, 3, -1]

Shortest paths so far:
0→1: 4
0→3: 1
0→4: 3 (0→3→4)

┌────────────────────────────────────────────┐
│ Iteration 3                                │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 4 (dist=3)
Mark 4 as visited

visited: [1, 0, 0, 1, 1, 0]

Update neighbors of 4:
- 4→1 (weight=3): dist[1]=3+3=6 > 4, no update
- 4→3 (weight=2): 3 already visited
- 4→5 (weight=3): dist[5] = 3+3 = 6, parent[5]=4

dist:    [0, 4, ∞, 1, 3, 6]
parent:  [-1, 0, -1, 0, 3, 4]

Shortest paths so far:
0→1: 4
0→3: 1
0→4: 3 (0→3→4)
0→5: 6 (0→3→4→5)

┌────────────────────────────────────────────┐
│ Iteration 4                                │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 1 (dist=4)
Mark 1 as visited

visited: [1, 1, 0, 1, 1, 0]

Update neighbors of 1:
- 1→0 (weight=4): 0 already visited
- 1→2 (weight=2): dist[2] = 4+2 = 6, parent[2]=1
- 1→4 (weight=3): 4 already visited

dist:    [0, 4, 6, 1, 3, 6]
parent:  [-1, 0, 1, 0, 3, 4]

Shortest paths so far:
0→1: 4
0→2: 6 (0→1→2)
0→3: 1
0→4: 3 (0→3→4)
0→5: 6 (0→3→4→5)

┌────────────────────────────────────────────┐
│ Iteration 5                                │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 2 (dist=6)
Mark 2 as visited

visited: [1, 1, 1, 1, 1, 0]

Update neighbors of 2:
- 2→1 (weight=2): 1 already visited
- 2→5 (weight=1): dist[5] = 6+1 = 7 > 6, no update

dist:    [0, 4, 6, 1, 3, 6]
parent:  [-1, 0, 1, 0, 3, 4]

No improvements

┌────────────────────────────────────────────┐
│ Iteration 6 (Final)                        │
└────────────────────────────────────────────┘

Pick unvisited vertex with min dist: u = 5 (dist=6)
Mark 5 as visited

visited: [1, 1, 1, 1, 1, 1]

All vertices visited!

┌────────────────────────────────────────────┐
│ Final Shortest Paths from Source 0        │
└────────────────────────────────────────────┘

Vertex  Distance  Path
──────  ────────  ─────────────────
  0       0       0
  1       4       0 → 1
  2       6       0 → 1 → 2
  3       1       0 → 3
  4       3       0 → 3 → 4
  5       6       0 → 3 → 4 → 5

Visual Shortest Path Tree:
       4        2
    0 ─── 1 ─── 2
    │     
   1│    
    │     
    3 ─── 4 ─── 5
       2    3

All paths are shortest from source 0!
```

### Time Complexity
- **Simple Implementation**: O(V²)
- **With Min Heap**: O((V + E) log V)

### Space Complexity
- **O(V)** for arrays

---

## 🚀 Quick Reference Summary

### Graph Representations

| Representation | Space | Add Edge | Check Edge | Find Neighbors |
|----------------|-------|----------|------------|----------------|
| **Adjacency Matrix** | O(V²) | O(1) | O(1) | O(V) |
| **Adjacency List** | O(V+E) | O(1) | O(deg(v)) | O(deg(v)) |

### Graph Traversals

| Algorithm | Data Structure | Time (Matrix) | Time (List) | Use Case |
|-----------|---------------|---------------|-------------|----------|
| **DFS** | Stack/Recursion | O(V²) | O(V+E) | Topological sort, cycle detection |
| **BFS** | Queue | O(V²) | O(V+E) | Shortest path (unweighted) |

### Minimum Spanning Tree

| Algorithm | Approach | Time | Best For |
|-----------|----------|------|----------|
| **Prim's** | Grows from vertex | O(V²) or O(E log V) | Dense graphs |
| **Kruskal's** | Sort edges | O(E log E) | Sparse graphs |

### Shortest Path & Closure

| Algorithm | Purpose | Time | Constraint |
|-----------|---------|------|------------|
| **Dijkstra** | Single source shortest path | O(V²) or O(E log V) | Non-negative weights |
| **Warshall** | Transitive closure | O(V³) | All pairs reachability |

---

## 📝 Exam Important Questions

1. **Explain** graph representations. Compare adjacency matrix vs adjacency list with example.

2. **Trace DFS and BFS** on given graph. Show visited array and output sequence.

3. **Apply Prim's algorithm** to find MST:
   ```
   Graph with vertices 0-4, show all iterations with key and parent arrays.
   ```

4. **Apply Kruskal's algorithm** to find MST:
   ```
   Show edge sorting, union-find operations, and cycle detection.
   ```

5. **Find transitive closure** using Warshall's algorithm for given directed graph.

6. **Apply Dijkstra's algorithm** to find shortest path from vertex 0 to all vertices.

7. **Implement** DFS and BFS in C using adjacency matrix.

8. **Find connected components** in disconnected graph using DFS.

9. **Compare** Prim's vs Kruskal's algorithm. When to use each?

10. **Explain** Union-Find data structure with path compression and union by rank.

---

*End of Unit-5*
