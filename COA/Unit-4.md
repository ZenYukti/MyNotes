# Unit-4: Memory Organization

---

## 1. Memory Hierarchy

### Concept
- **Speed vs Cost vs Capacity** tradeoff
- Frequently used data in faster memory
- Less used data in slower, cheaper memory

### Memory Hierarchy Diagram

```
        ┌───────────────┐
        │   Registers   │  ← Fastest, Smallest, Most Expensive
        └───────┬───────┘     (~1 ns, ~1 KB)
                │
        ┌───────▼───────┐
        │  Cache (L1)   │     (~2-5 ns, ~64 KB)
        └───────┬───────┘
                │
        ┌───────▼───────┐
        │  Cache (L2)   │     (~10 ns, ~256 KB)
        └───────┬───────┘
                │
        ┌───────▼───────┐
        │  Cache (L3)   │     (~20 ns, ~8 MB)
        └───────┬───────┘
                │
        ┌───────▼───────┐
        │  Main Memory  │     (~100 ns, ~8-32 GB)
        │     (RAM)     │
        └───────┬───────┘
                │
        ┌───────▼───────┐
        │   Secondary   │     (~5 ms, ~1 TB+)
        │    Storage    │
        │   (SSD/HDD)   │
        └───────┬───────┘
                │
        ┌───────▼───────┐
        │   Tertiary    │  ← Slowest, Largest, Cheapest
        │    Storage    │     (~seconds, unlimited)
        │   (Tape/Cloud)│
        └───────────────┘
```

### Hierarchy Characteristics

| Level | Access Time | Capacity | Cost/Byte |
|-------|-------------|----------|-----------|
| Registers | 1 ns | 1 KB | Highest |
| L1 Cache | 2-5 ns | 64 KB | Very High |
| L2 Cache | 10 ns | 256 KB | High |
| L3 Cache | 20 ns | 8 MB | Medium |
| Main Memory | 100 ns | 8-32 GB | Low |
| SSD | 0.1 ms | 500 GB - 2 TB | Very Low |
| HDD | 5 ms | 1-10 TB | Lowest |

---

## 2. Semiconductor RAM Memories

### 2.1 Types of RAM

```
              RAM
               │
       ┌───────┴───────┐
       │               │
     SRAM            DRAM
  (Static RAM)   (Dynamic RAM)
       │               │
   Fast, Expensive  Slow, Cheap
   Cache Memory    Main Memory
```

### 2.2 SRAM (Static RAM)

**Structure**: Flip-flops (6 transistors per bit)

```
Memory Cell (1 bit):
     VDD
      │
  ┌───┴───┐
  │ Flip- │
  │  Flop │
  └───┬───┘
      │
   Word Line ──┤
      │
   Bit Line ───┴─── Data
```

**Characteristics:**
- **Fast** (1-10 ns)
- **Expensive** (~$10/GB)
- **No refresh** needed
- **Low density** (6T per bit)
- **Power hungry**
- **Used in**: Cache memory

### 2.3 DRAM (Dynamic RAM)

**Structure**: Capacitor + Transistor (1T1C)

```
Memory Cell (1 bit):
   Word Line ───┤├─── Transistor
                 │
                ═╪═  Capacitor
                 │
                GND

Capacitor stores charge:
  Charged = 1
  Discharged = 0
```

**Characteristics:**
- **Slower** (50-70 ns)
- **Cheap** (~$1/GB)
- **Needs refresh** (every 64 ms)
- **High density** (1T per bit)
- **Low power**
- **Used in**: Main memory

### SRAM vs DRAM

| Feature | SRAM | DRAM |
|---------|------|------|
| **Structure** | 6 Transistors | 1T + 1C |
| **Speed** | Fast (1-10 ns) | Slow (50-70 ns) |
| **Cost** | Expensive | Cheap |
| **Density** | Low | High |
| **Refresh** | No | Yes (every 64ms) |
| **Power** | High | Low |
| **Volatility** | Volatile | Volatile |
| **Usage** | Cache | Main Memory |

---

## 3. Memory Organization

### 3.1 Memory Cell Array

```
    Bit Lines (Data)
    B0   B1   B2   B3
     │    │    │    │
W0 ──┼────┼────┼────┼──  4×4 Memory Array
     │    │    │    │
W1 ──┼────┼────┼────┼──  Each intersection:
     │    │    │    │    Memory Cell
W2 ──┼────┼────┼────┼──
     │    │    │    │
W3 ──┼────┼────┼────┼──

Word Lines (Address)
```

### 3.2 2D Memory Organization

**Structure**: Organized in rows and columns

```
┌─────────────────────────────────────────┐
│          2D Memory (n × m)              │
│                                         │
│  Address ──► Row Decoder                │
│    (k bits)       │                     │
│              ┌────▼────┐                │
│              │  Word   │                │
│              │  Lines  │                │
│              └────┬────┘                │
│                   │                     │
│         ┌─────────▼─────────┐           │
│         │   Memory Array    │           │
│         │    (n × m bits)   │           │
│         └─────────┬─────────┘           │
│                   │                     │
│              ┌────▼────┐                │
│              │  Sense  │                │
│              │  Amps   │                │
│              └────┬────┘                │
│                   │                     │
│         Data ◄────┴────                 │
│        (m bits)                         │
└─────────────────────────────────────────┘

Example: 1K × 8 memory
  - 1024 words
  - 8 bits per word
  - 10-bit address (2^10 = 1024)
```

**Example: 1K × 8 Memory**

```
Address Space: 2^10 = 1024 locations
Word Size: 8 bits

Address Format:
┌────────────────────┐
│   10-bit Address   │
└────────────────────┘

Organization:
- 1024 rows (words)
- 8 columns (bits per word)
- Total: 1024 × 8 = 8192 bits
```

### 3.3 2½D Memory Organization

**Concept**: Multiple 2D arrays (banks)

```
┌──────────────────────────────────────────┐
│        2½D Memory Organization           │
│                                          │
│  Address                                 │
│  (14 bits)                               │
│     │                                    │
│     ├──► Bank Select (2 bits) ──┐       │
│     │                            │       │
│     └──► Row Address (12 bits) ──┼──┐   │
│                                  │  │   │
│    ┌────────┐  ┌────────┐  ┌───▼──▼───┐│
│    │ Bank 0 │  │ Bank 1 │  │ Bank ... ││
│    │ 4K×8   │  │ 4K×8   │  │  4K×8    ││
│    └───┬────┘  └───┬────┘  └────┬─────┘│
│        │           │             │      │
│        └───────────┴─────────────┘      │
│                    │                    │
│                 Data Out                │
│                  (8 bits)               │
└──────────────────────────────────────────┘

Example: 16K × 8 memory using 4 banks
  - 4 banks of 4K × 8 each
  - 2 bits: Bank select
  - 12 bits: Row address within bank
  - Total: 14-bit address
```

**Advantages:**
- **Parallel access** to different banks
- **Higher throughput**
- **Reduced access conflicts**

---

## 4. ROM (Read-Only Memory)

### Types of ROM

```
               ROM
                │
    ┌───────────┼───────────┐
    │           │           │
  Mask ROM    PROM        EPROM
  (Factory)  (One-time)  (UV erasable)
                              │
                           EEPROM
                        (Electrically
                         erasable)
                              │
                          Flash Memory
```

### 4.1 ROM Types

| Type | Programmable | Erasable | Erase Method | Uses |
|------|--------------|----------|--------------|------|
| **Mask ROM** | No (factory) | No | - | Firmware |
| **PROM** | Once | No | - | Low volume |
| **EPROM** | Multiple | Yes | UV light (20min) | Development |
| **EEPROM** | Multiple | Yes | Electrical (byte) | Settings |
| **Flash** | Multiple | Yes | Electrical (block) | Storage, USB |

### 4.2 ROM Applications

- **BIOS/UEFI** firmware
- **Bootstrap loader**
- **Microcode** storage
- **Lookup tables**
- **Character generators**
- **Embedded systems**

---

## 5. Cache Memory

### 5.1 Cache Concept

```
      CPU ◄───────► Cache ◄───────► Main Memory
      Fast          Very Fast       Slower
                    Small           Large
                    Expensive       Cheap

Principle of Locality:
  - Temporal: Recently used data likely to be used again
  - Spatial: Nearby data likely to be used soon
```

### 5.2 Cache Terminology

| Term | Definition |
|------|------------|
| **Hit** | Data found in cache |
| **Miss** | Data not in cache (fetch from main memory) |
| **Hit Rate** | % of accesses that hit |
| **Miss Rate** | % of accesses that miss |
| **Block** | Unit of transfer between cache and memory |
| **Line** | Storage location in cache for one block |

### 5.3 Cache Performance

**Access Time:**
```
Average Access Time = Hit Rate × Cache Access Time
                     + Miss Rate × (Cache Time + Memory Time)

Example:
  Hit Rate = 90%
  Cache Time = 10 ns
  Memory Time = 100 ns

  Avg Time = 0.9 × 10 + 0.1 × (10 + 100)
           = 9 + 11
           = 20 ns

Without cache: 100 ns
Speedup = 100/20 = 5×
```

---

## 6. Cache Mapping Techniques

### 6.1 Direct Mapping

**Concept**: Each memory block maps to exactly one cache line

```
Cache Line = (Memory Block) mod (Number of Cache Lines)
```

**Example: 8 Cache Lines, 32 Memory Blocks**

```
Memory Block → Cache Line
     0       →     0
     1       →     1
     2       →     2
     ...
     7       →     7
     8       →     0  (same as block 0)
     9       →     1  (same as block 1)
     ...
    15       →     7
    16       →     0  (same as blocks 0, 8)
```

**Address Format:**

```
┌────────────┬───────────┬──────────┐
│    Tag     │   Index   │  Offset  │
└────────────┴───────────┴──────────┘
     5 bits      3 bits      2 bits
      │           │           │
      │           │           └─► Byte within block
      │           └─────────────► Cache line number
      └─────────────────────────► Identify block

Example: 32-byte cache, 4-byte blocks
  - 8 cache lines (32/4)
  - Index: 3 bits (2^3 = 8)
  - Offset: 2 bits (4 bytes)
```

**Cache Structure:**

```
┌───────┬─────────┬────────────────┐
│ Valid │   Tag   │     Data       │
├───────┼─────────┼────────────────┤
│   1   │  0010   │ [Block Data]   │  Line 0
│   0   │  ----   │ [Block Data]   │  Line 1
│   1   │  0101   │ [Block Data]   │  Line 2
│  ...  │  ...    │      ...       │  ...
│   1   │  1001   │ [Block Data]   │  Line 7
└───────┴─────────┴────────────────┘
```

**Example: Memory Access**

```
Main Memory: 64 KB
Cache: 8 KB
Block Size: 16 bytes

Address: 16-bit
  - Offset: 4 bits (16 bytes = 2^4)
  - Index: 9 bits (8KB / 16B = 512 lines = 2^9)
  - Tag: 3 bits (16 - 4 - 9)

Access Address: 0x1234
┌────┬──────────┬─────┐
│001 │000100011│0100 │
└────┴──────────┴─────┘
 Tag    Index    Offset

Steps:
1. Extract Index: 000100011₂ = 35₁₀
2. Check Line 35 in cache
3. Compare Tag: 001 with stored tag
4. If match: HIT → Return data
5. If not: MISS → Fetch from memory
```

**Advantages:**
- **Simple** hardware
- **Fast** lookup
- **Low cost**

**Disadvantages:**
- **Conflict misses** (multiple blocks map to same line)
- **Low flexibility**

### 6.2 Associative Mapping (Fully Associative)

**Concept**: Any memory block can go in any cache line

```
Memory Block → Any Cache Line

No Index bits - All Tag!
```

**Address Format:**

```
┌────────────────────────┬──────────┐
│          Tag           │  Offset  │
└────────────────────────┴──────────┘
       12 bits              2 bits
         │                    │
         │                    └─► Byte within block
         └──────────────────────► Identifies block
```

**Cache Structure:**

```
┌───────┬──────────────┬────────────────┐
│ Valid │     Tag      │     Data       │
├───────┼──────────────┼────────────────┤
│   1   │ 000010010011 │ [Block Data]   │  Line 0
│   1   │ 010100110101 │ [Block Data]   │  Line 1
│   0   │ ------------ │ [Block Data]   │  Line 2
│  ...  │     ...      │      ...       │  ...
│   1   │ 100110101001 │ [Block Data]   │  Line 7
└───────┴──────────────┴────────────────┘

Access: Compare tag with ALL cache lines simultaneously
```

**Search Process:**

```
1. Extract Tag from address
2. Compare with ALL cache line tags (parallel)
3. If any match: HIT
4. If no match: MISS
```

**Advantages:**
- **No conflict misses**
- **Maximum flexibility**
- **Better hit rate**

**Disadvantages:**
- **Complex** hardware
- **Expensive** (parallel comparators)
- **Slower** than direct mapping

### 6.3 Set-Associative Mapping

**Concept**: Hybrid of direct and associative
- Cache divided into **sets**
- Each set contains multiple **ways** (lines)
- Block maps to a set (like direct)
- Can go in any way within set (like associative)

```
Set = (Memory Block) mod (Number of Sets)
```

**Example: 2-Way Set Associative**

```
8 Cache Lines = 4 Sets × 2 Ways

Set 0: Line 0, Line 1   (2 ways)
Set 1: Line 2, Line 3
Set 2: Line 4, Line 5
Set 3: Line 6, Line 7

Memory Block → Set → Any way in that set
     0       → Set 0 → Way 0 or Way 1
     1       → Set 1 → Way 0 or Way 1
     ...
     8       → Set 0 → Way 0 or Way 1 (same set as block 0)
```

**Address Format:**

```
┌────────────┬───────────┬──────────┐
│    Tag     │   Index   │  Offset  │
└────────────┴───────────┴──────────┘
     6 bits      2 bits      2 bits
      │           │           │
      │           │           └─► Byte within block
      │           └─────────────► Set number
      └─────────────────────────► Identify block

Index selects set, Tag compared within set
```

**Cache Structure (2-Way):**

```
       Way 0                    Way 1
┌─────┬─────┬──────┐    ┌─────┬─────┬──────┐
│Valid│ Tag │ Data │    │Valid│ Tag │ Data │
├─────┼─────┼──────┤    ├─────┼─────┼──────┤
│  1  │ 011 │ [D0] │    │  1  │ 101 │ [D1] │  Set 0
├─────┼─────┼──────┤    ├─────┼─────┼──────┤
│  0  │ --- │ [D2] │    │  1  │ 010 │ [D3] │  Set 1
├─────┼─────┼──────┤    ├─────┼─────┼──────┤
│  1  │ 100 │ [D4] │    │  0  │ --- │ [D5] │  Set 2
├─────┼─────┼──────┤    ├─────┼─────┼──────┤
│  1  │ 110 │ [D6] │    │  1  │ 001 │ [D7] │  Set 3
└─────┴─────┴──────┘    └─────┴─────┴──────┘
```

**Search Process:**

```
1. Extract Index → Select Set
2. Compare Tag with both ways in parallel
3. If match in either way: HIT
4. If no match: MISS
```

**Advantages:**
- **Fewer conflict misses** than direct
- **Simpler** than fully associative
- **Good compromise**

**Disadvantages:**
- **More complex** than direct
- **More expensive** than direct

### Mapping Comparison

| Feature | Direct | 2-Way Set | 4-Way Set | Fully Assoc |
|---------|--------|-----------|-----------|-------------|
| **Placement** | Fixed | 2 choices | 4 choices | Any line |
| **Comparators** | 1 | 2 | 4 | N (all lines) |
| **Hit Rate** | Low | Medium | High | Highest |
| **Hardware** | Simple | Moderate | Complex | Most Complex |
| **Cost** | Low | Medium | High | Highest |
| **Speed** | Fast | Medium | Slower | Slowest |

**Example: 8-line cache, access pattern: 0, 8, 0, 8, 0...**

```
Direct Mapping:
  Block 0 → Line 0
  Block 8 → Line 0 (replaces block 0)
  Block 0 → Line 0 (replaces block 8)
  Result: MISS, MISS, MISS... (0% hit rate)

2-Way Set Associative:
  Block 0 → Set 0, Way 0
  Block 8 → Set 0, Way 1
  Block 0 → Set 0, Way 0 (HIT)
  Block 8 → Set 0, Way 1 (HIT)
  Result: MISS, MISS, HIT, HIT... (50% hit rate after warmup)
```

---

## 7. Cache Replacement Policies

When cache is full and new block needed, which to replace?

### 7.1 FIFO (First In First Out)

```
Replace the oldest block in cache

Example: 3-block cache, access: 0, 1, 2, 3, 0, 1

┌──────┬───────────────┬────────┐
│Access│  Cache State  │ Result │
├──────┼───────────────┼────────┤
│  0   │    [0]        │  MISS  │
│  1   │    [0,1]      │  MISS  │
│  2   │    [0,1,2]    │  MISS  │
│  3   │    [1,2,3]    │  MISS  │ (0 replaced)
│  0   │    [2,3,0]    │  MISS  │ (1 replaced)
│  1   │    [3,0,1]    │  MISS  │ (2 replaced)
└──────┴───────────────┴────────┘

Hit Rate: 0/6 = 0%
```

### 7.2 LRU (Least Recently Used)

```
Replace block not used for longest time

Example: 3-block cache, access: 0, 1, 2, 3, 0, 1

┌──────┬───────────────┬────────┬─────────────┐
│Access│  Cache State  │ Result │   LRU Age   │
├──────┼───────────────┼────────┼─────────────┤
│  0   │    [0]        │  MISS  │  0(new)     │
│  1   │    [0,1]      │  MISS  │  0,1(new)   │
│  2   │    [0,1,2]    │  MISS  │  0,1,2(new) │
│  3   │    [1,2,3]    │  MISS  │  1,2,3(new) │ (0=oldest)
│  0   │    [1,3,0]    │  MISS  │  1,3,0(new) │ (2=oldest)
│  1   │    [1,3,0]    │  HIT   │  3,0,1(new) │
└──────┴───────────────┴────────┴─────────────┘

Hit Rate: 1/6 = 16.7%
```

### 7.3 LFU (Least Frequently Used)

```
Replace block used least number of times

Tracks access count for each block
```

### 7.4 Random

```
Replace random block

Simple but unpredictable performance
```

### Replacement Policy Comparison

| Policy | Hardware | Performance | Predictability |
|--------|----------|-------------|----------------|
| **FIFO** | Simple | Poor | High |
| **LRU** | Complex | Best | High |
| **LFU** | Complex | Good | Medium |
| **Random** | Simplest | Fair | Low |

---

## 8. Auxiliary Memories

### 8.1 Magnetic Disk (HDD)

**Structure:**

```
┌─────────────────────────────────────┐
│         Magnetic Disk               │
│                                     │
│  ┌──────────────────────────────┐  │
│  │       Platter (disk)         │  │
│  │   ┌────────────────────┐     │  │
│  │   │   Track            │     │  │
│  │   │  ┌──────┐          │     │  │
│  │   │  │Sector│          │     │  │
│  │   │  └──────┘          │     │  │
│  │   └────────────────────┘     │  │
│  │        ▲                     │  │
│  │        │ Read/Write Head     │  │
│  │        │                     │  │
│  └────────┼─────────────────────┘  │
│           │                        │
│      Arm Movement                  │
└─────────────────────────────────────┘

Components:
- Platter: Rotating disk
- Track: Concentric circle
- Sector: Arc of track (512-4096 bytes)
- Cylinder: Same track on all platters
- Read/Write Head: Magnetic sensor
```

**Access Time:**
```
Total Access Time = Seek Time + Rotational Latency + Transfer Time

Seek Time: Move head to correct track (5-10 ms)
Rotational Latency: Wait for sector (avg 4 ms @ 7200 RPM)
Transfer Time: Read/write data (~100 µs for 4KB)

Example:
  Seek: 8 ms
  Rotational: 4 ms
  Transfer: 0.1 ms
  Total: 12.1 ms
```

**Characteristics:**
- **Capacity**: 1-20 TB
- **Speed**: 5400-15000 RPM
- **Access Time**: 5-15 ms
- **Transfer Rate**: 100-200 MB/s
- **Cost**: ~$20/TB
- **Volatile**: No

### 8.2 Magnetic Tape

```
┌─────────────────────────────────┐
│    Magnetic Tape                │
│                                 │
│  ┌──────────────────────────┐  │
│  │ ══════════════════════  │  │
│  │     Sequential Data      │  │
│  │ ══════════════════════  │  │
│  └──────────────────────────┘  │
│       │              │          │
│    Supply         Take-up       │
│     Reel           Reel         │
└─────────────────────────────────┘
```

**Characteristics:**
- **Sequential access** only
- **Very slow** (seconds to minutes)
- **Very cheap** (~$5/TB)
- **High capacity** (unlimited)
- **Used for**: Backup, archival
- **Offline storage**

### 8.3 Optical Disks

```
Types:
- CD (Compact Disc): 700 MB
- DVD (Digital Versatile Disc): 4.7 GB (single layer)
- Blu-ray: 25 GB (single layer), 50 GB (dual layer)

Variants:
- ROM: Read-only (factory pressed)
- R: Recordable (write once)
- RW: Rewritable (multiple writes)
```

**Characteristics:**
- **Removable media**
- **Read by laser**
- **Slower than HDD** (150 KB/s - 10 MB/s)
- **Portable**
- **Used for**: Distribution, backup

### 8.4 Solid State Drive (SSD)

**Structure**: Flash memory (no moving parts)

```
┌──────────────────────────────┐
│         SSD                  │
│                              │
│  ┌────────────────────────┐ │
│  │   Flash Memory Chips   │ │
│  │   (NAND Flash)         │ │
│  └────────────────────────┘ │
│             ▲                │
│             │                │
│  ┌──────────┴─────────────┐ │
│  │   Controller           │ │
│  │   (Wear Leveling)      │ │
│  └────────────────────────┘ │
└──────────────────────────────┘
```

**Characteristics:**
- **No moving parts**
- **Very fast** (0.1 ms access, 500+ MB/s)
- **Expensive** (~$100/TB)
- **Limited writes** (~100K-1M cycles per cell)
- **Silent, durable**
- **Wear leveling** to extend life

### Auxiliary Memory Comparison

| Type | Capacity | Speed | Cost | Volatility | Use Case |
|------|----------|-------|------|------------|----------|
| **HDD** | 1-20 TB | 5-15 ms | Low | No | General storage |
| **SSD** | 256GB-4TB | 0.1 ms | High | No | OS, applications |
| **Tape** | Unlimited | Seconds | Very Low | No | Backup, archival |
| **Optical** | 700MB-50GB | Slow | Low | No | Distribution |

---

## 9. Virtual Memory

### 9.1 Concept

**Problem**: Programs larger than physical RAM

**Solution**: Use disk as extension of RAM

```
┌────────────────────────────────────────┐
│     Virtual Memory Space               │
│     (Program's view: 4 GB)             │
│  ┌──────────────────────────────────┐  │
│  │                                  │  │
│  │    Process Address Space         │  │
│  │                                  │  │
│  └──────────┬───────────────────────┘  │
│             │                          │
│             │ OS + Hardware            │
│             │ (MMU)                    │
│             ▼                          │
│  ┌─────────────────────┐              │
│  │   Physical RAM      │              │
│  │   (Actual: 512 MB)  │              │
│  └──────────┬──────────┘              │
│             │                          │
│             │ Page Swapping            │
│             ▼                          │
│  ┌─────────────────────┐              │
│  │   Disk (Swap Space) │              │
│  │   (Virtual: 3.5 GB) │              │
│  └─────────────────────┘              │
└────────────────────────────────────────┘

MMU: Memory Management Unit
```

### 9.2 Paging

**Concept**:
- Virtual memory divided into **pages** (4 KB typical)
- Physical memory divided into **frames** (same size)
- Map pages to frames

```
Virtual Address:
┌──────────────┬──────────────┐
│ Page Number  │    Offset    │
└──────────────┴──────────────┘
    20 bits        12 bits
     │              │
     │              └──► Byte within page (4KB = 2^12)
     └─────────────────► Page number (2^20 pages)

Physical Address:
┌──────────────┬──────────────┐
│Frame Number  │    Offset    │
└──────────────┴──────────────┘
```

**Page Table:**

```
┌─────────────┬────────────┬───────┬───────┐
│ Page Number │Frame Number│ Valid │ Dirty │
├─────────────┼────────────┼───────┼───────┤
│     0       │     5      │   1   │   0   │
│     1       │     -      │   0   │   -   │ (Not in RAM)
│     2       │     3      │   1   │   1   │
│    ...      │    ...     │  ...  │  ...  │
│   1023      │     7      │   1   │   0   │
└─────────────┴────────────┴───────┴───────┘

Valid bit: 1 = in RAM, 0 = on disk
Dirty bit: 1 = modified, 0 = unmodified
```

### 9.3 Address Translation

```
Virtual Address: 0x00012345
┌────────┬────────┐
│  0001  │  2345  │
└────────┴────────┘
  Page 1   Offset

Step 1: Look up Page 1 in Page Table
        Page 1 → Frame 5 (if valid=1)

Step 2: Construct Physical Address
        Frame 5 + Offset 2345
        Physical Address: 0x00052345

If valid=0: PAGE FAULT
  → Load page from disk
  → Update page table
  → Retry access
```

### 9.4 Page Replacement Algorithms

When RAM full, which page to swap out?

#### FIFO (First In First Out)
```
Replace oldest page

Example: 3 frames, access: 0,1,2,3,0,1,4

┌──────┬────────────┬────────┐
│Access│  Frames    │ Result │
├──────┼────────────┼────────┤
│  0   │  [0, , ]   │  Fault │
│  1   │  [0,1, ]   │  Fault │
│  2   │  [0,1,2]   │  Fault │
│  3   │  [3,1,2]   │  Fault │ (0 out)
│  0   │  [3,0,2]   │  Fault │ (1 out)
│  1   │  [3,0,1]   │  Fault │ (2 out)
│  4   │  [4,0,1]   │  Fault │ (3 out)
└──────┴────────────┴────────┘

Page Faults: 7/7 = 100%
```

#### LRU (Least Recently Used)
```
Replace page not used for longest time

Example: 3 frames, access: 0,1,2,3,0,1,4

┌──────┬────────────┬────────┬──────────┐
│Access│  Frames    │ Result │   LRU    │
├──────┼────────────┼────────┼──────────┤
│  0   │  [0, , ]   │  Fault │  0       │
│  1   │  [0,1, ]   │  Fault │  0,1     │
│  2   │  [0,1,2]   │  Fault │  0,1,2   │
│  3   │  [3,1,2]   │  Fault │  3,1,2   │ (0=LRU)
│  0   │  [3,0,2]   │  Fault │  3,0,2   │ (1=LRU)
│  1   │  [3,0,1]   │  Fault │  3,0,1   │ (2=LRU)
│  4   │  [4,0,1]   │  Fault │  4,0,1   │ (3=LRU)
└──────┴────────────┴────────┴──────────┘

Page Faults: 7/7 = 100% (worse case)
```

#### Optimal (Theoretical)
```
Replace page not needed for longest time (future knowledge)

Best possible, but not implementable (needs future info)
```

### 9.5 Translation Lookaside Buffer (TLB)

**Problem**: Page table access adds overhead

**Solution**: Cache recent page translations

```
┌────────────────────────────────────────┐
│  Virtual Address                       │
└──────────┬─────────────────────────────┘
           │
           ▼
     ┌──────────┐
     │   TLB    │ (Hardware cache)
     │ (16-512  │
     │ entries) │
     └────┬─────┘
          │
    ┌─────┴─────┐
    │           │
   Hit         Miss
    │           │
    │           ▼
    │     ┌──────────┐
    │     │Page Table│ (In RAM)
    │     │(1M entries)
    │     └────┬─────┘
    │          │
    └──────┬───┘
           │
           ▼
   Physical Address
```

**Performance:**
```
TLB hit: 1 memory access (page table skipped)
TLB miss: 2 memory accesses (page table + actual data)

Example:
  TLB hit rate = 95%
  Time with TLB = 0.95×1 + 0.05×2 = 1.05 accesses
  Time without TLB = 2 accesses
  Speedup = 2/1.05 = 1.9×
```

---

## 🚀 Quick Reference Summary

### Memory Hierarchy
```
Registers → Cache → RAM → SSD → HDD → Tape
(Fastest, smallest) → (Slowest, largest)
```

### Cache Mapping
- **Direct**: Fixed placement, simple
- **Associative**: Any placement, complex
- **Set-Associative**: Hybrid, practical

### Cache Replacement
- **FIFO**: Replace oldest
- **LRU**: Replace least recently used
- **Random**: Replace random

### Virtual Memory
- **Paging**: Fixed-size blocks (pages/frames)
- **Page Table**: Maps pages to frames
- **TLB**: Caches page translations
- **Page Replacement**: FIFO, LRU, Optimal

---

## 📝 Exam Important Questions

1. **Explain** memory hierarchy with characteristics of each level.

2. **Compare** SRAM and DRAM.

3. **Describe** cache mapping techniques:
   - Direct mapping
   - Set-associative mapping
   - Fully associative mapping

4. **Calculate**: Given cache configuration, determine hit/miss for address sequence.

5. **Explain** virtual memory concept and its implementation.

6. **Describe** paging with address translation example.

7. **Compare** HDD and SSD characteristics.

8. **Demonstrate** LRU page replacement for given page reference string.

9. **Calculate** effective access time with cache and TLB.

10. **Design** a 2-way set-associative cache for given specifications.

---

*End of Unit-4*
