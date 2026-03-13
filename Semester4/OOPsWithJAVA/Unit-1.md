# 🟣 ZenYukti
### Smart Notes for Serious Students
> 🌐 [zenyukti.in](https://zenyukti.in)

---

# ☕ Java — Exam Notes (1-Hour Prep)
> **Unit: Introduction, OOP, Packages**

---

## 1. Why Java?

- **Platform independent** — Write Once, Run Anywhere (WORA)
- **Object-Oriented** — everything is a class/object
- **Secure, Robust, Multithreaded**
- **Automatic memory management** (Garbage Collection)
- **Strongly typed** — strict type checking at compile time

---

## 2. History of Java

| Year | Event |
|------|-------|
| 1991 | Started as **Project Green** by James Gosling at Sun Microsystems |
| 1995 | Officially released as **Java 1.0** |
| 1996 | JDK 1.0 released |
| 2009 | Sun Microsystems acquired by **Oracle** |
| Now | Maintained by Oracle; latest versions release every 6 months |

- Original name: **Oak** → renamed to **Java**
- Designed for **consumer electronics**, later for internet

---

## 3. JVM, JRE, JDK

```
┌────────────────────────────────┐
│  JDK (Java Development Kit)    │  ← for developers (compile + run)
│  ┌──────────────────────────┐  │
│  │  JRE (Java Runtime Env)  │  │  ← for running Java programs
│  │  ┌────────────────────┐  │  │
│  │  │  JVM (Java VM)     │  │  │  ← executes bytecode
│  │  └────────────────────┘  │  │
│  └──────────────────────────┘  │
└────────────────────────────────┘
```

- **JVM** — Converts **bytecode → machine code**; platform-specific; provides memory management, garbage collection
- **JRE** — JVM + core libraries; needed to **run** Java programs
- **JDK** — JRE + compiler (javac) + tools; needed to **develop** Java programs

---

## 4. Java Environment & Compilation

### Compilation Process
```
Source Code (.java)
      ↓ javac (compiler)
  Bytecode (.class)
      ↓ JVM (java command)
  Machine Code (execution)
```

- `javac Hello.java` → compiles → `Hello.class`
- `java Hello` → runs the bytecode via JVM

### Java Source File Structure
```java
package mypackage;              // 1. Package declaration (optional)

import java.util.Scanner;       // 2. Import statements

public class Hello {            // 3. Class definition
    public static void main(String[] args) {  // 4. main method
        System.out.println("Hello World");
    }
}
```

**Rules:**
- File name = **public class name** (e.g., `Hello.java`)
- Only **one public class** per file
- `main()` is the entry point

---

## 5. Data Types

### Primitive Types
| Type | Size | Example |
|------|------|---------|
| `byte` | 1 byte | -128 to 127 |
| `short` | 2 bytes | -32768 to 32767 |
| `int` | 4 bytes | Default integer |
| `long` | 8 bytes | Large integers |
| `float` | 4 bytes | 3.14f |
| `double` | 8 bytes | 3.14159 (default decimal) |
| `char` | 2 bytes | 'A' (Unicode) |
| `boolean` | 1 bit | true / false |

### Non-Primitive (Reference Types)
- **String, Arrays, Classes, Interfaces**

---

## 6. Variables

- **Local** — inside method; no default value; must initialize before use
- **Instance** — inside class, outside method; default values (0, null, false)
- **Static** — belongs to class, shared by all objects; declared with `static`

```java
class Demo {
    int x = 10;           // instance variable
    static int y = 20;    // static variable
    void method() {
        int z = 30;       // local variable
    }
}
```

---

## 7. Operators

| Type | Operators |
|------|-----------|
| Arithmetic | `+ - * / %` |
| Relational | `== != > < >= <=` |
| Logical | `&& \|\| !` |
| Assignment | `= += -= *= /=` |
| Bitwise | `& \| ^ ~ << >>` |
| Ternary | `condition ? val1 : val2` |
| Increment/Decrement | `++ --` |

---

## 8. Control Flow

```java
// if-else
if (x > 0) { } else if (x < 0) { } else { }

// switch
switch(x) { case 1: break; default: }

// for loop
for (int i = 0; i < 10; i++) { }

// while
while (condition) { }

// do-while
do { } while (condition);

// for-each
for (int item : array) { }

// break / continue / return
```

---

## 9. Arrays

```java
int[] arr = new int[5];              // declaration
int[] arr = {1, 2, 3, 4, 5};        // initialization
arr[0] = 10;                         // access
arr.length                           // size

// 2D Array
int[][] matrix = new int[3][3];
```

- Arrays are **objects** in Java
- Index starts at **0**
- Fixed size once created

---

## 10. String

```java
String s = "Hello";
String s2 = new String("Hello");

// Common Methods
s.length()           // length
s.charAt(0)          // character at index
s.substring(1, 3)    // substring
s.toUpperCase()      // uppercase
s.toLowerCase()      // lowercase
s.equals("Hello")    // compare (use this, not ==)
s.contains("ell")    // contains check
s.replace("l","r")   // replace
s.trim()             // remove spaces
s.split(",")         // split into array
```

- **Strings are immutable** in Java
- `==` compares references; `.equals()` compares content
- `StringBuilder` / `StringBuffer` — mutable string alternatives

---

## 11. Defining Classes & Objects

```java
class Student {
    // fields
    String name;
    int age;

    // constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // method
    void display() {
        System.out.println(name + " " + age);
    }
}

// Creating Object
Student s = new Student("Alice", 20);
s.display();
```

- **Class** = blueprint/template
- **Object** = instance of a class
- `new` keyword allocates memory and calls constructor

---

## 12. Constructors

- Special method to **initialize objects**
- Same name as class, **no return type**
- Called automatically when object is created

```java
class Box {
    int w, h;
    Box() { w = 0; h = 0; }          // default constructor
    Box(int w, int h) {               // parameterized constructor
        this.w = w; this.h = h;
    }
    Box(Box b) {                      // copy constructor
        this.w = b.w; this.h = b.h;
    }
}
```

- If no constructor defined → Java provides **default constructor**
- `this` refers to current object
- **Constructor Overloading** — multiple constructors with different parameters

---

## 13. Access Specifiers

| Modifier | Same Class | Same Package | Subclass | Other |
|----------|-----------|--------------|----------|-------|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `default` (no modifier) | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

---

## 14. Static Members

- `static` members belong to the **class**, not to any object
- Shared across all instances
- Accessed via class name: `ClassName.member`

```java
class Counter {
    static int count = 0;     // static variable
    Counter() { count++; }

    static void show() {      // static method
        System.out.println(count);
    }
}
Counter.show();  // call without object
```

- `static` methods **cannot** use `this` or access instance variables directly

---

## 15. Final Members

| Usage | Meaning |
|-------|---------|
| `final variable` | Value cannot be changed (constant) |
| `final method` | Cannot be overridden in subclass |
| `final class` | Cannot be extended (no subclass) |

```java
final int MAX = 100;          // constant
final class MathUtils { }     // cannot extend
```

---

## 16. Comments

```java
// Single line comment

/* Multi-line
   comment */

/** Javadoc comment
 *  @param x the input
 *  @return result
 */
```

---

---

# OBJECT ORIENTED PROGRAMMING

---

## 17. Inheritance

- A **subclass** inherits fields and methods from a **superclass**
- Use `extends` keyword
- Promotes **code reuse**
- Java supports **single inheritance** (one parent only); multiple via interfaces

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}

Dog d = new Dog();
d.eat();   // inherited
d.bark();  // own method
```

### Types of Inheritance in Java
- **Single** — A extends B
- **Multilevel** — A extends B extends C
- **Hierarchical** — B and C both extend A
- ❌ **Multiple** — NOT supported via classes (use interfaces)

### `super` keyword
- `super.method()` — call parent class method
- `super(args)` — call parent constructor

---

## 18. Method Overriding

- **Subclass provides its own implementation** of a method already in superclass
- Same method name, same parameters, same return type
- Enables **runtime polymorphism**
- Use `@Override` annotation (optional but recommended)

```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Cat extends Animal {
    @Override
    void sound() { System.out.println("Meow"); }
}
```

---

## 19. Method Overloading

- **Same method name, different parameters** (number, type, or order)
- In the **same class**
- Resolved at **compile time** (static polymorphism)

```java
class Math {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}
```

### Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|------------|------------|
| Class | Same class | Parent-child |
| Parameters | Different | Same |
| Return type | Can differ | Must be same (or covariant) |
| Resolved at | Compile time | Runtime |
| Type | Static polymorphism | Dynamic polymorphism |

---

## 20. Encapsulation

- **Wrapping data (fields) and methods in one unit (class)**
- Hide internal data using `private`; expose via `public` getters/setters
- Also called **data hiding**

```java
class Account {
    private double balance;          // hidden

    public double getBalance() {     // getter
        return balance;
    }
    public void setBalance(double b) { // setter
        if (b >= 0) balance = b;
    }
}
```

- Benefits: Security, control over data, flexibility to change internal implementation

---

## 21. Polymorphism

- **Same interface, different behavior**
- Two types:
  - **Compile-time (Static)** — Method Overloading
  - **Runtime (Dynamic)** — Method Overriding via parent reference

```java
Animal a = new Dog();   // parent reference → child object
a.sound();              // calls Dog's sound() at runtime
```

- **Dynamic Method Dispatch** — runtime decides which overridden method to call based on actual object type

---

## 22. Abstraction

- **Hiding implementation details, showing only essential features**
- Achieved via:
  - **Abstract classes**
  - **Interfaces**

---

## 23. Abstract Class

- Declared with `abstract` keyword
- **Cannot be instantiated** (no objects directly)
- Can have both **abstract methods** (no body) and **concrete methods** (with body)
- Subclass **must implement** all abstract methods (or be abstract itself)

```java
abstract class Shape {
    abstract double area();         // abstract method
    void display() {                // concrete method
        System.out.println("Shape");
    }
}

class Circle extends Shape {
    double r;
    Circle(double r) { this.r = r; }
    double area() { return 3.14 * r * r; }  // must implement
}
```

---

## 24. Interface

- A **fully abstract contract** — only abstract methods (pre-Java 8)
- Java 8+: can have `default` and `static` methods
- Implemented using `implements` keyword
- A class can implement **multiple interfaces** (solves multiple inheritance)
- All interface variables are `public static final` by default
- All interface methods are `public abstract` by default

```java
interface Drawable {
    void draw();              // implicitly public abstract
}
interface Colorable {
    void color();
}

class Circle implements Drawable, Colorable {
    public void draw() { System.out.println("Drawing"); }
    public void color() { System.out.println("Coloring"); }
}
```

### Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Abstract + Concrete | Abstract (+ default, static from Java 8) |
| Variables | Any type | `public static final` only |
| Constructor | ✅ Yes | ❌ No |
| Multiple inheritance | ❌ No | ✅ Yes |
| Use `extends` / `implements` | `extends` | `implements` |
| When to use | Shared base code | Define contract/capability |

---

---

# PACKAGES

---

## 25. Defining a Package

- **Package** = a namespace that organizes related classes/interfaces
- Declared at the **top of the source file** (first statement)
- Corresponds to a **directory structure** on disk

```java
package com.zenyukti.utils;    // package declaration

public class MathHelper {
    public int add(int a, int b) { return a + b; }
}
```

- Package naming convention: **reverse domain name** → `com.companyname.project`

---

## 26. CLASSPATH Setting

- **CLASSPATH** = tells JVM where to look for `.class` files
- Set via environment variable or `-cp` flag

```bash
# Set CLASSPATH environment variable
set CLASSPATH=C:\myproject\classes;.     # Windows
export CLASSPATH=/home/user/classes:.    # Linux/Mac

# Or use -cp flag at runtime
java -cp /path/to/classes MyClass
```

- `.` (dot) in CLASSPATH = current directory
- For packages, CLASSPATH should point to the **root** of the package hierarchy

---

## 27. Making JAR Files

- **JAR (Java ARchive)** = zips `.class` files into one portable file
- Used to distribute library packages

```bash
# Create JAR
jar cf mylib.jar com/zenyukti/utils/*.class

# Run JAR
java -jar myapp.jar

# View JAR contents
jar tf mylib.jar
```

- `c` = create, `f` = file, `t` = list, `x` = extract
- JAR includes a **MANIFEST.MF** file with metadata (e.g., main class)

---

## 28. Import & Static Import

### Import
```java
import java.util.Scanner;         // import specific class
import java.util.*;               // import all classes in package
```

### Static Import
```java
import static java.lang.Math.PI;
import static java.lang.Math.*;   // import all static members

// Now use directly without class name
double area = PI * r * r;         // instead of Math.PI
System.out.println(sqrt(16));     // instead of Math.sqrt(16)
```

- `java.lang` package is **auto-imported** (no need to import String, System, Math, etc.)

---

## 29. Naming Conventions for Packages

| Element | Convention | Example |
|---------|-----------|---------|
| **Package** | All lowercase | `com.zenyukti.app` |
| **Class** | PascalCase | `StudentManager` |
| **Method/Variable** | camelCase | `getStudentName()` |
| **Constant** | UPPER_SNAKE_CASE | `MAX_VALUE` |
| **Interface** | PascalCase | `Serializable` |

- Package name = reverse domain + project name: `com.google.maps`
- Use meaningful, short names — avoid underscores in package names

---

## 30. Built-in Packages (Know These)

| Package | Contains |
|---------|---------|
| `java.lang` | String, Math, Object, System (auto-imported) |
| `java.util` | Scanner, ArrayList, HashMap, Collections |
| `java.io` | File, InputStream, OutputStream |
| `java.net` | Socket, URL (networking) |
| `java.awt` | GUI components |
| `javax.swing` | Advanced GUI |

---

## 31. Quick Cheatsheet

| Concept | Key Point |
|---------|----------|
| **JVM** | Runs bytecode; platform-specific |
| **JRE** | JVM + libraries; for running |
| **JDK** | JRE + compiler; for developing |
| **Constructor** | Same name as class, no return type |
| **this** | Current object reference |
| **super** | Parent class reference |
| **static** | Belongs to class, not object |
| **final** | Variable=constant, method=no override, class=no extend |
| **abstract** | Must be overridden; class can't be instantiated |
| **interface** | Contract; supports multiple implementation |
| **Overloading** | Same name, different params → compile time |
| **Overriding** | Same name, same params → runtime |
| **Encapsulation** | private fields + public getters/setters |
| **Polymorphism** | One interface, many forms |
| **Package** | Namespace; reverse domain naming |
| **JAR** | Archive of .class files |
| **CLASSPATH** | Tells JVM where to find .class files |

---

> 💡 **Last-minute tips:**
> - JDK ⊃ JRE ⊃ JVM — remember the nesting
> - `.java` → `javac` → `.class` (bytecode) → `java` → output
> - `==` checks reference | `.equals()` checks content (for Strings!)
> - Overloading = same class, diff params | Overriding = subclass, same params
> - Interface: multiple implements allowed | Abstract class: single extends
> - `final class` can't be extended | `abstract class` can't be instantiated
> - Package naming: all lowercase, reverse domain (com.company.project)
> - `java.lang` is auto-imported — no need to import String, Math, System
> - Static members: call with class name, not object name
> - `super()` must be first statement in subclass constructor

---

---

**🟣 ZenYukti** | *Empowering learners with smart, structured study resources.*

🌐 [zenyukti.in](https://zenyukti.in)

© 2026 ZenYukti. All rights reserved. This material is intended for personal educational use only. Unauthorized reproduction or distribution is prohibited.