# Java New Features — Exam Notes

---

## 1. Functional Interface

An interface with **exactly one abstract method** (SAM — Single Abstract Method).  
Annotated with `@FunctionalInterface`. Used as the basis for lambda expressions.

```java
@FunctionalInterface
interface Greet {
    void sayHello(String name);
}
```

**Built-in Functional Interfaces (java.util.function):**

| Interface | Method | Use |
|---|---|---|
| `Predicate<T>` | `test(T)` → boolean | Condition check |
| `Function<T,R>` | `apply(T)` → R | Transform input |
| `Consumer<T>` | `accept(T)` → void | Consume input |
| `Supplier<T>` | `get()` → T | Supply value |
| `BiFunction<T,U,R>` | `apply(T,U)` → R | Two inputs |

---

## 2. Lambda Expression

A **short anonymous function**. Implements a functional interface.

```
(parameters) -> expression
(parameters) -> { statements; }
```

```java
// Without lambda
Runnable r = new Runnable() {
    public void run() { System.out.println("Hi"); }
};

// With lambda
Runnable r = () -> System.out.println("Hi");

// With parameters
Greet g = name -> System.out.println("Hello " + name);

// Predicate example
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4)); // true
```

---

## 3. Method References

Shorthand for lambdas that **call an existing method**.  
Syntax: `ClassName::methodName`

| Type | Syntax | Example |
|---|---|---|
| Static method | `Class::staticMethod` | `Math::sqrt` |
| Instance method (object) | `obj::method` | `str::toUpperCase` |
| Instance method (type) | `Class::instanceMethod` | `String::toLowerCase` |
| Constructor | `Class::new` | `ArrayList::new` |

```java
List<String> names = Arrays.asList("Alice", "Bob");

// Lambda
names.forEach(n -> System.out.println(n));

// Method Reference (equivalent)
names.forEach(System.out::println);
```

---

## 4. Stream API

Process **collections in a functional pipeline**. Streams are lazy and don't modify source.

```
Source → Intermediate Operations (lazy) → Terminal Operation (triggers execution)
```

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);

int result = nums.stream()
    .filter(n -> n % 2 == 0)     // [2, 4, 6]
    .map(n -> n * n)              // [4, 16, 36]
    .reduce(0, Integer::sum);     // 56

System.out.println(result); // 56
```

**Common Operations:**

| Intermediate | Terminal |
|---|---|
| `filter()` | `collect()` |
| `map()` | `forEach()` |
| `sorted()` | `count()` |
| `distinct()` | `reduce()` |
| `limit()` | `findFirst()` |
| `flatMap()` | `anyMatch()` / `allMatch()` |

```java
// Collect to List
List<String> result = names.stream()
    .filter(n -> n.startsWith("A"))
    .collect(Collectors.toList());
```

---

## 5. Default Methods (Java 8)

Methods with a **body inside an interface**. Allow adding methods to interfaces without breaking existing implementations.

```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle starting...");
    }
}

class Car implements Vehicle {
    // Can override or inherit default start()
}
```

---

## 6. Static Methods in Interface (Java 8)

Interface can have **static utility methods**.

```java
interface MathUtils {
    static int square(int n) { return n * n; }
}

// Call: MathUtils.square(5) → 25
```

> Cannot be overridden by implementing classes.

---

## 7. Base64 Encode & Decode (Java 8)

```java
import java.util.Base64;

String original = "Hello World";

// Encode
String encoded = Base64.getEncoder().encodeToString(original.getBytes());
System.out.println(encoded); // SGVsbG8gV29ybGQ=

// Decode
byte[] decoded = Base64.getDecoder().decode(encoded);
System.out.println(new String(decoded)); // Hello World
```

---

## 8. forEach Method (Java 8)

Iterate collections using lambda or method reference.

```java
List<String> list = Arrays.asList("A", "B", "C");

list.forEach(item -> System.out.println(item));
// OR
list.forEach(System.out::println);

// On Map
Map<String, Integer> map = new HashMap<>();
map.put("x", 1); map.put("y", 2);
map.forEach((k, v) -> System.out.println(k + " = " + v));
```

---

## 9. Try-With-Resources (Java 7+)

Auto-closes resources (files, connections) implementing `AutoCloseable`. No need for `finally`.

```java
// Old way
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
} finally {
    if (br != null) br.close();
}

// Try-with-resources (clean way)
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    System.out.println(br.readLine());
} // br is auto-closed here
```

> Multiple resources: `try (Res1 r1 = ...; Res2 r2 = ...) { }`

---

## 10. Type Annotations (Java 8)

Annotations can now be applied to **any type use**, not just declarations.

```java
@NotNull String name;           // field
List<@NonNull String> list;     // generic type
void method(@NotNull String s)  // parameter
```

---

## 11. Repeating Annotations (Java 8)

Same annotation can be applied **multiple times** to same element using `@Repeatable`.

```java
@Repeatable(Schedules.class)
@interface Schedule {
    String day();
}

@Schedule(day = "Monday")
@Schedule(day = "Friday")
class Meeting { }
```

---

## 12. Java Module System (Java 9)

Introduces **modules** to group packages with explicit dependencies. Configured via `module-info.java`.

```java
// module-info.java
module com.myapp {
    requires java.sql;        // depends on java.sql module
    exports com.myapp.utils;  // exposes this package
}
```

> Benefits: Strong encapsulation, reliable configuration, smaller JDK (jlink).

---

## 13. Diamond Syntax with Anonymous Inner Class (Java 9)

Before Java 9, diamond operator `<>` couldn't be used with anonymous classes.

```java
// Java 8 — had to specify type
Box<String> b = new Box<String>() { };

// Java 9+ — diamond works with anonymous class
Box<String> b = new Box<>() { };
```

---

## 14. Local Variable Type Inference — `var` (Java 10)

Compiler **infers the type** of local variables. Only for local variables with initializer.

```java
var list = new ArrayList<String>(); // inferred as ArrayList<String>
var name = "Java";                  // inferred as String
var num = 42;                       // inferred as int

// In loops
for (var item : list) {
    System.out.println(item);
}
```

> `var` is NOT a keyword — it's a reserved type name. Can't use for fields, params, or return types.

---

## 15. Switch Expressions (Java 14+)

Switch can now **return a value**. Cleaner syntax, no fall-through.

```java
// Old switch statement
int day = 3;
String name;
switch(day) {
    case 1: name = "Mon"; break;
    case 2: name = "Tue"; break;
    default: name = "Other";
}

// New switch expression (Java 14+)
String name = switch(day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    default -> "Other";
};
```

---

## 16. Yield Keyword (Java 14)

Used inside switch blocks to **return a value** from a multi-line case.

```java
int result = switch(day) {
    case 1 -> 10;
    case 2 -> {
        int val = day * 5;
        yield val; // returns value from block
    }
    default -> 0;
};
```

> `yield` is to switch blocks what `return` is to methods.

---

## 17. Text Blocks (Java 15)

Multi-line strings using triple quotes `"""`. Preserves formatting, no escape needed for `"`.

```java
// Old way
String json = "{\n  \"name\": \"Java\",\n  \"version\": 15\n}";

// Text Block
String json = """
        {
          "name": "Java",
          "version": 15
        }
        """;
```

---

## 18. Records (Java 16)

**Immutable data classes** with auto-generated constructor, getters, `equals()`, `hashCode()`, `toString()`.

```java
record Point(int x, int y) { }

// Usage
Point p = new Point(3, 4);
System.out.println(p.x());       // 3
System.out.println(p);           // Point[x=3, y=4]
```

> Equivalent to a class with final fields + all boilerplate. Cannot extend other classes.

---

## 19. Sealed Classes (Java 17)

Restricts which classes can **extend or implement** a class/interface.

```java
sealed class Shape permits Circle, Rectangle, Triangle { }

final class Circle extends Shape { }
final class Rectangle extends Shape { }
// Any other class CANNOT extend Shape
```

> `permits` lists allowed subclasses. Subclasses must be `final`, `sealed`, or `non-sealed`.

---

## Version Quick Reference

| Feature | Java Version |
|---|---|
| Lambda, Stream, Default Methods, forEach, Base64 | Java 8 |
| Module System, Diamond with Anonymous Class | Java 9 |
| `var` (Local Type Inference) | Java 10 |
| Switch Expressions (preview) | Java 12-13 |
| Switch Expressions (standard), `yield` | Java 14 |
| Text Blocks | Java 15 |
| Records | Java 16 |
| Sealed Classes | Java 17 |

---

## 5 Exam-Oriented Questions & Solutions

---

**Q1. What is a Functional Interface? Name 4 built-in ones.**

An interface with **exactly one abstract method**, usable as a lambda target. Annotated with `@FunctionalInterface`.

Built-in examples:
- `Predicate<T>` → `test()` → returns boolean
- `Function<T,R>` → `apply()` → transforms T to R
- `Consumer<T>` → `accept()` → takes input, returns nothing
- `Supplier<T>` → `get()` → no input, returns T

---

**Q2. What is the difference between `map()` and `flatMap()` in Stream API?**

- **`map()`** → transforms each element 1-to-1
- **`flatMap()`** → flattens nested collections (1-to-many)

```java
// map → Stream<String[]>
Stream<String[]> s1 = list.stream().map(s -> s.split(","));

// flatMap → Stream<String> (flattened)
Stream<String> s2 = list.stream().flatMap(s -> Arrays.stream(s.split(",")));
```

---

**Q3. What is the difference between Records and regular classes?**

| Feature | Record | Class |
|---|---|---|
| Fields | Implicitly `final` | Can be mutable |
| Constructor | Auto-generated | Must write manually |
| Getters | Auto-generated (no `get` prefix) | Must write manually |
| `equals/hashCode/toString` | Auto-generated | Must write manually |
| Inheritance | Cannot extend classes | Can extend |

```java
record Person(String name, int age) {}  // That's it — all boilerplate done!
```

---

**Q4. What are Sealed Classes and why are they useful?**

Sealed classes **restrict inheritance** to a known, fixed set of subclasses using `permits`.

```java
sealed interface Result permits Success, Failure {}
record Success(String data) implements Result {}
record Failure(String error) implements Result {}
```

**Use cases:** Model finite states (like enums but with data), enable exhaustive pattern matching in switch.

---

**Q5. What is the difference between Lambda and Method Reference? When to use each?**

Both implement functional interfaces, but:

- **Lambda** → write custom logic inline
- **Method Reference** → shorthand when lambda just calls an existing method

```java
// Lambda (custom logic)
list.forEach(s -> System.out.println(s.toUpperCase()));

// Method Reference (directly delegates to existing method)
list.forEach(System.out::println);

// Constructor reference
Supplier<List<String>> s = ArrayList::new;
```

Rule: If lambda body is just `obj.method(arg)` → use method reference.

---

*All 3 units done — go smash that exam!*

Brought to you by Team ZenYukti

![Footer Banner for ZenYukti - MyNotes](../../footer-image.png)