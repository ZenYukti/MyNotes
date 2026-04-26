# Functions & Boolean Algebra - Complete Study Notes

---

## 1. Functions: Definition & Classification

### Definition of Function
- **Function (f)**: A relation from set A to set B where each element in A is related to exactly one element in B
- Notation: `f: A → B` or `y = f(x)`
- **Domain**: Set A (input set)
- **Codomain**: Set B (output set)
- **Range**: Actual set of output values (subset of codomain)
- Key condition: Every element in domain must have exactly one image in codomain

### Classification of Functions

#### Based on Mapping Type

**1. One-to-One (Injective) Function**
- Each element in domain maps to a unique element in codomain
- No two different elements in domain have same image
- Mathematical test: If `f(x₁) = f(x₂)` then `x₁ = x₂`
- Example: `f(x) = 2x` is injective

**2. Onto (Surjective) Function**
- Every element in codomain is an image of at least one element from domain
- Range = Codomain
- For every `y ∈ B`, there exists at least one `x ∈ A` such that `f(x) = y`
- Example: `f: ℝ → ℝ`, `f(x) = x³` is onto

**3. Bijective Function (One-to-One and Onto)**
- Function is both injective and surjective
- Perfect pairing between domain and codomain
- Invertible function
- Example: `f(x) = 2x + 3` from ℝ to ℝ

**4. Many-to-One Function**
- Two or more elements in domain map to same element in codomain
- Example: `f(x) = x²` (both 2 and -2 map to 4)

#### Special Types of Functions

**5. Identity Function**
- Each element maps to itself
- `f(x) = x` for all `x ∈ A`
- Always bijective

**6. Constant Function**
- All elements in domain map to single element in codomain
- `f(x) = c` for all `x ∈ A`
- Neither injective nor surjective (unless codomain has single element)

**7. Inverse Function**
- Exists only for bijective functions
- Notation: `f⁻¹: B → A`
- Property: `f(f⁻¹(x)) = x` and `f⁻¹(f(x)) = x`

**8. Floor and Ceiling Functions**
- **Floor** `⌊x⌋`: Largest integer ≤ x
- **Ceiling** `⌈x⌉`: Smallest integer ≥ x
- Example: `⌊3.7⌋ = 3`, `⌈3.7⌉ = 4`

### Operations on Functions

**1. Composition of Functions**
- Notation: `(f ∘ g)(x) = f(g(x))`
- Domain of `g` must overlap with range requirements
- **Not commutative**: `f ∘ g ≠ g ∘ f` (generally)
- **Associative**: `(f ∘ g) ∘ h = f ∘ (g ∘ h)`

**2. Arithmetic Operations**
- **Addition**: `(f + g)(x) = f(x) + g(x)`
- **Subtraction**: `(f - g)(x) = f(x) - g(x)`
- **Multiplication**: `(f · g)(x) = f(x) · g(x)`
- **Division**: `(f / g)(x) = f(x) / g(x)`, where `g(x) ≠ 0`

**3. Inverse Operation**
- Only for bijective functions
- Steps to find inverse:
  - Replace `f(x)` with `y`
  - Swap `x` and `y`
  - Solve for `y`
  - Replace `y` with `f⁻¹(x)`

### Exam Questions - Functions

**Q1.** Let `f: ℝ → ℝ` be defined by `f(x) = 3x + 5` and `g: ℝ → ℝ` be defined by `g(x) = x²`. Find:
   - (a) `(f ∘ g)(x)`
   - (b) `(g ∘ f)(x)`
   - (c) Is composition commutative? Justify.

**Q2.** Determine whether the function `f(x) = x³ - x` is injective, surjective, or bijective. Justify your answer with proper reasoning.

**Q3.** Find the inverse of the function `f(x) = (2x + 3)/(x - 1)`, `x ≠ 1`. Also verify that `f(f⁻¹(x)) = x`.

**Q4.** Prove that if `f: A → B` and `g: B → C` are both bijective functions, then `g ∘ f: A → C` is also bijective.

**Q5.** For the functions `f(x) = ⌊x/2⌋` and `g(x) = ⌈x/2⌉`, find the values of:
   - (a) `f(7) + g(7)`
   - (b) `f(-5) + g(-5)`
   - (c) When does `f(x) = g(x)`?

---

## 2. Growth of Functions

### Big-O Notation (Upper Bound)

**Definition**
- `f(n) = O(g(n))` if there exist positive constants `c` and `n₀` such that:
  - `0 ≤ f(n) ≤ c·g(n)` for all `n ≥ n₀`
- `g(n)` is an **asymptotic upper bound** for `f(n)`
- Represents worst-case complexity

**Properties**
- **Transitivity**: If `f = O(g)` and `g = O(h)`, then `f = O(h)`
- **Sum rule**: `O(f + g) = O(max(f, g))`
- **Product rule**: `O(f · g) = O(f) · O(g)`
- Constant factors ignored: `O(cf(n)) = O(f(n))`

### Big-Omega Notation (Lower Bound)

**Definition**
- `f(n) = Ω(g(n))` if there exist positive constants `c` and `n₀` such that:
  - `0 ≤ c·g(n) ≤ f(n)` for all `n ≥ n₀`
- `g(n)` is an **asymptotic lower bound** for `f(n)`
- Represents best-case complexity

### Big-Theta Notation (Tight Bound)

**Definition**
- `f(n) = Θ(g(n))` if there exist positive constants `c₁`, `c₂`, and `n₀` such that:
  - `0 ≤ c₁·g(n) ≤ f(n) ≤ c₂·g(n)` for all `n ≥ n₀`
- `f(n)` grows at the **same rate** as `g(n)`
- `f(n) = Θ(g(n))` if and only if `f(n) = O(g(n))` AND `f(n) = Ω(g(n))`

### Little-o and Little-omega Notations

**Little-o (o)**
- `f(n) = o(g(n))` means `f(n)` grows **strictly slower** than `g(n)`
- `lim(n→∞) [f(n)/g(n)] = 0`

**Little-omega (ω)**
- `f(n) = ω(g(n))` means `f(n)` grows **strictly faster** than `g(n)`
- `lim(n→∞) [f(n)/g(n)] = ∞`

### Common Growth Rates (Slowest to Fastest)

1. `O(1)` - Constant
2. `O(log log n)` - Double logarithmic
3. `O(log n)` - Logarithmic
4. `O(√n)` - Square root
5. `O(n)` - Linear
6. `O(n log n)` - Linearithmic
7. `O(n²)` - Quadratic
8. `O(n³)` - Cubic
9. `O(nᵏ)` - Polynomial
10. `O(2ⁿ)` - Exponential
11. `O(n!)` - Factorial

### Important Rules & Properties

**Limit Comparison Method**
- Calculate `lim(n→∞) [f(n)/g(n)] = L`
- If `L = 0`: `f(n) = o(g(n))`
- If `0 < L < ∞`: `f(n) = Θ(g(n))`
- If `L = ∞`: `f(n) = ω(g(n))`

**Logarithm Properties**
- `log(ab) = log a + log b`
- `log(aᵇ) = b·log a`
- `logₐ n = (log n)/(log a)` (change of base)
- All logarithms differ by constant factor: `O(log₂ n) = O(logₑ n) = O(log₁₀ n)`

**Polynomial vs Exponential**
- Any polynomial grows slower than any exponential
- `nᵏ = o(aⁿ)` for any constant `k` and `a > 1`

### Exam Questions - Growth of Functions

**Q1.** Arrange the following functions in increasing order of growth rate:
   - `f₁(n) = n²log n`, `f₂(n) = 2ⁿ`, `f₃(n) = n!`, `f₄(n) = n³`, `f₅(n) = n log n`

**Q2.** Prove that `5n² + 3n + 2 = O(n²)` using the formal definition. Find suitable values of `c` and `n₀`.

**Q3.** Use the limit method to determine the relationship between `f(n) = n²` and `g(n) = n² + log n`. Is `f(n) = Θ(g(n))`?

**Q4.** Show that `f(n) = 3n³ + 2n² + 5` is `O(n³)` but not `O(n²)`.

**Q5.** If `f(n) = O(g(n))` and `g(n) = O(h(n))`, prove that `f(n) = O(h(n))` (transitivity property).

---

## 3. Boolean Algebra: Introduction & Axioms

### Introduction to Boolean Algebra

**Definition**
- Mathematical structure for logic and digital circuits
- Deals with binary variables (0 and 1, True and False)
- Invented by George Boole in 1854
- Foundation of digital logic design

**Binary Variables**
- Only two possible values: 0 (False) and 1 (True)
- Used in: Logic gates, digital circuits, computer operations
- Variables represented by: A, B, C, X, Y, Z, etc.

**Basic Operations**
1. **AND** (·, ∧): Logical multiplication
2. **OR** (+, ∨): Logical addition
3. **NOT** (', ¬, ‾): Logical complement

### Axioms of Boolean Algebra (Huntington's Postulates)

**Closure Property**
- If `A` and `B` are Boolean variables, then:
  - `A + B` is also a Boolean variable
  - `A · B` is also a Boolean variable

**Identity Elements**
- `A + 0 = A` (0 is identity for OR)
- `A · 1 = A` (1 is identity for AND)

**Commutative Laws**
- `A + B = B + A` (OR is commutative)
- `A · B = B · A` (AND is commutative)

**Distributive Laws**
- `A + (B · C) = (A + B) · (A + C)`
- `A · (B + C) = (A · B) + (A · C)`

**Complement Property**
- For every element A, there exists a complement A' such that:
  - `A + A' = 1`
  - `A · A' = 0`

**Distinct Elements**
- At least two distinct elements exist: 0 and 1
- `0 ≠ 1`

### Theorems of Boolean Algebra

**Idempotent Laws**
- `A + A = A`
- `A · A = A`

**Null (Dominance) Laws**
- `A + 1 = 1`
- `A · 0 = 0`

**Involution (Double Complement) Law**
- `(A')' = A`

**Absorption Laws**
- `A + (A · B) = A`
- `A · (A + B) = A`

**Associative Laws**
- `(A + B) + C = A + (B + C)`
- `(A · B) · C = A · (B · C)`

**De Morgan's Theorems** (Most Important!)
- `(A + B)' = A' · B'` (NOT of OR = AND of NOTs)
- `(A · B)' = A' + B'` (NOT of AND = OR of NOTs)
- Extended form: `(A + B + C + ...)' = A' · B' · C' · ...`
- Extended form: `(A · B · C · ...)' = A' + B' + C' + ...`

**Consensus Theorem**
- `A·B + A'·C + B·C = A·B + A'·C`
- Dual: `(A+B)·(A'+C)·(B+C) = (A+B)·(A'+C)`

**Transposition Theorem**
- `A·B + A'·C = (A+C)·(A'+B)`

### Truth Tables for Basic Operations

**AND Operation (·)**
| A | B | A·B |
|---|---|-----|
| 0 | 0 | 0   |
| 0 | 1 | 0   |
| 1 | 0 | 0   |
| 1 | 1 | 1   |

**OR Operation (+)**
| A | B | A+B |
|---|---|-----|
| 0 | 0 | 0   |
| 0 | 1 | 1   |
| 1 | 0 | 1   |
| 1 | 1 | 1   |

**NOT Operation (')**
| A | A' |
|---|------|
| 0 | 1    |
| 1 | 0    |

### Exam Questions - Boolean Algebra Basics

**Q1.** Prove using Boolean algebra theorems: `A + A'B = A + B`

**Q2.** Verify De Morgan's theorem `(A·B)' = A' + B'` using truth tables for all possible combinations of A and B.

**Q3.** Simplify the following expressions using Boolean algebra laws:
   - (a) `A·(A' + B)`
   - (b) `(A + B)·(A + B')`
   - (c) `A + A'·B + A'·B'·C`

**Q4.** Prove the absorption law: `A + (A · B) = A` using the axioms and theorems of Boolean algebra.

**Q5.** Show that `(A + B)·(A' + C)·(B + C) = (A + B)·(A' + C)` using the consensus theorem.

---

## 4. Algebraic Manipulation of Boolean Expressions

### Standard Forms of Boolean Expressions

**Sum of Products (SOP)**
- Also called **Disjunctive Normal Form (DNF)**
- OR of AND terms: `(A·B) + (A'·C) + (B·C')`
- Each AND term is called a **product term** or **minterm**
- Example: `F = A'·B·C + A·B'·C + A·B·C'`

**Product of Sums (POS)**
- Also called **Conjunctive Normal Form (CNF)**
- AND of OR terms: `(A+B)·(A'+C)·(B+C')`
- Each OR term is called a **sum term** or **maxterm**
- Example: `F = (A+B+C)·(A'+B+C')·(A+B'+C)`

### Minterms and Maxterms

**Minterms (m)**
- Product terms containing all variables (complemented or uncomplemented)
- For n variables: 2ⁿ possible minterms
- Minterm = 1 for exactly one combination
- Notation: `mᵢ` where i is decimal equivalent

**For 3 variables (A, B, C):**
- m₀ = A'·B'·C' (000)
- m₁ = A'·B'·C (001)
- m₂ = A'·B·C' (010)
- m₃ = A'·B·C (011)
- m₄ = A·B'·C' (100)
- m₅ = A·B'·C (101)
- m₆ = A·B·C' (110)
- m₇ = A·B·C (111)

**Maxterms (M)**
- Sum terms containing all variables
- Maxterm = 0 for exactly one combination
- Notation: `Mᵢ` where i is decimal equivalent

**For 3 variables (A, B, C):**
- M₀ = A+B+C (000)
- M₁ = A+B+C' (001)
- M₂ = A+B'+C (010)
- M₃ = A+B'+C' (011)
- M₄ = A'+B+C (100)
- M₅ = A'+B+C' (101)
- M₆ = A'+B'+C (110)
- M₇ = A'+B'+C' (111)

**Important Relationship:**
- `mᵢ = Mᵢ'` (complement of maxterm = corresponding minterm)
- `Mᵢ = mᵢ'` (complement of minterm = corresponding maxterm)

### Canonical Forms

**Canonical SOP (Sum of Minterms)**
- Function expressed as sum of minterms where function = 1
- Notation: `F = Σm(1, 3, 5, 7)` means `F = m₁ + m₃ + m₅ + m₇`
- Example: `F(A,B,C) = Σm(1,3,5,7) = A'B'C + A'BC + AB'C + ABC`

**Canonical POS (Product of Maxterms)**
- Function expressed as product of maxterms where function = 0
- Notation: `F = ΠM(0, 2, 4, 6)` means `F = M₀·M₂·M₄·M₆`
- Example: `F(A,B,C) = ΠM(0,2,4,6)`

**Conversion Between SOP and POS:**
- Minterms where F=1 ↔ Maxterms where F=0
- If `F = Σm(1,3,5,7)` then `F = ΠM(0,2,4,6)`

### Simplification Techniques

**Method 1: Using Boolean Theorems**
- Apply idempotent, absorption, distributive laws
- Look for common factors
- Apply De Morgan's theorems
- Example: `A'B + AB = B(A'+A) = B·1 = B`

**Method 2: Combining Terms**
- Combine terms that differ by one variable: `AB + AB' = A(B+B') = A`
- Example: `A'BC + ABC = BC(A'+A) = BC`

**Method 3: Factoring**
- Factor out common terms
- Example: `AC + A'C + BC = C(A+A') + BC = C + BC = C`

**Method 4: Adding Redundant Terms**
- Add `A·A' = 0` or `A+A' = 1` to help simplification
- Duplicate terms using `A = A+A = A·A`

### Steps for Simplification

1. **Identify** all terms in the expression
2. **Group** terms with common factors
3. **Apply** Boolean laws systematically
4. **Check** if further simplification possible
5. **Verify** using truth table if needed

### Exam Questions - Algebraic Manipulation

**Q1.** Simplify the following Boolean expressions:
   - (a) `F = A'B'C + A'BC + AB'C + ABC`
   - (b) `F = (A+B)(A+C')(B'+C)`
   - (c) `F = AB + AB'C + A'BC`

**Q2.** Convert `F(A,B,C) = Σm(1,3,5,7)` to:
   - (a) Canonical SOP form
   - (b) Canonical POS form
   - (c) Simplified form

**Q3.** Express the Boolean function `F = A'B + AC + BC` in:
   - (a) Sum of minterms notation
   - (b) Product of maxterms notation

**Q4.** Prove algebraically that `AB + A'C + BC = AB + A'C` (Consensus theorem).

**Q5.** Given `F₁ = Σm(0,2,5,7)` and `F₂ = ΠM(1,3,4,6)`, find:
   - (a) F₁ + F₂
   - (b) F₁ · F₂
   - (c) F₁'

---

## 5. Simplification of Boolean Functions

### Need for Simplification

**Why Simplify?**
- Reduce number of gates in circuit
- Lower cost of implementation
- Reduce power consumption
- Increase circuit speed
- Make circuit more reliable

**Methods of Simplification**
1. Algebraic manipulation (manual)
2. Karnaugh Maps (graphical, up to 6 variables)
3. Quine-McCluskey method (tabular, any number of variables)

### Karnaugh Map (K-Map) Basics

**Definition**
- Graphical method for simplifying Boolean expressions
- Visual representation of truth table
- Uses Gray code ordering (adjacent cells differ by 1 bit only)
- Works well for 2 to 6 variables (practical limit: 4-5 variables)

**Gray Code Property**
- Adjacent cells differ in only ONE variable
- Allows easy identification of terms that can be combined
- Example (2-bit): 00, 01, 11, 10

### K-Map for 2 Variables

**Layout:**
```
      B
    0   1
A 0 [ ] [ ]
  1 [ ] [ ]
```

**Cell numbering (minterms):**
```
      B
    0   1
A 0 m₀  m₁   (A'B', A'B)
  1 m₂  m₃   (AB', AB)
```

### K-Map for 3 Variables

**Layout:**
```
       BC
     00  01  11  10
A 0  [ ] [ ] [ ] [ ]
  1  [ ] [ ] [ ] [ ]
```

**Cell numbering:**
```
       BC
     00  01  11  10
A 0  m₀  m₁  m₃  m₂   (Row 0: A'B'C', A'B'C, A'BC, A'BC')
  1  m₄  m₅  m₇  m₆   (Row 1: AB'C', AB'C, ABC, ABC')
```

### K-Map for 4 Variables

**Layout:**
```
        CD
      00  01  11  10
AB 00 [ ] [ ] [ ] [ ]
   01 [ ] [ ] [ ] [ ]
   11 [ ] [ ] [ ] [ ]
   10 [ ] [ ] [ ] [ ]
```

**Cell numbering:**
```
        CD
      00  01  11  10
AB 00 m₀  m₁  m₃  m₂
   01 m₄  m₅  m₇  m₆
   11 m₁₂ m₁₃ m₁₅ m₁₄
   10 m₈  m₉  m₁₁ m₁₀
```

### K-Map Grouping Rules

**Rule 1: Group Size**
- Groups must contain 2ⁿ cells (1, 2, 4, 8, 16...)
- Larger groups → simpler expressions

**Rule 2: Rectangle Shape**
- Groups must be rectangular (including squares)
- No diagonal grouping

**Rule 3: Adjacency**
- Top edge adjacent to bottom edge (wrap-around)
- Left edge adjacent to right edge (wrap-around)
- Corner cells form groups of 4

**Rule 4: Grouping 1s (for SOP)**
- Circle all 1s in K-map
- Each 1 must be in at least one group
- A 1 can be in multiple groups if it leads to fewer terms

**Rule 5: Minimum Groups**
- Use minimum number of groups
- Make groups as large as possible
- Maximize overlap to minimize terms

**Rule 6: Don't Care Conditions (X or d)**
- Can be treated as 0 or 1 for convenience
- Use X to make larger groups
- Don't include X in final expression unless helpful

### Steps to Simplify Using K-Map

**For SOP (Grouping 1s):**
1. **Plot** the function on K-map (place 1s in corresponding cells)
2. **Identify** all 1s that must be grouped
3. **Form** largest possible groups of 2ⁿ cells
4. **Ensure** every 1 is covered by at least one group
5. **Write** product term for each group:
   - Variable = 0 everywhere in group → include as complemented
   - Variable = 1 everywhere in group → include as uncomplemented
   - Variable changes in group → eliminate variable
6. **Sum** all product terms (OR them together)

**For POS (Grouping 0s):**
1. Group all 0s instead of 1s
2. Write sum term for each group
3. Product all sum terms (AND them together)

### Prime Implicants

**Prime Implicant**
- A group that cannot be combined with another group to eliminate more variables
- Largest possible group covering certain cells

**Essential Prime Implicant**
- A prime implicant that covers at least one 1 (minterm) not covered by any other prime implicant
- MUST be included in final simplified expression

### Example of Reading K-Map Groups

**Group of 2 cells:** Eliminates 1 variable
- Example: Group covering `m₀(A'B'C')` and `m₁(A'B'C)` → Result: `A'B'`

**Group of 4 cells:** Eliminates 2 variables
- Example: Group covering `m₀, m₁, m₄, m₅` → Result: `B'`

**Group of 8 cells:** Eliminates 3 variables
- Example: Group covering entire row → Result: single variable

### Don't Care Conditions

**Types of Don't Cares:**
- **Output Don't Care (d):** Input combinations that never occur
- Used to make K-map grouping easier
- Notation: X, d, or φ

**How to Use:**
- Treat as 1 if it helps make larger groups
- Treat as 0 if not helpful
- Not shown in final output expression

**Example:**
- `F(A,B,C) = Σm(1,3,5,7) + d(0,2)`
- Can use 0 and 2 to form larger groups

### Exam Questions - Simplification

**Q1.** Simplify the following function using K-map:
   - `F(A,B,C) = Σm(0,1,2,5,7)`
   - Draw the K-map and identify all prime implicants

**Q2.** Use K-map to simplify: `F(A,B,C,D) = Σm(0,1,3,7,8,9,11,15)`. Identify essential prime implicants.

**Q3.** Simplify using K-map with don't cares:
   - `F(A,B,C) = Σm(1,3,5) + d(0,2,7)`
   - Show how don't cares help in grouping

**Q4.** For the function `F(A,B,C,D) = Σm(0,2,5,7,8,10,13,15)`:
   - (a) Draw 4-variable K-map
   - (b) Find simplified SOP form
   - (c) Draw the logic circuit using minimum gates

**Q5.** Simplify in POS form using K-map: `F(A,B,C) = ΠM(0,2,4,5,6)`. Group the 0s and obtain the minimal POS expression.

---

## 6. Karnaugh Maps (Advanced Concepts)

### Multi-Output K-Maps

**When to Use:**
- Multiple functions sharing same input variables
- Can identify common sub-expressions
- Reduces overall circuit complexity

**Approach:**
- Draw separate K-maps for each output
- Look for common groups across maps
- Factor out common terms

**Example:**
- `F₁(A,B,C) = Σm(1,3,5,7)`
- `F₂(A,B,C) = Σm(0,1,2,3)`
- Common term: Can share logic gates

### Five and Six Variable K-Maps

**5-Variable K-Map:**
- Two 4-variable K-maps side by side
- One for E=0, another for E=1
- Cells at same position in both maps are adjacent
- Group can span across both maps

**6-Variable K-Map:**
- Four 4-variable K-maps in 2×2 arrangement
- More complex but follows same principles
- Practical limit due to visualization difficulty

### K-Map Limitations

**Disadvantages:**
- Difficult for more than 6 variables
- Human error in grouping
- Not suitable for computer algorithms
- Cannot handle multiple outputs efficiently

**When Not to Use K-Map:**
- More than 6 variables → use Quine-McCluskey
- Need automated solution → use software tools
- Require formal proof → use algebraic methods

### K-Map vs Algebraic Simplification

**K-Map Advantages:**
- Visual and intuitive
- Guaranteed minimal solution
- Easy to identify essential prime implicants
- Fast for 2-5 variables

**Algebraic Advantages:**
- Works for any number of variables
- Can be computer-automated
- Provides step-by-step logical proof
- Better for theoretical work

### Practical K-Map Tips & Tricks

**Tip 1: Wrap-Around Recognition**
- Always check edges and corners first
- Edges wrap to opposite edges
- All four corners form a group of 4

**Tip 2: Don't Care Strategy**
- Include don't cares ONLY if they enlarge groups
- Don't force don't cares into groups if not needed

**Tip 3: Overlapping Groups**
- Same 1 can be in multiple groups
- Helps reduce total number of groups
- Essential for minimal expression

**Tip 4: Check for Prime Implicants**
- Circle all maximal groups first
- Then identify which are essential
- Add non-essential only if needed for coverage

**Tip 5: Verification**
- After simplification, verify with truth table
- Check that simplified expression gives same output
- Count gates to ensure minimization

### Common K-Map Patterns

**All 1s:**
- Result: F = 1 (tautology)

**Checkerboard Pattern:**
- Cannot be simplified much
- Results in many terms

**Single Row/Column of 1s:**
- Simplifies to 2-3 variables max

**Four Corners:**
- Forms a group of 4 in wrap-around
- Eliminates 2 variables

### Converting K-Map to Logic Circuit

**Steps:**
1. Get simplified SOP/POS from K-map
2. Each product term → AND gate
3. Combine products → OR gate (for SOP)
4. Count total gates required
5. Optimize further if possible

**Two-Level Implementation:**
- **SOP:** AND gates → OR gate
- **POS:** OR gates → AND gate

**Example:**
- `F = A'B + BC` requires:
  - One NOT gate (for A')
  - Two AND gates
  - One OR gate
  - Total: 4 gates

### NAND-NAND and NOR-NOR Implementation

**Why NAND/NOR?**
- Universal gates (can implement any function)
- Often cheaper to manufacture
- Better electrical properties

**SOP → NAND-NAND:**
- Replace all AND gates with NAND
- Replace final OR with NAND
- Add inverters where needed

**POS → NOR-NOR:**
- Replace all OR gates with NOR
- Replace final AND with NOR
- Add inverters where needed

### Exam Questions - K-Map Advanced

**Q1.** Simplify using 5-variable K-map:
   - `F(A,B,C,D,E) = Σm(0,1,4,5,8,9,12,13,16,17,20,21,24,25,28,29)`

**Q2.** Given two functions:
   - `F₁(A,B,C) = Σm(0,1,2,4,6)`
   - `F₂(A,B,C) = Σm(0,2,3,4,7)`
   - Use K-maps to find a shared sub-expression and minimize total gates.

**Q3.** Simplify and implement using:
   - `F(A,B,C,D) = Σm(1,3,5,7,9,11,13,15)`
   - (a) Minimal SOP form
   - (b) Draw two-level NAND-NAND circuit

**Q4.** Identify all prime implicants and essential prime implicants for:
   - `F(A,B,C,D) = Σm(0,1,2,5,8,9,10) + d(3,7,15)`
   - Justify why certain prime implicants are essential.

**Q5.** Compare the gate count for:
   - `F(A,B,C) = A'B'C + A'BC + AB'C + ABC`
   - (a) Without simplification
   - (b) After K-map simplification
   - Show the gate savings achieved.

---

# 📄 ONE-PAGE SUMMARY - Last Minute Revision

## Functions - Quick Reference

### Types
- **Injective (1-1):** Different inputs → different outputs
- **Surjective (Onto):** Range = Codomain
- **Bijective:** Both injective & surjective (invertible)

### Operations
- **Composition:** `(f∘g)(x) = f(g(x))` [Not commutative]
- **Inverse:** Only for bijective; `f(f⁻¹(x)) = x`

---

## Growth of Functions - Notation

| Notation | Meaning | Formula |
|----------|---------|---------|
| `O(g(n))` | Upper bound | `f(n) ≤ c·g(n)` for `n ≥ n₀` |
| `Ω(g(n))` | Lower bound | `f(n) ≥ c·g(n)` for `n ≥ n₀` |
| `Θ(g(n))` | Tight bound | `c₁·g(n) ≤ f(n) ≤ c₂·g(n)` |

### Growth Order (Slowest → Fastest)
`O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)`

**Key:** Polynomial < Exponential < Factorial

---

## Boolean Algebra - Essential Laws

### Fundamental Laws
| Law | Expression |
|-----|------------|
| **Identity** | `A + 0 = A`, `A · 1 = A` |
| **Null** | `A + 1 = 1`, `A · 0 = 0` |
| **Idempotent** | `A + A = A`, `A · A = A` |
| **Complement** | `A + A' = 1`, `A · A' = 0` |
| **Involution** | `(A')' = A` |
| **Absorption** | `A + AB = A`, `A(A+B) = A` |
| **Commutative** | `A + B = B + A`, `AB = BA` |
| **Associative** | `A+(B+C) = (A+B)+C` |
| **Distributive** | `A(B+C) = AB+AC` |

### ⭐ De Morgan's Theorems (Most Important!)
- `(A + B)' = A' · B'`
- `(A · B)' = A' + B'`

### Consensus Theorem
- `AB + A'C + BC = AB + A'C`

---

## Minterms & Maxterms (3 Variables)

| Decimal | Minterm | Notation | Maxterm | Notation |
|---------|---------|----------|---------|----------|
| 0 | A'B'C' | m₀ | A+B+C | M₀ |
| 1 | A'B'C | m₁ | A+B+C' | M₁ |
| 2 | A'BC' | m₂ | A+B'+C | M₂ |
| 3 | A'BC | m₃ | A+B'+C' | M₃ |
| 4 | AB'C' | m₄ | A'+B+C | M₄ |
| 5 | AB'C | m₅ | A'+B+C' | M₅ |
| 6 | ABC' | m₆ | A'+B'+C | M₆ |
| 7 | ABC | m₇ | A'+B'+C' | M₇ |

**Relation:** `mᵢ = Mᵢ'`

---

## K-Map Essential Rules

### Grouping Rules (for SOP)
1. **Group 1s only** (group 0s for POS)
2. **Sizes:** 1, 2, 4, 8, 16 cells (powers of 2)
3. **Shape:** Rectangular only
4. **Wraparound:** Edges and corners are adjacent
5. **Maximize:** Make largest groups possible
6. **Overlap:** Same 1 can be in multiple groups

### Reading Groups
- **Group of 2:** Eliminates 1 variable
- **Group of 4:** Eliminates 2 variables
- **Group of 8:** Eliminates 3 variables

### 3-Variable K-Map Template
```
       BC
     00  01  11  10
A 0  m₀  m₁  m₃  m₂
  1  m₄  m₅  m₇  m₆
```

**Gray Code Order:** 00 → 01 → 11 → 10

---

## Quick Tricks & Formulas

### Simplification Shortcuts
1. `AB + AB' = A` (combine adjacent terms)
2. `A + A'B = A + B` (absorption variant)
3. `(A+B)(A+C) = A + BC` (distributive)
4. Look for `XX' = 0` and `X+X' = 1` opportunities

### Common K-Map Patterns
- **4 corners** (in any K-map) = Group of 4
- **Entire row/column** = Simplifies heavily
- **Checkerboard** = Cannot simplify much

### Gate Count Reduction
- Before simplification: Count all literals
- After K-map: Significantly fewer gates
- **Goal:** Minimum product terms with minimum literals

### Don't Care (X) Strategy
- Use X to **enlarge** groups
- Ignore X if doesn't help
- X never appears in final answer

---

## Exam Pro Tips

1. **Functions:** Always check if bijective before finding inverse
2. **Growth:** Use limit method: `lim[f(n)/g(n)]` to compare
3. **Boolean:** Apply De Morgan's when you see `(A+B)'` or `(AB)'`
4. **K-Map:** Start with essential prime implicants, then add others
5. **Verification:** Create truth table to verify simplified expressions

---

## Common Exam Question Patterns

✓ Prove function is injective/surjective/bijective
✓ Find `(f∘g)(x)` and `(g∘f)(x)` and compare
✓ Prove `f(n) = O(g(n))` using definition
✓ Simplify Boolean expression using theorems
✓ Convert between SOP/POS and Σm/ΠM notation
✓ Draw K-map, group optimally, write simplified form
✓ Implement simplified expression with minimum gates

---

**🔥 Remember:** 
- Functions: Check domain, codomain, range carefully
- Growth: Polynomial always < Exponential
- Boolean: De Morgan's is your best friend
- K-Map: Bigger groups = Simpler expression!