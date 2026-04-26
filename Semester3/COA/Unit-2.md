# Unit-2: Arithmetic and Logic Unit

---

## 1. Introduction to ALU

### What is ALU?
- **Arithmetic Logic Unit** - Heart of CPU
- Performs **arithmetic** and **logical** operations
- Works with **integer** and **floating-point** numbers

### ALU Components

```
┌─────────────────────────────────────┐
│              ALU                    │
│                                     │
│  ┌──────────────────────────────┐  │
│  │   Arithmetic Unit            │  │
│  │   (+, -, ×, ÷, Increment)    │  │
│  └──────────────────────────────┘  │
│                                     │
│  ┌──────────────────────────────┐  │
│  │   Logic Unit                 │  │
│  │   (AND, OR, NOT, XOR, Shift) │  │
│  └──────────────────────────────┘  │
│                                     │
│  ┌──────────────────────────────┐  │
│  │   Status Flags               │  │
│  │   (Zero, Carry, Sign, etc.)  │  │
│  └──────────────────────────────┘  │
└─────────────────────────────────────┘
```

### Status Flags

| Flag | Name | Purpose |
|------|------|---------|
| **C** | Carry | Set if carry/borrow occurs |
| **Z** | Zero | Set if result is zero |
| **S** | Sign | Set if result is negative |
| **V** | Overflow | Set if overflow occurs |
| **P** | Parity | Set if result has even parity |

---

## 2. Basic Addition and Subtraction

### 2.1 Binary Addition

#### Half Adder
```
Inputs: A, B
Outputs: Sum, Carry

Truth Table:
A  B | Sum  Carry
-----|------------
0  0 |  0    0
0  1 |  1    0
1  0 |  1    0
1  1 |  0    1

Logic:
Sum = A ⊕ B
Carry = A · B
```

#### Full Adder
```
Inputs: A, B, Cin (Carry-in)
Outputs: Sum, Cout (Carry-out)

Truth Table:
A  B  Cin | Sum  Cout
----------|------------
0  0   0  |  0    0
0  0   1  |  1    0
0  1   0  |  1    0
0  1   1  |  0    1
1  0   0  |  1    0
1  0   1  |  0    1
1  1   0  |  0    1
1  1   1  |  1    1

Logic:
Sum = A ⊕ B ⊕ Cin
Cout = AB + BCin + ACin
```

### 2.2 Ripple Carry Adder (4-bit)

```
    A3 B3    A2 B2    A1 B1    A0 B0
     │ │      │ │      │ │      │ │
     ▼ ▼      ▼ ▼      ▼ ▼      ▼ ▼
   ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐
Cin│  FA  │ │  FA  │ │  FA  │ │  FA  │
───►      │ │      │ │      │ │      │
   └──┬───┘ └──┬───┘ └──┬───┘ └──┬───┘
      │        │        │        │
     C3       C2       C1       C0
      │        │        │        │
      └────────┴────────┴────────┴────► Cout
         │         │         │
         S3        S2        S1        S0
```

**Problem**: Carry propagation delay
- Each adder waits for previous carry
- For n-bit: Delay = n × (FA delay)

**Example: 4-bit Addition**
```
  A =  1 0 1 1  (11)
  B =  0 1 1 0  (6)
     +--------
       1 0 0 0 1  (17)
       │ │ │ │ │
       C C C C C
       4 3 2 1 0
```

---

## 3. Look-Ahead Carry Adder

### Problem with Ripple Carry
- Slow for large numbers
- Carry must ripple through all stages
- **Solution**: Calculate carries in parallel

### Carry Look-Ahead Logic

**Generate (G) and Propagate (P):**
```
Gi = Ai · Bi       (Generate carry)
Pi = Ai ⊕ Bi       (Propagate carry)
```

**Carry Equations:**
```
C0 = Input carry
C1 = G0 + P0·C0
C2 = G1 + P1·C1 = G1 + P1·G0 + P1·P0·C0
C3 = G2 + P2·C2 = G2 + P2·G1 + P2·P1·G0 + P2·P1·P0·C0
C4 = G3 + P3·C3 = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0 + P3·P2·P1·P0·C0
```

**Sum:**
```
Si = Pi ⊕ Ci
```

### 4-bit CLA Adder Example

**Example: Add 1011 + 0110**

```
Step 1: Calculate Generate and Propagate
        A =  1  0  1  1
        B =  0  1  1  0
             ----------
        G = A·B
        G3 = 0, G2 = 0, G1 = 1, G0 = 0
        
        P = A⊕B
        P3 = 1, P2 = 1, P1 = 0, P0 = 1

Step 2: Calculate Carries (C0 = 0)
        C1 = G0 + P0·C0
           = 0 + 1·0 = 0
        
        C2 = G1 + P1·G0 + P1·P0·C0
           = 1 + 0·0 + 0·1·0 = 1
        
        C3 = G2 + P2·G1 + P2·P1·G0 + P2·P1·P0·C0
           = 0 + 1·1 + 1·0·0 + 1·0·1·0 = 1
        
        C4 = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0 + P3·P2·P1·P0·C0
           = 0 + 1·0 + 1·1·1 + 1·1·0·0 + 1·1·0·1·0 = 1

Step 3: Calculate Sum
        S0 = P0 ⊕ C0 = 1 ⊕ 0 = 1
        S1 = P1 ⊕ C1 = 0 ⊕ 0 = 0
        S2 = P2 ⊕ C2 = 1 ⊕ 1 = 0
        S3 = P3 ⊕ C3 = 1 ⊕ 1 = 0

Result: 10001 (17 in decimal)
        1011 (11) + 0110 (6) = 10001 (17) ✓
```

### CLA Advantages
- **Parallel carry generation**
- **Faster** than ripple carry
- Fixed delay (independent of bit width)

### CLA Disadvantages
- **Complex hardware**
- More gates required
- Higher cost

---

## 4. Multiplication Algorithms

### 4.1 Unsigned Multiplication

#### Manual Method (4-bit × 4-bit)

**Example: 13 × 11 (1101 × 1011)**

```
                1 1 0 1  (Multiplicand = 13)
              × 1 0 1 1  (Multiplier = 11)
              ---------
                1 1 0 1  (M × 1)
              1 1 0 1    (M × 1, shifted)
            0 0 0 0      (M × 0, shifted)
        + 1 1 0 1        (M × 1, shifted)
        ---------------
        1 0 0 0 1 1 1 1  (143)

Verification: 13 × 11 = 143 ✓
```

#### Algorithm Steps
```
1. Initialize Product = 0
2. For each bit in Multiplier (right to left):
   a. If bit = 1: Add Multiplicand to Product
   b. Shift Multiplicand left
3. Result in Product
```

### 4.2 Signed Multiplication

**Problem**: Need to handle negative numbers
- **Sign-Magnitude**: Multiply magnitudes, determine sign
- **2's Complement**: Need special handling

---

## 5. Booth's Algorithm

### Need for Booth's Algorithm
- Efficient multiplication for signed numbers
- Reduces number of additions
- Works with 2's complement representation

### Booth's Algorithm Rules

Based on **current bit (Q0)** and **previous bit (Q-1)**:

| Q0 | Q-1 | Operation |
|----|-----|-----------|
| 0  | 0   | Shift only (no operation) |
| 0  | 1   | Add Multiplicand |
| 1  | 0   | Subtract Multiplicand |
| 1  | 1   | Shift only (no operation) |

### Algorithm Steps
```
1. Initialize:
   - AC (Accumulator) = 0
   - Q (Multiplier)
   - M (Multiplicand)
   - Q-1 = 0
   - SC (Step Counter) = n (number of bits)

2. Repeat SC times:
   a. Check Q0 and Q-1:
      - If 01: AC ← AC + M
      - If 10: AC ← AC - M
      - If 00 or 11: Do nothing
   b. Arithmetic Shift Right (AC, Q, Q-1)
   c. SC ← SC - 1

3. Result in (AC, Q)
```

### Booth's Algorithm Example 1

**Example: 7 × 3 (0111 × 0011)**

```
M = 0011 (3)
-M = 1101 (2's complement of 3)
Q = 0111 (7)

Initial:
AC = 0000, Q = 0111, Q-1 = 0, M = 0011, SC = 4

┌────┬──────────┬──────────┬─────┬───────────────────┬────┐
│ SC │    AC    │    Q     │ Q-1 │     Operation     │Q0Q-1│
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 4  │ 0000     │ 0111     │  0  │ Initial           │ 10 │
│    │          │          │     │ Q0Q-1=10, AC-M    │    │
│    │ 1101     │ 0111     │  0  │ After subtraction │    │
│    │ 1110     │ 1011     │  1  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 3  │ 1110     │ 1011     │  1  │                   │ 11 │
│    │          │          │     │ Q0Q-1=11, No op   │    │
│    │ 1111     │ 0101     │  1  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 2  │ 1111     │ 0101     │  1  │                   │ 01 │
│    │          │          │     │ Q0Q-1=01, AC+M    │    │
│    │ 0010     │ 0101     │  1  │ After addition    │    │
│    │ 0001     │ 0010     │  1  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 1  │ 0001     │ 0010     │  1  │                   │ 01 │
│    │          │          │     │ Q0Q-1=01, AC+M    │    │
│    │ 0100     │ 0010     │  1  │ After addition    │    │
│    │ 0010     │ 0001     │  0  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 0  │ 0010     │ 0001     │  0  │ Done              │    │
└────┴──────────┴──────────┴─────┴───────────────────┴────┘

Result: AC Q = 0010 0001
Combined: 00100001 (ignore extra bits for 4-bit result)
Result = 00010101 = 21

Verification: 7 × 3 = 21 ✓
```

### Booth's Algorithm Example 2

**Example: (-4) × 3 (1100 × 0011)**

```
M = 0011 (3)
-M = 1101 (2's complement)
Q = 1100 (-4 in 2's complement)

Initial:
AC = 0000, Q = 1100, Q-1 = 0, M = 0011, SC = 4

┌────┬──────────┬──────────┬─────┬───────────────────┬────┐
│ SC │    AC    │    Q     │ Q-1 │     Operation     │Q0Q-1│
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 4  │ 0000     │ 1100     │  0  │ Initial           │ 00 │
│    │          │          │     │ Q0Q-1=00, No op   │    │
│    │ 0000     │ 0110     │  0  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 3  │ 0000     │ 0110     │  0  │                   │ 00 │
│    │          │          │     │ Q0Q-1=00, No op   │    │
│    │ 0000     │ 0011     │  0  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 2  │ 0000     │ 0011     │  0  │                   │ 10 │
│    │          │          │     │ Q0Q-1=10, AC-M    │    │
│    │ 1101     │ 0011     │  0  │ After subtraction │    │
│    │ 1110     │ 1001     │  1  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 1  │ 1110     │ 1001     │  1  │                   │ 11 │
│    │          │          │     │ Q0Q-1=11, No op   │    │
│    │ 1111     │ 0100     │  1  │ Shift right       │    │
├────┼──────────┼──────────┼─────┼───────────────────┼────┤
│ 0  │ 1111     │ 0100     │  1  │ Done              │    │
└────┴──────────┴──────────┴─────┴───────────────────┴────┘

Result: AC Q = 1111 0100
This is -12 in 2's complement

Verification: (-4) × 3 = -12 ✓
```

### Booth's Advantage
- Works for both positive and negative numbers
- Reduces additions for consecutive 1s
- Example: 0111 (7) treated as 1000 - 0001

---

## 6. Array Multiplier

### 4×4 Array Multiplier Structure

```
        B3  B2  B1  B0  (Multiplicand)
      ×  A3  A2  A1  A0  (Multiplier)
      ------------------

A0: A0B3 A0B2 A0B1 A0B0 ─┐
A1: A1B3 A1B2 A1B1 A1B0 ─┤
A2: A2B3 A2B2 A2B1 A2B0 ─├─► Partial Products
A3: A3B3 A3B2 A3B1 A3B0 ─┘

Array of Full Adders combines partial products
```

### Array Multiplier Circuit (2×2)

```
        B1      B0
         │       │
    A1───┼───────┼───
         │       │
    ┌────┴───┐  │
    │ AND    │  │
    └────┬───┘  │
         │   ┌──┴────┐
    A0───┼───│ AND   │
         │   └───┬───┘
    ┌────┴───┐   │
    │   HA   │◄──┘
    └─┬────┬─┘
      │    │
      P2   P1   P0
```

**Features:**
- **Parallel operation** - all partial products generated simultaneously
- **Fast** - no sequential shifts
- **Hardware intensive** - requires many gates
- **Suitable** for high-speed applications

### Array Multiplier Example

**Example: 3 × 2 (11 × 10)**

```
Multiplicand (B) = 11
Multiplier (A) = 10

Partial Products:
A0·B = 0 × 11 = 00
A1·B = 1 × 11 = 11

Array Addition:
    0 0
  1 1
  -----
  1 1 0  (6)

Verification: 3 × 2 = 6 ✓
```

---

## 7. Division Algorithms

### 7.1 Restoring Division Algorithm

**Method**: Similar to manual division

```
Algorithm:
1. Initialize:
   - A (Accumulator) = 0
   - Q (Dividend)
   - M (Divisor)
   - n = number of bits

2. Repeat n times:
   a. Shift left (A, Q)
   b. A = A - M
   c. If A < 0 (MSB = 1):
      - Q0 = 0
      - A = A + M  (Restore)
   d. Else:
      - Q0 = 1

3. Quotient in Q, Remainder in A
```

### Restoring Division Example

**Example: 7 ÷ 3 (0111 ÷ 0011)**

```
M = 0011 (Divisor)
Q = 0111 (Dividend)
A = 0000 (Accumulator)

┌──────┬──────────┬──────────┬──────────────────────────┐
│ Step │    A     │    Q     │       Operation          │
├──────┼──────────┼──────────┼──────────────────────────┤
│  0   │ 0000     │ 0111     │ Initial                  │
├──────┼──────────┼──────────┼──────────────────────────┤
│  1   │ 0000     │ 1110     │ Shift left               │
│      │ 1101     │ 1110     │ A = A - M (negative)     │
│      │ 0000     │ 1110     │ Restore (A = A + M)      │
│      │ 0000     │ 1110     │ Q0 = 0                   │
├──────┼──────────┼──────────┼──────────────────────────┤
│  2   │ 0001     │ 1100     │ Shift left               │
│      │ 1110     │ 1100     │ A = A - M (negative)     │
│      │ 0001     │ 1100     │ Restore                  │
│      │ 0001     │ 1100     │ Q0 = 0                   │
├──────┼──────────┼──────────┼──────────────────────────┤
│  3   │ 0011     │ 1000     │ Shift left               │
│      │ 0000     │ 1000     │ A = A - M (positive)     │
│      │ 0000     │ 1001     │ Q0 = 1                   │
├──────┼──────────┼──────────┼──────────────────────────┤
│  4   │ 0001     │ 0010     │ Shift left               │
│      │ 1110     │ 0010     │ A = A - M (negative)     │
│      │ 0001     │ 0010     │ Restore                  │
│      │ 0001     │ 0010     │ Q0 = 0                   │
└──────┴──────────┴──────────┴──────────────────────────┘

Result:
Quotient (Q) = 0010 = 2
Remainder (A) = 0001 = 1

Verification: 7 ÷ 3 = 2 remainder 1 ✓
```

### 7.2 Non-Restoring Division

- **No restoration step** needed
- Alternates between addition and subtraction
- Faster than restoring division

---

## 8. Logical Operations

### 8.1 Basic Logical Operations

| Operation | Symbol | 4-bit Example |
|-----------|--------|---------------|
| AND | ∧ | 1010 ∧ 1100 = 1000 |
| OR | ∨ | 1010 ∨ 1100 = 1110 |
| NOT | ¬ | ¬1010 = 0101 |
| XOR | ⊕ | 1010 ⊕ 1100 = 0110 |
| NAND | ↑ | 1010 ↑ 1100 = 0111 |
| NOR | ↓ | 1010 ↓ 1100 = 0001 |

### 8.2 Shift Operations

#### Logical Shift Left (LSL)
```
Original:  1 0 1 1 0 1 0 0
           ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
LSL:       0 1 1 0 1 0 0 0
           │               ↑
           └───────────────┘
                          0 fills
```

#### Logical Shift Right (LSR)
```
Original:  1 0 1 1 0 1 0 0
           ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
LSR:       0 1 0 1 1 0 1 0
           ↑               │
           └───────────────┘
          0 fills
```

#### Arithmetic Shift Right (ASR)
```
Original:  1 0 1 1 0 1 0 0 (Negative number)
           ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
ASR:       1 1 0 1 1 0 1 0
           ↑ │
           └─┘ Sign bit preserved
```

#### Rotate Left (ROL)
```
Original:  1 0 1 1 0 1 0 0
           ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
ROL:       0 1 1 0 1 0 0 1
           │               ↑
           └───────────────┘
```

#### Rotate Right (ROR)
```
Original:  1 0 1 1 0 1 0 0
           ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
ROR:       0 1 0 1 1 0 1 0
           ↑               │
           └───────────────┘
```

---

## 9. Floating Point Arithmetic

### 9.1 Floating Point Representation

**Format**: ± M × B^E

- **M**: Mantissa (Fraction)
- **B**: Base (usually 2)
- **E**: Exponent

**Example**: 101.101₂
```
= 1.01101 × 2²
  │   │     │
  │   │     └─ Exponent
  │   └─────── Mantissa
  └─────────── Sign
```

### 9.2 Normalization

**Normalized form**: 1.xxxx × 2^E
- MSB of mantissa is always 1
- Provides maximum precision

**Example:**
```
0.00101 × 2³  →  1.01 × 2⁰  (Normalized)
110.11 × 2²   →  1.1011 × 2⁴  (Normalized)
```

---

## 10. IEEE 754 Floating Point Standard

### 10.1 Single Precision (32-bit)

```
┌─┬───────────┬──────────────────────────┐
│S│ Exponent  │       Mantissa          │
│ │  (8 bits) │       (23 bits)         │
└─┴───────────┴──────────────────────────┘
31     30-23           22-0

S: Sign bit (0 = positive, 1 = negative)
Exponent: Biased by 127
Mantissa: Implicit leading 1
```

**Value**: (-1)^S × 1.M × 2^(E-127)

**Special Cases:**
- **Zero**: E = 0, M = 0
- **Infinity**: E = 255, M = 0
- **NaN**: E = 255, M ≠ 0

### 10.2 Double Precision (64-bit)

```
┌─┬─────────────────┬────────────────────────────────────────────────────┐
│S│   Exponent      │                 Mantissa                          │
│ │   (11 bits)     │                (52 bits)                          │
└─┴─────────────────┴────────────────────────────────────────────────────┘
63    62-52                        51-0

Exponent: Biased by 1023
```

**Value**: (-1)^S × 1.M × 2^(E-1023)

### IEEE 754 Example 1: Convert 12.5 to IEEE 754

```
Step 1: Convert to binary
        12.5₁₀ = 1100.1₂

Step 2: Normalize
        1100.1 = 1.1001 × 2³

Step 3: Extract components
        Sign (S) = 0 (positive)
        Mantissa (M) = 1001 (fraction part after "1.")
        Exponent (E) = 3

Step 4: Bias exponent
        Biased E = 3 + 127 = 130₁₀ = 10000010₂

Step 5: IEEE 754 format (32-bit)
┌─┬──────────┬───────────────────────────┐
│0│10000010  │10010000000000000000000    │
└─┴──────────┴───────────────────────────┘
 S  Exponent          Mantissa

Result: 0 10000010 10010000000000000000000
Hex: 0x41480000
```

### IEEE 754 Example 2: Convert -0.75 to IEEE 754

```
Step 1: Convert to binary
        0.75₁₀ = 0.11₂

Step 2: Normalize
        0.11 = 1.1 × 2⁻¹

Step 3: Extract components
        Sign (S) = 1 (negative)
        Mantissa (M) = 1 (fraction part)
        Exponent (E) = -1

Step 4: Bias exponent
        Biased E = -1 + 127 = 126₁₀ = 01111110₂

Step 5: IEEE 754 format (32-bit)
┌─┬──────────┬───────────────────────────┐
│1│01111110  │10000000000000000000000    │
└─┴──────────┴───────────────────────────┘
 S  Exponent          Mantissa

Result: 1 01111110 10000000000000000000000
Hex: 0xBF400000
```

### IEEE 754 Example 3: Decode 0x40A00000

```
Binary: 0 10000001 01000000000000000000000

Step 1: Extract fields
        S = 0 (positive)
        E = 10000001₂ = 129₁₀
        M = 01000000000000000000000₂

Step 2: Unbias exponent
        Actual E = 129 - 127 = 2

Step 3: Reconstruct number
        Mantissa = 1.01₂ (implicit 1)
        Value = 1.01₂ × 2²
              = 101.0₂
              = 5.0₁₀

Result: 5.0
```

---

## 11. Floating Point Addition

### Algorithm
```
1. Compare exponents
2. Align mantissas (shift smaller exponent)
3. Add/subtract mantissas
4. Normalize result
5. Round if necessary
```

### Example: 3.5 + 1.25

```
Step 1: Convert to normalized form
        3.5 = 1.11 × 2¹
        1.25 = 1.01 × 2⁰

Step 2: Align exponents (make equal)
        1.25 = 0.101 × 2¹  (shift right, increase exponent)

Step 3: Add mantissas
        1.110 × 2¹
      + 0.101 × 2¹
      -----------
       10.011 × 2¹

Step 4: Normalize
       10.011 × 2¹ = 1.0011 × 2²

Step 5: Result
        1.0011 × 2² = 100.11₂ = 4.75₁₀

Verification: 3.5 + 1.25 = 4.75 ✓
```

---

## 12. Floating Point Multiplication

### Algorithm
```
1. Add exponents
2. Multiply mantissas
3. Normalize result
4. Adjust exponent
5. Determine sign
```

### Example: 2.5 × 3.0

```
Step 1: Normalize
        2.5 = 1.01 × 2¹
        3.0 = 1.1 × 2¹

Step 2: Add exponents
        E = 1 + 1 = 2

Step 3: Multiply mantissas
        1.01 × 1.1 = 1.111

Step 4: Combine
        1.111 × 2²

Step 5: Result
        1.111 × 2² = 111.1₂ = 7.5₁₀

Verification: 2.5 × 3.0 = 7.5 ✓
```

---

## 13. ALU Design

### Simple 4-bit ALU

```
         A (4-bit)     B (4-bit)
             │            │
             ▼            ▼
        ┌─────────────────────┐
        │                     │
        │   Function Select   │◄─── S0, S1, S2
        │      (Decoder)      │
        │                     │
        ├──────────┬──────────┤
        │Arithmetic│  Logic   │
        │  Unit    │  Unit    │
        └────┬─────┴─────┬────┘
             │           │
             └─────┬─────┘
                   ▼
              MUX (Output select)
                   │
                   ▼
             Result (4-bit)
                   │
              ┌────┴────┐
              │ Flags   │
              │ C Z S V │
              └─────────┘
```

### ALU Operations Table

| S2 S1 S0 | Operation | Function |
|----------|-----------|----------|
| 0 0 0 | Transfer A | F = A |
| 0 0 1 | Increment A | F = A + 1 |
| 0 1 0 | Add | F = A + B |
| 0 1 1 | Subtract | F = A - B |
| 1 0 0 | AND | F = A ∧ B |
| 1 0 1 | OR | F = A ∨ B |
| 1 1 0 | XOR | F = A ⊕ B |
| 1 1 1 | NOT A | F = ¬A |

---

## 🚀 Quick Reference Summary

### Adders
- **Half Adder**: 2 inputs, Sum + Carry
- **Full Adder**: 3 inputs (A, B, Cin), Sum + Cout
- **Ripple Carry**: Sequential, slow
- **Carry Look-Ahead**: Parallel, fast

### Multiplication
- **Booth's Algorithm**: Efficient for signed numbers
- **Array Multiplier**: Parallel, fast, hardware intensive

### Division
- **Restoring**: Restore if negative
- **Non-Restoring**: Alternating add/subtract

### IEEE 754 (Single Precision)
```
Sign (1) | Exponent (8) | Mantissa (23)
Value = (-1)^S × 1.M × 2^(E-127)
```

### Floating Point Operations
- **Addition**: Align exponents, add mantissas, normalize
- **Multiplication**: Add exponents, multiply mantissas

---

## 📝 Exam Important Questions

1. **Explain** Ripple Carry Adder and its limitations.

2. **Describe** Carry Look-Ahead Adder with 4-bit example.

3. **Explain** Booth's Algorithm. Multiply 7 × (-3) using Booth's method.

4. **Compare** Array Multiplier with Booth's multiplier.

5. **Perform** Restoring Division: 13 ÷ 5 (show all steps).

6. **Explain** IEEE 754 floating point standard (single precision).

7. **Convert** 13.75 to IEEE 754 32-bit format.

8. **Decode** IEEE 754: 0 10000010 10100000000000000000000

9. **Perform** Floating Point Addition: 5.5 + 2.25 (normalized form).

10. **Design** a 4-bit ALU supporting:
    - Addition, Subtraction
    - AND, OR, XOR
    - Include control signals and flag generation

---

*End of Unit-2*
