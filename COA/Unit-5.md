# Unit-5: Input/Output Organization

---

## 1. Peripheral Devices

### 1.1 Classification

```
              Peripheral Devices
                     │
        ┌────────────┼────────────┐
        │            │            │
     Input        Output      Storage
        │            │            │
   ┌────┴────┐  ┌────┴────┐  ┌────┴────┐
   │Keyboard │  │ Monitor │  │   HDD   │
   │  Mouse  │  │ Printer │  │   SSD   │
   │ Scanner │  │ Speaker │  │USB Drive│
   │ Webcam  │  │Projector│  │   CD    │
   │Microphone  │         │  │   DVD   │
   └─────────┘  └─────────┘  └─────────┘
```

### 1.2 Device Characteristics

| Device | Speed | Data Transfer |
|--------|-------|---------------|
| **Keyboard** | 10 bytes/sec | Character |
| **Mouse** | 100 bytes/sec | Coordinates |
| **Monitor** | 10 MB/sec | Video frame |
| **HDD** | 100 MB/sec | Block |
| **SSD** | 500 MB/sec | Block |
| **Network** | 100 MB/sec | Packet |

---

## 2. I/O Interface

### 2.1 Need for I/O Interface

**Problems without interface:**
- Different data formats
- Different speeds
- Different control signals
- Different timing requirements

**Solution**: I/O Interface (Controller)

```
┌──────────┐         ┌────────────┐         ┌──────────┐
│   CPU    │◄───────►│ I/O        │◄───────►│ Peripheral│
│          │  System │ Interface  │  Device │  Device  │
│          │   Bus   │(Controller)│  Bus    │          │
└──────────┘         └────────────┘         └──────────┘
                            │
                      ┌─────┴─────┐
                      │• Buffering │
                      │• Format    │
                      │  conversion│
                      │• Timing    │
                      │• Control   │
                      └───────────┘
```

### 2.2 I/O Interface Functions

1. **Data Buffering**
   - Temporary storage
   - Speed matching

2. **Format Conversion**
   - Serial ↔ Parallel
   - Analog ↔ Digital

3. **Timing and Control**
   - Handshaking signals
   - Synchronization

4. **Error Detection**
   - Parity check
   - CRC

5. **Device Selection**
   - Address decoding
   - Device identification

---

## 3. I/O Ports

### 3.1 Port Types

```
┌────────────────────────────────────┐
│        I/O Interface               │
│                                    │
│  ┌──────────────┐                  │
│  │ Data Register│ ◄── Read/Write   │
│  │   (8/16/32)  │     Data         │
│  └──────────────┘                  │
│                                    │
│  ┌──────────────┐                  │
│  │Status Register ◄── Check       │
│  │   (Flags)    │     Device       │
│  └──────────────┘     Status       │
│                                    │
│  ┌──────────────┐                  │
│  │Control Register ◄── Configure  │
│  │   (Commands) │     Device       │
│  └──────────────┘                  │
└────────────────────────────────────┘
```

### 3.2 Port Addressing

#### A. Memory-Mapped I/O
```
Same address space for memory and I/O

Memory: 0x0000 - 0xFFFF (64KB)
I/O:    0x0000 - 0x00FF (part of memory map)

Advantages:
  - Same instructions for memory and I/O
  - No special I/O instructions needed
  
Disadvantages:
  - Reduces available memory space
  - Slower (memory instructions more complex)
```

#### B. Isolated I/O (Port-Mapped)
```
Separate address spaces

Memory: 0x0000 - 0xFFFF
I/O:    0x00 - 0xFF (separate space)

Special Instructions:
  IN  AL, [port]    ; Read from port
  OUT [port], AL    ; Write to port

Advantages:
  - Full memory space available
  - Fast I/O instructions
  
Disadvantages:
  - Need special instructions
  - More complex CPU design
```

---

## 4. Interrupts

### 4.1 What is an Interrupt?

**Definition**: Signal that causes CPU to temporarily stop current program and execute interrupt service routine (ISR)

```
Normal Flow:
  Instr1 → Instr2 → Instr3 → Instr4 → ...

With Interrupt:
  Instr1 → Instr2 → [Interrupt!] → ISR → Instr3 → Instr4 → ...
                         ↓              ↑
                    Save State    Restore State
```

### 4.2 Interrupt Mechanism

```
Step 1: Interrupt Request (IRQ)
┌──────────┐
│ Device   │────► IRQ ────► CPU
└──────────┘

Step 2: Save Context
CPU: Save PC, Flags, Registers to Stack

Step 3: Jump to ISR
CPU: PC ← Interrupt Vector

Step 4: Execute ISR
┌──────────────────┐
│ Service Device   │
│ (Read/Write data)│
└──────────────────┘

Step 5: Return from Interrupt (IRET)
CPU: Restore PC, Flags, Registers from Stack

Step 6: Resume Normal Execution
```

### 4.3 Interrupt Hardware

```
┌─────────────────────────────────────────┐
│              CPU                        │
│  ┌──────────────────────────────────┐   │
│  │     Interrupt Controller         │   │
│  │    (Priority, Masking)           │   │
│  └──────────┬───────────────────────┘   │
└─────────────┼───────────────────────────┘
              │
    ┌─────────┴─────────────────┐
    │         │         │        │
   IRQ0     IRQ1      IRQ2     IRQ3
    │         │         │        │
┌───▼───┐ ┌───▼───┐ ┌───▼───┐ ┌───▼───┐
│Device1│ │Device2│ │Device3│ │Device4│
└───────┘ └───────┘ └───────┘ └───────┘
```

### 4.4 Interrupt Priority

**Problem**: Multiple interrupts arrive simultaneously

**Solution**: Priority system

```
Priority Levels (Highest to Lowest):
┌──────────────────────────────────┐
│ 1. Power Failure (Highest)       │
│ 2. Machine Error                 │
│ 3. Timer                         │
│ 4. Disk                          │
│ 5. Network                       │
│ 6. Keyboard (Lowest)             │
└──────────────────────────────────┘

Example:
  Keyboard interrupt arrives
  While servicing keyboard:
    Disk interrupt arrives (higher priority)
    → Pause keyboard ISR
    → Service disk
    → Resume keyboard ISR
```

### 4.5 Interrupt Masking

```
Enable/Disable specific interrupts

┌────────────────────────┐
│  Interrupt Mask        │
│  (8-bit register)      │
│  ┌─┬─┬─┬─┬─┬─┬─┬─┐     │
│  │1│0│1│1│0│1│0│1│     │
│  └─┴─┴─┴─┴─┴─┴─┴─┘     │
│   │ │ │ │ │ │ │ │      │
│   7 6 5 4 3 2 1 0      │
│                        │
│  1 = Enabled           │
│  0 = Disabled (Masked) │
└────────────────────────┘

Example:
  Bit 6 = 0: Timer interrupts masked
  Bit 5 = 1: Disk interrupts enabled
```

### 4.6 Vectored vs Non-Vectored Interrupts

#### Vectored Interrupts
```
Device provides interrupt vector (address of ISR)

┌──────────┐
│ Device   │───► Vector (e.g., 0x50)
└──────────┘           │
                       ▼
              ┌─────────────────┐
              │ Interrupt Vector│
              │     Table       │
              │  0x50: 0x1000   │ ← ISR address
              └─────────────────┘
                       │
                       ▼
                  ISR at 0x1000

Fast, direct jump to ISR
```

#### Non-Vectored Interrupts
```
CPU polls devices to identify interrupt source

1. Interrupt occurs
2. CPU: "Who interrupted?"
3. Poll each device
4. Device responds
5. CPU jumps to ISR

Slower, but simpler hardware
```

---

## 5. Types of Interrupts and Exceptions

### 5.1 Classification

```
        Interrupts & Exceptions
                 │
        ┌────────┴────────┐
        │                 │
    Hardware          Software
   Interrupts        Exceptions
        │                 │
   ┌────┴────┐      ┌─────┴─────┐
   │         │      │           │
External  Internal  Faults    Traps
   │         │      │           │
  I/O      Timer  Divide by 0  INT 0x80
Keyboard   Clock   Page Fault  Syscall
```

### 5.2 Hardware Interrupts

#### External (Asynchronous)
- Generated by **I/O devices**
- Independent of program execution
- Examples:
  - Keyboard press
  - Mouse click
  - Network packet arrival
  - Disk operation complete

#### Internal (Synchronous)
- Generated by **CPU** during execution
- Examples:
  - Timer interrupt
  - Performance counter overflow

### 5.3 Exceptions (Software Interrupts)

#### Faults
- Correctable errors
- Return to **same instruction** after handling
- Examples:
  - **Page fault**: Requested page not in memory
  - **Divide by zero**: Arithmetic error
  - **Invalid opcode**: Illegal instruction

```
Example: Page Fault
1. Instruction accesses memory
2. Page not in RAM (fault)
3. OS loads page from disk
4. Retry same instruction
5. Success!
```

#### Traps
- Intentional, for **system calls**
- Return to **next instruction**
- Examples:
  - `INT 0x80` (Linux system call)
  - `SYSCALL` instruction
  - `TRAP` instruction

```
Example: System Call
Program:         OS:
  ...
  INT 0x80   →  1. Save context
  ...        ←  2. Execute system call
                3. Restore context
                4. Return to next instruction
```

#### Aborts
- Unrecoverable errors
- **Cannot continue** execution
- Examples:
  - Hardware failure
  - Critical system error

### 5.4 Exception Handling

```
┌────────────────────────────────────────┐
│         Exception Occurs               │
└──────────────┬─────────────────────────┘
               │
               ▼
     ┌──────────────────┐
     │  Save Context    │
     │  (PC, Flags)     │
     └─────────┬────────┘
               │
               ▼
     ┌──────────────────┐
     │ Identify Exception│
     │ (Type, Code)     │
     └─────────┬────────┘
               │
               ▼
     ┌──────────────────┐
     │ Jump to Handler  │
     │ (Exception Table)│
     └─────────┬────────┘
               │
               ▼
     ┌──────────────────┐
     │  Execute Handler │
     │  (Fix problem)   │
     └─────────┬────────┘
               │
          ┌────┴────┐
          │         │
       Fault      Trap
          │         │
     ┌────▼───┐ ┌──▼────┐
     │ Retry  │ │ Next  │
     │ Same   │ │ Instr │
     └────────┘ └───────┘
```

---

## 6. Modes of Data Transfer

### 6.1 Programmed I/O

**Concept**: CPU actively waits for I/O

```
CPU:
1. Check device status
2. If busy: goto 1 (poll)
3. If ready: Transfer data
4. Repeat for each byte

┌──────────────────────────────────┐
│  Read from Keyboard:             │
│                                  │
│  Loop:                           │
│    Status ← Read Status Register │
│    If (Status.Ready == 0)        │
│      goto Loop                   │
│    Data ← Read Data Register     │
└──────────────────────────────────┘

Time Wasted: CPU polls continuously!
```

**Example: Read 1000 bytes from disk**

```
CPU Code:
for (i = 0; i < 1000; i++) {
    while (!(Status & READY))  // Busy wait
        ;
    Data[i] = ReadPort(DATA_PORT);
}

CPU busy for entire transfer!
```

**Characteristics:**
- **Simple** hardware
- **No additional** hardware needed
- **Wastes CPU time** (busy waiting)
- **Used for**: Slow devices (keyboard, mouse)

### 6.2 Interrupt-Initiated I/O

**Concept**: CPU does other work, device interrupts when ready

```
CPU:
1. Issue I/O command to device
2. Continue other work
3. When device ready: Interrupt
4. Transfer data in ISR
5. Return to work

┌──────────────────────────────────┐
│  Main Program:                   │
│    Issue Read Command            │
│    Continue computation...       │
│    ...more work...               │
│                                  │
│  [Interrupt from device]         │
│                                  │
│  ISR:                            │
│    Data ← Read Data Register     │
│    Process data                  │
│    Return                        │
└──────────────────────────────────┘

CPU free to do other work!
```

**Example: Read 1000 bytes from disk**

```
CPU Code:
Issue read command for next byte
Enable interrupts

ISR:
  Data[i++] = ReadPort(DATA_PORT);
  if (i < 1000)
    Issue read command for next byte
  else
    Transfer complete

CPU does other work between interrupts!
```

**Characteristics:**
- **Efficient** CPU utilization
- **Requires** interrupt hardware
- **Overhead** per interrupt (context switch)
- **Used for**: Moderate-speed devices (disk, network)

### 6.3 Direct Memory Access (DMA)

**Concept**: Device transfers data directly to/from memory without CPU

```
┌───────────┐         ┌───────────┐
│    CPU    │         │   Memory  │
└─────┬─────┘         └─────┬─────┘
      │                     │
      │                     │
      │   ┌─────────────┐   │
      └───┤ DMA         ├───┘
          │ Controller  │
          └──────┬──────┘
                 │
           ┌─────┴─────┐
           │  Device   │
           │  (Disk)   │
           └───────────┘

CPU only involved at start and end!
```

**DMA Operation:**

```
Step 1: CPU Setup
  - Write to DMA controller:
    • Source address
    • Destination address  
    • Transfer count
    • Direction (read/write)
  - Start DMA

Step 2: DMA Transfer (CPU free!)
  - DMA controller takes bus control
  - Transfers data block by block
  - Increments addresses
  - Decrements count

Step 3: Completion
  - DMA sends interrupt to CPU
  - CPU: "Transfer complete"
```

**Example: Transfer 1000 bytes from disk to memory**

```
CPU Code:
  DMA_Source = DISK_DATA_PORT;
  DMA_Dest = Memory_Buffer;
  DMA_Count = 1000;
  DMA_Start();
  
  // CPU does other work
  ...
  
  // Interrupt when done
  ISR:
    // Data already in memory!
    Process_Data(Memory_Buffer);
```

**DMA Registers:**

```
┌─────────────────────────────────┐
│  DMA Controller Registers       │
├─────────────────────────────────┤
│  Source Address Register (SAR)  │
│  Destination Address Reg (DAR)  │
│  Count Register (Bytes left)    │
│  Control Register (Start/Stop)  │
│  Status Register (Done/Error)   │
└─────────────────────────────────┘
```

**DMA Transfer Modes:**

#### A. Burst Mode
```
DMA takes bus for entire transfer
- Fast
- CPU completely blocked
- Used for fast devices
```

#### B. Cycle Stealing
```
DMA takes bus for one word at a time
- Slower
- CPU can access bus between transfers
- Minimal CPU impact
- Used for slower devices
```

#### C. Transparent Mode
```
DMA only uses bus when CPU doesn't need it
- Slowest
- Zero CPU impact
- Used for very slow devices
```

**Characteristics:**
- **Very efficient** (no CPU involvement)
- **Expensive** hardware
- **Used for**: High-speed devices (disk, network, video)

### Mode Comparison

| Feature | Programmed I/O | Interrupt I/O | DMA |
|---------|----------------|---------------|-----|
| **CPU Involvement** | Continuous | Per byte/word | Start + End only |
| **Data Transfer** | CPU | CPU | DMA controller |
| **Speed** | Slowest | Medium | Fastest |
| **Hardware** | Simplest | Moderate | Complex |
| **Cost** | Lowest | Medium | Highest |
| **CPU Utilization** | Poor | Good | Excellent |
| **Use Case** | Keyboard | Disk | Video, High-speed disk |

**Example: Disk Read Performance**

```
Transfer 1 MB from disk:

Programmed I/O:
  - CPU busy for ~10 seconds
  - 0% CPU available for other work

Interrupt I/O:
  - 1M interrupts
  - ~30% CPU available for other work

DMA:
  - 1 interrupt
  - ~99% CPU available for other work
```

---

## 7. I/O Channels and Processors

### 7.1 I/O Processor (IOP)

**Concept**: Dedicated processor for I/O operations

```
┌─────────────────────────────────────────┐
│           Main CPU                      │
│  (Application processing)               │
└──────────────┬──────────────────────────┘
               │
        ┌──────▼──────┐
        │   Memory    │
        └──────┬──────┘
               │
     ┌─────────┴─────────┐
     │                   │
┌────▼────┐         ┌────▼────┐
│   IOP   │         │   IOP   │
│(Channel)│         │(Channel)│
└────┬────┘         └────┬────┘
     │                   │
  ┌──┴──┐             ┌──┴──┐
  │     │             │     │
 Disk  Tape         Network Printer
```

**IOP Characteristics:**
- **Independent** processor
- Executes **I/O programs** (channel programs)
- **DMA capability**
- **Multiple devices** per channel
- **Used in**: Mainframes

### 7.2 I/O Channel

**Types:**

#### A. Selector Channel
```
Dedicated to ONE high-speed device at a time

┌──────────────┐
│   Selector   │───► Disk 1
│   Channel    │───► Disk 2 (only one active)
└──────────────┘───► Disk 3
```

#### B. Multiplexor Channel
```
Handles MULTIPLE slow devices simultaneously

┌──────────────┐
│ Multiplexor  │───► Terminal 1 \
│   Channel    │───► Terminal 2  ├─ Time-shared
└──────────────┘───► Terminal 3 /
```

#### C. Block Multiplexor
```
Handles multiple high-speed devices
Interleaves blocks from different devices

┌──────────────┐
│    Block     │───► Disk 1 \
│ Multiplexor  │───► Disk 2  ├─ Block interleaving
└──────────────┘───► Disk 3 /
```

### 7.3 Channel Program

**Example: Read 100 bytes from disk**

```
Channel Program (in memory):
┌────────────────────────────────┐
│ Cmd: Seek to track 10          │
│ Cmd: Read 100 bytes            │
│ Addr: Memory buffer 0x10000    │
│ Cmd: Interrupt when done       │
└────────────────────────────────┘

CPU:
  1. Write channel program to memory
  2. Start channel (give program address)
  3. Continue other work
  
Channel (IOP):
  1. Fetch channel program
  2. Execute commands sequentially
  3. Transfer data using DMA
  4. Interrupt CPU when done
```

---

## 8. Serial Communication

### 8.1 Serial vs Parallel

```
Parallel:
┌─────┐   Bit 0 ────────────────┐   ┌─────┐
│     │   Bit 1 ────────────────┤   │     │
│ TX  │   Bit 2 ────────────────┼───┤ RX  │
│     │   ...                   │   │     │
└─────┘   Bit 7 ────────────────┘   └─────┘
  8 wires - Fast but expensive

Serial:
┌─────┐                          ┌─────┐
│ TX  │──────────────────────────┤ RX  │
└─────┘    1 wire (+ ground)     └─────┘
  Slower but cheap, long distance
```

### 8.2 Synchronous Communication

**Concept**: Clock signal synchronizes transmitter and receiver

```
┌─────┐   Data  ────────────────┐   ┌─────┐
│ TX  │   Clock ────────────────┤   │ RX  │
└─────┘                          └   └─────┘

Clock:  ↑ ↓ ↑ ↓ ↑ ↓ ↑ ↓
Data:   1 0 1 1 0 1 0 0
        │ │ │ │ │ │ │ │
        Sample at clock edge
```

**Characteristics:**
- **Separate clock line** required
- **High speed** (no overhead)
- **Short distance** (clock skew)
- **Examples**: SPI, I2C

**Frame Format:**
```
┌──────┬──────────────┬──────┐
│ Sync │     Data     │ CRC  │
└──────┴──────────────┴──────┘
  Sync: Synchronization pattern
  Data: Payload (no gaps)
  CRC: Error check
```

### 8.3 Asynchronous Communication

**Concept**: No shared clock, each byte has start/stop bits

```
Idle ──┐     ┌────────────────────────┐
       │     │                        │
       └─────┘  Data Bits    ──────────  Idle
       Start               Stop
       bit (0)             bit (1)
```

**Frame Format:**
```
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬────┐
│ S │ D0│ D1│ D2│ D3│ D4│ D5│ D6│ D7│ St │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴────┘
  S: Start bit (0)
  D0-D7: Data bits (LSB first)
  St: Stop bit (1)
  
Optional: Parity bit between D7 and St
```

**Example: Send 'A' (0x41 = 01000001)**

```
Idle (1) ──┐     ┌─┐ ┌─────┐ ┌─┐ ┌─────────── Idle (1)
           │     │ │ │     │ │ │ │
           └─────┘ └─┘     └─┘ └─┘
           Start 1 0 0 0 0 0 1 0 Stop
           bit   └───────────────┘ bit
                   'A' = 01000001
                   (LSB first: 10000010)
```

**Characteristics:**
- **No clock line** needed
- **Lower speed** (20% overhead)
- **Any distance** (self-clocking)
- **Examples**: RS-232, UART

**Baud Rate**: Symbols (bits) per second
```
Example: 9600 baud
  - 9600 bits/sec
  - With 8N1 (8 data, no parity, 1 stop):
    • 10 bits per byte (1 start + 8 data + 1 stop)
    • 960 bytes/sec effective
```

### Synchronous vs Asynchronous

| Feature | Synchronous | Asynchronous |
|---------|-------------|--------------|
| **Clock** | Shared | No shared clock |
| **Speed** | High | Lower |
| **Overhead** | Low (no start/stop) | High (start/stop bits) |
| **Distance** | Short | Any |
| **Cost** | Higher (extra wire) | Lower |
| **Complexity** | Higher | Lower |
| **Examples** | SPI, I2C | RS-232, UART |

---

## 9. Standard Communication Interfaces

### 9.1 RS-232 (Serial Port)

```
9-pin D-Sub Connector:
Pin 1: DCD (Data Carrier Detect)
Pin 2: RXD (Receive Data)
Pin 3: TXD (Transmit Data)
Pin 4: DTR (Data Terminal Ready)
Pin 5: GND (Ground)
Pin 6: DSR (Data Set Ready)
Pin 7: RTS (Request To Send)
Pin 8: CTS (Clear To Send)
Pin 9: RI (Ring Indicator)
```

**Characteristics:**
- **Asynchronous** serial
- **Point-to-point** (one-to-one)
- **Distance**: Up to 50 feet
- **Speed**: Up to 115.2 Kbps
- **Voltage**: ±12V
- **Used for**: Modems, terminals

### 9.2 USB (Universal Serial Bus)

```
USB Connector Types:
- Type-A: Host (Computer)
- Type-B: Device (Printer)
- Mini/Micro: Mobile devices
- Type-C: Reversible, modern

USB Versions:
USB 1.1: 12 Mbps
USB 2.0: 480 Mbps
USB 3.0: 5 Gbps
USB 3.1: 10 Gbps
USB 4.0: 40 Gbps
```

**Characteristics:**
- **Serial** interface
- **Hot-pluggable**
- **Power delivery** (5V)
- **Up to 127 devices** (with hubs)
- **Automatic configuration** (plug and play)

**USB Tree Structure:**
```
        Computer (Root Hub)
              │
     ┌────────┼────────┐
     │        │        │
   Mouse  Keyboard   Hub
                      │
                 ┌────┼────┐
                 │         │
              Printer   Scanner
```

### 9.3 Ethernet

```
Speed Variants:
- 10 Mbps (10BASE-T)
- 100 Mbps (Fast Ethernet)
- 1 Gbps (Gigabit Ethernet)
- 10 Gbps (10 Gigabit Ethernet)

RJ-45 Connector (8 pins):
Pin 1: TX+ (Transmit +)
Pin 2: TX- (Transmit -)
Pin 3: RX+ (Receive +)
Pin 4: Unused
Pin 5: Unused
Pin 6: RX- (Receive -)
Pin 7: Unused
Pin 8: Unused
```

**Characteristics:**
- **Packet-based** communication
- **CSMA/CD** protocol (Carrier Sense Multiple Access / Collision Detection)
- **Distance**: Up to 100m (copper), km (fiber)

### 9.4 PCIe (Peripheral Component Interconnect Express)

```
PCIe Lanes:
x1: 1 lane (250 MB/s per direction)
x4: 4 lanes (1 GB/s per direction)
x16: 16 lanes (4 GB/s per direction)

Generations:
PCIe 1.0: 250 MB/s per lane
PCIe 2.0: 500 MB/s per lane
PCIe 3.0: 1 GB/s per lane
PCIe 4.0: 2 GB/s per lane
PCIe 5.0: 4 GB/s per lane
```

**Characteristics:**
- **Serial**, **point-to-point**
- **Full-duplex**
- **Used for**: Graphics cards, SSDs, network cards

### 9.5 SATA (Serial ATA)

```
SATA Versions:
SATA I:   1.5 Gbps (150 MB/s)
SATA II:  3.0 Gbps (300 MB/s)
SATA III: 6.0 Gbps (600 MB/s)

Connector: 7-pin data + 15-pin power
```

**Characteristics:**
- **Serial** interface (replaced parallel ATA)
- **Hot-pluggable**
- **Used for**: HDDs, SSDs, optical drives

### Interface Comparison

| Interface | Speed | Distance | Type | Use Case |
|-----------|-------|----------|------|----------|
| **RS-232** | 115 Kbps | 50 ft | Serial | Legacy devices |
| **USB 3.0** | 5 Gbps | 3 m | Serial | Peripherals |
| **Ethernet** | 1 Gbps | 100 m | Packet | Networking |
| **PCIe 3.0 x16** | 16 GB/s | Inches | Serial | Graphics cards |
| **SATA III** | 6 Gbps | 1 m | Serial | Storage |

---

## 🚀 Quick Reference Summary

### I/O Interface Functions
- Data buffering
- Format conversion
- Timing control
- Error detection
- Device selection

### Data Transfer Modes
- **Programmed I/O**: CPU polls device (slow, simple)
- **Interrupt I/O**: Device interrupts CPU (medium, efficient)
- **DMA**: Direct memory access (fast, complex)

### Interrupts
- **Hardware**: External (I/O), Internal (Timer)
- **Software**: Faults, Traps, Aborts
- **Priority**: Higher priority can interrupt lower
- **Masking**: Enable/disable specific interrupts

### Serial Communication
- **Synchronous**: Shared clock, fast, short distance
- **Asynchronous**: No clock, slower, any distance

### Standard Interfaces
- **RS-232**: 115 Kbps, legacy
- **USB**: 5-40 Gbps, plug-and-play
- **Ethernet**: 1-10 Gbps, networking
- **PCIe**: 16 GB/s, internal
- **SATA**: 6 Gbps, storage

---

## 📝 Exam Important Questions

1. **Explain** I/O interface and its functions.

2. **Compare** memory-mapped I/O and isolated I/O.

3. **Describe** interrupt mechanism with example.

4. **Explain** interrupt priority and masking.

5. **Compare** three modes of data transfer:
   - Programmed I/O
   - Interrupt-initiated I/O
   - DMA

6. **Explain** DMA operation with diagram.

7. **Compare** synchronous and asynchronous communication.

8. **Describe** RS-232 serial communication standard.

9. **Explain** USB interface characteristics and versions.

10. **Describe** I/O channels and processors with types.

---

*End of Unit-5*

*All COA Units Complete! 🎉*
