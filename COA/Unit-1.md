# Unit-1: Introduction to Computer Organization

---

## 1. Functional Units of Digital System

### Basic Computer System
A computer system consists of **five basic functional units**:

```
┌─────────────────────────────────────────────────────────────┐
│                     COMPUTER SYSTEM                          │
├──────────────┬──────────────┬──────────────┬────────────────┤
│    INPUT     │   PROCESSOR  │    MEMORY    │     OUTPUT     │
│    UNIT      │     UNIT     │     UNIT     │      UNIT      │
│              ├──────┬───────┤              │                │
│              │ ALU  │  CU   │              │                │
└──────────────┴──────┴───────┴──────────────┴────────────────┘
```

### 1.1 Input Unit
- **Function**: Accept data and instructions from outside world
- **Examples**: Keyboard, Mouse, Scanner, Microphone
- **Operations**:
  - Converts input data to binary
  - Transmits to memory or processor

### 1.2 Output Unit
- **Function**: Send processed results to outside world
- **Examples**: Monitor, Printer, Speaker, Projector
- **Operations**:
  - Converts binary to human-readable form
  - Displays/prints results

### 1.3 Memory Unit
- **Function**: Store data and instructions
- **Types**:
  1. **Primary Memory** (RAM, ROM) - Fast, limited capacity
  2. **Secondary Memory** (HDD, SSD) - Slower, large capacity

**Memory Hierarchy:**
```
        Registers (Fastest, Smallest)
             ↓
        Cache Memory
             ↓
        Main Memory (RAM)
             ↓
        Secondary Storage (Slowest, Largest)
```

### 1.4 Arithmetic Logic Unit (ALU)
- **Function**: Perform arithmetic and logical operations
- **Arithmetic Operations**: +, -, ×, ÷
- **Logical Operations**: AND, OR, NOT, XOR
- **Comparison**: <, >, =, ≠

### 1.5 Control Unit (CU)
- **Function**: Control and coordinate all units
- **Operations**:
  - Fetch instructions from memory
  - Decode instructions
  - Generate control signals
  - Control data flow

---

## 2. Interconnections and Buses

### Computer Interconnection Structure

```
┌──────────┐        ┌──────────┐        ┌──────────┐
│   CPU    │◄──────►│  Memory  │◄──────►│   I/O    │
└──────────┘        └──────────┘        └──────────┘
     │                    │                    │
     └────────────────────┴────────────────────┘
                    System Bus
```

### What is a Bus?
- **Definition**: Common pathway for transferring data between components
- **Structure**: Set of parallel conducting wires
- **Purpose**: Reduce number of interconnections

---

## 3. Bus Architecture

### 3.1 Single Bus Structure

```
┌─────┐   ┌─────┐   ┌────────┐   ┌─────┐   ┌─────┐
│ CPU │───│ I/O │───│ Memory │───│ I/O │───│ I/O │
└─────┘   └─────┘   └────────┘   └─────┘   └─────┘
            │              │
            └──────┬───────┘
                   │
           Single System Bus
```

**Advantages:**
- Simple design
- Low cost
- Easy to expand

**Disadvantages:**
- Only one transfer at a time (bottleneck)
- Limited speed

### 3.2 Multiple Bus Structure

```
          ┌──────────────┐
          │     CPU      │
          └───────┬──────┘
                  │
          ┌───────┴───────┐
          │               │
      ┌───▼────┐     ┌────▼────┐
      │  Cache │     │  Main   │
      │ Memory │     │ Memory  │
      └───┬────┘     └────┬────┘
          │               │
          └───────┬───────┘
                  │
          ┌───────▼───────┐
          │   I/O Bus     │
          └───────┬───────┘
                  │
         ┌────────┼────────┐
         │        │        │
      ┌──▼──┐  ┌──▼──┐  ┌──▼──┐
      │ I/O │  │ I/O │  │ I/O │
      └─────┘  └─────┘  └─────┘
```

**Advantages:**
- Multiple transfers simultaneously
- Better performance
- Separate high-speed and low-speed devices

**Disadvantages:**
- Complex design
- Higher cost

---

## 4. Types of Buses

### 4.1 Data Bus
- **Function**: Transfer actual data
- **Direction**: **Bidirectional** (data flows both ways)
- **Width**: 8, 16, 32, or 64 bits
- **Example**: Transfer data between CPU and memory

### 4.2 Address Bus
- **Function**: Carry memory addresses
- **Direction**: **Unidirectional** (CPU to Memory/I/O)
- **Width**: Determines addressable memory
  - 16-bit: 2¹⁶ = 64 KB
  - 32-bit: 2³² = 4 GB
  - 64-bit: 2⁶⁴ = 16 EB

### 4.3 Control Bus
- **Function**: Carry control signals
- **Direction**: **Bidirectional**
- **Signals**:
  - Memory Read/Write
  - I/O Read/Write
  - Clock signals
  - Reset
  - Interrupt requests

### Bus Lines Comparison

| Bus Type | Function | Direction | Width |
|----------|----------|-----------|-------|
| Data Bus | Data transfer | Bidirectional | 8/16/32/64 bits |
| Address Bus | Address location | Unidirectional | 16/32/64 bits |
| Control Bus | Control signals | Bidirectional | Variable |

### Example: Memory Read Operation

```
Step 1: CPU places address on Address Bus
        Address Bus → [Memory Address]
        
Step 2: CPU sends READ signal on Control Bus
        Control Bus → [Memory Read Signal]
        
Step 3: Memory places data on Data Bus
        Data Bus ← [Data from Memory]
        
Step 4: CPU reads data from Data Bus
```

---

## 5. Bus Arbitration

### Need for Bus Arbitration
- Multiple devices want to use bus simultaneously
- Only **one master** can use bus at a time
- **Arbitration**: Process of granting bus access

### 5.1 Centralized Bus Arbitration

#### A. Daisy Chain Method

```
        ┌──────────────┐
        │ Bus Arbiter  │
        └──┬───┬───┬───┘
           │   │   │
    BG ────┼───┼───┼──────►
           │   │   │
    ┌──────▼──┐│   │
    │ Device 1││   │
    │(Highest)││   │
    └──────┬──┘│   │
           │   │   │
        ┌──▼───▼──┐│
        │ Device 2││
        └──────┬──┘│
               │   │
            ┌──▼───▼──┐
            │ Device 3│
            │(Lowest) │
            └─────────┘

Bus Request (BR) ────────────► To Arbiter
Bus Grant (BG) ──────────────► Daisy chain
```

**Working:**
1. Any device can send BR (Bus Request)
2. Arbiter sends BG (Bus Grant) signal
3. BG propagates through devices in priority order
4. First device needing bus takes control
5. Blocks BG from reaching lower priority devices

**Advantages:**
- Simple implementation
- Low cost (minimal hardware)
- Easy to add devices

**Disadvantages:**
- Priority fixed by position
- Lower priority devices may starve
- BG propagation delay

#### B. Polling Method

```
        ┌──────────────┐
        │ Bus Arbiter  │
        └──┬───┬───┬───┘
           │   │   │
    Address Lines (n bits)
           │   │   │
    ┌──────▼──┐│   │
    │ Device 1││   │
    └──────┬──┘│   │
           │   │   │
        ┌──▼───▼──┐│
        │ Device 2││
        └──────┬──┘│
               │   │
            ┌──▼───▼──┐
            │ Device 3│
            └─────────┘

Bus Busy Line ◄────────────── From devices
```

**Working:**
1. Devices send BR to arbiter
2. Arbiter sends device address on address lines
3. Addressed device activates Bus Busy line
4. Takes control of bus

**Advantages:**
- Flexible priority (can be changed)
- No propagation delay
- Fair access possible

**Disadvantages:**
- Additional address lines needed
- Requires device address decoding
- Arbiter complexity increases

#### C. Independent Request Method

```
        ┌──────────────┐
        │ Bus Arbiter  │
        │  (Priority   │
        │   Logic)     │
        └┬─┬─┬────┬─┬─┬┘
         │ │ │    │ │ │
    BR1──┘ │ │    │ │ └──BG1
    BR2────┘ │    │ └────BG2
    BR3──────┘    └──────BG3
         │               │
    ┌────▼───┐      ┌───▼────┐
    │Device 1│      │Device 2│
    └────────┘      └────────┘
```

**Working:**
1. Each device has separate BR and BG lines
2. Arbiter has priority logic
3. Grants bus to highest priority requester

**Advantages:**
- Fastest arbitration
- Flexible priority
- No propagation delay

**Disadvantages:**
- Complex hardware (2n lines for n devices)
- Expensive
- More control pins on arbiter

### 5.2 Distributed Bus Arbitration

```
Device 1 ◄──────┬──────► Device 2 ◄──────┬──────► Device 3
                │                         │
         Arbitration Lines         Arbitration Lines
```

**Working:**
- No central arbiter
- Devices communicate directly
- Each device has arbitration logic
- Priority determined by device ID

**Advantages:**
- No central bottleneck
- Reliable (no single point of failure)

**Disadvantages:**
- Complex device logic
- Synchronization issues

### Bus Arbitration Comparison

| Method | Hardware | Speed | Priority | Cost |
|--------|----------|-------|----------|------|
| Daisy Chain | Simple | Slow | Fixed | Low |
| Polling | Moderate | Medium | Flexible | Medium |
| Independent | Complex | Fast | Flexible | High |
| Distributed | Complex | Fast | Flexible | High |

---

## 6. Register Transfer

### 6.1 Registers
- **Definition**: Fast storage locations in CPU
- **Size**: 8, 16, 32, or 64 bits
- **Purpose**: Hold temporary data and addresses

### Common Registers

| Register | Symbol | Purpose |
|----------|--------|---------|
| Program Counter | PC | Next instruction address |
| Instruction Register | IR | Current instruction |
| Memory Address Register | MAR | Memory address for R/W |
| Memory Data Register | MDR | Data to/from memory |
| Accumulator | AC | ALU operand/result |
| General Purpose | R0-Rn | Temporary storage |

### 6.2 Register Transfer Language (RTL)

**Notation:**
```
R2 ← R1          // Copy R1 to R2
R3 ← R1 + R2     // Add R1 and R2, store in R3
M[AR] ← R1       // Store R1 at memory address in AR
R2 ← M[AR]       // Load from memory to R2
```

**Control Conditions:**
```
If (P = 1) then (R2 ← R1)    // Transfer if P is 1
P: R2 ← R1                   // Short form
```

### Register Transfer Example

**Example: ADD R1, R2, R3 (R1 = R2 + R3)**

```
Initial State:
R2 = 5
R3 = 10
R1 = ?

Step 1: Fetch operands
        Temp1 ← R2         // Temp1 = 5
        Temp2 ← R3         // Temp2 = 10

Step 2: Perform addition
        Temp3 ← Temp1 + Temp2    // Temp3 = 15

Step 3: Store result
        R1 ← Temp3         // R1 = 15

Final State:
R1 = 15
R2 = 5
R3 = 10
```

---

## 7. Bus Transfer

### 7.1 Single Bus Transfer

```
┌────┐   ┌────┐   ┌────┐   ┌────┐
│ R1 │   │ R2 │   │ R3 │   │ R4 │
└─┬──┘   └─┬──┘   └─┬──┘   └─┬──┘
  │        │        │        │
  └────────┴────────┴────────┘
           Common Bus
```

**Transfer Operation:**
```
Time T0: R1 → Bus
Time T1: Bus → R2
```

### 7.2 Three-State Buffer

```
Input ──┬──┐
        │  │
Enable ─┴──┤►── Output
           │
         ─┴──

Enable = 0: High impedance (disconnected)
Enable = 1: Output = Input
```

### Bus Transfer Example

**Example: Transfer data from R1 to R3**

```
Initial:
R1 = 25
R2 = 10
R3 = 0
R4 = 15

Step 1: Enable R1 output to bus
        Bus ← R1           // Bus = 25
        
Step 2: Enable R3 input from bus
        R3 ← Bus           // R3 = 25

Final:
R1 = 25
R2 = 10
R3 = 25
R4 = 15
```

---

## 8. Memory Transfer

### 8.1 Memory Read Operation

```
Step 1: Place address in MAR
        MAR ← Address

Step 2: Send READ signal
        Control ← READ

Step 3: Wait for memory
        (Memory access time)

Step 4: Data available in MDR
        MDR ← M[MAR]

Step 5: Transfer to register
        R ← MDR
```

### 8.2 Memory Write Operation

```
Step 1: Place address in MAR
        MAR ← Address

Step 2: Place data in MDR
        MDR ← Data

Step 3: Send WRITE signal
        Control ← WRITE

Step 4: Wait for write completion
        (Memory write time)

Step 5: Data written to memory
        M[MAR] ← MDR
```

### Memory Transfer Example

**Example: Read from memory location 100H**

```
Initial State:
MAR = ?
MDR = ?
Memory[100H] = 42

Operation:
T0: MAR ← 100H            // Set address
T1: Control ← READ        // Send read signal
T2: Wait                  // Memory access delay
T3: MDR ← M[MAR]          // MDR = 42
T4: AC ← MDR              // AC = 42

Final State:
MAR = 100H
MDR = 42
AC = 42
Memory[100H] = 42 (unchanged)
```

---

## 9. Processor Organization

### 9.1 Single Accumulator Organization

```
┌───────────────────────────────┐
│            CPU                │
│  ┌──────────┐                 │
│  │   ALU    │                 │
│  └────┬─────┘                 │
│       │                       │
│  ┌────▼─────┐                 │
│  │    AC    │  (Accumulator)  │
│  └──────────┘                 │
│                               │
│  ┌──────────┐                 │
│  │   Temp   │  (Temporary)    │
│  └──────────┘                 │
└───────────────────────────────┘
```

**Characteristics:**
- Single accumulator for ALU operations
- Simple design
- More memory accesses needed

**Example: A = (B + C) × D**
```
LOAD B        // AC ← B
ADD C         // AC ← AC + C
STORE Temp    // Temp ← AC
LOAD D        // AC ← D
MUL Temp      // AC ← AC × Temp
STORE A       // A ← AC
```

### 9.2 General Register Organization

```
┌─────────────────────────────────────┐
│              CPU                    │
│  ┌──────────┐                       │
│  │   ALU    │                       │
│  └────┬─────┘                       │
│       │                             │
│  ┌────┴──────────────┐              │
│  │  Register File    │              │
│  │  R0  R1  R2  R3   │              │
│  │  R4  R5  R6  R7   │              │
│  └───────────────────┘              │
└─────────────────────────────────────┘
```

**Characteristics:**
- Multiple general-purpose registers
- Reduced memory traffic
- Faster execution

**Example: A = (B + C) × D**
```
LOAD R1, B     // R1 ← B
LOAD R2, C     // R2 ← C
ADD R3, R1, R2 // R3 ← R1 + R2
LOAD R4, D     // R4 ← D
MUL R5, R3, R4 // R5 ← R3 × R4
STORE A, R5    // A ← R5
```

---

## 10. General Register Organization

### Register Selection

```
      Source Registers          Destination
      ┌────┬────┬────┐         ┌────┐
SEL A │ R0 │ R1 │... │    ┌───►│ R0 │
      └─┬──┴──┬─┴────┘    │    ├────┤
        │     │           │    │ R1 │
      ┌─▼─────▼──┐        │    ├────┤
SEL B │   MUX    │        │    │... │
      └─────┬────┘        │    ├────┤
            │             │    │ R7 │
      ┌─────▼─────┐       │    └────┘
      │    ALU    │       │       ▲
      └─────┬─────┘       │       │
            │             │    DECODER
            └─────────────┘       │
                              Destination
                              Select
```

### Control Word Format

```
┌──────┬──────┬──────┬──────────┬──────────┐
│ SELA │ SELB │ SELD │ Operation│   Mode   │
│(3bits)│(3bits)│(3bits)│ (5 bits) │ (3 bits) │
└──────┴──────┴──────┴──────────┴──────────┘
   │      │      │         │          │
   │      │      │         │          └─► Load/Store
   │      │      │         └───────────► ALU function
   │      │      └─────────────────────► Dest register
   │      └────────────────────────────► Source B
   └───────────────────────────────────► Source A
```

### Example: R3 ← R1 + R2

```
Control Word:
SELA = 001 (Select R1)
SELB = 010 (Select R2)
SELD = 011 (Select R3)
OPR  = ADD
Mode = Register

Execution:
1. R1 → ALU Input A
2. R2 → ALU Input B
3. ALU performs addition
4. Result → R3
```

---

## 11. Stack Organization

### 11.1 Stack Concepts

**Definition**: LIFO (Last In First Out) data structure

```
        ┌─────────┐
        │   TOS   │ ← SP (Stack Pointer)
        ├─────────┤
        │         │
        ├─────────┤
        │         │
        ├─────────┤
        │         │
        ├─────────┤
        │  Base   │
        └─────────┘

TOS = Top of Stack
SP = Stack Pointer (points to TOS)
```

### 11.2 Stack Operations

#### PUSH Operation
```
Initial Stack (SP = 3):
        ┌─────────┐
    3 → │   10    │ ← SP
        ├─────────┤
    2   │   20    │
        ├─────────┤
    1   │   30    │
        ├─────────┤
    0   │   40    │
        └─────────┘

PUSH 15:
Step 1: SP ← SP + 1      // SP = 4
Step 2: M[SP] ← 15       // Store 15

After PUSH (SP = 4):
        ┌─────────┐
    4 → │   15    │ ← SP
        ├─────────┤
    3   │   10    │
        ├─────────┤
    2   │   20    │
        ├─────────┤
    1   │   30    │
        ├─────────┤
    0   │   40    │
        └─────────┘
```

#### POP Operation
```
Before POP (SP = 4):
        ┌─────────┐
    4 → │   15    │ ← SP
        ├─────────┤
    3   │   10    │
        ├─────────┤
    2   │   20    │
        └─────────┘

POP to R:
Step 1: R ← M[SP]        // R = 15
Step 2: SP ← SP - 1      // SP = 3

After POP (SP = 3):
        ┌─────────┐
    4   │   15    │ (no longer accessible)
        ├─────────┤
    3 → │   10    │ ← SP
        ├─────────┤
    2   │   20    │
        └─────────┘
```

### 11.3 Types of Stacks

#### A. Register Stack
- Implemented using registers
- Limited size (64-128 words)
- Very fast access
- Stack Pointer is a register

#### B. Memory Stack
- Implemented in main memory
- Large capacity
- Slower than register stack
- Stack Pointer in CPU, stack in memory

### Stack Applications

1. **Function Calls**: Store return addresses
2. **Expression Evaluation**: Postfix notation
3. **Interrupt Handling**: Save CPU state
4. **Recursion**: Store local variables

---

## 12. Addressing Modes

### Definition
Method of specifying operand location in instruction

### 12.1 Immediate Addressing

**Format**: `MOV R1, #5`

```
┌──────────┬──────────┬──────────┐
│  Opcode  │ Register │  Value   │
│   MOV    │    R1    │    5     │
└──────────┴──────────┴──────────┘
```

**Execution**: R1 ← 5

**Characteristics:**
- Operand is part of instruction
- Fast (no memory access)
- Limited value range
- Used for constants

**Example:**
```
MOV R1, #10      // R1 = 10
ADD R2, R1, #5   // R2 = R1 + 5 = 15
```

### 12.2 Direct Addressing

**Format**: `LOAD R1, 500`

```
┌──────────┬──────────┬──────────┐
│  Opcode  │ Register │ Address  │
│   LOAD   │    R1    │   500    │
└──────────┴──────────┴──────────┘
         │                │
         │                ▼
         │         ┌─────────────┐
         │    500: │     25      │
         │         └─────────────┘
         │                │
         └────────────────┴──► R1 = 25
```

**Execution**: R1 ← M[500]

**Characteristics:**
- Address in instruction
- One memory access
- Limited address space
- Simple implementation

**Example:**
```
Memory[100] = 50
LOAD R1, 100     // R1 = 50
```

### 12.3 Indirect Addressing

**Format**: `LOAD R1, (500)`

```
┌──────────┬──────────┬──────────┐
│  Opcode  │ Register │ Address  │
│   LOAD   │    R1    │  (500)   │
└──────────┴──────────┴──────────┘
         │                │
         │                ▼
         │         ┌─────────────┐
         │    500: │    1000     │ (Address)
         │         └─────────────┘
         │                │
         │                ▼
         │         ┌─────────────┐
         │   1000: │     75      │
         │         └─────────────┘
         │                │
         └────────────────┴──► R1 = 75
```

**Execution**: R1 ← M[M[500]]

**Characteristics:**
- Two memory accesses
- Large address space
- Slower execution
- Useful for pointers

**Example:**
```
Memory[500] = 1000
Memory[1000] = 75
LOAD R1, (500)   // R1 = 75
```

### 12.4 Register Addressing

**Format**: `ADD R3, R1, R2`

```
┌──────────┬──────┬──────┬──────┐
│  Opcode  │ Dest │ Src1 │ Src2 │
│   ADD    │  R3  │  R1  │  R2  │
└──────────┴──────┴──────┴──────┘
                │      │      │
        ┌───────┘      │      └───────┐
        │              │              │
    ┌───▼───┐      ┌───▼───┐     ┌───▼───┐
    │  R3   │      │  R1   │     │  R2   │
    │       │  ←   │  10   │  +  │  20   │
    └───────┘      └───────┘     └───────┘
        │
        ▼
       30
```

**Execution**: R3 ← R1 + R2

**Characteristics:**
- No memory access
- Fastest mode
- Limited operands (only registers)

**Example:**
```
R1 = 10, R2 = 20
ADD R3, R1, R2   // R3 = 30
```

### 12.5 Register Indirect Addressing

**Format**: `LOAD R1, (R2)`

```
┌──────────┬──────────┬──────────┐
│  Opcode  │   Dest   │  Source  │
│   LOAD   │    R1    │   (R2)   │
└──────────┴──────────┴──────────┘
                │           │
                │       ┌───▼────┐
                │       │   R2   │
                │       │  500   │ (Address)
                │       └────────┘
                │           │
                │           ▼
                │    ┌─────────────┐
                │    │ Memory[500] │
                │    │     45      │
                │    └─────────────┘
                │           │
                └───────────┴──► R1 = 45
```

**Execution**: R1 ← M[R2]

**Characteristics:**
- One memory access
- Flexible addressing
- Useful for arrays and pointers

**Example:**
```
R2 = 500
Memory[500] = 45
LOAD R1, (R2)    // R1 = 45
```

### 12.6 Indexed Addressing

**Format**: `LOAD R1, 100(R2)`

```
┌──────────┬──────┬──────────┬──────┐
│  Opcode  │ Dest │   Base   │ Index│
│   LOAD   │  R1  │   100    │  R2  │
└──────────┴──────┴──────────┴──────┘
                │       │         │
                │       │     ┌───▼────┐
                │       │     │   R2   │
                │       │     │   10   │
                │       │     └────────┘
                │       │         │
                │       └────┬────┘
                │            ▼
                │    Effective Address
                │      = 100 + 10
                │      = 110
                │            │
                │            ▼
                │     ┌─────────────┐
                │     │Memory[110]  │
                │     │     55      │
                │     └─────────────┘
                │            │
                └────────────┴──► R1 = 55
```

**Execution**: R1 ← M[100 + R2]

**Characteristics:**
- Effective Address = Base + Index
- One memory access
- Useful for arrays

**Example:**
```
Array starts at 100
R2 = 10 (offset)
Memory[110] = 55
LOAD R1, 100(R2)  // R1 = 55
```

### 12.7 Base Register Addressing

**Format**: `LOAD R1, (R2)+100`

```
Similar to indexed, but:
- R2 contains base address
- 100 is offset
- EA = R2 + 100
```

**Characteristics:**
- Base in register, offset in instruction
- Useful for accessing data structures
- Relocatable code

### 12.8 Relative Addressing

**Format**: `JMP 10` (PC-relative)

```
Current PC = 100
Offset = 10

Effective Address = PC + Offset
                  = 100 + 10
                  = 110

Jump to address 110
```

**Characteristics:**
- Relative to Program Counter
- Used in branch instructions
- Position-independent code

**Example:**
```
PC = 100
JMP +10          // Jump to 110
JMP -5           // Jump to 95
```

### 12.9 Auto-increment/Auto-decrement

#### Auto-increment: `LOAD R1, (R2)+`
```
Before:
R2 = 500
Memory[500] = 25

Execution:
1. R1 ← M[R2]    // R1 = 25
2. R2 ← R2 + 1   // R2 = 501

After:
R1 = 25
R2 = 501
```

#### Auto-decrement: `LOAD R1, -(R2)`
```
Before:
R2 = 500
Memory[499] = 30

Execution:
1. R2 ← R2 - 1   // R2 = 499
2. R1 ← M[R2]    // R1 = 30

After:
R1 = 30
R2 = 499
```

**Characteristics:**
- Useful for stack operations
- Efficient for array traversal

### Addressing Modes Summary

| Mode | Format | EA Calculation | Memory Access | Speed |
|------|--------|----------------|---------------|-------|
| Immediate | #Value | - | 0 | Fastest |
| Register | R1 | - | 0 | Fastest |
| Direct | Address | Address | 1 | Fast |
| Indirect | (Address) | M[Address] | 2 | Slow |
| Register Indirect | (R1) | R1 | 1 | Fast |
| Indexed | X(R1) | X + R1 | 1 | Fast |
| Relative | Offset | PC + Offset | 1 | Fast |

### Addressing Mode Examples

**Example: Array Access**
```
Array A starts at address 1000
Access A[5]

Method 1: Indexed Addressing
LOAD R1, 1000(R5)    // R5 = 5
EA = 1000 + 5 = 1005

Method 2: Register Indirect
LOAD R2, #1005       // Calculate address
LOAD R1, (R2)        // Access element
```

**Example: Pointer Usage**
```
int *ptr = &x;
*ptr = 10;

Assembly:
LOAD R1, X_ADDR      // R1 = address of X
STORE 10, (R1)       // Store 10 at *ptr
```

---

## 🚀 Quick Reference Summary

### Functional Units
- **Input, Output, Memory, ALU, Control Unit**

### Bus Types
- **Data Bus**: Bidirectional, carries data
- **Address Bus**: Unidirectional, carries addresses
- **Control Bus**: Bidirectional, carries control signals

### Bus Arbitration Methods
1. **Daisy Chain**: Simple, fixed priority
2. **Polling**: Flexible priority, requires address lines
3. **Independent Request**: Fast, expensive

### Register Transfer Notation
```
R2 ← R1           // Copy
R3 ← R1 + R2      // Add
M[AR] ← R1        // Store
```

### Stack Operations
```
PUSH: SP ← SP + 1; M[SP] ← Data
POP:  Data ← M[SP]; SP ← SP - 1
```

### Addressing Modes
- **Immediate**: #Value
- **Direct**: Address
- **Indirect**: (Address)
- **Register**: R1
- **Indexed**: Base(Index)

---

## 📝 Exam Important Questions

1. **Explain** the five functional units of a computer system with a neat diagram.

2. **Describe** bus architecture. Compare single bus and multiple bus structures.

3. **Explain** the three types of buses (Data, Address, Control) with their characteristics.

4. **Describe** centralized bus arbitration methods:
   - Daisy chain
   - Polling
   - Independent request

5. **Explain** register transfer operations with examples.

6. **Describe** the difference between single accumulator and general register organization.

7. **Explain** stack organization with PUSH and POP operations.

8. **Describe** all addressing modes with examples:
   - Immediate, Direct, Indirect
   - Register, Register Indirect
   - Indexed, Relative

9. **Compare** different addressing modes based on speed and memory access.

10. **Solve**: Given instructions, determine effective address for different addressing modes.

---

*End of Unit-1*
