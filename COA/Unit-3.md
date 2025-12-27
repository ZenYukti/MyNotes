# Unit-3: Control Unit

---

## 1. Introduction to Control Unit

### What is Control Unit?
- **Brain of CPU** - coordinates all operations
- Generates **control signals** for data path
- Controls **timing** of operations

### Control Unit Functions

```
┌─────────────────────────────────────────┐
│          CONTROL UNIT                   │
│                                         │
│  • Fetch instructions from memory      │
│  • Decode instructions                 │
│  • Generate control signals            │
│  • Sequence operations                 │
│  • Handle interrupts                   │
└─────────────────────────────────────────┘
          │
          ▼
    Control Signals
          │
    ┌─────┴─────┬─────────┬───────────┐
    ▼           ▼         ▼           ▼
   ALU      Registers   Memory      I/O
```

---

## 2. Instruction Types

### 2.1 Data Transfer Instructions
Move data between registers, memory, I/O

| Instruction | Description | Example |
|-------------|-------------|---------|
| LOAD | Memory → Register | LOAD R1, M[100] |
| STORE | Register → Memory | STORE M[100], R1 |
| MOV | Register → Register | MOV R2, R1 |
| PUSH | Register → Stack | PUSH R1 |
| POP | Stack → Register | POP R1 |

### 2.2 Arithmetic Instructions
Perform mathematical operations

| Instruction | Description | Example |
|-------------|-------------|---------|
| ADD | Addition | ADD R3, R1, R2 |
| SUB | Subtraction | SUB R3, R1, R2 |
| MUL | Multiplication | MUL R3, R1, R2 |
| DIV | Division | DIV R3, R1, R2 |
| INC | Increment | INC R1 |
| DEC | Decrement | DEC R1 |

### 2.3 Logical Instructions
Perform logical operations

| Instruction | Description | Example |
|-------------|-------------|---------|
| AND | Bitwise AND | AND R3, R1, R2 |
| OR | Bitwise OR | OR R3, R1, R2 |
| XOR | Bitwise XOR | XOR R3, R1, R2 |
| NOT | Bitwise NOT | NOT R1 |
| SHL | Shift Left | SHL R1, 2 |
| SHR | Shift Right | SHR R1, 2 |

### 2.4 Control Transfer Instructions
Change program flow

| Instruction | Description | Example |
|-------------|-------------|---------|
| JMP | Unconditional jump | JMP 500 |
| JZ | Jump if zero | JZ 500 |
| JNZ | Jump if not zero | JNZ 500 |
| JC | Jump if carry | JC 500 |
| CALL | Call subroutine | CALL SUB1 |
| RET | Return from subroutine | RET |

---

## 3. Instruction Formats

### 3.1 Three-Address Format

```
┌──────────┬──────────┬──────────┬──────────┐
│  Opcode  │   Dest   │  Source1 │  Source2 │
└──────────┴──────────┴──────────┴──────────┘

Example: ADD R1, R2, R3    // R1 = R2 + R3
```

**Advantages:**
- Shorter programs
- Less memory traffic

**Disadvantages:**
- Longer instruction length

### 3.2 Two-Address Format

```
┌──────────┬──────────┬──────────┐
│  Opcode  │   Dest   │  Source  │
│          │ /Source1 │          │
└──────────┴──────────┴──────────┘

Example: ADD R1, R2    // R1 = R1 + R2
```

**Advantages:**
- Shorter instruction
- Common format

**Disadvantages:**
- Destination modified (original lost)

### 3.3 One-Address Format

```
┌──────────┬──────────┐
│  Opcode  │  Address │
└──────────┴──────────┘

Example: ADD M[100]    // AC = AC + M[100]
         (Uses Accumulator)
```

**Advantages:**
- Short instruction
- Simple design

**Disadvantages:**
- More instructions needed
- Heavy use of accumulator

### 3.4 Zero-Address Format

```
┌──────────┐
│  Opcode  │
└──────────┘

Example: ADD    // TOS = (TOS-1) + TOS
         (Stack-based)
```

**Advantages:**
- Shortest instruction
- Good for expressions

**Disadvantages:**
- Many push/pop operations

### Instruction Format Comparison

**Example: C = (A + B) × (D - E)**

#### Three-Address:
```
ADD R1, A, B       // R1 = A + B
SUB R2, D, E       // R2 = D - E
MUL C, R1, R2      // C = R1 × R2
```
**3 instructions**

#### Two-Address:
```
LOAD R1, A         // R1 = A
ADD R1, B          // R1 = R1 + B
LOAD R2, D         // R2 = D
SUB R2, E          // R2 = R2 - E
MUL R1, R2         // R1 = R1 × R2
STORE C, R1        // C = R1
```
**6 instructions**

#### One-Address (Accumulator):
```
LOAD A             // AC = A
ADD B              // AC = AC + B
STORE Temp         // Temp = AC
LOAD D             // AC = D
SUB E              // AC = AC - E
MUL Temp           // AC = AC × Temp
STORE C            // C = AC
```
**7 instructions**

#### Zero-Address (Stack):
```
PUSH A             // Push A
PUSH B             // Push B
ADD                // Pop 2, push sum
PUSH D             // Push D
PUSH E             // Push E
SUB                // Pop 2, push difference
MUL                // Pop 2, push product
POP C              // Pop to C
```
**8 instructions**

---

## 4. Instruction Cycle

### Basic Instruction Cycle

```
     ┌────────────┐
     │   FETCH    │
     └─────┬──────┘
           │
           ▼
     ┌────────────┐
     │   DECODE   │
     └─────┬──────┘
           │
           ▼
     ┌────────────┐
     │  EXECUTE   │
     └─────┬──────┘
           │
           └────────────┐
                        │
                        ▼
               ┌────────────────┐
               │  STORE RESULT  │
               └────────────────┘
```

---

## 5. Fetch and Execute Cycles

### 5.1 Fetch Cycle

**Steps:**
```
T0: MAR ← PC                    // Address to MAR
T1: MBR ← M[MAR], PC ← PC + 1  // Fetch & increment PC
T2: IR ← MBR                    // Instruction to IR
T3: Decode instruction          // Decode opcode
```

**Register Transfers:**
```
Initial State:
PC = 100
IR = ?
Memory[100] = ADD R1, R2

Fetch Cycle:
T0: MAR ← 100           // MAR = 100
T1: MBR ← M[100]        // MBR = ADD R1, R2
    PC ← 101            // PC = 101
T2: IR ← MBR            // IR = ADD R1, R2

Result:
PC = 101 (next instruction)
IR = ADD R1, R2
```

### 5.2 Execute Cycle

Depends on instruction type

#### Example 1: ADD R1, R2, R3
```
T4: R1 ← R2 + R3        // Perform addition
```

#### Example 2: LOAD R1, M[500]
```
T4: MAR ← 500           // Address to MAR
T5: MBR ← M[MAR]        // Read memory
T6: R1 ← MBR            // Transfer to register
```

#### Example 3: STORE M[500], R1
```
T4: MAR ← 500           // Address to MAR
T5: MBR ← R1            // Data to MBR
T6: M[MAR] ← MBR        // Write to memory
```

---

## 6. Complete Instruction Execution

### Example: Execute "LOAD R1, M[200]"

```
Initial State:
PC = 100
Memory[100] = LOAD R1, M[200]
Memory[200] = 42
R1 = ?

FETCH CYCLE:
───────────
T0: MAR ← PC            // MAR = 100
T1: MBR ← M[MAR]        // MBR = LOAD R1, M[200]
    PC ← PC + 1         // PC = 101
T2: IR ← MBR            // IR = LOAD R1, M[200]
T3: Decode              // Identify: LOAD instruction

EXECUTE CYCLE:
─────────────
T4: MAR ← 200           // Address from instruction
T5: MBR ← M[MAR]        // MBR = 42
T6: R1 ← MBR            // R1 = 42

Final State:
PC = 101
IR = LOAD R1, M[200]
R1 = 42
```

### Example: Execute "ADD R3, R1, R2"

```
Initial State:
PC = 100
Memory[100] = ADD R3, R1, R2
R1 = 5
R2 = 10
R3 = ?

FETCH CYCLE:
───────────
T0: MAR ← PC            // MAR = 100
T1: MBR ← M[MAR]        // MBR = ADD R3, R1, R2
    PC ← PC + 1         // PC = 101
T2: IR ← MBR            // IR = ADD R3, R1, R2
T3: Decode              // Identify: ADD instruction

EXECUTE CYCLE:
─────────────
T4: R3 ← R1 + R2        // R3 = 5 + 10 = 15

Final State:
PC = 101
R1 = 5
R2 = 10
R3 = 15
```

---

## 7. Micro-operations

### Definition
Elementary operations performed during one clock cycle

### Types of Micro-operations

#### 1. Register Transfer
```
R1 ← R2                 // Copy R2 to R1
R3 ← R1 + R2           // Add and store
```

#### 2. Memory Transfer
```
MAR ← Address          // Load address
MBR ← M[MAR]          // Read memory
M[MAR] ← MBR          // Write memory
```

#### 3. Arithmetic
```
AC ← AC + 1            // Increment
AC ← AC + MBR          // Add
```

#### 4. Logical
```
AC ← AC ∧ MBR          // AND operation
AC ← ¬AC               // NOT operation
```

#### 5. Shift
```
AC ← shl(AC)           // Shift left
AC ← shr(AC)           // Shift right
```

---

## 8. Program Control

### 8.1 Status Flags

| Flag | Condition | Set When |
|------|-----------|----------|
| **Z** (Zero) | Result = 0 | All bits zero |
| **C** (Carry) | Carry out | Unsigned overflow |
| **S** (Sign) | Result < 0 | MSB = 1 |
| **V** (Overflow) | Signed overflow | Sign bit incorrect |
| **P** (Parity) | Even parity | Even number of 1s |

### 8.2 Branch Instructions

#### Unconditional Branch
```
JMP 500        // Always jump to 500
```

#### Conditional Branch
```
Example Program:
100: LOAD R1, X
101: CMP R1, #10     // Compare R1 with 10
102: JZ EQUAL        // Jump if equal (Z=1)
103: JG GREATER      // Jump if greater (Z=0, S=0)
104: ...

Execution:
If X = 10:  Z=1, jump to EQUAL
If X > 10:  Z=0, S=0, jump to GREATER
If X < 10:  Continue to 104
```

### 8.3 Subroutine Call and Return

```
Main Program:
100: ...
101: CALL SUB1       // Call subroutine
102: ...             // Return here

Subroutine:
200: SUB1: ...       // Subroutine starts
201: ...
202: RET             // Return to caller

CALL Execution:
────────────────
T0: SP ← SP + 1      // Increment stack pointer
T1: M[SP] ← PC       // Save return address (102)
T2: PC ← 200         // Jump to subroutine

RET Execution:
─────────────
T0: PC ← M[SP]       // Restore return address
T1: SP ← SP - 1      // Decrement stack pointer
```

---

## 9. RISC (Reduced Instruction Set Computer)

### RISC Characteristics

```
┌──────────────────────────────────────┐
│         RISC Philosophy              │
│                                      │
│  • Simple instructions               │
│  • Load/Store architecture           │
│  • Large register file               │
│  • Fixed instruction length          │
│  • Single-cycle execution            │
│  • Hardwired control                 │
│  • Pipelining friendly               │
└──────────────────────────────────────┘
```

### RISC vs CISC

| Feature | RISC | CISC |
|---------|------|------|
| **Instruction Set** | Small (~100) | Large (~200-300) |
| **Instruction Length** | Fixed | Variable |
| **Addressing Modes** | Few (2-3) | Many (5-20) |
| **Registers** | Many (32+) | Few (8-16) |
| **Memory Access** | Load/Store only | Any instruction |
| **Execution Time** | Single cycle | Multiple cycles |
| **Control** | Hardwired | Microprogrammed |
| **Pipeline** | Easy | Difficult |
| **Code Size** | Larger | Smaller |
| **Examples** | ARM, MIPS, SPARC | x86, VAX |

### RISC Example

```
RISC Code:
LOAD R1, A         // Load A from memory
LOAD R2, B         // Load B from memory
ADD R3, R1, R2     // R3 = R1 + R2
STORE C, R3        // Store result to C

CISC Code:
ADD C, A, B        // Direct memory-to-memory

RISC: 4 instructions, simpler hardware
CISC: 1 instruction, complex hardware
```

---

## 10. Pipelining

### 10.1 Concept

**Sequential Execution:**
```
Instruction 1: Fetch → Decode → Execute → Store
Instruction 2:                            Fetch → Decode → Execute → Store
Instruction 3:                                                       Fetch → Decode...

Total Time: n × 4 cycles (for n instructions)
```

**Pipelined Execution:**
```
Time: 1   2   3   4   5   6   7   8
──────────────────────────────────────
I1:   F   D   E   S
I2:       F   D   E   S
I3:           F   D   E   S
I4:               F   D   E   S
I5:                   F   D   E   S

Total Time: 4 + (n-1) cycles
```

### 10.2 Pipeline Stages

```
┌─────────┐   ┌────────┐   ┌─────────┐   ┌────────┐
│  FETCH  │──►│ DECODE │──►│ EXECUTE │──►│  WRITE │
│   (IF)  │   │  (ID)  │   │  (EX)   │   │  (WB)  │
└─────────┘   └────────┘   └─────────┘   └────────┘
```

### 10.3 Pipeline Example

**4-stage pipeline processing 6 instructions:**

```
┌──────┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│Cycle │ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │ 8 │ 9 │
├──────┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
│  I1  │ F │ D │ E │ W │   │   │   │   │   │
│  I2  │   │ F │ D │ E │ W │   │   │   │   │
│  I3  │   │   │ F │ D │ E │ W │   │   │   │
│  I4  │   │   │   │ F │ D │ E │ W │   │   │
│  I5  │   │   │   │   │ F │ D │ E │ W │   │
│  I6  │   │   │   │   │   │ F │ D │ E │ W │
└──────┴───┴───┴───┴───┴───┴───┴───┴───┴───┘

Sequential: 6 × 4 = 24 cycles
Pipelined: 4 + 5 = 9 cycles
Speedup = 24/9 = 2.67×
```

### 10.4 Pipeline Hazards

#### A. Structural Hazard
**Cause**: Hardware resource conflict

```
Example:
I1 needs memory (Fetch)
I4 needs memory (Write)
Both at same time → Conflict!

Solution:
- Separate instruction and data memory
- Stall pipeline
```

#### B. Data Hazard
**Cause**: Data dependency between instructions

```
Example:
I1: ADD R1, R2, R3    // R1 = R2 + R3
I2: SUB R4, R1, R5    // Uses R1 (not ready yet!)

┌──────┬───┬───┬───┬───┬───┐
│Cycle │ 1 │ 2 │ 3 │ 4 │ 5 │
├──────┼───┼───┼───┼───┼───┤
│  I1  │ F │ D │ E │ W │   │
│  I2  │   │ F │ D │ X │ X │ (Stall: R1 not ready)
└──────┴───┴───┴───┴───┴───┘

Solutions:
1. Forwarding/Bypassing
2. Stalling
3. Compiler reordering
```

**Data Forwarding:**
```
      ┌─────────────────┐
      │                 │
 ┌────▼────┐       ┌────▼────┐
 │ Execute │       │ Execute │
 │   I1    │───────┤   I2    │
 └─────────┘       └─────────┘
     │                  ▲
     └──────────────────┘
    Forward result before Write
```

#### C. Control Hazard
**Cause**: Branch instructions

```
Example:
100: ADD R1, R2, R3
101: SUB R4, R1, R5
102: BEQ 200         // Branch if equal
103: MUL R6, R7, R8  // Should this execute?
...
200: ...             // Branch target

Problem: Don't know branch outcome until Execute stage

┌──────┬───┬───┬───┬───┬───┐
│Cycle │ 1 │ 2 │ 3 │ 4 │ 5 │
├──────┼───┼───┼───┼───┼───┤
│ 102  │ F │ D │ E │ W │   │
│ 103  │   │ F │ D │ X │   │ (May be wrong!)
└──────┴───┴───┴───┴───┴───┘

Solutions:
1. Branch Prediction
2. Delayed Branch
3. Branch Target Buffer
```

### 10.5 Pipeline Performance

**Speedup Formula:**
```
Speedup = Time without pipeline / Time with pipeline
        = (n × k) / (k + n - 1)

Where:
n = number of instructions
k = number of pipeline stages
```

**Example:**
```
n = 10 instructions
k = 5 stages

Without pipeline: 10 × 5 = 50 cycles
With pipeline: 5 + 9 = 14 cycles

Speedup = 50/14 = 3.57×
```

**Ideal vs Actual:**
```
Ideal Speedup = k (number of stages)
Actual Speedup < k (due to hazards)
```

---

## 11. Hardwired Control

### Characteristics
- Control logic implemented using **gates**
- **Fast** execution
- **Fixed** control logic
- Used in **RISC** processors

### Control Signal Generation

```
┌──────────────────────────────────────┐
│      Instruction Register (IR)       │
└──────────┬───────────────────────────┘
           │
           ▼
     ┌──────────┐
     │ Decoder  │
     └─────┬────┘
           │
           ▼
    ┌──────────────┐
    │  Combinational│
    │     Logic     │
    └──────┬───────┘
           │
           ▼
    Control Signals
    (ALU, Memory, Registers)
```

### Example: Control Signals for ADD

```
Instruction: ADD R3, R1, R2

Control Signals:
────────────────
T0: PC_out, MAR_in
T1: Memory_read, MBR_in, PC_increment
T2: MBR_out, IR_in
T3: Decode
T4: R1_out, ALU_A_in
    R2_out, ALU_B_in
    ALU_op = ADD
    ALU_out, R3_in
```

---

## 12. Microprogrammed Control

### 12.1 Concept

- Control logic implemented in **microprogram**
- Stored in **control memory**
- **Flexible** - easy to modify
- Used in **CISC** processors

### Architecture

```
┌──────────────────────────────────────┐
│      Instruction Register (IR)       │
└──────────┬───────────────────────────┘
           │
           ▼
    ┌────────────┐
    │  Control   │
    │  Address   │
    │  Register  │
    │   (CAR)    │
    └─────┬──────┘
          │
          ▼
    ┌──────────────┐
    │   Control    │◄──── Microinstructions
    │   Memory     │
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │   Control    │
    │   Data       │
    │   Register   │
    │   (CDR)      │
    └──────┬───────┘
           │
           ▼
    Control Signals
```

### 12.2 Microinstruction Format

```
┌──────────────┬──────────────┬──────────────┐
│   Control    │   ALU        │   Branch     │
│   Fields     │   Control    │   Control    │
└──────────────┴──────────────┴──────────────┘
```

### 12.3 Micro-operation Sequencing

**Example: LOAD R1, M[500]**

```
Microprogram:
─────────────
μ1: MAR ← IR(address)        // Extract address
μ2: MBR ← M[MAR]             // Read memory
μ3: R1 ← MBR                 // Transfer to register
μ4: CAR ← Fetch_routine      // Next instruction

Each μ is one microinstruction
```

### 12.4 Horizontal vs Vertical Microprogramming

#### Horizontal Microprogramming

```
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│  PC  │ MAR  │ MBR  │  IR  │ ALU  │ REG  │ MEM  │
│  out │  in  │  in  │  in  │  op  │ ctrl │ ctrl │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┘

- One bit per control signal
- Wide microinstruction (50-100 bits)
- Fast (parallel operations)
- Low-level control
```

**Example:**
```
PC_out | MAR_in | Memory_read | MBR_in | IR_in | ...
   1   |   1    |      0      |   0    |   0   | ...
```

#### Vertical Microprogramming

```
┌──────────────┬──────────────┐
│   Operation  │   Operands   │
│    Code      │              │
└──────────────┴──────────────┘

- Encoded operations
- Narrow microinstruction (10-20 bits)
- Slower (needs decoding)
- High-level control
```

**Example:**
```
Opcode | Operand1 | Operand2
  MAR  |    PC    |    -
```

#### Comparison

| Feature | Horizontal | Vertical |
|---------|------------|----------|
| **Width** | Wide (50-100 bits) | Narrow (10-20 bits) |
| **Speed** | Fast | Slower |
| **Parallelism** | High | Low |
| **Flexibility** | Low | High |
| **Memory** | Large | Small |
| **Encoding** | Direct (1 bit/signal) | Encoded |
| **Example** | Mainframes | Microcontrollers |

---

## 🚀 Quick Reference Summary

### Instruction Formats
- **3-Address**: ADD R1, R2, R3
- **2-Address**: ADD R1, R2
- **1-Address**: ADD M[100]
- **0-Address**: ADD (stack)

### Instruction Cycle
```
Fetch → Decode → Execute → Store
```

### Pipeline Stages
```
IF (Fetch) → ID (Decode) → EX (Execute) → WB (Write)
```

### Pipeline Hazards
- **Structural**: Hardware conflict
- **Data**: Data dependency
- **Control**: Branch uncertainty

### RISC Characteristics
- Simple instructions
- Load/Store architecture
- Large register file
- Fixed instruction length
- Single-cycle execution

### Control Unit Types
- **Hardwired**: Fast, fixed, gates
- **Microprogrammed**: Flexible, control memory

### Microprogramming
- **Horizontal**: Wide, fast, parallel
- **Vertical**: Narrow, slow, sequential

---

## 📝 Exam Important Questions

1. **Explain** different instruction formats with examples.

2. **Describe** instruction cycle with fetch and execute phases.

3. **Demonstrate** execution of: LOAD R1, M[100] with all micro-operations.

4. **Explain** pipelining concept. Show 5 instructions in 4-stage pipeline.

5. **Describe** three types of pipeline hazards with examples and solutions.

6. **Compare** RISC and CISC architectures.

7. **Calculate** pipeline speedup for 20 instructions in 5-stage pipeline.

8. **Explain** hardwired vs microprogrammed control.

9. **Describe** horizontal and vertical microprogramming with comparison.

10. **Design** microprogram for ADD R3, R1, R2 instruction.

---

*End of Unit-3*
