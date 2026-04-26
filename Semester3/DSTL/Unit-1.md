# Set Theory & Relations - Comprehensive Notes

---

## 1. Set Theory: Introduction

### Basic Concepts
- **Set**: A well-defined collection of distinct objects
  - Objects in a set are called **elements** or **members**
  - Notation: A = {1, 2, 3, 4, 5}
  - Element notation: a ∈ A (a belongs to A), b ∉ A (b does not belong to A)

### Types of Sets
- **Finite Set**: Contains countable number of elements
  - Example: A = {1, 2, 3}
- **Infinite Set**: Contains unlimited elements
  - Example: N = {1, 2, 3, 4, ...}
- **Empty/Null Set**: Contains no elements
  - Notation: ∅ or {}
- **Singleton Set**: Contains exactly one element
  - Example: A = {5}
- **Universal Set**: Set containing all elements under consideration
  - Notation: U or ξ
- **Subset**: A ⊆ B if every element of A is in B
  - **Proper Subset**: A ⊂ B if A ⊆ B and A ≠ B
- **Power Set**: Set of all subsets of a set A
  - Notation: P(A) or 2^A
  - If |A| = n, then |P(A)| = 2^n

### Set Representation Methods
- **Roster/Tabular Form**: List all elements
  - Example: A = {2, 4, 6, 8}
- **Set-Builder Form**: Define property of elements
  - Example: A = {x | x is an even number less than 10}
- **Venn Diagram**: Visual representation using circles/shapes

---

## 2. Combination of Sets

### Basic Operations

#### Union (∪)
- **Definition**: A ∪ B = {x | x ∈ A or x ∈ B}
- Combines all elements from both sets
- Example: {1, 2} ∪ {2, 3} = {1, 2, 3}
- **Properties**:
  - Commutative: A ∪ B = B ∪ A
  - Associative: (A ∪ B) ∪ C = A ∪ (B ∪ C)
  - Identity: A ∪ ∅ = A
  - Idempotent: A ∪ A = A

#### Intersection (∩)
- **Definition**: A ∩ B = {x | x ∈ A and x ∈ B}
- Contains common elements from both sets
- Example: {1, 2, 3} ∩ {2, 3, 4} = {2, 3}
- **Properties**:
  - Commutative: A ∩ B = B ∩ A
  - Associative: (A ∩ B) ∩ C = A ∩ (B ∩ C)
  - Identity: A ∩ U = A
  - Idempotent: A ∩ A = A

#### Difference (−)
- **Definition**: A − B = {x | x ∈ A and x ∉ B}
- Elements in A but not in B
- Example: {1, 2, 3} − {2, 3, 4} = {1}
- **Properties**:
  - NOT Commutative: A − B ≠ B − A
  - A − ∅ = A
  - A − A = ∅

#### Complement (A' or Ā)
- **Definition**: A' = U − A = {x | x ∈ U and x ∉ A}
- All elements in universal set but not in A
- **Properties**:
  - (A')' = A
  - A ∪ A' = U
  - A ∩ A' = ∅
  - U' = ∅ and ∅' = U

#### Symmetric Difference (⊕ or Δ)
- **Definition**: A ⊕ B = (A − B) ∪ (B − A) = (A ∪ B) − (A ∩ B)
- Elements in either A or B but not in both
- Example: {1, 2, 3} ⊕ {2, 3, 4} = {1, 4}
- **Properties**:
  - Commutative: A ⊕ B = B ⊕ A
  - Associative: (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)

#### Cartesian Product (×)
- **Definition**: A × B = {(a, b) | a ∈ A and b ∈ B}
- Set of all ordered pairs
- Example: {1, 2} × {a, b} = {(1,a), (1,b), (2,a), (2,b)}
- **Properties**:
  - |A × B| = |A| × |B|
  - NOT Commutative: A × B ≠ B × A
  - A × ∅ = ∅

### Important Laws

#### De Morgan's Laws
- (A ∪ B)' = A' ∩ B'
- (A ∩ B)' = A' ∪ B'

#### Distributive Laws
- A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)
- A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)

#### Absorption Laws
- A ∪ (A ∩ B) = A
- A ∩ (A ∪ B) = A

### Exam-Focused Questions

1. **Prove De Morgan's Law**: (A ∪ B)' = A' ∩ B' using Venn diagrams or algebraic method.

2. **Given**: U = {1, 2, 3, 4, 5, 6, 7, 8}, A = {1, 2, 3, 4}, B = {3, 4, 5, 6}. Find:
   - A ∪ B
   - A ∩ B
   - A − B
   - A ⊕ B
   - (A ∪ B)'

3. **Show that**: A − (B ∪ C) = (A − B) ∩ (A − C) using set theory laws.

4. **If** |A| = 3 and |B| = 4, find:
   - |A × B|
   - |P(A)|
   - Number of proper subsets of A

5. **Simplify**: (A ∪ B) ∩ (A ∪ B') using Boolean algebra of sets.

---

## 3. Relations: Definition

### Basic Concept
- **Relation**: A subset of Cartesian product A × B
  - Notation: R ⊆ A × B
  - If (a, b) ∈ R, we write aRb
  - R: A → B denotes a relation from A to B

### Types of Relations

#### Based on Sets
- **Binary Relation**: Relation from set A to set B
- **Relation on a Set**: R ⊆ A × A (same set)
- **Empty Relation**: R = ∅
- **Universal Relation**: R = A × A (all possible ordered pairs)

#### Special Relations
- **Identity Relation**: I_A = {(a, a) | a ∈ A}
  - Every element related to itself only
- **Inverse Relation**: R^(-1) = {(b, a) | (a, b) ∈ R}
  - Reverse all ordered pairs

### Domain, Range, and Co-domain
- **Domain**: Set of all first elements
  - Dom(R) = {a | (a, b) ∈ R for some b ∈ B}
- **Range**: Set of all second elements
  - Range(R) = {b | (a, b) ∈ R for some a ∈ A}
- **Co-domain**: The set B in R: A → B

### Number of Relations
- Number of possible relations from A to B = 2^(|A|×|B|)
- If |A| = m and |B| = n, then number of relations = 2^(mn)

---

## 4. Operations on Relations

### Union of Relations
- **Definition**: R₁ ∪ R₂ = {(a, b) | (a, b) ∈ R₁ or (a, b) ∈ R₂}
- Example: R₁ = {(1,2), (2,3)}, R₂ = {(2,3), (3,4)}
  - R₁ ∪ R₂ = {(1,2), (2,3), (3,4)}

### Intersection of Relations
- **Definition**: R₁ ∩ R₂ = {(a, b) | (a, b) ∈ R₁ and (a, b) ∈ R₂}
- Contains common ordered pairs

### Difference of Relations
- **Definition**: R₁ − R₂ = {(a, b) | (a, b) ∈ R₁ and (a, b) ∉ R₂}

### Complement of Relation
- **Definition**: R' = (A × B) − R
- All pairs not in R

### Inverse Relation
- **Definition**: R^(-1) = {(b, a) | (a, b) ∈ R}
- **Properties**:
  - (R^(-1))^(-1) = R
  - Dom(R^(-1)) = Range(R)
  - Range(R^(-1)) = Dom(R)

---

## 5. Properties of Relations

### Reflexive Relation
- **Definition**: ∀a ∈ A, (a, a) ∈ R
- Every element related to itself
- Example: "is equal to" (=)
- **Check**: All diagonal elements (a, a) must be present

### Irreflexive Relation
- **Definition**: ∀a ∈ A, (a, a) ∉ R
- No element related to itself
- Example: "is less than" (<)

### Symmetric Relation
- **Definition**: If (a, b) ∈ R, then (b, a) ∈ R
- Example: "is sibling of"
- **Matrix Check**: Matrix = Matrix transpose

### Antisymmetric Relation
- **Definition**: If (a, b) ∈ R and (b, a) ∈ R, then a = b
- Example: "is less than or equal to" (≤)
- Can have (a, a) but not both (a, b) and (b, a) if a ≠ b

### Asymmetric Relation
- **Definition**: If (a, b) ∈ R, then (b, a) ∉ R
- Example: "is less than" (<)
- Implies irreflexive and antisymmetric

### Transitive Relation
- **Definition**: If (a, b) ∈ R and (b, c) ∈ R, then (a, c) ∈ R
- Example: "is ancestor of"
- **Check**: Closure under composition

### Important Combinations

#### Equivalence Relation
- Must be: **Reflexive + Symmetric + Transitive**
- Example: Equality (=), Congruence modulo n
- **Partitions** the set into equivalence classes

#### Partial Order Relation (Poset)
- Must be: **Reflexive + Antisymmetric + Transitive**
- Example: ≤ on real numbers, ⊆ on sets
- Denoted as (A, ≤) or (A, ⪯)

#### Total/Linear Order
- Partial order where every pair is comparable
- ∀a, b ∈ A, either a ≤ b or b ≤ a

### Exam-Focused Questions

1. **Determine properties**: Given R = {(1,1), (2,2), (3,3), (1,2), (2,1)} on A = {1, 2, 3}. Check if R is reflexive, symmetric, antisymmetric, and transitive.

2. **Prove**: If R is symmetric and transitive, and ∀a ∈ A, ∃b such that (a,b) ∈ R, then R is reflexive.

3. **Find equivalence classes**: For relation R on Z defined by aRb if a − b is divisible by 3. Show R is an equivalence relation and find equivalence classes.

4. **Given**: R is a relation on set {1, 2, 3, 4} such that R is reflexive and symmetric. What is the minimum number of ordered pairs R must contain?

5. **Show**: If R₁ and R₂ are equivalence relations on set A, then R₁ ∩ R₂ is also an equivalence relation.

---

## 6. Composite Relations

### Definition
- **Composite Relation (R₁ ∘ R₂)**: If R₁: A → B and R₂: B → C
  - R₂ ∘ R₁ = {(a, c) | ∃b ∈ B such that (a, b) ∈ R₁ and (b, c) ∈ R₂}
  - Read "R₂ following R₁" or "R₂ composed with R₁"

### Computing Composition
- Find intermediate element b
- (a, b) must be in first relation
- (b, c) must be in second relation
- Result contains (a, c)

### Example
- R₁ = {(1, 2), (1, 3), (2, 4)}
- R₂ = {(2, 5), (3, 6), (4, 5)}
- R₂ ∘ R₁ = {(1, 5), (1, 6), (2, 5)}

### Properties
- **Associative**: (R₃ ∘ R₂) ∘ R₁ = R₃ ∘ (R₂ ∘ R₁)
- **NOT Commutative**: R₂ ∘ R₁ ≠ R₁ ∘ R₂ (in general)
- **Identity**: R ∘ I_A = I_B ∘ R = R

### Powers of Relations
- **R^n** = R ∘ R ∘ ... ∘ R (n times)
- R^1 = R
- R^2 = R ∘ R
- R^(n+1) = R^n ∘ R

### Matrix Representation
- Relations can be represented as Boolean matrices
- Composition = Boolean matrix multiplication
- Use AND (∧) for multiplication, OR (∨) for addition

---

## 7. Equality of Relations

### Definition
- **Two relations R₁ and R₂ are equal** if:
  - R₁ ⊆ R₂ and R₂ ⊆ R₁
  - i.e., R₁ = R₂ ⟺ ∀(a, b), (a, b) ∈ R₁ ⟺ (a, b) ∈ R₂

### Checking Equality
- Both must have same domain
- Both must have same range
- All ordered pairs must be identical

### Example
- R₁ = {(1, 2), (2, 3)} and R₂ = {(2, 3), (1, 2)}
- R₁ = R₂ (order doesn't matter in sets)

### Properties
- Reflexive: R = R
- Symmetric: If R₁ = R₂, then R₂ = R₁
- Transitive: If R₁ = R₂ and R₂ = R₃, then R₁ = R₃

---

## 8. Recursive Definition of Relations

### Concept
- Define relation in terms of itself
- Base case + Recursive step

### Transitive Closure
- **Definition**: Smallest transitive relation containing R
- Denoted as R⁺ or R^*
- R⁺ = R ∪ R² ∪ R³ ∪ ... ∪ R^n
- For finite sets: R⁺ = R ∪ R² ∪ ... ∪ R^n where n = |A|

### Methods to Find Transitive Closure

#### Warshall's Algorithm
- Efficient algorithm: O(n³)
- Uses dynamic programming approach
- Steps:
  1. Create adjacency matrix M from relation R
  2. For k = 1 to n:
     - For i = 1 to n:
       - For j = 1 to n:
         - M[i][j] = M[i][j] OR (M[i][k] AND M[k][j])

#### Path Method
- Find all paths of length 1, 2, 3, ..., n
- Union of all these paths

### Reflexive Closure
- Smallest reflexive relation containing R
- R⁰ = R ∪ I_A (add all diagonal elements)

### Symmetric Closure
- Smallest symmetric relation containing R
- R^s = R ∪ R^(-1) (add inverse pairs)

### Example
- R = {(1, 2), (2, 3)}
- Transitive closure: R⁺ = {(1, 2), (2, 3), (1, 3)}

---

## 9. Order of Relations

### Partial Order (Poset)
- **Definition**: A relation that is reflexive, antisymmetric, and transitive
- Notation: (A, ≤) or (A, ⪯)
- Example: (P(S), ⊆) - power set with subset relation

### Comparable Elements
- Elements a, b are **comparable** if a ≤ b or b ≤ a
- Otherwise, they are **incomparable**

### Special Elements in Poset

#### Maximal Element
- Element a is **maximal** if:
  - ∀b ∈ A, a ≤ b ⟹ a = b
  - No element greater than a

#### Minimal Element
- Element a is **minimal** if:
  - ∀b ∈ A, b ≤ a ⟹ a = b
  - No element smaller than a

#### Greatest Element (Maximum)
- Element a is **greatest** if:
  - ∀b ∈ A, b ≤ a
  - All elements are ≤ a
  - Unique if it exists

#### Least Element (Minimum)
- Element a is **least** if:
  - ∀b ∈ A, a ≤ b
  - a is ≤ all elements
  - Unique if it exists

#### Upper Bound
- For subset B ⊆ A, element u is **upper bound** if:
  - ∀b ∈ B, b ≤ u

#### Lower Bound
- For subset B ⊆ A, element l is **lower bound** if:
  - ∀b ∈ B, l ≤ b

#### Least Upper Bound (LUB/Supremum)
- Smallest element among all upper bounds
- Notation: sup(B) or ⋁B

#### Greatest Lower Bound (GLB/Infimum)
- Greatest element among all lower bounds
- Notation: inf(B) or ⋀B

### Total/Linear Order
- Poset where all pairs are comparable
- ∀a, b ∈ A, either a ≤ b or b ≤ a
- Example: (ℝ, ≤), (ℕ, ≤)

### Well-Ordered Set
- Total order where every non-empty subset has a least element
- Example: (ℕ, ≤) is well-ordered

### Exam-Focused Questions

1. **Consider** the poset (P({1, 2, 3}), ⊆). Draw the Hasse diagram and identify maximal, minimal, greatest, and least elements.

2. **Find**: LUB and GLB of {6, 8, 12} in the poset (D₃₆, |) where D₃₆ is the set of divisors of 36 and | is the "divides" relation.

3. **Prove**: In a finite poset, every maximal chain has the same length if and only if the poset is graded.

4. **Given**: A = {2, 3, 4, 6, 12, 24, 36} with relation "divides". Is this a total order? Justify.

5. **Show**: If a poset has a greatest element, then it is unique. Similarly for least element.

---

## 10. Hasse Diagram

### Definition
- **Hasse Diagram**: Graphical representation of a finite poset
- Simplifies visualization by removing:
  - Reflexive edges (loops)
  - Transitive edges (redundant connections)
  - Direction arrows (use vertical positioning instead)

### Construction Rules
1. **Draw elements** as vertices
2. **Position**: If a < b, draw a higher than b
3. **Connect** a to b with a line if:
   - a < b (a is related to b)
   - No c exists such that a < c < b (no intermediate element)
4. **Remove** all self-loops
5. **Remove** all arrows (direction is bottom to top)

### Reading Hasse Diagrams
- **a ≤ b** if there's an upward path from a to b
- **Comparable**: Path exists between elements
- **Incomparable**: No path exists

### Example
- Set A = {1, 2, 3, 6} with divides relation (|)
- Hasse Diagram:
  ```
       6
      / \
     2   3
      \ /
       1
  ```

### Advantages
- Clear visualization
- Easy identification of maximal/minimal elements
- Quick comparison of elements
- Space-efficient representation

### Applications
- Analyzing lattices
- Finding LUB and GLB
- Identifying order properties
- Set containment visualization

---

## 11. POSET (Partially Ordered Set)

### Formal Definition
- **POSET**: An ordered pair (A, ≤) where:
  - A is a non-empty set
  - ≤ is a partial order relation on A

### Properties Review
1. **Reflexive**: a ≤ a for all a ∈ A
2. **Antisymmetric**: If a ≤ b and b ≤ a, then a = b
3. **Transitive**: If a ≤ b and b ≤ c, then a ≤ c

### Examples of Posets
- **(ℕ, ≤)**: Natural numbers with standard ordering
- **(P(S), ⊆)**: Power set with subset relation
- **(D_n, |)**: Divisors of n with "divides" relation
- **(ℝ, ≤)**: Real numbers

### Chain
- **Chain**: Totally ordered subset
- Every pair of elements is comparable
- **Maximal Chain**: Cannot be extended
- **Length**: Number of edges in chain

### Antichain
- **Antichain**: Subset where no two elements are comparable
- Example: {2, 3, 5} in (ℕ, |)
- **Width**: Size of maximum antichain

### Dilworth's Theorem
- Minimum number of chains to cover poset = width of poset

### Covering Relation
- **a covers b** (b ⋖ a) if:
  - b < a
  - No c exists with b < c < a
- Used to construct Hasse diagrams

---

## 12. Lattices: Definition & Types

### Definition
- **Lattice**: A poset (L, ≤) where every pair {a, b} has:
  - **LUB (Join)**: a ∨ b (least upper bound)
  - **GLB (Meet)**: a ∧ b (greatest lower bound)

### Algebraic Definition
- Lattice (L, ∨, ∧) where:
  - ∨ (join) and ∧ (meet) are binary operations
  - Both operations are:
    - Commutative
    - Associative
    - Idempotent
  - Absorption laws hold

### Lattice Properties

#### Idempotent Laws
- a ∨ a = a
- a ∧ a = a

#### Commutative Laws
- a ∨ b = b ∨ a
- a ∧ b = b ∧ a

#### Associative Laws
- (a ∨ b) ∨ c = a ∨ (b ∨ c)
- (a ∧ b) ∧ c = a ∧ (b ∧ c)

#### Absorption Laws
- a ∨ (a ∧ b) = a
- a ∧ (a ∨ b) = a

### Sublattice
- Subset S of lattice L is a **sublattice** if:
  - Closed under ∨ and ∧ operations
  - For a, b ∈ S: a ∨ b ∈ S and a ∧ b ∈ S

---

## 13. Bounded Lattice

### Definition
- **Bounded Lattice**: Lattice with:
  - **Greatest element** (1 or ⊤): ∀a ∈ L, a ≤ 1
  - **Least element** (0 or ⊥): ∀a ∈ L, 0 ≤ a

### Properties
- **0 ∨ a = a** for all a (identity for join)
- **1 ∧ a = a** for all a (identity for meet)
- **0 ∧ a = 0** for all a
- **1 ∨ a = 1** for all a

### Example
- (P(S), ⊆) is bounded with:
  - 0 = ∅ (empty set)
  - 1 = S (universal set)

### Notation
- Bounded lattice: (L, ∨, ∧, 0, 1)

---

## 14. Complemented Lattice

### Definition
- **Complemented Lattice**: Bounded lattice where every element has a complement
- For each a ∈ L, ∃a' such that:
  - **a ∨ a' = 1** (upper bound property)
  - **a ∧ a' = 0** (lower bound property)

### Properties of Complements
- Complement may not be unique (unless distributive)
- **0' = 1** and **1' = 0**
- If lattice is distributive, complement is unique

### Uniqueness
- In distributive lattice: if a' and a'' are complements of a, then a' = a''

### Example
- (P(S), ⊆) is complemented with:
  - A' = S − A (set complement)

### Boolean Algebra
- **Boolean Algebra**: Complemented distributive lattice
- Satisfies De Morgan's laws:
  - (a ∨ b)' = a' ∧ b'
  - (a ∧ b)' = a' ∨ b'

---

## 15. Distributed Lattice

### Definition
- **Distributive Lattice**: Lattice satisfying distributive laws:
  - **a ∧ (b ∨ c) = (a ∧ b) ∨ (a ∧ c)**
  - **a ∨ (b ∧ c) = (a ∨ b) ∧ (a ∨ c)**

### Properties
- If one distributive law holds, the other also holds
- Every chain is a distributive lattice
- Complements are unique in distributive lattices

### Theorem
- A lattice is distributive if and only if it contains neither:
  - Diamond sublattice (M₃)
  - Pentagon sublattice (N₅)

### Non-Distributive Lattices
- **Diamond (M₃)**:
  ```
       1
      /|\
     a b c
      \|/
       0
  ```
  - Example where distributivity fails

- **Pentagon (N₅)**:
  ```
       1
       |
       a
      / \
     b   c
      \ /
       0
  ```

### Examples
- (ℕ, |): Distributive
- (P(S), ⊆): Distributive
- Divisor lattices: Generally distributive

---

## 16. Modular Lattice

### Definition
- **Modular Lattice**: Lattice satisfying modular law:
  - **If a ≤ c, then a ∨ (b ∧ c) = (a ∨ b) ∧ c**

### Properties
- Every distributive lattice is modular
- Not every modular lattice is distributive
- Diamond (M₃) is modular but not distributive

### Relationship Hierarchy
```
Distributive → Modular → General Lattice
```

### Theorem
- A lattice is modular if and only if it does not contain pentagon (N₅) as sublattice

### Dedekind's Modular Law
- Alternative form: a ≤ c ⟹ a ∨ (b ∧ c) = (a ∨ b) ∧ c

### Applications
- Vector spaces
- Subgroup lattices
- Projective geometry

---

## 17. Complete Lattice

### Definition
- **Complete Lattice**: Lattice where every subset S has:
  - **Supremum (LUB)**: ⋁S
  - **Infimum (GLB)**: ⋀S

### Properties
- Every complete lattice is bounded
  - 0 = ⋀L (infimum of all elements)
  - 1 = ⋁L (supremum of all elements)
- Finite lattices are always complete

### Completeness vs Boundedness
- **Bounded ≠ Complete** (for infinite lattices)
- **Complete ⟹ Bounded** (always true)

### Examples
- **Complete**: (P(S), ⊆) for any set S
- **Not Complete**: (ℚ, ≤) - rationals lack supremum for some subsets
- **Complete**: (ℝ, ≤) - reals are complete

### Knaster-Tarski Theorem
- Every monotone function on complete lattice has a fixed point
- Used in programming language semantics

### Chain-Complete Lattice
- **CPO (Complete Partial Order)**: Every chain has supremum
- Weaker than complete lattice
- Important in domain theory

### Exam-Focused Questions

1. **Prove**: Every distributive lattice is modular. Give an example of a modular lattice that is not distributive.

2. **Given** lattice (D₃₀, |) where D₃₀ = {1, 2, 3, 5, 6, 10, 15, 30}:
   - Draw Hasse diagram
   - Check if it's distributive
   - Check if it's complemented
   - Find complement of 6 if it exists

3. **Show**: In a complemented distributive lattice, complements are unique.

4. **Determine**: Which of the following are complete lattices?
   - (ℕ, ≤)
   - (P(S), ⊆)
   - ({1, 2, 3, 6}, |)
   - Open interval (0, 1) with ≤

5. **Verify** absorption laws for lattice operations on the set {1, 2, 3, 6, 9, 18} with divisibility relation.

---

## Quick Reference Summary

### Relation Properties Checklist
- ✓ **Reflexive**: Every (a,a) present
- ✓ **Symmetric**: (a,b) ⟹ (b,a)
- ✓ **Transitive**: (a,b) and (b,c) ⟹ (a,c)
- ✓ **Antisymmetric**: (a,b) and (b,a) ⟹ a=b
- ✓ **Equivalence** = Reflexive + Symmetric + Transitive
- ✓ **Partial Order** = Reflexive + Antisymmetric + Transitive

### Lattice Types Hierarchy
```
Complete Lattice
    ↓
Bounded Lattice
    ↓
Distributive Lattice → Boolean Algebra (if complemented)
    ↓
Modular Lattice
    ↓
Lattice
    ↓
POSET
```

### Important Formulas
- Number of relations from A to B: **2^(|A|×|B|)**
- Number of subsets: **|P(A)| = 2^|A|**
- Transitive closure: **R⁺ = R ∪ R² ∪ ... ∪ R^n**

---

## 🚀 LAST MINUTE REVISION SHEET - 1 PAGE SUMMARY

### 📐 ESSENTIAL FORMULAS

#### Set Operations
- **Number of relations**: A to B = `2^(|A|×|B|)`
- **Power set size**: `|P(A)| = 2^|A|`
- **Cartesian product size**: `|A × B| = |A| × |B|`
- **Inclusion-Exclusion**: `|A ∪ B| = |A| + |B| - |A ∩ B|`
- **De Morgan's Laws**: 
  - `(A ∪ B)' = A' ∩ B'`
  - `(A ∩ B)' = A' ∪ B'`

#### Relations
- **Transitive Closure**: `R⁺ = R ∪ R² ∪ R³ ∪ ... ∪ R^n` (for n = |A|)
- **Inverse**: `R^(-1) = {(b,a) | (a,b) ∈ R}`
- **Composition**: `R₂ ∘ R₁ = {(a,c) | ∃b: (a,b)∈R₁ and (b,c)∈R₂}`

#### Lattice Operations
- **Absorption Laws**: 
  - `a ∨ (a ∧ b) = a`
  - `a ∧ (a ∨ b) = a`
- **Distributive Laws**: 
  - `a ∧ (b ∨ c) = (a ∧ b) ∨ (a ∧ c)`
  - `a ∨ (b ∧ c) = (a ∨ b) ∧ (a ∨ c)`
- **Modular Law**: `If a ≤ c, then a ∨ (b ∧ c) = (a ∨ b) ∧ c`
- **Complement Laws**: 
  - `a ∨ a' = 1`
  - `a ∧ a' = 0`

---

### 🎯 KEY CONCEPTS - QUICK CHECK

#### Relation Properties (Most Tested!)
| Property | Condition | Example |
|----------|-----------|---------|
| **Reflexive** | (a,a) ∈ R for all a | = (equals) |
| **Symmetric** | (a,b) ∈ R ⟹ (b,a) ∈ R | "is sibling of" |
| **Transitive** | (a,b), (b,c) ∈ R ⟹ (a,c) ∈ R | < (less than) |
| **Antisymmetric** | (a,b), (b,a) ∈ R ⟹ a=b | ≤ (less than or equal) |

**🔑 Golden Combinations:**
- **Equivalence Relation** = Reflexive + Symmetric + Transitive
- **Partial Order (POSET)** = Reflexive + Antisymmetric + Transitive

#### POSET Elements (Know Differences!)
- **Maximal**: No element greater than it (can be multiple)
- **Maximum/Greatest**: Greater than ALL elements (unique if exists)
- **Minimal**: No element smaller than it (can be multiple)
- **Minimum/Least**: Smaller than ALL elements (unique if exists)
- **Upper Bound**: Element ≥ all elements in subset
- **LUB (Join)**: Smallest upper bound = a ∨ b
- **Lower Bound**: Element ≤ all elements in subset
- **GLB (Meet)**: Greatest lower bound = a ∧ b

#### Lattice Hierarchy (Remember This!)
```
Complete Lattice (every subset has LUB & GLB)
    ↓
Bounded Lattice (has 0 and 1)
    ↓
Distributive Lattice (a∧(b∨c) = (a∧b)∨(a∧c))
    ↓ (if complemented)
Boolean Algebra (complements + distributive)
    ↓
Modular Lattice (weaker than distributive)
    ↓
Lattice (every pair has LUB & GLB)
    ↓
POSET (partial order)
```

---

### 💡 EXAM TRICKS & TIPS

#### ✅ Quick Verification Tricks

**1. Check Reflexive (Matrix Method):**
   - All diagonal elements must be 1
   - Check (1,1), (2,2), (3,3)...

**2. Check Symmetric (Matrix Method):**
   - Matrix = Matrix transpose
   - If M[i][j] = 1, then M[j][i] must = 1

**3. Check Transitive (Warshall's Algorithm):**
   - If (a,b) and (b,c) exist, (a,c) must exist
   - For small sets: check all paths manually

**4. Identify Lattice Type:**
   - Has 0 and 1? → **Bounded**
   - Every element has complement? → **Complemented**
   - Passes distributive law? → **Distributive**
   - Distributive + Complemented → **Boolean Algebra**

**5. Hasse Diagram Shortcuts:**
   - Remove self-loops (reflexive)
   - Remove arrows showing transitivity
   - Draw higher elements above lower ones
   - Connect only immediate successors

#### 🎓 Common Exam Patterns

**Pattern 1: Prove Relation is Equivalence**
- Step 1: Show reflexive (all (a,a) present)
- Step 2: Show symmetric (prove if (a,b) then (b,a))
- Step 3: Show transitive (prove chain property)
- Bonus: Find equivalence classes (partition the set)

**Pattern 2: Find Transitive Closure**
- Method A: Compute R, R², R³... until no new pairs
- Method B: Use Warshall's algorithm for matrix
- Remember: Stop when R^n = R^(n-1)

**Pattern 3: Draw Hasse Diagram from Relation**
- List all pairs in relation
- Remove reflexive pairs (a,a)
- Remove transitive pairs if direct path exists
- Arrange vertically (smaller at bottom)

**Pattern 4: Prove Lattice Properties**
- Check every pair has LUB and GLB
- Verify using Hasse diagram or operation table
- For distributive: test a∧(b∨c) = (a∧b)∨(a∧c)

#### ⚠️ Common Mistakes to Avoid

1. **Antisymmetric ≠ NOT Symmetric**
   - Can have (a,a) pairs in antisymmetric
   - Example: ≤ is antisymmetric but not "not symmetric"

2. **Maximal ≠ Maximum**
   - Maximal: nothing above it (can be multiple)
   - Maximum: above everything (unique)

3. **Composition Order Matters**
   - R₂ ∘ R₁ ≠ R₁ ∘ R₂ (not commutative!)
   - Read right to left: R₂ ∘ R₁ means "do R₁ first"

4. **Distributive ⟹ Modular, but NOT vice versa**
   - Diamond (M₃) is modular but NOT distributive

5. **Complete Lattice (infinite) ≠ Bounded Lattice**
   - Finite lattices are always complete
   - Infinite bounded lattice may not be complete

---

### 🔥 MEMORIZE THESE

**Set Laws (Most Tested):**
- Idempotent: A ∪ A = A, A ∩ A = A
- Identity: A ∪ ∅ = A, A ∩ U = A
- Complement: A ∪ A' = U, A ∩ A' = ∅
- Absorption: A ∪ (A ∩ B) = A

**Relation Closures:**
- Reflexive Closure: R ∪ I_A
- Symmetric Closure: R ∪ R^(-1)
- Transitive Closure: R ∪ R² ∪ R³ ∪ ...

**Lattice Must-Knows:**
- Every lattice has: Join (∨) and Meet (∧)
- Bounded has: 0 (least) and 1 (greatest)
- Boolean Algebra = Complemented + Distributive + Bounded
- Pentagon (N₅) → NOT modular, NOT distributive
- Diamond (M₃) → Modular, NOT distributive

---

### ⏰ 5-Minute Before Exam Checklist

✓ Properties: Reflexive (all diagonals), Symmetric (mirror), Transitive (chain)
✓ Equivalence = R + S + T | Partial Order = R + A + T
✓ Hasse: Remove loops, remove transitive edges, no arrows
✓ LUB = smallest upper bound | GLB = greatest lower bound
✓ Lattice = every pair has LUB & GLB
✓ De Morgan's Laws for sets and Boolean algebra
✓ Transitive closure = R ∪ R² ∪ ... until stable
✓ Composition goes RIGHT to LEFT
✓ Warshall's algorithm for transitive closure (O(n³))

---

**🎯 Final Tip**: Practice drawing Hasse diagrams and checking properties on small sets (3-4 elements). These visual problems are exam favorites and easy marks if you know the method!

**Good Luck! 🌟**

---

*End of Notes*