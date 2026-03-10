# 🟣 ZenYukti
### Smart Notes for Serious Students
> 🌐 [zenyukti.in](https://zenyukti.in)

---

# 📚 Regular Expressions & Languages — Exam Notes
> **Unit: Regular Expressions and Languages**

---

## 1. Regular Expressions (RE)

### Definition
- A **Regular Expression** is a **symbolic notation** to describe a **Regular Language**
- Built using basic symbols and operations

### Basic Regular Expressions over Σ
| Expression | Language Denoted |
|------------|-----------------|
| **∅** | Empty language (no strings) |
| **ε** | Language containing only empty string `{ε}` |
| **a** (a ∈ Σ) | Language `{a}` |
| **r₁ + r₂** | **Union**: L(r₁) ∪ L(r₂) |
| **r₁ · r₂** | **Concatenation**: L(r₁) · L(r₂) |
| **r\*** | **Kleene Star**: zero or more repetitions of r |
| **(r)** | Same language as r (grouping) |

### Operator Precedence (High to Low)
1. `*` (Kleene Star) — highest
2. `.` (Concatenation)
3. `+` (Union) — lowest

### Examples
- `(0+1)*` — All strings over {0,1} including ε
- `(0+1)*00(0+1)*` — All binary strings containing `00`
- `0*1*` — Zero or more 0s followed by zero or more 1s
- `(00)*(11)*` — Even number of 0s followed by even number of 1s
- `(0+1)*1(0+1)` — All binary strings where second-last symbol is `1`

### Identities of Regular Expressions
- `∅ + r = r` (identity for union)
- `ε · r = r · ε = r` (identity for concatenation)
- `∅ · r = r · ∅ = ∅` (annihilator)
- `r* = r+ + ε`
- `r** = r*`
- `(r + s)* = (r* s*)* = (r* + s*)*`
- `r+ = r · r*`

---

## 2. Transition Graph (Generalized NFA)

### Definition
- A **Transition Graph (TG)** is a generalization of NFA where:
  - **Edge labels** can be **Regular Expressions** (not just single symbols)
  - Multiple start/final states may exist
  - Accepts a string if some path from start to final state exists whose labels concatenate to the string

### Key Points
- More powerful **representation** tool (not more power than DFA)
- Used in **Kleene's Theorem** proof
- **Arden's Theorem** uses algebraic form of transition graphs

---

## 3. Kleene's Theorem

> **Theorem:** A language is **Regular** if and only if it can be described by a **Regular Expression**.

### Two Parts:
- **Part 1:** If a language is accepted by a **FA (DFA/NFA)**, then there exists a **Regular Expression** for it
  - Method: Convert FA → Regular Expression using **state elimination** or **Arden's Theorem**
- **Part 2:** If a language is described by a **Regular Expression**, then there exists an **FA** that accepts it
  - Method: Convert RE → ε-NFA → NFA → DFA

### RE → FA (Construction)
| RE | Automaton |
|----|-----------|
| `∅` | FA with no accepting state |
| `ε` | FA: start = final, no transitions |
| `a` | FA: q₀ →(a)→ q₁ (final) |
| `r₁ + r₂` | NFA with ε-transitions to both FAs |
| `r₁ · r₂` | Connect FA₁ final states to FA₂ start via ε |
| `r*` | Add new start/final + ε-loops |

---

## 4. Finite Automata and Regular Expressions — Arden's Theorem

### Statement
> If **P** and **Q** are regular expressions over Σ, and **ε ∉ L(P)**, then the equation:
> **X = QP\* + ... → X = Q · P\***
>
> More precisely: The equation **X = XP + Q** has a **unique solution** X = **QP\***

### Arden's Theorem (Precise Form)
- Given: `X = XP + Q` where ε ∉ L(P)
- Solution: **X = QP\***
- This is the **unique** solution

### Algebraic Method Using Arden's Theorem (FA → RE)

**Steps:**
1. Write a **system of equations** for each state of the FA:
   - For each state `qᵢ`, write: `Rᵢ = (sum of Rⱼ·aⱼᵢ for each transition into qᵢ) + ε` (if qᵢ is start state)
2. **Solve** the system by substituting equations into each other
3. Apply **Arden's Theorem** wherever a variable appears on both sides
4. The expression for the **final state(s)** gives the Regular Expression

### Example Pattern
- If state q₀ is start and q₁ is final:
  - `R₀ = ε + R₀·a + R₁·b`
  - `R₁ = R₀·c`
  - Substitute R₁ into R₀, apply Arden's theorem → get R₀, then R₁ = answer

### Key Rules for Arden's Method
- If a **final state** has equation `X = XP + Q` → apply `X = QP*`
- If ε ∈ L(P), solution may **not be unique** (theorem doesn't apply directly)
- The RE for the language = expression of the **start state** in terms of final state equations

---

## 5. Regular and Non-Regular Languages

### Regular Languages
- Languages described by **Regular Expressions** or accepted by **Finite Automata**
- Examples:
  - All strings over {a,b}
  - Strings ending in `ab`
  - Strings with even number of a's

### Non-Regular Languages (require more powerful models)
- Examples:
  - `{aⁿbⁿ | n ≥ 1}` — equal number of a's and b's
  - `{aⁿ | n is a prime}`
  - `{ww | w ∈ {a,b}*}` — string repeated twice
- These **cannot** be recognized by any finite automaton

---

## 6. Closure Properties of Regular Languages

> A class of languages is **closed** under an operation if applying the operation to languages in the class gives a language still in the class.

### Regular Languages ARE Closed Under:

| Operation | Description |
|-----------|-------------|
| **Union** | L₁ ∪ L₂ is regular |
| **Concatenation** | L₁ · L₂ is regular |
| **Kleene Star** | L* is regular |
| **Complement** | L̄ = Σ* - L is regular |
| **Intersection** | L₁ ∩ L₂ is regular |
| **Difference** | L₁ - L₂ is regular |
| **Reversal** | L^R is regular |
| **Homomorphism** | h(L) is regular |
| **Inverse Homomorphism** | h⁻¹(L) is regular |

### Proof Techniques
- **Union/Concat/Star** — Directly via RE or NFA construction
- **Complement** — Swap final/non-final states in DFA
- **Intersection** — Use De Morgan's: `L₁ ∩ L₂ = complement(complement(L₁) ∪ complement(L₂))`
  - Or use **Product Construction** of two DFAs
- **Reversal** — Reverse all transitions, swap start/final states

---

## 7. Pigeonhole Principle

### Statement
> If **n+1** or more objects are placed into **n** boxes, then at least one box contains **two or more** objects.

### Application in Automata
- If a DFA has `n` states and a string of length `≥ n` is processed:
  - The machine visits **n+1 states** for n+1 transitions
  - By pigeonhole, **at least one state is repeated** → there is a **loop**
- This forms the basis of the **Pumping Lemma**

---

## 8. Pumping Lemma for Regular Languages

### Statement
> If **L** is a regular language, then there exists a constant **p ≥ 1** (pumping length) such that for every string **w ∈ L** with **|w| ≥ p**, we can write **w = xyz** where:
> 1. **|y| ≥ 1** (y is non-empty)
> 2. **|xy| ≤ p** (xy is within first p characters)
> 3. **∀ i ≥ 0, xyⁱz ∈ L** (pumping y any number of times stays in L)

### Key Intuition
- `p` = number of states in the DFA
- `y` corresponds to the **loop** found by Pigeonhole Principle
- Pumping y (repeating the loop) keeps the string in the language

### Important Notes
- Pumping Lemma is a **necessary** condition for regularity
- It is **NOT sufficient** — some non-regular languages may satisfy it
- Used as a **proof by contradiction** to show a language is **NOT regular**

---

## 9. Application of Pumping Lemma (Proving Non-Regularity)

### Method (Proof by Contradiction)
1. **Assume** L is regular with pumping length `p`
2. **Choose** a specific string `w ∈ L` with `|w| ≥ p` (choose cleverly!)
3. **Consider all possible** splits `w = xyz` satisfying `|y| ≥ 1` and `|xy| ≤ p`
4. **Show** that for some `i ≥ 0`, `xyⁱz ∉ L`
5. **Conclude** — contradiction! L is **not regular**

### Classic Example: L = {aⁿbⁿ | n ≥ 1}

1. Assume L is regular with pumping length `p`
2. Choose `w = aᵖbᵖ` ∈ L, |w| = 2p ≥ p ✓
3. Since `|xy| ≤ p` and `|y| ≥ 1`, y consists of **only a's** → `y = aᵏ` for some k ≥ 1
4. Pump: `xy²z = aᵖ⁺ᵏbᵖ` — more a's than b's → **∉ L**
5. Contradiction! ∴ L is **not regular** ✓

### Another Example: L = {aᵖ | p is prime}
1. Assume regular, pumping length `n`
2. Choose `w = aᵐ` where m is prime and m ≥ n
3. `w = xyz`, |y| = k ≥ 1
4. Pump i times: `xyⁱz` has length `m + (i-1)k`
5. Choose i such that `m + (i-1)k` is not prime → contradiction ✓

### Tips for Choosing the Right String `w`
- Use the **simplest** string that exploits the language's constraint
- For `aⁿbⁿ` → choose `aᵖbᵖ`
- For `aⁿ²` → choose `aᵖ²`
- For `wwR` → choose `aᵖbᵖ`

---

## 10. Decidability — Decision Properties

### What is Decidability?
- A **decision problem** is a yes/no question about a language/automaton
- A problem is **decidable** if there exists an algorithm that always gives a correct yes/no answer

### Key Decision Problems for Regular Languages (All Decidable ✅)

| Problem | Question | Algorithm |
|---------|----------|-----------|
| **Membership** | Is string `w ∈ L(M)`? | Run DFA M on w |
| **Emptiness** | Is `L(M) = ∅`? | Check if any final state is reachable from q₀ |
| **Finiteness** | Is `L(M)` finite? | Check for cycles on path from q₀ to final state |
| **Equivalence** | Is `L(M₁) = L(M₂)`? | Minimize both DFAs and check isomorphism |
| **Subset** | Is `L(M₁) ⊆ L(M₂)`? | Check `L(M₁) ∩ complement(L(M₂)) = ∅` |
| **Universality** | Is `L(M) = Σ*`? | Check complement is empty |

### Algorithms in Detail

- **Emptiness Test:**
  - Mark q₀, then mark all states reachable from marked states
  - If no final state is marked → L = ∅

- **Finiteness Test:**
  - Remove states not reachable from q₀ and not leading to final state
  - If remaining graph has a **cycle** → L is infinite
  - Else → L is finite

- **Equivalence Test:**
  - Minimize both DFAs → if same structure (isomorphic) → equivalent
  - OR: Check if `(L₁ - L₂) ∪ (L₂ - L₁) = ∅` (symmetric difference = ∅)

---

## 11. Finite Automata and Regular Languages — Key Connections

### Summary of Equivalences
```
Regular Expression  ←→  NFA  ←→  DFA  ←→  Regular Grammar
         ↑_________________________________↑
                  All describe Regular Languages
```

### Conversion Map
| From | To | Method |
|------|----|--------|
| RE | ε-NFA | Thompson's Construction |
| ε-NFA | NFA | ε-closure elimination |
| NFA | DFA | Subset Construction |
| DFA | RE | Arden's Theorem / State Elimination |
| DFA | Minimized DFA | Table Filling Algorithm |

### Regular Grammar ↔ FA
- **Right Linear Grammar** → NFA directly
- **DFA** → Right Linear Grammar: For each transition δ(A, a) = B, write rule A → aB; if B is final, add B → ε

---

# ❓ Top 12 Exam Questions with Answers

---

### Q1. What is a Regular Expression? State the operations used.
**Answer:**
- A **Regular Expression** is a formal notation to describe **Regular Languages** using:
  - **Union (r₁ + r₂):** strings in either language
  - **Concatenation (r₁ · r₂):** strings from r₁ followed by r₂
  - **Kleene Star (r*):** zero or more repetitions of r
- Base cases: ∅, ε, and individual symbols
- Precedence: `*` > `.` > `+`

---

### Q2. State and explain Kleene's Theorem.
**Answer:**
- **Kleene's Theorem:** A language L is regular **if and only if** it is denoted by some regular expression
- **Part 1 (FA → RE):** Any language accepted by a FA can be expressed as a RE
  - Convert using Arden's Theorem or state elimination on transition graph
- **Part 2 (RE → FA):** Any RE can be converted to an ε-NFA using Thompson's Construction:
  - RE for union → parallel NFA with ε-transitions
  - RE for concatenation → sequential NFA with ε-connections
  - RE for star → NFA with ε loop

---

### Q3. State Arden's Theorem and solve: X = X·a + b
**Answer:**
- **Arden's Theorem:** If ε ∉ L(P), the equation X = X·P + Q has unique solution **X = Q·P\***
- Given: `X = X·a + b`
  - Here P = `a`, Q = `b`, ε ∉ L(a) ✓
  - Solution: **X = b·a\***
  - This means: one `b` followed by zero or more `a`s

---

### Q4. Write the steps of the Algebraic Method using Arden's Theorem to convert DFA to RE.
**Answer:**
1. Write one equation per state based on incoming transitions
2. For start state qᵢ, add `+ ε` to its equation
3. Substitute equations to eliminate intermediate states
4. Wherever a variable appears on both sides (self-loop form), apply Arden's: `X = XP + Q → X = QP*`
5. The RE for the language = expression for the **start state** (or union of expressions for all final states)

---

### Q5. List the closure properties of Regular Languages.
**Answer:**
Regular languages are closed under:
- **Union:** L₁ ∪ L₂ — via NFA construction
- **Concatenation:** L₁ · L₂ — via NFA connection
- **Kleene Star:** L* — via NFA with ε-loop
- **Complement:** L̄ — swap final/non-final in DFA
- **Intersection:** L₁ ∩ L₂ — product construction or De Morgan's
- **Set Difference:** L₁ − L₂ = L₁ ∩ L̄₂
- **Reversal:** L^R — reverse transitions in DFA
- **Homomorphism & Inverse Homomorphism**

---

### Q6. State the Pumping Lemma. What is it used for?
**Answer:**
- **Statement:** For regular language L with pumping length `p`, every string `w ∈ L` with `|w| ≥ p` can be split as `w = xyz` where:
  1. `|y| ≥ 1`
  2. `|xy| ≤ p`
  3. `∀ i ≥ 0: xyⁱz ∈ L`
- **Used for:** Proving a language is **NOT regular** (proof by contradiction)
- **Note:** It's a necessary condition, not sufficient

---

### Q7. Prove that L = {aⁿbⁿ | n ≥ 1} is not regular using Pumping Lemma.
**Answer:**
1. Assume L is regular with pumping length `p`
2. Choose `w = aᵖbᵖ ∈ L`, |w| = 2p ≥ p ✓
3. Any split `w = xyz` with `|xy| ≤ p` and `|y| ≥ 1` means y = `aᵏ` (k ≥ 1) — only a's
4. Pump: `xy²z = aᵖ⁺ᵏbᵖ` → has more a's than b's → **∉ L**
5. This contradicts the pumping lemma ∴ L is **not regular** ✓

---

### Q8. What is the Pigeonhole Principle and how does it relate to Pumping Lemma?
**Answer:**
- **Pigeonhole Principle:** If n+1 items are put into n containers, some container has ≥ 2 items
- **In automata context:** A DFA with `n` states processing a string of length ≥ `n` visits `n+1` states
- By Pigeonhole, **at least one state repeats** → there is a **cycle** in the computation
- This cycle corresponds to the **y** part in pumping lemma — pumping y means going around the loop any number of times
- Thus Pigeonhole Principle is the **mathematical foundation** of Pumping Lemma

---

### Q9. What are decision properties of Regular Languages? List them.
**Answer:**
Decision properties are algorithmic yes/no questions about regular languages — all are **decidable**:
- **Membership:** Is w ∈ L(M)? — Run DFA on w
- **Emptiness:** Is L(M) = ∅? — Check reachability of final states
- **Finiteness:** Is L(M) finite? — Check for cycles on productive paths
- **Equivalence:** Is L(M₁) = L(M₂)? — Minimize both DFAs and compare
- **Universality:** Is L(M) = Σ*? — Check if complement is empty
- **Subset:** Is L(M₁) ⊆ L(M₂)? — Check L₁ ∩ L̄₂ = ∅

---

### Q10. How do you test if a Regular Language is empty or finite?
**Answer:**
- **Emptiness Test:**
  - Compute all states reachable from start state q₀
  - If none of them is a final state → **L = ∅**
  - Else → L ≠ ∅
- **Finiteness Test:**
  - Remove states not reachable from q₀ (useless states)
  - Remove states from which no final state is reachable (dead states)
  - In the remaining graph, check for **cycles**
  - If a cycle exists → **L is infinite**; else → **L is finite**

---

### Q11. Write RE for: (a) All binary strings with even number of 0s (b) All strings over {a,b} ending in 'abb'
**Answer:**
- **(a)** Even number of 0s over {0,1}:
  - `(1* 0 1* 0 1*)* = (1* 0 1* 0)* 1*`
  - Simplified: `(1*01*0)*1*`
- **(b)** Strings over {a,b} ending in `abb`:
  - `(a+b)*abb`

---

### Q12. What is a Transition Graph? How does it differ from NFA?
**Answer:**
- A **Transition Graph** is a generalized NFA where:
  - Edge labels can be **regular expressions** (not just single symbols or ε)
  - Can have **multiple start/final states**
- **Difference from NFA:**

| Feature | NFA | Transition Graph |
|---------|-----|-----------------|
| Edge labels | Single symbols or ε | Regular Expressions |
| Start states | One | Can be multiple |
| Power | Equal to DFA | Equal to DFA |
| Use | FA model | Intermediate in RE↔FA conversion |

- Used in **Kleene's Theorem** proof as intermediate representation

---

> 💡 **Last-minute tips:**
> - Pumping Lemma = proof tool to show **non-regularity** only
> - Arden's: `X = XP + Q → X = QP*` (remember ε ∉ P condition!)
> - Closure: Regular languages are closed under **all** Boolean operations
> - All decision problems for regular languages are **decidable**
> - Kleene's Theorem = bridge between RE and FA (both ways)
> - `|xy| ≤ p` forces `y` to be in the **first p characters**

---

---

<center>
<b>ZenYukti</b> | Empowering learners with smart, structured study resources.

🌐 [zenyukti.in](https://zenyukti.in)

© 2026 ZenYukti. All rights reserved. 

This material is intended for personal educational use only. Unauthorized reproduction or distribution is prohibited.

</center>