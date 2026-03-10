# 🟣 ZenYukti
### Smart Notes for Serious Students
> 🌐 [zenyukti.in](https://zenyukti.in)

---

# 📚 Automata Theory — Exam Notes
> **Unit: Basic Concepts and Automata Theory**

---

## 1. Introduction to Theory of Computation

### Three Central Areas
- **Automata** — Study of abstract machines and what problems they can solve
- **Computability** — What can/cannot be computed at all (decidability)
- **Complexity** — How much time/space is needed to solve a problem

---

## 2. Basic Definitions

- **Symbol** — A basic/atomic unit (character), e.g., `a`, `b`, `0`, `1`
- **Alphabet (Σ)** — A finite, non-empty set of symbols, e.g., `Σ = {0, 1}`
- **String (Word)** — A finite sequence of symbols from an alphabet, e.g., `0110`
  - **Empty String (ε)** — String with zero symbols; length = 0
  - **Length of string** `|w|` — Number of symbols in string `w`
  - **Concatenation** — Joining two strings: if `x = ab`, `y = cd`, then `xy = abcd`
  - **Kleene Star (Σ*)** — Set of ALL strings over Σ including ε
  - **Σ⁺** — All strings over Σ **excluding** ε
- **Formal Language (L)** — Any subset of Σ*, i.e., a set of strings over an alphabet

---

## 3. Deterministic Finite Automaton (DFA)

### Definition
A **DFA** is a 5-tuple: **M = (Q, Σ, δ, q₀, F)**

| Component | Meaning |
|-----------|---------|
| **Q** | Finite set of **states** |
| **Σ** | **Input alphabet** |
| **δ** | **Transition function**: δ: Q × Σ → Q |
| **q₀** | **Start/Initial state** (q₀ ∈ Q) |
| **F** | Set of **Final/Accepting states** (F ⊆ Q) |

### Key Properties of DFA
- For every state and every input symbol, there is **exactly one** next state
- **No ambiguity** — fully deterministic
- **Dead/Trap state** — A non-accepting state that loops on all inputs

### Representation Methods
- **Transition Diagram** (State diagram) — Circles = states, arrows = transitions, double circle = final state
- **Transition Table** — Rows = states, columns = input symbols, entries = next state

### Acceptability
- A string `w` is **accepted** if starting from `q₀`, after reading all of `w`, the machine ends in a **final state (F)**
- A string is **rejected** if it ends in a non-final state
- **Language of DFA** `L(M)` = set of all strings accepted by M

---

## 4. Non-Deterministic Finite Automaton (NFA)

### Definition
An **NFA** is also a 5-tuple: **M = (Q, Σ, δ, q₀, F)**

| Component | Difference from DFA |
|-----------|---------------------|
| **δ** | δ: Q × Σ → **2^Q** (returns a **set** of states) |

### Key Properties of NFA
- For a state and input, there can be **zero, one, or multiple** next states
- **Multiple paths** can be explored simultaneously
- A string is **accepted** if **at least one** path leads to a final state
- **More expressive in representation** but NOT more powerful than DFA

### NFA vs DFA — Key Differences

| Feature | DFA | NFA |
|---------|-----|-----|
| Next states per transition | Exactly 1 | 0, 1, or many |
| Transition function output | Single state | Set of states |
| Dead state | Explicitly needed | Implicitly (empty set) |
| Complexity | Harder to design | Easier to design |
| Power | Equal | Equal |

---

## 5. Equivalence of DFA and NFA

> **Theorem:** For every NFA, there exists an equivalent DFA that accepts the same language.

### Subset Construction Algorithm (NFA → DFA)
1. Start state of DFA = `{q₀}` (set containing NFA's start state)
2. For each DFA state (which is a **set of NFA states**) and each input symbol:
   - Compute union of δ(q, a) for all q in the set
3. A DFA state is **final** if it contains **at least one NFA final state**
4. Continue until no new states are generated

> ⚠️ If NFA has `n` states, DFA can have up to **2ⁿ states** (exponential blowup)

---

## 6. NFA with ε-Transitions (ε-NFA)

### What is ε-Transition?
- A transition that occurs **without consuming any input symbol**
- Represented as moves on **ε (empty string)**
- Allows moving between states "for free"

### ε-Closure
- **ε-closure(q)** = Set of all states reachable from state `q` using **only ε-transitions** (including `q` itself)
- **ε-closure(S)** = Union of ε-closure of all states in set S

### ε-NFA Formal Definition
- Same 5-tuple but **δ: Q × (Σ ∪ {ε}) → 2^Q**

---

## 7. Equivalence of NFA with and without ε-Transitions

> **Theorem:** Every ε-NFA has an equivalent NFA (without ε-transitions) and DFA.

### ε-NFA → NFA Conversion
1. Compute **ε-closure** of each state
2. New transition: `δ'(q, a)` = ε-closure(δ(ε-closure(q), a))
3. A state is **final** if its ε-closure contains any final state of ε-NFA

### ε-NFA → DFA (Combined)
1. Start = ε-closure(q₀)
2. For each state set S and symbol a:
   - Move(S, a) = ε-closure of all states reachable from S on `a`
3. Mark as final if any NFA final state is included

---

## 8. Finite Automata with Output

### 8.1 Moore Machine

**Definition:** A **Moore Machine** is a 6-tuple: **(Q, Σ, Δ, δ, λ, q₀)**

| Component | Meaning |
|-----------|---------|
| **Q** | Finite set of states |
| **Σ** | Input alphabet |
| **Δ** | Output alphabet |
| **δ** | Transition function: Q × Σ → Q |
| **λ** | **Output function: Q → Δ** (output depends on **state**) |
| **q₀** | Initial state |

- **Output is associated with states**
- Output length = Input length + 1 (outputs on entering each state including start)

---

### 8.2 Mealy Machine

**Definition:** A **Mealy Machine** is a 6-tuple: **(Q, Σ, Δ, δ, λ, q₀)**

| Component | Meaning |
|-----------|---------|
| **λ** | **Output function: Q × Σ → Δ** (output depends on **state AND input**) |

- **Output is associated with transitions**
- Output length = Input length (one output per input symbol)

---

### 8.3 Moore vs Mealy — Quick Comparison

| Feature | Moore Machine | Mealy Machine |
|---------|--------------|---------------|
| Output depends on | **State only** | **State + Input** |
| Output function | λ: Q → Δ | λ: Q × Σ → Δ |
| Output timing | On entering state | On transition |
| Output length | \|input\| + 1 | \|input\| |
| States needed | Generally **more** | Generally **fewer** |

---

## 9. Equivalence of Moore and Mealy Machines

> **Theorem:** For every Moore machine, there is an equivalent Mealy machine and vice versa.

### Mealy → Moore Conversion
- Each state `q` in Mealy may need to be **split** into multiple states in Moore
- New state `[q, b]` created for each output `b` that leads into `q`
- Start state = `[q₀, λ(q₀, ε)]` (if initial output needed, add ε output)

### Moore → Mealy Conversion
- Simpler: For each transition `δ(q, a) = p`, set Mealy output = Moore output of **destination state** `p`
- i.e., `λ_mealy(q, a) = λ_moore(δ(q, a))`

---

## 10. Minimization of Finite Automata

> **Goal:** Find the **minimum state DFA** equivalent to a given DFA (unique up to isomorphism)

### Why Minimize?
- Reduce memory/computation
- Every regular language has a **unique minimum DFA**

### Table Filling Algorithm (Myhill-Nerode / Mark method)

**Steps:**
1. **Remove unreachable states** first (states not reachable from q₀)
2. Create a table of all pairs `(p, q)` where p ≠ q
3. **Mark** all pairs where one state is final and other is non-final (distinguishable base case)
4. **Iterate:** Mark pair `(p, q)` if for some input `a`, `(δ(p,a), δ(q,a))` is already marked
5. Repeat until no new pairs are marked
6. **Unmarked pairs** = **Equivalent (indistinguishable) states** → merge them
7. Build minimized DFA from equivalence classes

### Key Terms
- **Distinguishable states** — States that can be told apart by some input string
- **Indistinguishable states** — No string can distinguish them → can be merged
- **Equivalence class** — Group of indistinguishable states merged into one state

---

## 🔑 Summary Hierarchy

```
ε-NFA  ≡  NFA  ≡  DFA   (All recognize Regular Languages)
       ↓
  Moore Machine  ≡  Mealy Machine  (Finite Automata with Output)
```

---

---

# ❓ Top 10 Exam Questions with Answers

---

### Q1. What is a DFA? Give its formal definition.
**Answer:**
- A **Deterministic Finite Automaton** is a 5-tuple **(Q, Σ, δ, q₀, F)** where:
  - Q = finite set of states
  - Σ = input alphabet
  - δ: Q × Σ → Q = transition function (deterministic — exactly one next state)
  - q₀ = start state
  - F ⊆ Q = set of final/accepting states
- A string is accepted if the machine ends in a state ∈ F after reading the entire string.

---

### Q2. How does NFA differ from DFA? Are they equally powerful?
**Answer:**
- In NFA, δ: Q × Σ → **2^Q** — each transition can lead to a **set of states** (0, 1, or many)
- NFA accepts a string if **at least one** computation path reaches a final state
- **Yes**, NFA and DFA are **equally powerful** — both recognize exactly the class of **Regular Languages**
- Every NFA can be converted to an equivalent DFA using the **Subset Construction** algorithm

---

### Q3. Explain the Subset Construction (NFA to DFA conversion) with key steps.
**Answer:**
1. DFA start state = **{q₀}** (ε-closure if ε-NFA)
2. For each DFA state (set of NFA states) S and input `a`:  
   `δ_DFA(S, a) = ∪{ δ_NFA(q, a) | q ∈ S }`
3. A DFA state is **final** if it contains **at least one** NFA final state
4. Repeat for all new states until no new states are discovered
- **Worst case:** DFA can have **2ⁿ states** for an NFA with `n` states

---

### Q4. What is ε-closure? How is it used in ε-NFA to DFA conversion?
**Answer:**
- **ε-closure(q)** = set of all states reachable from `q` using **only ε-transitions** (including `q`)
- **ε-closure(S)** = union of ε-closure of all states in set S
- **In conversion:**
  - DFA start state = ε-closure(q₀)
  - For each state set S and input `a`:  
    `Move(S, a)` = ε-closure of all states reachable from S on `a`
  - Final if ε-closure contains any NFA final state

---

### Q5. Differentiate Moore Machine and Mealy Machine with output function.
**Answer:**

| | Moore | Mealy |
|-|-------|-------|
| Output function | **λ: Q → Δ** | **λ: Q × Σ → Δ** |
| Output depends on | State only | State + Input |
| Output per input | \|w\| + 1 | \|w\| |
| States | More | Fewer |

- **Moore** — output written on state (circle)
- **Mealy** — output written on transition (arrow)

---

### Q6. How do you convert a Moore Machine to a Mealy Machine?
**Answer:**
- For each transition `δ(q, a) = p` in Moore machine:
  - Set Mealy output: `λ_mealy(q, a) = λ_moore(p)` — output of **destination** state
- Same states and transitions; just move output from states to transitions
- This is always possible and the resulting Mealy machine is equivalent

---

### Q7. Explain the Minimization of DFA using the Table Filling Algorithm.
**Answer:**
1. Remove all **unreachable states**
2. Create a triangular table for all state pairs `(p, q)`
3. **Base:** Mark `(p, q)` if exactly one is a final state
4. **Induction:** Mark `(p, q)` if `(δ(p,a), δ(q,a))` is already marked for any input `a`
5. Repeat until no change
6. **Unmarked pairs** → merge into single equivalence class state
7. Construct minimized DFA from these classes

---

### Q8. What are distinguishable and indistinguishable states?
**Answer:**
- **Distinguishable:** States `p` and `q` are distinguishable if there exists a string `w` such that exactly one of `δ*(p,w)`, `δ*(q,w)` is a final state
- **Indistinguishable:** No such string exists — both states behave identically for all inputs
- Indistinguishable states can be **merged** without changing the language accepted
- The minimized DFA has **one state per equivalence class** of indistinguishable states

---

### Q9. Prove that the class of languages accepted by NFA = class accepted by DFA.
**Answer:**
- **DFA ⊆ NFA:** Every DFA is a special case of NFA (where |δ(q,a)| = 1 always) ✓
- **NFA ⊆ DFA:** Given any NFA N with n states, construct DFA D using **Subset Construction**:
  - States of D = subsets of Q (at most 2ⁿ)
  - D simulates all possible NFA computations in parallel
  - L(D) = L(N) — same language accepted
- Therefore: **NFA ≡ DFA** in language-recognizing power ✓

---

### Q10. What is the significance of ε-transitions? Give an example use case.
**Answer:**
- **ε-transitions** allow state changes **without reading input** — spontaneous moves
- **Significance:**
  - Simplify NFA construction (e.g., union of two automata — connect with ε to new start state)
  - Help in representing **concatenation and Kleene star** operations on languages easily
  - Do **not** add power — ε-NFA ≡ NFA ≡ DFA
- **Example:** To build NFA for `L₁ ∪ L₂`, create new start state with ε-transitions to start states of both NFA₁ and NFA₂
- **Removal:** Replace ε-transitions using ε-closure computation during NFA→DFA conversion

---

> 💡 **Last-minute tips:**
> - Always remember the 5-tuple definitions for DFA/NFA
> - Moore output → on **state** | Mealy output → on **transition**
> - Minimization: mark distinguishable pairs, merge unmarked ones
> - ε-closure always includes the state **itself**
> - NFA = DFA in power (not complexity of representation)

---

---
<center>
**ZenYukti** | *Empowering learners with smart, structured study resources.*

🌐 [zenyukti.in](https://zenyukti.in)

© 2026 ZenYukti. All rights reserved. 

This material is intended for personal educational use only. Unauthorized reproduction or distribution is prohibited.
</center>