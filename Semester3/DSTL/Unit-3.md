# Theory of Logics & Predicate Logic - Complete Study Notes

---

## 1. Proposition

### What is a Proposition?
- **Definition**: A declarative statement that is either TRUE or FALSE, but not both
- Must have a definite truth value
- Cannot be questions, commands, or exclamations

### Types of Propositions
- **Simple/Atomic Proposition**: Cannot be broken down further
  - Example: "It is raining" (p)
  - Example: "5 is an odd number" (q)
- **Compound/Molecular Proposition**: Formed by combining simple propositions using logical connectives
  - Example: "It is raining AND it is cold"
  - Example: "If x > 5, then x > 3"

### Logical Connectives
- **Negation (¬)**: NOT operator
  - ¬p reads as "not p"
  - Reverses the truth value
- **Conjunction (∧)**: AND operator
  - p ∧ q reads as "p and q"
  - True only when both are true
- **Disjunction (∨)**: OR operator
  - p ∨ q reads as "p or q"
  - False only when both are false
- **Conditional/Implication (→)**: IF-THEN operator
  - p → q reads as "if p then q"
  - False only when p is true and q is false
  - p is antecedent, q is consequent
- **Biconditional (↔)**: IF AND ONLY IF operator
  - p ↔ q reads as "p if and only if q"
  - True when both have same truth value

### Important Properties
- **Precedence Order**: ¬ > ∧ > ∨ > → > ↔
- Parentheses can override precedence
- Well-formed formulas follow proper syntax rules

### Exam-Focused Questions
1. **Identify which of the following are propositions and determine their truth values:**
   - a) "What time is it?"
   - b) "Paris is the capital of France"
   - c) "x + 2 = 5"
   - d) "This statement is false"

2. **Convert the following statements into propositional logic using appropriate connectives:**
   - "If it rains, then the ground is wet and the match is cancelled"
   - "Either the exam is easy or I studied well"

3. **Given p: "I study hard", q: "I pass the exam". Write the following in symbolic form:**
   - "I study hard but I don't pass the exam"
   - "If I don't study hard, then I don't pass the exam"

4. **What is the truth value of (p → q) when p is false and q is true? Explain why.**

5. **Construct the compound proposition: "If the server is down then the website is not accessible, and if the website is accessible then the server is not down."**

---

## 2. Truth Tables

### Definition
- **Truth Table**: A mathematical table showing all possible truth values of a logical expression
- Lists all possible combinations of input values
- Shows corresponding output for each combination

### Construction Rules
- For n propositional variables, there are 2ⁿ rows
- List all possible combinations systematically (usually in binary order)
- Evaluate complex expressions step-by-step from innermost to outermost

### Truth Tables for Basic Connectives

**Negation (¬p)**
| p | ¬p |
|---|-----|
| T | F |
| F | T |

**Conjunction (p ∧ q)**
| p | q | p ∧ q |
|---|---|-------|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | F |

**Disjunction (p ∨ q)**
| p | q | p ∨ q |
|---|---|-------|
| T | T | T |
| T | F | T |
| F | T | T |
| F | F | F |

**Implication (p → q)**
| p | q | p → q |
|---|---|-------|
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | T |

**Biconditional (p ↔ q)**
| p | q | p ↔ q |
|---|---|-------|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | T |

### Special Truth Tables
- **Exclusive OR (XOR)**: p ⊕ q = (p ∨ q) ∧ ¬(p ∧ q)
  - True when exactly one is true
- **NAND**: ¬(p ∧ q)
  - Functionally complete operator
- **NOR**: ¬(p ∨ q)
  - Functionally complete operator

### Applications
- Verify logical equivalences
- Check if formulas are tautology, contradiction, or contingency
- Design digital circuits
- Verify arguments validity

### Exam-Focused Questions
1. **Construct the truth table for: (p → q) ∧ (q → r) → (p → r)**

2. **Using truth tables, verify whether (p → q) ≡ (¬p ∨ q)**

3. **Create a truth table for: ¬(p ∧ q) ↔ (¬p ∨ ¬q) and identify what law this represents.**

4. **Given three propositions p, q, r, how many rows will the truth table have? Construct the truth table for (p ∨ q) → r**

5. **Prove using truth tables that p → (q → r) ≡ (p ∧ q) → r**

---

## 3. Tautology

### Definition
- **Tautology**: A compound proposition that is ALWAYS TRUE regardless of truth values of its components
- Every row in truth table shows T
- Also called a **valid formula**

### Examples of Tautologies
- **Law of Excluded Middle**: p ∨ ¬p
  - Either p is true or not-p is true
- **Law of Identity**: p → p
  - If p then p
- **Double Negation**: ¬(¬p) ↔ p
  - Not not p is equivalent to p
- **Implication Tautology**: p → (p ∨ q)
- **Modus Ponens Structure**: ((p → q) ∧ p) → q
- **Hypothetical Syllogism**: ((p → q) ∧ (q → r)) → (p → r)

### Properties
- Represented by symbol T or 1
- Disjunction of a proposition with its negation is always a tautology
- Used to establish logical equivalences
- Foundation for valid inference rules

### How to Identify
- Construct truth table - all entries in final column are T
- Use known tautologies and logical equivalences
- If ¬F is a tautology, then F is a contradiction

### Exam-Focused Questions
1. **Prove that ((p → q) ∧ ¬q) → ¬p is a tautology using truth table.**

2. **Show that (p ∧ q) → p is a tautology without constructing full truth table.**

3. **Is (p → q) ∨ (q → p) a tautology? Justify your answer.**

4. **Prove that ¬(p ↔ q) ↔ (p ↔ ¬q) is a tautology.**

5. **Given that p → q is a tautology, what can you conclude about p and q?**

---

## 4. Satisfiability

### Definition
- **Satisfiability**: A formula is satisfiable if there exists at least ONE assignment of truth values that makes it TRUE
- At least one row in truth table has T in final column
- Also called **consistent formula**

### Types of Formulas by Satisfiability
- **Tautology**: Always true (always satisfiable)
- **Satisfiable but not Tautology**: Sometimes true (contingency)
- **Unsatisfiable**: Never true (contradiction)

### Examples
- **Satisfiable**: p ∧ q
  - True when both p and q are true
- **Satisfiable**: p ∨ ¬p
  - This is also a tautology
- **Not Satisfiable**: p ∧ ¬p
  - This is a contradiction

### SAT Problem
- **Boolean Satisfiability Problem**: Determine if variables can be assigned values to make formula true
- First problem proven to be NP-complete
- Practical applications in:
  - Circuit design verification
  - Software verification
  - Planning problems
  - Scheduling

### Testing Satisfiability
- **Method 1**: Construct truth table, check for at least one T
- **Method 2**: Try to find a satisfying assignment directly
- **Method 3**: Use SAT solvers for complex formulas
- **Method 4**: Convert to CNF (Conjunctive Normal Form) and analyze

### Exam-Focused Questions
1. **Determine whether (p → q) ∧ (q → r) ∧ p ∧ ¬r is satisfiable.**

2. **Is the formula (p ∨ q) ∧ (¬p ∨ r) ∧ (¬q ∨ ¬r) satisfiable? If yes, provide a satisfying assignment.**

3. **Explain why every tautology is satisfiable, but not every satisfiable formula is a tautology.**

4. **Given the formula (p ∧ q) ∨ (¬p ∧ ¬q), find all satisfying truth assignments.**

5. **Convert the following to CNF and determine satisfiability: (p → q) ∧ (p ∨ r) ∧ ¬q ∧ ¬r**

---

## 5. Contradiction

### Definition
- **Contradiction**: A compound proposition that is ALWAYS FALSE regardless of truth values
- Every row in truth table shows F
- Also called **unsatisfiable formula** or **inconsistent formula**
- Represented by symbol F or 0

### Examples of Contradictions
- **Basic Contradiction**: p ∧ ¬p
  - Cannot be both true and false simultaneously
- **Complex Example**: (p → q) ∧ p ∧ ¬q
  - Contradicts modus ponens
- **Another Example**: (p ∨ q) ∧ ¬p ∧ ¬q
  - Claims both that one is true and both are false

### Properties
- Negation of a contradiction is a tautology
- If F is a contradiction, then ¬F is a tautology
- Conjunction with a contradiction always yields contradiction
- Disjunction with a contradiction yields the other proposition

### Relationship with Other Concepts
- **Contradiction vs Tautology**: Exact opposites
  - ¬(Tautology) = Contradiction
  - ¬(Contradiction) = Tautology
- **Contradiction vs Satisfiability**: 
  - Contradictions are unsatisfiable
  - Not satisfiable = contradiction

### Uses in Logic
- **Proof by Contradiction**: Assume ¬P and derive contradiction to prove P
- **Inconsistency Detection**: Identify conflicting requirements
- **Logical System Validation**: Check for internal consistency

### Exam-Focused Questions
1. **Prove that (p ∨ q) ∧ (¬p) ∧ (¬q) is a contradiction.**

2. **Show that if F is a contradiction, then F → p is a tautology for any proposition p.**

3. **Determine whether ((p → q) ∧ (q → r) ∧ p ∧ ¬r) is a contradiction.**

4. **Explain why (p ↔ q) ∧ (p ↔ ¬q) is a contradiction.**

5. **If p ∧ Q is a contradiction, what can you conclude about the relationship between p and Q?**

---

## 6. Algebra of Propositions

### Definition
- Set of laws and equivalences for manipulating logical expressions
- Similar to algebraic manipulation of mathematical expressions
- Used to simplify and transform logical formulas

### Logical Equivalence (≡)
- Two propositions are logically equivalent if they have identical truth values for all possible assignments
- Notation: P ≡ Q or P ⇔ Q
- Can substitute one for another in any formula

### Fundamental Laws

**Identity Laws**
- p ∧ T ≡ p
- p ∨ F ≡ p

**Domination Laws**
- p ∨ T ≡ T
- p ∧ F ≡ F

**Idempotent Laws**
- p ∨ p ≡ p
- p ∧ p ≡ p

**Double Negation Law**
- ¬(¬p) ≡ p

**Commutative Laws**
- p ∨ q ≡ q ∨ p
- p ∧ q ≡ q ∧ p

**Associative Laws**
- (p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
- (p ∧ q) ∧ r ≡ p ∧ (q ∧ r)

**Distributive Laws**
- p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
- p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)

**De Morgan's Laws** (Very Important)
- ¬(p ∧ q) ≡ ¬p ∨ ¬q
- ¬(p ∨ q) ≡ ¬p ∧ ¬q

**Absorption Laws**
- p ∨ (p ∧ q) ≡ p
- p ∧ (p ∨ q) ≡ p

**Negation Laws**
- p ∨ ¬p ≡ T (Law of Excluded Middle)
- p ∧ ¬p ≡ F (Law of Contradiction)

### Conditional Equivalences

**Implication Equivalence**
- p → q ≡ ¬p ∨ q (Most Important)
- p → q ≡ ¬q → ¬p (Contrapositive)

**Biconditional Equivalence**
- p ↔ q ≡ (p → q) ∧ (q → p)
- p ↔ q ≡ (p ∧ q) ∨ (¬p ∧ ¬q)

### Normal Forms

**Conjunctive Normal Form (CNF)**
- Conjunction of disjunctions
- Example: (p ∨ q) ∧ (¬p ∨ r) ∧ (q ∨ ¬r)
- Form: (literal₁ ∨ ... ∨ literalₙ) ∧ ... ∧ (literal₁ ∨ ... ∨ literalₘ)

**Disjunctive Normal Form (DNF)**
- Disjunction of conjunctions
- Example: (p ∧ q) ∨ (¬p ∧ r) ∨ (q ∧ ¬r)
- Form: (literal₁ ∧ ... ∧ literalₙ) ∨ ... ∨ (literal₁ ∧ ... ∧ literalₘ)

### Exam-Focused Questions
1. **Simplify the following using laws of propositional algebra: (p ∧ q) ∨ (p ∧ ¬q)**

2. **Prove using algebraic laws that (p → q) ∧ (p → ¬q) ≡ ¬p**

3. **Convert to CNF: (p → q) ∧ (r → s)**

4. **Use De Morgan's laws to simplify: ¬((p ∨ q) ∧ (r ∨ s))**

5. **Show that (p ∨ q) ∧ (¬p ∨ r) → (q ∨ r) is a tautology using algebraic manipulation.**

---

## 7. Theory of Inference

### Definition
- **Inference**: Process of deriving new propositions from given propositions
- **Argument**: Sequence of propositions with premises and conclusion
- **Valid Argument**: If premises are true, conclusion must be true
- **Sound Argument**: Valid argument with true premises

### Argument Structure
- **Premises**: Given propositions (P₁, P₂, ..., Pₙ)
- **Conclusion**: Derived proposition (Q)
- **Notation**: P₁, P₂, ..., Pₙ ⊢ Q or P₁ ∧ P₂ ∧ ... ∧ Pₙ → Q

### Rules of Inference

**Modus Ponens (Law of Detachment)**
- p → q
- p
- ∴ q
- "If p implies q, and p is true, then q is true"

**Modus Tollens**
- p → q
- ¬q
- ∴ ¬p
- "If p implies q, and q is false, then p is false"

**Hypothetical Syllogism**
- p → q
- q → r
- ∴ p → r
- "Chain of implications"

**Disjunctive Syllogism**
- p ∨ q
- ¬p
- ∴ q
- "If one of two is true, and first is false, second must be true"

**Addition**
- p
- ∴ p ∨ q
- "If p is true, then p or anything is true"

**Simplification**
- p ∧ q
- ∴ p (or ∴ q)
- "If both are true, each individually is true"

**Conjunction**
- p
- q
- ∴ p ∧ q
- "If both are true separately, their conjunction is true"

**Resolution**
- p ∨ q
- ¬p ∨ r
- ∴ q ∨ r
- "Elimination of complementary literals"

### Fallacies (Invalid Arguments)

**Fallacy of Affirming the Conclusion**
- p → q
- q
- ∴ p (INVALID)

**Fallacy of Denying the Hypothesis**
- p → q
- ¬p
- ∴ ¬q (INVALID)

### Testing Validity
- **Method 1**: Truth table - check if conclusion is true whenever all premises are true
- **Method 2**: Apply rules of inference step by step
- **Method 3**: Assume premises true and conclusion false; if contradiction, argument is valid
- **Method 4**: Use equivalence laws to transform premises into conclusion

### Exam-Focused Questions
1. **Determine the validity of: "If it rains, the ground is wet. The ground is not wet. Therefore, it is not raining." Identify the rule used.**

2. **Using rules of inference, prove: p → q, q → r, p ⊢ r**

3. **Show that the following argument is valid using rules of inference:**
   - p → q
   - r → s
   - p ∨ r
   - ¬q
   - ∴ s

4. **Identify the fallacy: "If I study, I will pass. I passed. Therefore, I studied."**

5. **Prove using inference rules: (p ∨ q), (p → r), (q → s) ⊢ (r ∨ s)**

---

## 8. Predicate Logic

### Definition
- **Predicate Logic**: Extension of propositional logic that deals with predicates and quantifiers
- Also called **First-Order Logic (FOL)** or **Predicate Calculus**
- Allows reasoning about objects, their properties, and relationships

### Components of Predicate Logic

**Objects/Individuals**
- Specific entities in the domain (constants)
- Examples: John, 5, New York
- Represented by lowercase letters: a, b, c, x, y, z

**Predicates**
- Properties or relations that can be true or false about objects
- Examples: isEven(x), isTallerThan(x, y), isPrime(n)
- **Unary Predicate**: Takes one argument - P(x)
- **Binary Predicate**: Takes two arguments - Q(x, y)
- **n-ary Predicate**: Takes n arguments - R(x₁, x₂, ..., xₙ)

**Functions**
- Map objects to objects
- Examples: father(x), sum(x, y), square(n)
- Represented by lowercase letters followed by arguments

**Variables**
- Represent arbitrary objects in domain
- Examples: x, y, z
- Can be bound (quantified) or free (unquantified)

### Difference from Propositional Logic
- Propositional logic: Treats statements as atomic units
- Predicate logic: Breaks statements into components
- Example: "All humans are mortal"
  - Propositional: p (single unit)
  - Predicate: ∀x (Human(x) → Mortal(x))

### Advantages
- More expressive power
- Can represent complex relationships
- Can reason about infinite domains
- Foundation for mathematics and programming

### Exam-Focused Questions
1. **Express "Every student in the class has read at least one book" in predicate logic.**

2. **What is the difference between P(x) and P(a) where x is a variable and a is a constant?**

3. **Given predicates Student(x) and Smart(x), write in predicate logic: "Some students are smart but not all students are smart."**

4. **Convert to predicate logic: "If someone is a parent, then they have a child."**

5. **Express "No even number is odd" using predicate logic with predicates Even(x) and Odd(x).**

---

## 9. First Order Predicate

### Definition
- **First-Order Predicate**: Predicates that quantify only over individuals/objects, not over predicates themselves
- Variables range over domain elements (objects)
- Cannot make statements about predicates or sets of predicates
- Foundation of mathematical logic

### Order Hierarchy
- **Zeroth-Order Logic**: Propositional logic (no variables)
- **First-Order Logic**: Variables range over individuals
- **Second-Order Logic**: Variables can range over predicates/sets
- **Higher-Order Logic**: Even more general quantification

### Structure of First-Order Statements

**Domain of Discourse (Universe)**
- Set of all objects under consideration
- Examples: All integers, All humans, All real numbers
- Domain must be clearly defined

**Atomic Formulas**
- Basic building blocks
- Form: P(t₁, t₂, ..., tₙ) where P is predicate, tᵢ are terms
- Terms can be constants, variables, or function applications

**Terms**
- **Constant**: Fixed object (a, b, c, John, 5)
- **Variable**: Placeholder (x, y, z)
- **Function Application**: f(t₁, ..., tₙ)
- Examples: x, father(John), sum(3, 4)

### Examples in Different Domains

**Number Domain**
- Domain: All integers
- isEven(x): "x is even"
- isPrime(n): "n is prime"
- greaterThan(x, y): "x > y"

**People Domain**
- Domain: All people
- isMale(x): "x is male"
- parentOf(x, y): "x is parent of y"
- age(x): Function returning age of x

**Geometric Domain**
- Domain: All geometric shapes
- isCircle(x): "x is a circle"
- intersects(x, y): "x intersects y"
- area(x): Function returning area of x

### Why "First-Order"?
- Quantification is only over domain elements (first-order entities)
- Cannot say "for all predicates P" (that would be second-order)
- Can say "for all x" where x is an object
- Restriction ensures decidability and consistency

### Exam-Focused Questions
1. **Explain why ∀P ∃x P(x) is not a first-order logic statement.**

2. **In first-order logic with domain of real numbers, express: "Every positive number has a square root."**

3. **Given domain of all students and predicates Enrolled(x, y) meaning "x is enrolled in course y", write: "Every student is enrolled in at least one course."**

4. **What is the domain of discourse for the statement: ∀x (x² ≥ 0)?**

5. **Convert to first-order logic: "There exists a number that is greater than all other numbers" and explain why this might be problematic.**

---

## 10. Well-Formed Formula (WFF) of Predicate

### Definition
- **Well-Formed Formula (WFF)**: Syntactically correct formula in predicate logic
- Must follow strict formation rules
- Also called **valid formula** or **grammatically correct formula**

### Formation Rules

**Rule 1: Atomic Formulas**
- If P is an n-ary predicate and t₁, ..., tₙ are terms, then P(t₁, ..., tₙ) is a WFF
- Example: Student(John), greaterThan(x, 5)

**Rule 2: Negation**
- If α is a WFF, then ¬α is a WFF
- Example: ¬Student(x), ¬(P(x) ∧ Q(x))

**Rule 3: Binary Connectives**
- If α and β are WFFs, then (α ∧ β), (α ∨ β), (α → β), (α ↔ β) are WFFs
- Example: (P(x) ∧ Q(y)) → R(z)

**Rule 4: Quantifiers**
- If α is a WFF and x is a variable, then (∀x α) and (∃x α) are WFFs
- Example: ∀x P(x), ∃y (Q(y) ∧ R(y))

**Rule 5: Nothing Else**
- Only formulas constructed by above rules are WFFs

### Examples of WFFs
- P(x) ✓
- ∀x (P(x) → Q(x)) ✓
- ∃y (R(y) ∧ ∀x S(x, y)) ✓
- ¬(∀x P(x)) ↔ (∃x ¬P(x)) ✓

### Examples of Non-WFFs
- P(x ✗ (missing closing parenthesis)
- ∀ P(x) ✗ (quantifier without variable)
- ∀x ∧ Q(x) ✗ (improper use of connective)
- P ∨ (x) ✗ (predicate without proper application)

### Components of WFF

**Terms**
- Constants: a, b, c, 1, 2
- Variables: x, y, z
- Functions: f(x), g(x, y)

**Formulas**
- Atomic: P(x), Q(x, y)
- Compound: Using connectives and quantifiers

### Variable Scope

**Bound Variables**
- Variable governed by a quantifier
- In ∀x P(x), x is bound
- In ∃y (P(y) ∧ Q(y)), y is bound throughout

**Free Variables**
- Not governed by any quantifier
- In P(x) ∧ ∀y Q(y), x is free, y is bound
- In ∃x P(x, y), x is bound, y is free

**Scope of Quantifier**
- Range where quantifier applies
- ∀x (P(x) → Q(x)): scope is (P(x) → Q(x))
- Usually indicated by parentheses

### Closed vs Open Formulas

**Closed Formula (Sentence)**
- No free variables
- Has definite truth value
- Example: ∀x P(x), ∃y (Q(y) ∧ ∀z R(z))

**Open Formula**
- Contains free variables
- Truth value depends on variable assignment
- Example: P(x), Q(x) ∧ ∃y R(y)

### Exam-Focused Questions
1. **Determine which are WFFs and which are not:**
   - a) ∀x (P(x) → Q(x, y))
   - b) ∃x P(x) ∧ Q(y)
   - c) ∀x ∃y ∀z (P(x, y) → Q(y, z))
   - d) P(x, ) ∨ Q(y)

2. **Identify bound and free variables in: ∀x (P(x, y) → ∃z Q(z, y))**

3. **Write a WFF expressing: "For every x, if x is even, there exists a y such that x = 2y"**

4. **Is ∀x (P(x)) ∨ Q(y) a closed formula? Explain.**

5. **Construct a WFF with at least two quantifiers expressing: "Everyone has a parent who is older than them."**

---

## 11. Quantifiers

### Definition
- **Quantifiers**: Symbols that specify the quantity of objects in domain satisfying a predicate
- Express "all" or "some" in formal logic
- Bind variables in predicates

### Types of Quantifiers

### Universal Quantifier (∀)

**Notation**: ∀x P(x)
- Reads: "For all x, P(x)" or "Every x satisfies P"
- Symbol: ∀ (inverted A for "All")

**Meaning**
- P(x) is true for every object x in the domain
- All domain elements satisfy the predicate

**Examples**
- ∀x (x + 0 = x): "For all x, adding zero gives x"
- ∀n (Even(n) → Divisible(n, 2)): "All even numbers are divisible by 2"
- ∀x (Human(x) → Mortal(x)): "All humans are mortal"

**Truth Conditions**
- True if P(x) is true for EVERY x in domain
- False if even ONE counterexample exists

### Existential Quantifier (∃)

**Notation**: ∃x P(x)
- Reads: "There exists x such that P(x)" or "Some x satisfies P"
- Symbol: ∃ (inverted E for "Exists")

**Meaning**
- P(x) is true for at least one object x in the domain
- At least one domain element satisfies the predicate

**Examples**
- ∃x (x² = 4): "There exists an x such that x squared equals 4"
- ∃n Prime(n): "There exists a prime number"
- ∃x (Student(x) ∧ Smart(x)): "Some student is smart"

**Truth Conditions**
- True if P(x) is true for AT LEAST ONE x in domain
- False if no x satisfies P(x)

### Unique Existential Quantifier (∃!)

**Notation**: ∃!x P(x)
- Reads: "There exists exactly one x such that P(x)"
- Means: ∃x (P(x) ∧ ∀y (P(y) → y = x))

**Examples**
- ∃!x (x + 5 = 8): "Exactly one number when added to 5 gives 8"
- ∃!p (President(p) ∧ CurrentlyServing(p)): "Exactly one current president"

### Nested Quantifiers

**Multiple Quantifiers**
- Order matters significantly
- ∀x ∃y P(x, y) ≠ ∃y ∀x P(x, y)

**∀x ∃y P(x, y)**
- "For every x, there exists some y such that P(x, y)"
- Different y may exist for different x
- Example: ∀x ∃y (y > x): "For every number, there's a larger one"

**∃y ∀x P(x, y)**
- "There exists a y such that for all x, P(x, y)"
- Same y works for all x
- Example: ∃y ∀x (y > x): "There's a number larger than all numbers" (FALSE for reals)

**∀x ∀y P(x, y)**
- "For all x and all y, P(x, y)"
- Example: ∀x ∀y (x + y = y + x): "Addition is commutative"

**∃x ∃y P(x, y)**
- "There exist x and y such that P(x, y)"
- Example: ∃x ∃y (x < y): "There are two numbers where one is less than the other"

### Quantifier Negation Rules

**De Morgan's Laws for Quantifiers**
- ¬(∀x P(x)) ≡ ∃x ¬P(x)
  - "Not all satisfy P" = "Some don't satisfy P"
- ¬(∃x P(x)) ≡ ∀x ¬P(x)
  - "None exists satisfying P" = "All don't satisfy P"

**Nested Quantifier Negation**
- ¬(∀x ∃y P(x, y)) ≡ ∃x ∀y ¬P(x, y)
- ¬(∃x ∀y P(x, y)) ≡ ∀x ∃y ¬P(x, y)

### Domain Dependence
- Truth value depends on domain of discourse
- ∀x (x² ≥ 0) is true for reals, meaningless for colors
- Always specify or understand the domain

### Common Translations

**"All A are B"**
- ∀x (A(x) → B(x))
- Use implication (→)

**"Some A are B"**
- ∃x (A(x) ∧ B(x))
- Use conjunction (∧)

**"No A are B"**
- ∀x (A(x) → ¬B(x)) or ¬∃x (A(x) ∧ B(x))

**"Not all A are B"**
- ∃x (A(x) ∧ ¬B(x))

### Exam-Focused Questions
1. **Translate to predicate logic: "Every student who studies hard passes the exam."**

2. **What is the difference in meaning between ∀x ∃y Loves(x, y) and ∃y ∀x Loves(x, y)?**

3. **Negate the following and simplify: ∀x ∃y (P(x, y) → Q(y))**

4. **Express using quantifiers: "There is exactly one even prime number."**

5. **Given domain of integers, determine truth value: ∀x ∃y (x + y = 0)**

---

## 12. Inference Theory of Predicate Logic

### Definition
- **Inference in Predicate Logic**: Rules for deriving new formulas from given formulas
- Extension of propositional inference rules
- Additional rules for quantifiers

### Rules from Propositional Logic
- All propositional inference rules still apply
- Modus Ponens, Modus Tollens, etc.
- Applied to predicate formulas

### Quantifier Inference Rules

### Universal Instantiation (UI)

**Rule**: ∀x P(x) ⊢ P(c) where c is any constant
- From "for all x", we can infer it holds for any specific c
- Example: ∀x Mortal(x) ⊢ Mortal(Socrates)

**Application**
- Can instantiate with any term in the domain
- Multiple instantiations allowed
- Foundation for reasoning about individuals

### Universal Generalization (UG)

**Rule**: P(c) ⊢ ∀x P(x) where c is arbitrary
- If P holds for arbitrary c, it holds for all x
- c must not be specifically chosen, must be arbitrary

**Conditions**
- c must be arbitrary (not a specific constant)
- No assumptions made about c
- Example: If proven for arbitrary n, true for all n

**Caution**
- Cannot generalize from specific instances
- "Socrates is mortal" doesn't prove "All are mortal"

### Existential Instantiation (EI)

**Rule**: ∃x P(x) ⊢ P(c) where c is a new constant
- If something exists satisfying P, call it c
- c must be a NEW name not used before
- Example: ∃x Witness(x) ⊢ Witness(w) (w is new)

**Conditions**
- c must be fresh/new constant
- Cannot reuse existing constants
- Use only once per existential

### Existential Generalization (EG)

**Rule**: P(c) ⊢ ∃x P(x)
- If P holds for specific c, then something exists satisfying P
- Example: Mortal(Socrates) ⊢ ∃x Mortal(x)

**Application**
- Always valid from specific to existential
- Can generalize from any term
- Used to establish existence

### Additional Inference Rules

**Universal Modus Ponens**
- ∀x (P(x) → Q(x))
- P(a)
- ∴ Q(a)

**Universal Modus Tollens**
- ∀x (P(x) → Q(x))
- ¬Q(a)
- ∴ ¬P(a)

### Resolution in Predicate Logic

**Unification**
- Process of making different terms identical
- Example: P(x) and P(a) can unify with substitution {x/a}

**Resolution Rule**
- Extends propositional resolution
- Requires unification of predicates
- Used in automated theorem proving

### Proof Strategies

**Direct Proof**
1. Assume premises
2. Apply inference rules step by step
3. Derive conclusion

**Proof by Cases**
- Consider all possible cases
- Prove conclusion in each case

**Proof by Contradiction**
1. Assume negation of conclusion
2. Derive contradiction
3. Conclude original statement

### Common Proof Patterns

**Proving ∀x P(x)**
1. Let x be arbitrary
2. Show P(x) holds
3. Generalize to ∀x P(x)

**Proving ∃x P(x)**
1. Find specific witness c
2. Show P(c) holds
3. Generalize to ∃x P(x)

**Proving ∀x (P(x) → Q(x))**
1. Assume arbitrary x and P(x)
2. Derive Q(x)
3. Generalize

### Example Proof

**Prove**: ∀x (P(x) → Q(x)), ∀x P(x) ⊢ ∀x Q(x)

1. ∀x (P(x) → Q(x))          [Premise]
2. ∀x P(x)                    [Premise]
3. Let c be arbitrary         [Assumption]
4. P(c) → Q(c)                [UI from 1]
5. P(c)                       [UI from 2]
6. Q(c)                       [Modus Ponens on 4, 5]
7. ∀x Q(x)                    [UG from 6]

### Restrictions and Cautions

**UI Restrictions**
- Can instantiate to any term
- Can use multiple times

**UG Restrictions**
- Variable must be arbitrary
- Not derived from EI
- No free assumptions about it

**EI Restrictions**
- Must use NEW constant
- Use only once per existential statement
- Cannot use if constant already exists

**EG Restrictions**
- Can always be applied
- No special restrictions

### Exam-Focused Questions
1. **Prove using inference rules: ∀x (P(x) → Q(x)), ∀x (Q(x) → R(x)), P(a) ⊢ R(a)**

2. **What is wrong with this proof?**
   - ∃x P(x) [Given]
   - P(a) [EI]
   - ∃x P(x) [Given again]
   - P(a) [EI - using same constant]

3. **Prove: ∀x P(x), ∀x (P(x) → Q(x)) ⊢ ∀x Q(x)**

4. **Show that ∀x (P(x) ∨ Q(x)) ⊢ (∀x P(x)) ∨ (∃x Q(x)) is invalid by providing a counterexample.**

5. **Use inference rules to prove: ∀x (Student(x) → Smart(x)), Student(John) ⊢ Smart(John)**

---

## 📝 ONE-PAGE LAST MINUTE SUMMARY

### 🔑 KEY FORMULAS & LAWS

**Basic Logical Connectives**
- ¬p: NOT p (negation)
- p ∧ q: p AND q (conjunction)
- p ∨ q: p OR q (disjunction)
- p → q: IF p THEN q (implication)
- p ↔ q: p IFF q (biconditional)

**Critical Equivalences**
- p → q ≡ ¬p ∨ q ⭐ (MOST IMPORTANT)
- p → q ≡ ¬q → ¬p (Contrapositive)
- p ↔ q ≡ (p → q) ∧ (q → p)
- ¬(p ∧ q) ≡ ¬p ∨ ¬q ⭐ (De Morgan's)
- ¬(p ∨ q) ≡ ¬p ∧ ¬q ⭐ (De Morgan's)

**Quantifier Negations**
- ¬(∀x P(x)) ≡ ∃x ¬P(x) ⭐
- ¬(∃x P(x)) ≡ ∀x ¬P(x) ⭐

**Key Laws**
- p ∨ ¬p ≡ T (Excluded Middle)
- p ∧ ¬p ≡ F (Contradiction)
- ¬(¬p) ≡ p (Double Negation)
- p ∨ T ≡ T (Domination)
- p ∧ F ≡ F (Domination)

### 🎯 QUICK DEFINITIONS

**Tautology**: Always TRUE (all T in truth table)
**Contradiction**: Always FALSE (all F in truth table)
**Satisfiable**: At least one TRUE (at least one T in truth table)
**Valid Argument**: If premises true, conclusion must be true
**WFF**: Syntactically correct formula following formation rules

### 🚀 INFERENCE RULES (Propositional)

1. **Modus Ponens**: p → q, p ⊢ q ⭐
2. **Modus Tollens**: p → q, ¬q ⊢ ¬p ⭐
3. **Hypothetical Syllogism**: p → q, q → r ⊢ p → r
4. **Disjunctive Syllogism**: p ∨ q, ¬p ⊢ q
5. **Resolution**: p ∨ q, ¬p ∨ r ⊢ q ∨ r

### 🎓 PREDICATE LOGIC ESSENTIALS

**Quantifier Rules**
- **UI**: ∀x P(x) ⊢ P(c) (any constant)
- **UG**: P(c) ⊢ ∀x P(x) (c arbitrary)
- **EI**: ∃x P(x) ⊢ P(c) (NEW constant)
- **EG**: P(c) ⊢ ∃x P(x) (any constant)

**Translations**
- "All A are B" → ∀x (A(x) → B(x)) ⭐ Use →
- "Some A are B" → ∃x (A(x) ∧ B(x)) ⭐ Use ∧
- "No A are B" → ∀x (A(x) → ¬B(x))
- ∀x ∃y P(x,y) ≠ ∃y ∀x P(x,y) ⭐ Order matters!

### ⚡ EXAM TRICKS & TIPS

**Truth Table Tricks**
- For n variables: 2ⁿ rows
- Tautology: All TRUE column
- Contradiction: All FALSE column
- To prove equivalence: columns must match

**Implication p → q Truth**
- Only FALSE when: p=T and q=F
- Remember: "False implies anything" (F → T is TRUE)

**Quantifier Order**
- ∀x ∃y: "For each x, find some y" (easier to satisfy)
- ∃y ∀x: "Find one y that works for all x" (harder)

**Proof Strategy**
- For ∀: Pick arbitrary element, prove for it
- For ∃: Find ONE example that works
- For →: Assume antecedent, derive consequent
- For ¬: Assume opposite, find contradiction

**Common Mistakes to Avoid**
- Don't confuse → with ∧ in "All A are B"
- Don't use same constant in multiple EI
- Remember De Morgan's when negating quantifiers
- Check variable scope in nested quantifiers

**Quick Validity Check**
- Find row where all premises TRUE
- If conclusion FALSE there → INVALID
- If conclusion TRUE in all such rows → VALID

### 🔥 MUST REMEMBER

1. **p → q ≡ ¬p ∨ q** (Test favorite!)
2. De Morgan's for both connectives AND quantifiers
3. Quantifier order matters: ∀∃ ≠ ∃∀
4. EI requires NEW constant
5. For proofs: UI first, then rules, then UG/EG
6. Tautology = Valid = Unsatisfiable negation

**Final Tip**: Practice translating English to logic and back. Most errors come from misreading "all" vs "some"!

---

**End of Notes - Good Luck! 🎯**