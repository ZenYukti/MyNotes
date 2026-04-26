# Graph Theory & Combinatorics - Complete Study Notes

---

## 1. Graphs: Definition and Terminology

### Basic Definitions

- **Graph G = (V, E)**
  - V: Set of vertices (nodes)
  - E: Set of edges connecting vertices
  - Example: G = ({a, b, c}, {(a,b), (b,c)})

- **Types of Edges**
  - Undirected edge: {u, v} - no direction
  - Directed edge: (u, v) - goes from u to v
  - Loop: Edge connecting vertex to itself
  - Multiple edges: More than one edge between same vertices

### Key Terminology

- **Degree of a vertex**
  - deg(v): Number of edges incident to v
  - In directed graphs: in-degree and out-degree
  - Loop contributes 2 to degree

- **Handshaking Theorem**
  - Sum of all degrees = 2|E|
  - Number of odd-degree vertices is always even

- **Path and Circuit**
  - Path: Sequence of vertices where each adjacent pair is connected
  - Simple path: No repeated vertices
  - Circuit/Cycle: Path that starts and ends at same vertex
  - Simple circuit: No repeated edges

- **Connectivity**
  - Connected graph: Path exists between every pair of vertices
  - Connected component: Maximal connected subgraph
  - Strongly connected (directed): Path exists in both directions

- **Special Vertices**
  - Isolated vertex: deg(v) = 0
  - Pendant vertex: deg(v) = 1
  - Adjacent vertices: Connected by an edge

- **Subgraph**
  - H = (V', E') where V' ⊆ V and E' ⊆ E

### Exam Questions

1. **Prove the Handshaking Theorem and use it to show that the number of vertices with odd degree in any graph is even.**

2. **Given a graph with 10 vertices where each vertex has degree 3, how many edges does the graph have? Is such a graph possible?**

3. **Define connected graph and strongly connected graph. Give an example of a directed graph that is connected but not strongly connected.**

4. **If a graph has 15 edges and all vertices have degree at least 3, what is the maximum number of vertices it can have?**

5. **Explain with examples: simple path, simple circuit, and cycle. What is the minimum number of edges required to have a cycle in a graph with n vertices?**

---

## 2. Representation of Graphs

### Adjacency Matrix

- **Definition**
  - n × n matrix A where A[i][j] = 1 if edge exists between vi and vj
  - For weighted graphs: A[i][j] = weight of edge
  - For directed graphs: A[i][j] = 1 if edge goes from vi to vj

- **Properties**
  - Symmetric for undirected graphs
  - Diagonal elements represent loops
  - Space complexity: O(n²)
  - Edge lookup: O(1)
  - Finding all neighbors: O(n)

### Adjacency List

- **Definition**
  - Array of lists where index i contains list of neighbors of vertex i
  - For weighted graphs: Store (neighbor, weight) pairs

- **Properties**
  - Space complexity: O(|V| + |E|)
  - More space-efficient for sparse graphs
  - Edge lookup: O(deg(v))
  - Finding all neighbors: O(deg(v))

### Incidence Matrix

- **Definition**
  - |V| × |E| matrix where M[i][j] = 1 if vertex vi is incident to edge ej
  - For directed graphs: -1 for source, +1 for destination

- **Properties**
  - Space complexity: O(|V| × |E|)
  - Useful for certain algorithms
  - Row sum = degree of vertex

### Comparison

- **Adjacency Matrix vs List**
  - Matrix better for dense graphs (|E| ≈ |V|²)
  - List better for sparse graphs (|E| << |V|²)
  - Matrix better for quick edge existence check
  - List better for iterating through neighbors

### Exam Questions

1. **Draw a graph with 5 vertices and 7 edges. Represent it using (a) Adjacency Matrix (b) Adjacency List (c) Incidence Matrix.**

2. **Compare adjacency matrix and adjacency list representations in terms of space complexity and time complexity for common operations.**

3. **Given an adjacency matrix of an undirected graph, how can you find the degree of each vertex? Write the formula.**

4. **When would you prefer adjacency list over adjacency matrix? Justify with space complexity analysis for sparse and dense graphs.**

5. **For a directed graph represented as an adjacency matrix, how do you calculate in-degree and out-degree of a vertex?**

---

## 3. Multigraphs

### Definition

- **Multigraph**
  - Graph that allows multiple edges between same pair of vertices
  - May or may not allow loops
  - Denoted as G = (V, E) where E is a multiset

### Types

- **Pseudograph**
  - Allows both multiple edges and loops
  - Most general type

- **Multigraph (strict)**
  - Allows multiple edges
  - No loops allowed

- **Simple Graph**
  - No multiple edges
  - No loops
  - At most one edge between any pair of vertices

### Properties

- **Degree in Multigraphs**
  - Degree calculation same as simple graphs
  - Each loop adds 2 to degree
  - Handshaking theorem still applies

- **Applications**
  - Road networks (multiple roads between cities)
  - Computer networks (multiple connections)
  - Flight routes (multiple flights between airports)

### Exam Questions

1. **Define multigraph, pseudograph, and simple graph. Draw an example of each.**

2. **Can a multigraph have an odd number of edges if all vertices have even degree? Justify your answer.**

3. **Draw a multigraph with 4 vertices where degree sequence is (4, 4, 3, 3). Is it possible without loops?**

4. **How does the adjacency matrix representation change for multigraphs compared to simple graphs?**

5. **Give three real-world applications of multigraphs and explain why multiple edges are necessary in those scenarios.**

---

## 4. Bipartite Graphs

### Definition

- **Bipartite Graph**
  - Graph G = (V, E) where V can be partitioned into two disjoint sets V₁ and V₂
  - Every edge connects a vertex in V₁ to a vertex in V₂
  - No edges within V₁ or V₂

### Properties

- **Characterization**
  - Graph is bipartite ⟺ it contains no odd-length cycles
  - Can be 2-colored (chromatic number ≤ 2)
  - Can be checked using BFS/DFS with 2-coloring

- **Complete Bipartite Graph Km,n**
  - |V₁| = m, |V₂| = n
  - Every vertex in V₁ connected to every vertex in V₂
  - Total edges = m × n
  - Regular if m = n

### Testing for Bipartiteness

- **Algorithm (BFS/DFS based)**
  - Start with any vertex, assign color 1
  - Assign opposite color to all neighbors
  - Continue until all vertices colored
  - If conflict arises, graph is not bipartite

### Applications

- **Matching Problems**
  - Job assignment (workers to jobs)
  - Marriage problem (men to women)
  - Resource allocation

- **Real-world Examples**
  - Student-course enrollment
  - Actor-movie relationships
  - Collaboration networks

### Exam Questions

1. **Prove that a graph is bipartite if and only if it contains no odd-length cycles.**

2. **How many edges does a complete bipartite graph K₄,₆ have? Draw K₃,₃ and explain why it's non-planar.**

3. **Write an algorithm to check whether a given graph is bipartite. Analyze its time complexity.**

4. **Give the vertex set partition for the following graph and verify it's bipartite: Vertices {1,2,3,4,5,6}, Edges {(1,2), (1,4), (2,3), (3,4), (4,5), (5,6)}**

5. **Explain the application of bipartite graphs in the maximum matching problem. What is Hall's Marriage Theorem?**

---

## 5. Planar Graphs

### Definition

- **Planar Graph**
  - Graph that can be drawn on a plane without edge crossings
  - Edges may be curved
  - Same graph can have planar and non-planar drawings

### Euler's Formula

- **For connected planar graphs**
  - v - e + f = 2
  - v = number of vertices
  - e = number of edges
  - f = number of faces (including outer face)

### Important Theorems

- **Corollary 1**
  - For planar graph with v ≥ 3: e ≤ 3v - 6
  - Used to prove non-planarity

- **Corollary 2**
  - For planar graph with no triangles and v ≥ 3: e ≤ 2v - 4
  - Useful for bipartite planar graphs

- **Degree of faces**
  - Sum of degrees of all faces = 2e
  - Each edge borders at most 2 faces

### Non-Planar Graphs

- **Kuratowski's Theorem**
  - Graph is planar ⟺ it contains no subdivision of K₅ or K₃,₃
  - K₅: Complete graph on 5 vertices
  - K₃,₃: Complete bipartite graph

- **Wagner's Theorem**
  - Graph is planar ⟺ it contains no K₅ or K₃,₃ as a minor

### Testing Planarity

- **Methods**
  - Check using Euler's formula (necessary but not sufficient)
  - Check for K₅ or K₃,₃ subdivisions
  - Use planarity testing algorithms (linear time exists)

### Exam Questions

1. **State and prove Euler's formula for planar graphs. Use it to prove that K₅ is non-planar.**

2. **A connected planar graph has 10 vertices and 18 edges. How many faces does it have? Is this possible?**

3. **Prove that K₃,₃ is non-planar using (a) Euler's formula (b) Kuratowski's theorem.**

4. **What is the maximum number of edges in a planar graph with 8 vertices? Justify using the appropriate inequality.**

5. **Explain Kuratowski's theorem. Identify whether the Petersen graph is planar or not.**

---

## 6. Isomorphism and Homeomorphism of Graphs

### Graph Isomorphism

- **Definition**
  - Graphs G₁ = (V₁, E₁) and G₂ = (V₂, E₂) are isomorphic
  - If bijection f: V₁ → V₂ exists
  - Such that (u, v) ∈ E₁ ⟺ (f(u), f(v)) ∈ E₂
  - Written as G₁ ≅ G₂

- **Necessary Conditions**
  - Same number of vertices (|V₁| = |V₂|)
  - Same number of edges (|E₁| = |E₂|)
  - Same degree sequence
  - Same number of cycles of each length
  - Preserve connectivity

- **Sufficient Condition**
  - Finding explicit bijection that preserves adjacency
  - Not always easy to verify

### Testing Isomorphism

- **Invariants (properties preserved)**
  - Number of vertices of each degree
  - Diameter and radius
  - Chromatic number
  - Number of spanning trees
  - Eigenvalues of adjacency matrix

- **Algorithm Complexity**
  - No polynomial-time algorithm known
  - Not proven to be NP-complete
  - Lies in complexity class GI

### Homeomorphism

- **Definition**
  - Graphs G₁ and G₂ are homeomorphic
  - If both can be obtained from same graph by inserting vertices into edges
  - Preserves topological structure

- **Elementary Subdivision**
  - Remove edge (u, v)
  - Add new vertex w
  - Add edges (u, w) and (w, v)

- **Properties**
  - Homeomorphic graphs have same planarity
  - Used in Kuratowski's theorem
  - Weaker than isomorphism

### Comparison

- **Isomorphism vs Homeomorphism**
  - Isomorphism: Exact structural equivalence
  - Homeomorphism: Topological equivalence
  - All isomorphic graphs are homeomorphic
  - Not all homeomorphic graphs are isomorphic

### Exam Questions

1. **Define graph isomorphism. Determine whether the following two graphs are isomorphic: G₁: vertices {1,2,3,4}, edges {(1,2), (2,3), (3,4), (4,1)} and G₂: vertices {a,b,c,d}, edges {(a,c), (c,b), (b,d), (d,a)}**

2. **List five necessary conditions for two graphs to be isomorphic. Are these conditions sufficient? Explain with an example.**

3. **What is the difference between graph isomorphism and graph homeomorphism? Give an example where two graphs are homeomorphic but not isomorphic.**

4. **Prove that if two graphs are isomorphic, they must have the same chromatic number.**

5. **How is graph isomorphism related to Kuratowski's theorem? Explain the role of homeomorphism in testing planarity.**

---

## 7. Euler and Hamiltonian Paths

### Euler Paths and Circuits

- **Definitions**
  - **Euler path**: Path that uses every edge exactly once
  - **Euler circuit**: Circuit that uses every edge exactly once
  - Named after Leonhard Euler (Königsberg bridge problem)

- **Existence Theorems**
  - **Euler circuit exists** ⟺ Graph is connected and all vertices have even degree
  - **Euler path exists** ⟺ Graph is connected and exactly 0 or 2 vertices have odd degree
  - If 2 odd-degree vertices exist, path starts at one and ends at other

- **Finding Euler Circuits**
  - **Fleury's Algorithm**: Remove edges carefully, avoid bridges unless necessary
  - **Hierholzer's Algorithm**: Follow arbitrary paths, merge cycles
  - Time complexity: O(|E|)

### Hamiltonian Paths and Circuits

- **Definitions**
  - **Hamiltonian path**: Path that visits every vertex exactly once
  - **Hamiltonian circuit**: Circuit that visits every vertex exactly once
  - Named after William Rowan Hamilton

- **Existence Conditions**
  - No simple necessary and sufficient condition exists
  - NP-complete problem to determine existence

- **Sufficient Conditions**
  - **Dirac's Theorem**: If G has n ≥ 3 vertices and deg(v) ≥ n/2 for all v, then G has Hamiltonian circuit
  - **Ore's Theorem**: If deg(u) + deg(v) ≥ n for all non-adjacent u, v, then G has Hamiltonian circuit
  - These are sufficient but not necessary

### Comparison

- **Euler vs Hamiltonian**
  - Euler: Focuses on edges
  - Hamiltonian: Focuses on vertices
  - Euler: Polynomial-time algorithms exist
  - Hamiltonian: NP-complete problem
  - Euler: Simple characterization
  - Hamiltonian: No simple characterization

### Applications

- **Euler Paths**
  - Route planning (traverse all roads)
  - Circuit design
  - DNA sequencing

- **Hamiltonian Paths**
  - Traveling salesman problem
  - Knight's tour on chessboard
  - Network routing

### Exam Questions

1. **State and prove the necessary and sufficient condition for the existence of an Euler circuit in a connected graph.**

2. **Determine whether the following graph has (a) Euler path (b) Euler circuit (c) Hamiltonian path (d) Hamiltonian circuit: Vertices {1,2,3,4,5}, Edges {(1,2), (2,3), (3,4), (4,5), (5,1), (1,3)}**

3. **Compare Euler circuits and Hamiltonian circuits in terms of definition, existence conditions, and computational complexity.**

4. **State Dirac's theorem and Ore's theorem. Use Dirac's theorem to prove that K₅ has a Hamiltonian circuit.**

5. **Explain why determining the existence of a Hamiltonian circuit is more difficult than determining the existence of an Euler circuit.**

---

## 8. Graph Coloring

### Vertex Coloring

- **Definition**
  - Assignment of colors to vertices
  - Adjacent vertices get different colors
  - Goal: Use minimum number of colors

- **Chromatic Number χ(G)**
  - Minimum number of colors needed
  - χ(Kₙ) = n (complete graph)
  - χ(Kₘ,ₙ) = 2 (bipartite graph)
  - χ(Cₙ) = 2 if n even, 3 if n odd (cycle)

### Important Theorems

- **Four Color Theorem**
  - Every planar graph can be colored with at most 4 colors
  - Proved using computer assistance (1976)
  - One of the most famous theorems in graph theory

- **Five Color Theorem**
  - Every planar graph can be colored with at most 5 colors
  - Has non-computer proof

- **Greedy Coloring**
  - Order vertices arbitrarily
  - Assign smallest available color to each vertex
  - Uses at most Δ + 1 colors (Δ = max degree)

- **Brooks' Theorem**
  - If G is connected and not complete or odd cycle
  - Then χ(G) ≤ Δ (max degree)

### Edge Coloring

- **Definition**
  - Assignment of colors to edges
  - Adjacent edges (sharing vertex) get different colors

- **Edge Chromatic Number χ'(G)**
  - Minimum colors needed for edge coloring
  - Δ ≤ χ'(G) ≤ Δ + 1 (Vizing's theorem)
  - Class 1 graphs: χ'(G) = Δ
  - Class 2 graphs: χ'(G) = Δ + 1

### Applications

- **Vertex Coloring**
  - Scheduling problems (time slots)
  - Register allocation in compilers
  - Frequency assignment in mobile networks
  - Sudoku puzzles

- **Edge Coloring**
  - Scheduling problems (time slots for meetings)
  - Timetabling
  - Sports scheduling

### Algorithms

- **Greedy Algorithm**
  - Simple, fast
  - Not always optimal
  - Approximation guarantee

- **Backtracking**
  - Explores all possibilities
  - Finds optimal solution
  - Exponential time complexity

### Exam Questions

1. **Define chromatic number. Find the chromatic number of (a) K₆ (b) K₃,₄ (c) C₇ (d) Petersen graph**

2. **State the Four Color Theorem and Five Color Theorem. Why is the Four Color Theorem significant in mathematics?**

3. **Prove that every bipartite graph has chromatic number at most 2. Is the converse true?**

4. **Explain the greedy coloring algorithm. What is the worst-case number of colors it might use for a graph with maximum degree Δ?**

5. **State Brooks' Theorem. Give an example of a graph where the chromatic number equals the maximum degree, and an example where it's less.**

---

## 9. Combinatorics: Introduction

### What is Combinatorics?

- **Definition**
  - Branch of mathematics dealing with counting, arrangement, and combination
  - Studies discrete structures
  - Foundation for probability and algorithm analysis

### Basic Principles

- **Rule of Sum (Addition Principle)**
  - If task A can be done in m ways
  - And task B can be done in n ways
  - And A and B cannot be done simultaneously
  - Then A OR B can be done in m + n ways

- **Rule of Product (Multiplication Principle)**
  - If task A can be done in m ways
  - And for each way, task B can be done in n ways
  - Then A AND B can be done in m × n ways

### Set Theory Basics

- **Fundamental Concepts**
  - Set: Collection of distinct objects
  - Subset: A ⊆ B (all elements of A in B)
  - Power set: Set of all subsets, |P(A)| = 2^|A|
  - Cartesian product: A × B = {(a,b) : a ∈ A, b ∈ B}

- **Principle of Inclusion-Exclusion**
  - |A ∪ B| = |A| + |B| - |A ∩ B|
  - |A ∪ B ∪ C| = |A| + |B| + |C| - |A ∩ B| - |A ∩ C| - |B ∩ C| + |A ∩ B ∩ C|
  - Generalizes to n sets

### Basic Counting Objects

- **Permutations**
  - Arrangement of objects in specific order
  - n objects: n! permutations
  - r objects from n: P(n,r) = n!/(n-r)!

- **Combinations**
  - Selection of objects without regard to order
  - r objects from n: C(n,r) = n!/(r!(n-r)!)
  - Also written as (n choose r) or ⁿCᵣ

### Exam Questions

1. **State and explain the Rule of Sum and Rule of Product with examples. How do you decide which principle to apply?**

2. **How many different 4-digit numbers can be formed using digits 1,2,3,4,5,6 if (a) repetition is allowed (b) repetition is not allowed?**

3. **Use the Principle of Inclusion-Exclusion to find the number of integers from 1 to 1000 that are divisible by 2, 3, or 5.**

4. **Prove that C(n,r) = C(n,n-r). Give a combinatorial interpretation of this identity.**

5. **How many subsets does a set with n elements have? Prove your answer.**

---

## 10. Counting Techniques

### Permutations

- **Simple Permutations**
  - P(n,r) = n!/(n-r)!
  - Arrangement of r objects from n distinct objects
  - Order matters

- **Permutations with Repetition**
  - n objects with repetitions allowed
  - Choose r positions: nʳ ways
  - Example: 4-digit PIN using 0-9: 10⁴ = 10,000

- **Circular Permutations**
  - Arranging n objects in a circle
  - (n-1)! ways
  - Fix one object to avoid rotational duplicates

- **Permutations with Identical Objects**
  - n objects with n₁ of type 1, n₂ of type 2, ..., nₖ of type k
  - Formula: n!/(n₁! × n₂! × ... × nₖ!)
  - Example: Letters in "MISSISSIPPI"

### Combinations

- **Simple Combinations**
  - C(n,r) = n!/(r!(n-r)!)
  - Selection of r objects from n
  - Order doesn't matter

- **Combinations with Repetition**
  - Choosing r objects from n types with repetition
  - Formula: C(n+r-1, r) = C(n+r-1, n-1)
  - Also called "stars and bars" method

### Binomial Theorem

- **Formula**
  - (x + y)ⁿ = Σ C(n,k) × xⁿ⁻ᵏ × yᵏ for k=0 to n
  - Binomial coefficients: C(n,k)

- **Properties**
  - C(n,0) + C(n,1) + ... + C(n,n) = 2ⁿ
  - C(n,r) = C(n-1,r-1) + C(n-1,r) (Pascal's identity)
  - Useful for generating functions

### Distribution Problems

- **Distinct Objects to Distinct Boxes**
  - n objects into r boxes: rⁿ ways
  - At most one per box: P(n,r) ways

- **Distinct Objects to Identical Boxes**
  - Stirling numbers of second kind S(n,r)
  - Partitioning n objects into r non-empty groups

- **Identical Objects to Distinct Boxes**
  - Stars and bars: C(n+r-1, r-1)
  - Example: Distributing 10 candies to 3 children

- **Identical Objects to Identical Boxes**
  - Partition numbers p(n,r)
  - Most complex case

### Exam Questions

1. **How many ways can 5 boys and 3 girls be arranged in a row if (a) no restrictions (b) boys and girls alternate (c) girls are together?**

2. **Find the number of distinct permutations of the letters in "ENGINEERING".**

3. **In how many ways can 10 identical books be distributed among 4 students if each student must get at least one book?**

4. **Prove Pascal's identity: C(n,r) = C(n-1,r-1) + C(n-1,r). Give both algebraic and combinatorial proofs.**

5. **Using binomial theorem, find the coefficient of x⁵ in the expansion of (2x + 3)⁸.**

---

## 11. Pigeonhole Principle

### Basic Principle

- **Statement**
  - If n+1 objects are placed into n boxes
  - At least one box contains at least 2 objects
  - Simple but powerful counting argument

- **Formal Statement**
  - If f: A → B and |A| > |B|
  - Then f is not injective (one-to-one)
  - At least two elements in A map to same element in B

### Generalized Pigeonhole Principle

- **Statement**
  - If n objects are placed into k boxes
  - At least one box contains at least ⌈n/k⌉ objects
  - ⌈x⌉ is ceiling function (smallest integer ≥ x)

- **Formula**
  - If n = qk + r where 0 ≤ r < k
  - At least one box has at least q+1 objects

### Applications

- **Number Theory**
  - Among n+1 integers, at least 2 have same remainder when divided by n
  - Birthday paradox: In 367 people, at least 2 share birthday

- **Graph Theory**
  - In any graph with n vertices, at least 2 vertices have same degree
  - In any group of 6 people, either 3 are mutual friends or 3 are mutual strangers

- **Combinatorial Problems**
  - Sequence problems
  - Existence proofs
  - Ramsey theory

### Problem-Solving Strategies

- **Identify Pigeons and Holes**
  - Pigeons: Objects to be placed
  - Holes: Categories or boxes
  - Key is choosing right categorization

- **Count Carefully**
  - Determine number of pigeons
  - Determine number of holes
  - Apply appropriate version of principle

### Advanced Applications

- **Ramsey Theory**
  - R(3,3) = 6: In group of 6 people, 3 mutual friends or strangers exist
  - Uses pigeonhole principle for existence proofs

- **Dirichlet's Approximation**
  - For any irrational α and integer N
  - Exists integers p, q with 1 ≤ q ≤ N such that |α - p/q| < 1/(qN)

### Exam Questions

1. **State the Pigeonhole Principle and Generalized Pigeonhole Principle. Give a real-world example of each.**

2. **Show that among any 13 people, at least 2 have birthdays in the same month.**

3. **Prove that in any group of 6 people, there must be 3 mutual acquaintances or 3 mutual strangers.**

4. **If 100 integers are selected from 1 to 200, prove that there must be two integers such that one divides the other.**

5. **Use the Pigeonhole Principle to prove that in any sequence of n² + 1 distinct numbers, there exists either an increasing subsequence or a decreasing subsequence of length n + 1.**

---

## LAST MINUTE SUMMARY - 1 PAGE

### QUICK FORMULAS REFERENCE

**Graph Theory Basics**
- Handshaking Theorem: Σ deg(v) = 2|E|
- Complete graph Kₙ: edges = n(n-1)/2
- Euler's Formula (planar): v - e + f = 2
- Planar inequality: e ≤ 3v - 6 (v ≥ 3)
- Bipartite planar: e ≤ 2v - 4

**Counting Formulas**
- Permutations: P(n,r) = n!/(n-r)!
- Combinations: C(n,r) = n!/[r!(n-r)!]
- Circular permutations: (n-1)!
- Permutations with repetition: nʳ
- With identical objects: n!/(n₁!n₂!...nₖ!)
- Stars and bars: C(n+r-1, r-1)
- Binomial: (x+y)ⁿ = Σ C(n,k)xⁿ⁻ᵏyᵏ

**Key Theorems**
- Pascal's Identity: C(n,r) = C(n-1,r-1) + C(n-1,r)
- Sum of combinations: Σ C(n,k) = 2ⁿ
- PIE (2 sets): |A∪B| = |A| + |B| - |A∩B|

### CRITICAL CONCEPTS

**Euler vs Hamiltonian**
- **Euler Path/Circuit**: Uses every EDGE once
  - Circuit exists ⟺ all even degrees
  - Path exists ⟺ exactly 0 or 2 odd degrees
- **Hamiltonian Path/Circuit**: Visits every VERTEX once
  - No simple test (NP-complete)
  - Dirac: deg(v) ≥ n/2 for all v → Has circuit

**Graph Coloring**
- Chromatic number χ(G): minimum colors needed
- χ(Kₙ) = n, χ(bipartite) = 2
- Four Color Theorem: planar graphs need ≤ 4 colors
- Greedy uses ≤ Δ + 1 colors

**Planarity Quick Check**
- K₅ and K₃,₃ are NON-planar
- Use e ≤ 3v - 6 to test
- If v=5, e≤9; K₅ has 10 edges → non-planar

**Bipartite Test**
- Graph is bipartite ⟺ no odd cycles
- Can be 2-colored
- Test using BFS with 2 colors

### PROBLEM-SOLVING TRICKS

**Graph Problems**
1. **Check degree sequence**: Sum must be even
2. **For planar**: Try Euler's formula first
3. **Isomorphism**: Compare degree sequences, cycle counts
4. **For paths**: Count odd-degree vertices

**Counting Problems**
1. **Order matters?** → Permutations
2. **Order doesn't matter?** → Combinations
3. **Repetition allowed?** → Use power rule (nʳ) or stars-and-bars
4. **At least one constraint?** → Use (total - none) or PIE
5. **Identical objects?** → Stars and bars C(n+r-1, r-1)

**Pigeonhole Applications**
1. **Identify pigeons and holes clearly**
2. **If n+1 pigeons, n holes** → At least 2 in one hole
3. **Generalized**: ⌈n/k⌉ in at least one hole
4. **Birthday problem**: 367 people → 2 share birthday
5. **Remainder trick**: n+1 numbers → 2 have same mod n

**Quick Decision Tree**
```
Graph Problem?
├─ Path using all edges? → Check Euler conditions
├─ Path visiting all vertices? → Check Hamiltonian (Dirac/Ore)
├─ Can draw without crossing? → Check planarity (e ≤ 3v-6)
├─ Can 2-color? → Check bipartite (no odd cycles)
└─ Minimum colors needed? → Find chromatic number

Counting Problem?
├─ Arrangements (order matters)? → Permutations P(n,r)
├─ Selections (order doesn't matter)? → Combinations C(n,r)
├─ Two tasks: AND or OR?
│   ├─ AND → Multiply (Rule of Product)
│   └─ OR → Add (Rule of Sum)
├─ Distribute objects?
│   ├─ Distinct → Distinct: rⁿ
│   ├─ Identical → Distinct: C(n+r-1, r-1)
│   └─ Check constraints carefully
└─ Existence proof? → Try Pigeonhole Principle
```

### COMMON EXAM MISTAKES TO AVOID

❌ **Graph Theory**
- Confusing vertices and edges in formulas
- Forgetting outer face in planar graphs (f includes it!)
- Using e ≤ 3v - 6 for v < 3 (only valid for v ≥ 3)
- Mixing up Euler (edges) and Hamiltonian (vertices)
- Forgetting loops count 2 toward degree

❌ **Combinatorics**
- Using permutation when combination needed (check if order matters!)
- Forgetting to subtract in inclusion-exclusion
- Not accounting for "at least one" constraints
- Circular permutation: use (n-1)! not n!
- Stars and bars: C(n+r-1, r-1) NOT C(n+r, r)

### MUST-REMEMBER FACTS

**Graph Theory**
✓ Odd-degree vertices always come in pairs
✓ K₅ and K₃,₃ → non-planar (memorize these!)
✓ Complete graph Kₙ: n(n-1)/2 edges, all vertices degree n-1
✓ Tree with n vertices has exactly n-1 edges
✓ Bipartite ⟺ no odd cycles ⟺ 2-colorable
✓ Planar → at most 3v-6 edges (v≥3)

**Combinatorics**
✓ 0! = 1 (important for formulas!)
✓ C(n,0) = C(n,n) = 1
✓ C(n,1) = n, C(n,2) = n(n-1)/2
✓ Sum of row in Pascal's triangle = 2ⁿ
✓ Power set of n elements: 2ⁿ subsets
✓ Pigeonhole: n+1 pigeons, n holes → collision guaranteed

### RAPID-FIRE PRACTICE CHECKS

**Can you answer instantly?**
1. K₇ has how many edges? **Answer: 21** [7×6/2]
2. Graph with all even degrees has Euler? **Yes (if connected)**
3. Can K₅ be drawn on plane? **No (non-planar)**
4. χ(K₄,₃) = ? **Answer: 2** (bipartite)
5. Ways to arrange AABBCC? **Answer: 90** [6!/(2!2!2!)]
6. C(10,3) = ? **Answer: 120** [10×9×8/6]
7. 50 people, at least 2 same birthday month? **Yes (Pigeonhole)**
8. Complete bipartite K₅,₇ edges? **Answer: 35** [5×7]

### FINAL EXAM STRATEGY

**Time Management**
- Proofs (Euler's formula, bipartite): 10-15 min each
- Calculations (counting): 5-7 min each
- True/False with justification: 3-5 min each
- Drawing graphs: 5 min each

**High-Yield Topics** (likely to appear)
1. ⭐ Euler path/circuit conditions + finding one
2. ⭐ Planarity testing (Euler's formula application)
3. ⭐ Permutations with identical objects
4. ⭐ Combinations with/without repetition
5. ⭐ Pigeonhole Principle applications
6. ⭐ Graph coloring + chromatic number
7. ⭐ Bipartite graph identification

**Before You Start**
✓ Write down key formulas on rough paper
✓ Read question twice before solving
✓ Show all steps (partial credit!)
✓ Check if your answer makes logical sense
✓ Verify degree sum is even in graph problems
✓ Double-check factorial calculations

**Last Hour Revision**
1. Handshaking theorem + applications (15 min)
2. Euler's formula + planarity tests (15 min)
3. All counting formulas + 2-3 problems (20 min)
4. Pigeonhole principle examples (10 min)

---

## END OF NOTES

**Good luck with your exam! 🎯**

*Remember: Understanding > Memorization. Focus on WHY formulas work, not just WHAT they are.*