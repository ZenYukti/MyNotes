# Algebraic Structures - Comprehensive Notes

---

## 1. Algebraic Structures - Introduction

### Definition
- An **algebraic structure** consists of a non-empty set with one or more binary operations satisfying certain axioms
- Components: **Set + Operation(s) + Axioms**
- Common structures: Groups, Rings, Fields, Vector Spaces

### Types of Binary Operations
- **Closure**: If a, b ∈ S, then a * b ∈ S
- **Associativity**: (a * b) * c = a * (b * c)
- **Commutativity**: a * b = b * a
- **Identity**: ∃ e ∈ S such that a * e = e * a = a
- **Inverse**: For each a ∈ S, ∃ a⁻¹ such that a * a⁻¹ = a⁻¹ * a = e

### Hierarchy
- **Magma**: Set with one binary operation (closure only)
- **Semigroup**: Magma + Associativity
- **Monoid**: Semigroup + Identity element
- **Group**: Monoid + Inverse for every element
- **Ring**: Set with two operations (addition and multiplication)
- **Field**: Ring with additional properties

### Exam Questions
1. Define an algebraic structure and list three examples with their defining properties.
2. Differentiate between a monoid and a group with suitable examples.
3. What is the minimum requirement for a set with a binary operation to be called a semigroup?
4. Prove that the set of integers under addition forms a group.
5. Give an example of a structure that is a monoid but not a group, and justify your answer.

---

## 2. Groups

### Definition
- A **group** (G, *) is a set G with a binary operation * satisfying:
  - **G1 (Closure)**: ∀ a, b ∈ G, a * b ∈ G
  - **G2 (Associativity)**: ∀ a, b, c ∈ G, (a * b) * c = a * (b * c)
  - **G3 (Identity)**: ∃ e ∈ G such that ∀ a ∈ G, a * e = e * a = a
  - **G4 (Inverse)**: ∀ a ∈ G, ∃ a⁻¹ ∈ G such that a * a⁻¹ = a⁻¹ * a = e

### Abelian (Commutative) Groups
- A group G is **abelian** if ∀ a, b ∈ G, a * b = b * a
- Also called **commutative groups**
- Examples: (ℤ, +), (ℝ, +), (ℚ*, ×)

### Important Properties
- **Uniqueness of identity**: The identity element is unique
- **Uniqueness of inverse**: Each element has exactly one inverse
- **Cancellation laws**: 
  - Left: If a * b = a * c, then b = c
  - Right: If b * a = c * a, then b = c
- **(a⁻¹)⁻¹ = a**: Inverse of inverse is the element itself
- **(a * b)⁻¹ = b⁻¹ * a⁻¹**: Inverse of product (order reverses)

### Common Examples
- **(ℤ, +)**: Integers under addition (abelian, infinite)
- **(ℤₙ, +)**: Integers modulo n under addition (abelian, finite)
- **(ℝ*, ×)**: Non-zero real numbers under multiplication (abelian, infinite)
- **GL(n, ℝ)**: General linear group (non-abelian for n ≥ 2)
- **Dₙ**: Dihedral group of order 2n (non-abelian for n ≥ 3)

### Order of a Group
- **Order** of a group G, denoted |G|, is the number of elements in G
- Can be **finite** or **infinite**
- Examples:
  - |ℤ₆| = 6 (finite)
  - |ℤ| = ∞ (infinite)

### Exam Questions
1. Prove that the identity element in a group is unique.
2. Show that (ℤ₆, +₆) forms a group. Is it abelian? Justify.
3. If G is a group and a, b ∈ G, prove that (ab)⁻¹ = b⁻¹a⁻¹.
4. Verify the cancellation law in groups: if ab = ac, then b = c.
5. Give an example of a non-abelian group and demonstrate why it's non-commutative.

---

## 3. Subgroups and Order

### Definition of Subgroup
- A subset H of a group G is a **subgroup** if H itself is a group under the same operation
- Notation: H ≤ G (H is a subgroup of G)
- H < G means H is a **proper subgroup** (H ≠ G)

### Subgroup Test (Two-Step Test)
For H ⊆ G to be a subgroup:
- **Non-empty**: H ≠ ∅
- **Closure**: ∀ a, b ∈ H, a * b ∈ H
- **Inverse**: ∀ a ∈ H, a⁻¹ ∈ H

### One-Step Subgroup Test
- **H ≠ ∅**
- **∀ a, b ∈ H, a * b⁻¹ ∈ H**
- This single condition implies closure and inverse property

### Finite Subgroup Test
For finite H ⊆ G:
- **H ≠ ∅**
- **Closure**: ∀ a, b ∈ H, a * b ∈ H
- Inverse property follows automatically for finite sets

### Trivial Subgroups
- **{e}**: Contains only the identity (trivial subgroup)
- **G**: The entire group (improper subgroup)
- All groups have at least these two subgroups

### Order of an Element
- The **order** of element a ∈ G, denoted |a| or o(a), is the smallest positive integer n such that aⁿ = e
- If no such n exists, a has **infinite order**
- Properties:
  - |e| = 1 (identity has order 1)
  - |a| = |a⁻¹|
  - If |a| = n, then aᵏ = e ⟺ n | k

### Important Results
- The **center** of G: Z(G) = {a ∈ G : ax = xa, ∀ x ∈ G} is a subgroup
- The **centralizer** of a: C(a) = {g ∈ G : ga = ag} is a subgroup
- Intersection of subgroups is a subgroup
- Union of subgroups is generally NOT a subgroup

### Exam Questions
1. Prove that the intersection of two subgroups of G is also a subgroup of G.
2. Using the one-step subgroup test, show that H = {0, 3, 6, 9} is a subgroup of (ℤ₁₂, +₁₂).
3. Find all subgroups of (ℤ₆, +₆) and verify using the subgroup test.
4. If |a| = 12, find the order of a³, a⁴, and a⁶.
5. Give an example to show that the union of two subgroups need not be a subgroup.

---

## 4. Cyclic Groups

### Definition
- A group G is **cyclic** if ∃ a ∈ G such that every element of G can be expressed as aⁿ for some integer n
- Notation: G = ⟨a⟩ (G is generated by a)
- Element a is called a **generator** of G

### Properties
- **All cyclic groups are abelian** (but not all abelian groups are cyclic)
- Every subgroup of a cyclic group is cyclic
- If |G| = n, then G is isomorphic to ℤₙ
- If G is infinite cyclic, then G is isomorphic to ℤ

### Generators
- For cyclic group G = ⟨a⟩ of order n:
  - aᵏ is a generator ⟺ gcd(k, n) = 1
  - Number of generators = φ(n) (Euler's totient function)
- For infinite cyclic groups ℤ:
  - Only generators are 1 and -1

### Subgroups of Cyclic Groups
- If G = ⟨a⟩ with |G| = n, then for each divisor d of n:
  - ∃ exactly one subgroup of order d
  - This subgroup is ⟨aⁿ/ᵈ⟩
- **Fundamental Theorem of Cyclic Groups**: Every subgroup of a cyclic group is cyclic

### Examples
- **(ℤ, +)**: Infinite cyclic, generated by 1 or -1
- **(ℤₙ, +ₙ)**: Finite cyclic, multiple generators
- ℤ₆ = ⟨1⟩ = ⟨5⟩; generators are 1 and 5 (since gcd(1,6)=1, gcd(5,6)=1)
- **(ℝ*, ×)**: Not cyclic (abelian but not cyclic)

### Order of Elements in Cyclic Groups
- In G = ⟨a⟩ with |G| = n:
  - |aᵏ| = n/gcd(k, n)
  - If gcd(k, n) = 1, then |aᵏ| = n (aᵏ is a generator)

### Exam Questions
1. Prove that every cyclic group is abelian.
2. Find all generators of ℤ₁₂. How many generators does it have?
3. List all subgroups of ℤ₁₈ and identify their generators.
4. If G is a cyclic group of order 20, find the order of all possible elements in G.
5. Prove that every subgroup of a cyclic group is cyclic.

---

## 5. Cosets

### Definition
- Let H be a subgroup of G and a ∈ G
- **Left coset**: aH = {ah : h ∈ H}
- **Right coset**: Ha = {ha : h ∈ H}
- For abelian groups, left and right cosets are the same

### Properties of Cosets
- a ∈ aH (every element is in its own coset)
- aH = bH ⟺ a⁻¹b ∈ H ⟺ b ∈ aH
- Two cosets are either **identical** or **disjoint** (no overlap)
- |aH| = |bH| = |H| (all cosets have the same size)
- aH = H ⟺ a ∈ H

### Coset Decomposition
- The set of all distinct left cosets of H partitions G
- G = a₁H ∪ a₂H ∪ ... ∪ aᵣH (disjoint union)
- Number of distinct cosets is called the **index** of H in G
- Notation: [G : H] = number of distinct cosets

### Index of a Subgroup
- **Index** [G : H] = |G| / |H| (for finite groups)
- [G : H] = number of distinct left (or right) cosets of H in G
- If [G : H] = 2, then H is a normal subgroup

### Examples
- In ℤ₆, let H = {0, 3}
  - Cosets: 0+H = {0, 3}, 1+H = {1, 4}, 2+H = {2, 5}
  - [ℤ₆ : H] = 3
- In S₃, let H = {e, (12)}
  - Left cosets partition S₃ into 3 cosets

### Exam Questions
1. Find all left cosets of H = {0, 4, 8} in (ℤ₁₂, +₁₂).
2. Prove that if aH = bH, then a⁻¹b ∈ H.
3. Show that any two left cosets of H in G are either identical or disjoint.
4. If |G| = 20 and |H| = 5, find the index [G : H] and interpret its meaning.
5. Prove that all left cosets of H in G have the same cardinality as H.

---

## 6. Lagrange's Theorem

### Statement
- If G is a finite group and H is a subgroup of G, then:
  - **|H| divides |G|**
  - **|G| = |H| × [G : H]**
- The order of any subgroup divides the order of the group

### Proof Outline
- Cosets of H partition G into disjoint sets
- Each coset has exactly |H| elements
- Number of cosets = [G : H]
- Therefore: |G| = |H| × [G : H]

### Corollaries
1. **Order of an element divides order of group**: If a ∈ G, then |a| divides |G|
2. **Groups of prime order are cyclic**: If |G| = p (prime), then G is cyclic
3. **Fermat's Little Theorem**: If |G| = n and a ∈ G, then aⁿ = e
4. If |G| = p (prime), then G has no proper non-trivial subgroups

### Applications
- **Finding possible subgroup orders**: Only divisors of |G| can be orders of subgroups
- **Determining group structure**: Limits the possible subgroup lattice
- **Element orders**: All element orders must divide |G|
- **Euler's Theorem**: aᶲ⁽ⁿ⁾ ≡ 1 (mod n) for gcd(a,n) = 1

### Limitations (Converse is False)
- If d divides |G|, there may NOT exist a subgroup of order d
- Example: A₄ has order 12, but no subgroup of order 6
- For abelian groups, the converse holds (guaranteed subgroup for each divisor)

### Important Examples
- In ℤ₁₂, possible subgroup orders: 1, 2, 3, 4, 6, 12
- In S₃ (order 6), subgroup orders can only be 1, 2, 3, 6
- In ℤ₇ (order 7, prime), only subgroups are {0} and ℤ₇

### Exam Questions
1. State and prove Lagrange's Theorem.
2. If G is a group of order 15, what are the possible orders of elements in G?
3. Prove that every group of prime order is cyclic.
4. Show that aⁿ = e for all a in a group G of order n.
5. Can a group of order 12 have a subgroup of order 5? Justify using Lagrange's theorem.

---

## 7. Normal Subgroups

### Definition
- A subgroup N of G is **normal** if ∀ g ∈ G: gNg⁻¹ = N
- Equivalently: gN = Ng (left and right cosets are equal)
- Notation: N ⊴ G

### Equivalent Conditions
N ⊴ G if and only if:
- gNg⁻¹ = N for all g ∈ G
- gNg⁻¹ ⊆ N for all g ∈ G (sufficient condition)
- gng⁻¹ ∈ N for all g ∈ G, n ∈ N
- Left and right cosets coincide: gN = Ng

### Properties
- **Every subgroup of an abelian group is normal** (since gng⁻¹ = gg⁻¹n = n)
- The trivial subgroups {e} and G are always normal
- If [G : N] = 2, then N is normal
- Kernel of a homomorphism is always normal

### Simple Groups
- A group G is **simple** if it has no normal subgroups except {e} and G
- Examples: ℤₚ (p prime), Aₙ for n ≥ 5
- Building blocks of group theory (analogous to prime numbers)

### Quotient Groups (Factor Groups)
- If N ⊴ G, then G/N = {aN : a ∈ G} forms a group
- Operation: (aN)(bN) = (ab)N
- **Order**: |G/N| = |G| / |N| = [G : N]
- G/N is called the **quotient group** or **factor group**

### Examples
- In (ℤ, +), every subgroup nℤ is normal
- In S₃, A₃ (alternating group) is normal (index 2)
- In a non-abelian group, not all subgroups are normal
- Center Z(G) is always a normal subgroup

### Exam Questions
1. Prove that every subgroup of an abelian group is normal.
2. Show that if [G : H] = 2, then H is a normal subgroup of G.
3. Define a quotient group and give an example with proper verification.
4. Find all normal subgroups of S₃.
5. Prove that the kernel of a group homomorphism is a normal subgroup.

---

## 8. Permutation and Symmetric Groups

### Permutations
- A **permutation** of a set A is a bijective function σ: A → A
- For finite set {1, 2, ..., n}, permutations form a group
- **Composition** of permutations is the group operation
- **Identity permutation**: ε(i) = i for all i

### Symmetric Group Sₙ
- **Sₙ** = group of all permutations of {1, 2, ..., n}
- **Order**: |Sₙ| = n!
- **Non-abelian** for n ≥ 3
- Examples:
  - |S₃| = 6
  - |S₄| = 24
  - |S₅| = 120

### Cycle Notation
- **Cycle**: (a₁ a₂ ... aₖ) means a₁ → a₂ → ... → aₖ → a₁
- **Length** of cycle (a₁ a₂ ... aₖ) is k
- **Disjoint cycles** commute: (1 2)(3 4) = (3 4)(1 2)
- Every permutation can be written as a product of disjoint cycles (unique up to order)

### Transpositions
- **Transposition**: A cycle of length 2, e.g., (i j)
- Also called a **2-cycle**
- Every permutation can be written as a product of transpositions (not unique)
- (a₁ a₂ ... aₖ) = (a₁ a₂)(a₂ a₃)...(aₖ₋₁ aₖ)

### Even and Odd Permutations
- A permutation is **even** if it can be expressed as a product of an even number of transpositions
- A permutation is **odd** if it requires an odd number of transpositions
- **Sign** of permutation σ: sgn(σ) = +1 (even) or -1 (odd)
- sgn(σ₁σ₂) = sgn(σ₁) × sgn(σ₂)

### Alternating Group Aₙ
- **Aₙ** = set of all even permutations in Sₙ
- Aₙ is a **normal subgroup** of Sₙ
- **Order**: |Aₙ| = n!/2
- A₃ is the smallest non-trivial normal subgroup of S₃
- Aₙ is **simple** for n ≥ 5

### Order of a Permutation
- **Order** of a permutation = LCM of the lengths of its disjoint cycles
- Examples:
  - |(1 2 3)(4 5)| = lcm(3, 2) = 6
  - |(1 2)(3 4)(5 6)| = lcm(2, 2, 2) = 2

### Exam Questions
1. Express the permutation σ = (1 3 5)(2 4) as a product of transpositions.
2. Find the order of the permutation (1 2 3 4)(5 6 7) in S₇.
3. Prove that the set of all even permutations forms a subgroup of Sₙ.
4. How many elements are there in S₅? How many are even permutations?
5. Show that A₃ is a normal subgroup of S₃.

---

## 9. Group Homomorphisms

### Definition
- A **homomorphism** φ: G → G' is a function satisfying:
  - **φ(ab) = φ(a)φ(b)** for all a, b ∈ G
- Preserves the group operation
- Maps identity to identity: φ(eG) = eG'
- Maps inverses to inverses: φ(a⁻¹) = [φ(a)]⁻¹

### Types of Homomorphisms
- **Isomorphism**: Homomorphism that is bijective
  - Groups G and G' are **isomorphic**: G ≅ G'
  - Isomorphic groups have identical structure
- **Endomorphism**: Homomorphism from G to itself (φ: G → G)
- **Automorphism**: Isomorphism from G to itself
- **Monomorphism**: Injective homomorphism (one-to-one)
- **Epimorphism**: Surjective homomorphism (onto)

### Kernel and Image
- **Kernel**: Ker(φ) = {a ∈ G : φ(a) = e'} ⊆ G
  - Ker(φ) is always a **normal subgroup** of G
  - φ is injective ⟺ Ker(φ) = {e}
- **Image**: Im(φ) = {φ(a) : a ∈ G} ⊆ G'
  - Im(φ) is a **subgroup** of G' (not necessarily normal)
  - φ is surjective ⟺ Im(φ) = G'

### Properties of Homomorphisms
- φ(eG) = eG' (identity mapped to identity)
- φ(aⁿ) = [φ(a)]ⁿ for all n ∈ ℤ
- If H ≤ G, then φ(H) ≤ G'
- If H' ≤ G', then φ⁻¹(H') ≤ G
- If a has finite order, then |φ(a)| divides |a|

### First Isomorphism Theorem
- If φ: G → G' is a homomorphism, then:
  - **G/Ker(φ) ≅ Im(φ)**
- Establishes connection between quotient groups and images
- One of the fundamental theorems of group theory

### Examples
- φ: (ℤ, +) → (ℤₙ, +ₙ) defined by φ(x) = x mod n
  - Ker(φ) = nℤ, Im(φ) = ℤₙ
- φ: (ℝ, +) → (ℝ⁺, ×) defined by φ(x) = eˣ
  - This is an isomorphism
- det: GL(n, ℝ) → (ℝ*, ×) (determinant is a homomorphism)
  - Ker(det) = SL(n, ℝ) (special linear group)

### Exam Questions
1. Prove that if φ: G → G' is a homomorphism, then Ker(φ) is a normal subgroup of G.
2. Define φ: ℤ → ℤ₆ by φ(n) = n mod 6. Find Ker(φ) and Im(φ).
3. State and prove the First Isomorphism Theorem.
4. Show that φ: G → G' is injective if and only if Ker(φ) = {e}.
5. Give an example of an automorphism of a group and verify it's a homomorphism.

---

## 10. Rings - Definition and Elementary Properties

### Definition
- A **ring** (R, +, ·) is a set R with two binary operations + and · satisfying:
  - **(R, +) is an abelian group**:
    - Closure, associativity, identity (0), inverses (−a), commutativity
  - **Multiplication is associative**: (ab)c = a(bc)
  - **Distributive laws**:
    - a(b + c) = ab + ac (left distributive)
    - (b + c)a = ba + ca (right distributive)

### Types of Rings
- **Commutative Ring**: ab = ba for all a, b ∈ R
- **Ring with Unity (Identity)**: ∃ 1 ∈ R such that 1·a = a·1 = a for all a
- **Integral Domain**: Commutative ring with unity and no zero divisors
- **Division Ring**: Every non-zero element has a multiplicative inverse
- **Field**: Commutative division ring

### Important Elements
- **Zero Element**: 0 ∈ R such that a + 0 = a for all a (additive identity)
- **Unity/Identity**: 1 ∈ R such that 1·a = a·1 = a (multiplicative identity)
- **Zero Divisor**: Non-zero a such that ∃ non-zero b with ab = 0
- **Unit**: Element u with multiplicative inverse (u·v = 1)
- **Idempotent**: Element a such that a² = a

### Properties of Rings
- a · 0 = 0 · a = 0 for all a ∈ R
- (−a)b = a(−b) = −(ab)
- (−a)(−b) = ab
- If R has unity: (−1)a = −a
- a(b − c) = ab − ac (distributive law variant)

### Examples of Rings
- **(ℤ, +, ×)**: Integers (commutative, with unity, integral domain)
- **(ℤₙ, +ₙ, ×ₙ)**: Integers modulo n (commutative, with unity)
- **(ℚ, +, ×)**, **(ℝ, +, ×)**, **(ℂ, +, ×)**: Fields
- **M₂(ℝ)**: 2×2 matrices (non-commutative, with unity)
- **2ℤ**: Even integers (commutative, no unity)

### Subrings
- A subset S of ring R is a **subring** if:
  - (S, +) is a subgroup of (R, +)
  - S is closed under multiplication
  - If R has unity 1, then 1 ∈ S (convention varies)

### Ideals
- A subring I of R is an **ideal** if:
  - ∀ r ∈ R, a ∈ I: ra ∈ I and ar ∈ I
- Ideals are to rings what normal subgroups are to groups
- Used to construct quotient rings

### Exam Questions
1. Prove that in any ring R, a · 0 = 0 for all a ∈ R.
2. Define an integral domain and give two examples.
3. Show that (2ℤ, +, ×) is a ring. Does it have a unity?
4. What is a zero divisor? Give an example from ℤ₆.
5. Prove that if R is a ring with unity, then the unity element is unique.

---

## 11. Fields - Definition and Elementary Properties

### Definition
- A **field** (F, +, ·) is a commutative ring with unity where every non-zero element has a multiplicative inverse
- Requirements:
  - **(F, +) is an abelian group**
  - **(F*, ·) is an abelian group** (F* = F \ {0})
  - **Distributive law**: a(b + c) = ab + ac

### Equivalent Characterization
A field is:
- A commutative ring with unity
- In which every non-zero element is a unit
- No zero divisors exist (a·b = 0 ⟹ a = 0 or b = 0)

### Properties of Fields
- Every field is an **integral domain**
- Every finite integral domain is a field
- Fields have exactly two ideals: {0} and F itself
- Characteristic of a field: smallest n such that n·1 = 0 (or 0 if no such n exists)
- Characteristic is either 0 or prime

### Examples of Fields
- **ℚ**: Rational numbers (characteristic 0, infinite)
- **ℝ**: Real numbers (characteristic 0, infinite)
- **ℂ**: Complex numbers (characteristic 0, infinite)
- **ℤₚ** (p prime): Integers mod p (characteristic p, finite)
- **GF(pⁿ)**: Galois fields of order pⁿ

### Non-Examples
- **ℤ**: Not a field (2 has no multiplicative inverse)
- **ℤ₆**: Not a field (2·3 = 0, has zero divisors)
- **M₂(ℝ)**: Not a field (non-commutative, has zero divisors)

### Subfields
- A subset K of field F is a **subfield** if K is itself a field under the same operations
- Examples:
  - ℚ is a subfield of ℝ
  - ℝ is a subfield of ℂ

### Prime Fields
- A **prime field** has no proper subfields
- Every field contains a unique smallest subfield (its prime field)
- Prime fields:
  - Characteristic 0: ℚ
  - Characteristic p: ℤₚ

### Field Extensions
- If K is a subfield of F, then F is a **field extension** of K
- Notation: F/K or F:K
- Degree of extension: [F:K] = dimension of F as a vector space over K

### Important Theorems
- **Every finite integral domain is a field**
- **Characteristic of a field is 0 or prime**
- **ℤₙ is a field ⟺ n is prime**
- Fields have no non-trivial ideals

### Exam Questions
1. Prove that every field is an integral domain.
2. Show that ℤ₅ is a field, but ℤ₆ is not.
3. What is the characteristic of a field? Find the characteristic of ℚ, ℝ, and ℤ₇.
4. Prove that in a field, if ab = 0, then either a = 0 or b = 0.
5. State and prove that every finite integral domain is a field.

---

## 📌 FINAL SUMMARY - Last Minute Reference

### Essential Definitions

**Group (G, *)**: 
- Closure, Associativity, Identity, Inverse
- Abelian if commutative

**Subgroup H ≤ G**:
- Non-empty, closed under operation and inverses
- One-step test: ab⁻¹ ∈ H

**Cyclic Group**:
- G = ⟨a⟩ = {aⁿ : n ∈ ℤ}
- All cyclic groups are abelian

**Normal Subgroup N ⊴ G**:
- gNg⁻¹ = N for all g ∈ G
- Equivalently: gN = Ng

**Ring (R, +, ·)**:
- (R, +) is abelian group
- Multiplication associative + distributive

**Field F**:
- Commutative ring with unity
- Every non-zero element has inverse

---

### Key Formulas

**Order of element a^k in cyclic group of order n**:
- |aᵏ| = n/gcd(k, n)

**Number of generators of ℤₙ**:
- φ(n) where gcd(k, n) = 1

**Lagrange's Theorem**:
- |G| = |H| × [G : H]
- |H| divides |G|

**Order of quotient group**:
- |G/N| = |G| / |N|

**Order of permutation**:
- LCM of cycle lengths

**First Isomorphism Theorem**:
- G/Ker(φ) ≅ Im(φ)

**Number of elements in Sₙ**:
- |Sₙ| = n!

**Number of even permutations**:
- |Aₙ| = n!/2

---

### Critical Properties

**Groups**:
- Identity is unique
- Inverse is unique
- (ab)⁻¹ = b⁻¹a⁻¹
- Cancellation laws hold

**Subgroups**:
- {e} and G always subgroups
- Intersection of subgroups is subgroup
- Union generally NOT a subgroup

**Cosets**:
- aH = bH ⟺ a⁻¹b ∈ H
- All cosets have same size as H
- Cosets partition G

**Cyclic Groups**:
- Every subgroup is cyclic
- Subgroup of order d exists for each d | n
- All cyclic groups are abelian

**Normal Subgroups**:
- All subgroups of abelian groups are normal
- [G : H] = 2 ⟹ H ⊴ G
- Ker(φ) is always normal

**Homomorphisms**:
- φ(e) = e'
- φ(a⁻¹) = [φ(a)]⁻¹
- Ker(φ) ⊴ G
- φ injective ⟺ Ker(φ) = {e}

**Rings**:
- a · 0 = 0
- (−a)b = −(ab)
- Unity is unique (if exists)

**Fields**:
- No zero divisors
- Characteristic 0 or prime
- ℤₙ is field ⟺ n is prime

---

### Important Results Summary

✓ **All cyclic groups are abelian**
✓ **Every subgroup of cyclic group is cyclic**
✓ **Groups of prime order are cyclic**
✓ **Every finite integral domain is a field**
✓ **Every field is an integral domain**
✓ **Kernel of homomorphism is normal subgroup**
✓ **aⁿ = e for all a in group of order n**

---

### Quick Recognition Guide

**Is it a Group?**
- Check: Closure, Associativity, Identity, Inverse

**Is it Cyclic?**
- Find generator: does ⟨a⟩ = G?

**Is H a Subgroup?**
- Use one-step test: ab⁻¹ ∈ H?

**Is N Normal?**
- Check: gNg⁻¹ ⊆ N for all g?
- Or check: gN = Ng for all g?

**Is it a Field?**
- Commutative ring with unity?
- Every non-zero element invertible?

---

### Common Exam Tricks

1. **Finding subgroups**: Use divisors of |G| (Lagrange)
2. **Generators**: Check gcd(k, n) = 1
3. **Order of element**: Use |aᵏ| = n/gcd(k,n)
4. **Normal subgroups**: Check index = 2, or kernel
5. **Quotient group size**: |G|/|N|
6. **Isomorphism**: Check Ker(φ) = {e} for injection
7. **Fields**: ℤₚ is field only if p is prime
8. **Permutation order**: LCM of cycle lengths
9. **Coset equality**: Show a⁻¹b ∈ H
10. **Ring properties**: Always verify 0·a = 0

---

### Study Checklist

□ Can you prove identity/inverse uniqueness?
□ Know all four group axioms by heart?
□ Understand coset properties completely?
□ Can state Lagrange's theorem + proof outline?
□ Know when subgroups are normal?
□ Understand First Isomorphism Theorem?
□ Can compute in symmetric groups?
□ Know ring vs field distinction?
□ Can verify homomorphisms?
□ Understand characteristic of fields?

**Good luck with your exam! 🎯**