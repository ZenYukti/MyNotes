# 🟣 ZenYukti
### Smart Notes for Serious Students
> 🌐 [zenyukti.in](https://zenyukti.in)

---

# ☕ Java — Exception Handling, I/O & Multithreading
> **Last-Minute Exam Notes**

---

# EXCEPTION HANDLING

---

## 1. The Idea Behind Exception

- **Exception** = an unexpected event that **disrupts normal program flow** at runtime
- Without handling → program **crashes abruptly**
- Java provides structured way to handle errors gracefully
- Example: dividing by zero, accessing null object, file not found

---

## 2. Exceptions vs Errors

| | Exception | Error |
|-|-----------|-------|
| **Cause** | Program logic / external factors | JVM / system level |
| **Recoverable?** | ✅ Yes | ❌ No |
| **Examples** | NullPointerException, IOException | OutOfMemoryError, StackOverflowError |
| **Should handle?** | Yes | Generally no |

- Both `Exception` and `Error` extend **`Throwable`**

```
Throwable
├── Error           (StackOverflowError, OutOfMemoryError)
└── Exception
    ├── Checked     (IOException, SQLException)
    └── Unchecked / RuntimeException
                    (NullPointerException, ArithmeticException)
```

---

## 3. Types of Exceptions

### Checked Exceptions
- Checked at **compile time**
- Must be handled (try-catch) or declared (throws)
- Examples: `IOException`, `FileNotFoundException`, `SQLException`, `ClassNotFoundException`

### Unchecked Exceptions (RuntimeException)
- Checked at **runtime**
- Don't need to be declared or caught (but can be)
- Examples: `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`, `ClassCastException`, `NumberFormatException`

---

## 4. Control Flow in Exceptions

```java
try {
    // risky code
    int x = 10 / 0;       // throws ArithmeticException
    System.out.println("This won't print");
} catch (ArithmeticException e) {
    System.out.println("Caught: " + e.getMessage());
} finally {
    System.out.println("Always executes");
}
```

**Flow:**
- Exception thrown → JVM looks for matching `catch` block
- If found → executes `catch` → then `finally`
- If not found → propagates up the call stack
- `finally` **always executes** (even if no exception, even with return)

---

## 5. JVM Reaction to Exceptions

When exception occurs and **not caught:**
1. JVM creates an **exception object** with message, type, stack trace
2. JVM searches call stack for a matching handler (catch block)
3. If found → handler executes
4. If **not found anywhere** → JVM calls **default exception handler**
   - Prints exception type, message, and stack trace
   - **Terminates the program**

---

## 6. try, catch, finally, throw, throws

### try
- Block of code that **might throw** an exception

### catch
- Catches a specific exception type
- Multiple catch blocks allowed (specific → general order)

```java
try { ... }
catch (FileNotFoundException e) { ... }   // specific first
catch (IOException e) { ... }
catch (Exception e) { ... }               // general last
```

### finally
- Always executes — used for **cleanup** (close files, DB connections)
- Runs even if: no exception | exception caught | exception not caught | `return` in try

```java
finally {
    file.close();   // cleanup code
}
```

### throw
- **Manually throw** an exception
- `throw new ExceptionType("message");`

```java
if (age < 0) throw new IllegalArgumentException("Age can't be negative");
```

### throws
- Declares that a method **may throw** an exception (caller must handle)
- Used in method signature

```java
void readFile() throws IOException {
    // method might throw IOException
}
```

### throw vs throws

| | `throw` | `throws` |
|-|---------|---------|
| Purpose | Actually throw an exception | Declare possible exception |
| Location | Inside method body | Method signature |
| Followed by | Exception object | Exception class name(s) |
| Example | `throw new IOException()` | `void m() throws IOException` |

---

## 7. Multi-catch (Java 7+)

```java
catch (IOException | SQLException e) {
    System.out.println("Caught: " + e);
}
```

---

## 8. In-built Exceptions

| Exception | Cause |
|-----------|-------|
| `ArithmeticException` | Division by zero |
| `NullPointerException` | Using null reference |
| `ArrayIndexOutOfBoundsException` | Invalid array index |
| `ClassCastException` | Invalid type cast |
| `NumberFormatException` | Invalid string-to-number conversion |
| `StackOverflowError` | Infinite recursion |
| `IOException` | I/O failure |
| `FileNotFoundException` | File not found |
| `IllegalArgumentException` | Invalid argument passed |

---

## 9. User-Defined Exceptions

- Extend `Exception` (checked) or `RuntimeException` (unchecked)

```java
class InsufficientFundsException extends Exception {
    InsufficientFundsException(String msg) {
        super(msg);           // pass message to parent
    }
}

class Bank {
    void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance)
            throw new InsufficientFundsException("Not enough funds");
    }
}
```

---

## 10. Checked vs Unchecked — Summary

| | Checked | Unchecked |
|-|---------|-----------|
| Detected at | Compile time | Runtime |
| Must handle? | ✅ Yes | ❌ No (optional) |
| Extends | `Exception` | `RuntimeException` |
| Examples | IOException, SQLException | NullPointerException, ArithmeticException |

---

---

# INPUT / OUTPUT BASICS

---

## 11. Java I/O Overview

- All I/O is in **`java.io`** package
- Two main types of streams:

```
Streams
├── Byte Streams    → read/write raw bytes (binary data, images)
└── Character Streams → read/write characters (text files, Unicode)
```

---

## 12. Byte Streams

- Handle **8-bit bytes** — for binary files (images, audio, etc.)
- Base classes:
  - **`InputStream`** — reading bytes
  - **`OutputStream`** — writing bytes

| Class | Purpose |
|-------|---------|
| `FileInputStream` | Read bytes from file |
| `FileOutputStream` | Write bytes to file |
| `BufferedInputStream` | Buffered reading (faster) |
| `BufferedOutputStream` | Buffered writing (faster) |
| `DataInputStream` | Read primitive types |
| `DataOutputStream` | Write primitive types |

```java
// Reading a file byte by byte
FileInputStream fis = new FileInputStream("file.txt");
int ch;
while ((ch = fis.read()) != -1) {
    System.out.print((char) ch);
}
fis.close();

// Writing bytes to file
FileOutputStream fos = new FileOutputStream("output.txt");
fos.write("Hello".getBytes());
fos.close();
```

---

## 13. Character Streams

- Handle **16-bit Unicode characters** — for text files
- Base classes:
  - **`Reader`** — reading characters
  - **`Writer`** — writing characters

| Class | Purpose |
|-------|---------|
| `FileReader` | Read characters from file |
| `FileWriter` | Write characters to file |
| `BufferedReader` | Buffered reading (line by line) |
| `BufferedWriter` | Buffered writing |
| `PrintWriter` | Formatted text output |

```java
// Reading text file line by line
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
String line;
while ((line = br.readLine()) != null) {
    System.out.println(line);
}
br.close();

// Writing text to file
BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"));
bw.write("Hello World");
bw.newLine();
bw.close();
```

---

## 14. Byte Streams vs Character Streams

| | Byte Stream | Character Stream |
|-|------------|-----------------|
| Unit | 8-bit byte | 16-bit char (Unicode) |
| Base classes | InputStream / OutputStream | Reader / Writer |
| Best for | Binary files (images, audio) | Text files |
| Example classes | FileInputStream, FileOutputStream | FileReader, FileWriter |

---

## 15. try-with-resources (Java 7+)

- Auto-closes streams — no need for explicit `close()`

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null)
        System.out.println(line);
}  // br.close() called automatically
```

---

---

# MULTITHREADING

---

## 16. What is a Thread?

- **Thread** = smallest unit of execution within a process
- **Multithreading** = multiple threads running concurrently in one program
- Each thread has its own: **stack, PC register, local variables**
- All threads share: **heap memory, static fields, code**
- Benefits: better CPU use, responsive UI, parallel tasks

---

## 17. Thread Life Cycle

```
  [NEW] ──start()──→ [RUNNABLE] ──scheduler──→ [RUNNING]
                          ↑                         │
                          │              sleep/wait/I/O
                     notify/I/O done                ↓
                          └──────────── [WAITING/BLOCKED]
                                                    │
                                            run() completes
                                                    ↓
                                             [TERMINATED]
```

**States:**
- **New** — thread object created, not started
- **Runnable** — `start()` called, ready to run (waiting for CPU)
- **Running** — actually executing
- **Blocked/Waiting** — waiting for lock, I/O, or `sleep()`
- **Terminated** — `run()` completed or exception thrown

---

## 18. Creating Threads — Two Ways

### Way 1: Extend `Thread` class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + getName());
    }
}

MyThread t = new MyThread();
t.start();    // don't call run() directly — call start()
```

### Way 2: Implement `Runnable` interface ⭐ (preferred)

```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task running");
    }
}

Thread t = new Thread(new MyTask());
t.start();

// Lambda (Java 8+)
Thread t2 = new Thread(() -> System.out.println("Lambda thread"));
t2.start();
```

### Extend Thread vs Implement Runnable

| | Extend Thread | Implement Runnable |
|-|--------------|-------------------|
| Inheritance | Can't extend any other class | Can extend another class |
| Reusability | Lower | Higher |
| Preferred? | ❌ No | ✅ Yes |

---

## 19. Common Thread Methods

| Method | Description |
|--------|-------------|
| `start()` | Starts thread (calls run() internally) |
| `run()` | Thread's task — override this |
| `sleep(ms)` | Pause thread for ms milliseconds |
| `join()` | Wait for this thread to finish |
| `isAlive()` | Check if thread is still running |
| `getName()` | Get thread name |
| `setName(name)` | Set thread name |
| `currentThread()` | Get reference to currently running thread |
| `yield()` | Hint to scheduler to let other threads run |

---

## 20. Thread Priorities

- Priority range: **1 (MIN) to 10 (MAX)**, default = **5 (NORM)**
- Higher priority = more likely to get CPU (not guaranteed)

```java
Thread t = new Thread(task);
t.setPriority(Thread.MAX_PRIORITY);   // 10
t.setPriority(Thread.MIN_PRIORITY);   // 1
t.setPriority(Thread.NORM_PRIORITY);  // 5
int p = t.getPriority();
```

- Priority is a **hint** to scheduler — actual behavior is JVM/OS dependent

---

## 21. Synchronizing Threads

### Why Synchronization?
- Multiple threads accessing **shared resource** → **Race Condition**
- Race condition = unpredictable results due to interleaved execution
- Solution: **Synchronization** — only one thread at a time accesses critical section

### `synchronized` keyword

```java
// Synchronized method
class Counter {
    int count = 0;
    synchronized void increment() {
        count++;     // only one thread at a time
    }
}

// Synchronized block (more fine-grained)
void method() {
    synchronized(this) {
        // critical section
        count++;
    }
}
```

- **Monitor/Lock** — every object has a lock; `synchronized` acquires it
- Only **one thread** can hold a lock at a time — others wait
- `synchronized` method → locks the **object** (`this`)
- `synchronized static` method → locks the **class**

---

## 22. Inter-thread Communication

- Threads can **coordinate** using wait/notify — avoids busy waiting
- Must be called inside a `synchronized` block

| Method | Description |
|--------|-------------|
| `wait()` | Releases lock and waits until notified |
| `notify()` | Wakes up **one** waiting thread |
| `notifyAll()` | Wakes up **all** waiting threads |

```java
class SharedBuffer {
    int data;
    boolean hasData = false;

    synchronized void produce(int val) throws InterruptedException {
        while (hasData) wait();       // wait if buffer full
        data = val;
        hasData = true;
        notify();                     // wake up consumer
    }

    synchronized int consume() throws InterruptedException {
        while (!hasData) wait();      // wait if buffer empty
        hasData = false;
        notify();                     // wake up producer
        return data;
    }
}
```

- Classic example: **Producer-Consumer problem**
- `wait()` releases the lock; `notify()` does not immediately release

---

## 23. Deadlock in Threads

- Two threads each **holding a lock** and waiting for the other's lock
- Prevention: always acquire locks in the **same order**

```java
// Thread 1: locks A then B
// Thread 2: locks B then A → DEADLOCK
```

---

## 24. Quick Cheatsheet

| Term | Key Point |
|------|----------|
| **Exception** | Disrupts normal flow; recoverable |
| **Error** | JVM-level; not recoverable |
| **Checked** | Must handle at compile time (IOException) |
| **Unchecked** | Runtime exceptions (NullPointerException) |
| **try** | Wraps risky code |
| **catch** | Handles specific exception |
| **finally** | Always executes; used for cleanup |
| **throw** | Manually throw an exception (inside method) |
| **throws** | Declare exception in method signature |
| **Byte Stream** | 8-bit; binary files; InputStream/OutputStream |
| **Character Stream** | 16-bit; text files; Reader/Writer |
| **BufferedReader** | Read text file line by line |
| **Thread** | Lightweight unit of execution |
| **start()** | Launch thread (don't call run() directly!) |
| **sleep()** | Pause thread temporarily |
| **synchronized** | One thread at a time; prevents race condition |
| **wait()** | Release lock and wait |
| **notify()** | Wake one waiting thread |
| **Race Condition** | Multiple threads corrupting shared data |

---

> 💡 **Last-minute tips:**
> - `throw` = inside body | `throws` = in signature — don't confuse!
> - `finally` always runs — even if return in try
> - Checked = compile time = must handle | Unchecked = runtime = optional
> - Call `start()` NOT `run()` — calling run() directly doesn't create a new thread!
> - Runnable > extending Thread (allows extending other classes)
> - `wait()`, `notify()`, `notifyAll()` must be inside `synchronized` block
> - BufferedReader + FileReader = fastest way to read text file line by line
> - try-with-resources auto-closes streams (cleaner code)
> - Thread priority is a hint — JVM/OS may not strictly follow it
> - Race condition → use synchronized | Waiting for condition → use wait/notify

---

---

**🟣 ZenYukti** | *Empowering learners with smart, structured study resources.*

🌐 [zenyukti.in](https://zenyukti.in)

© 2026 ZenYukti. All rights reserved. This material is intended for personal educational use only. Unauthorized reproduction or distribution is prohibited.