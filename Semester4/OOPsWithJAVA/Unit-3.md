# Java New Features - Exam Ready Notes

---

## 1. Functional Interfaces (Java 8)

### Definition
- Interface with **exactly ONE abstract method**
- Can have multiple default/static methods
- Annotated with `@FunctionalInterface` (optional but recommended)
- Foundation for Lambda expressions

### Key Points
- **SAM (Single Abstract Method)** interface
- Can inherit from other interfaces
- `@FunctionalInterface` ensures compile-time checking
- Used extensively with lambdas and Stream API

### Built-in Functional Interfaces

| Interface | Method | Parameters | Return | Use |
|-----------|--------|------------|--------|-----|
| `Predicate<T>` | `test(T t)` | T | boolean | Testing condition |
| `Function<T,R>` | `apply(T t)` | T | R | Transform T to R |
| `Consumer<T>` | `accept(T t)` | T | void | Consume/process |
| `Supplier<T>` | `get()` | none | T | Supply value |
| `BiFunction<T,U,R>` | `apply(T,U)` | T, U | R | Two inputs |
| `UnaryOperator<T>` | `apply(T t)` | T | T | Same type I/O |
| `BinaryOperator<T>` | `apply(T,T)` | T, T | T | Two same type |

### Code Examples
```java
// Custom functional interface
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
    // Can have default/static methods
    default void print() { }
}

// Using built-in
Predicate<Integer> isEven = n -> n % 2 == 0;
Function<String, Integer> toLength = s -> s.length();
Consumer<String> printer = System.out::println;
Supplier<Double> random = Math::random;
```

### Exam Questions

**Q1.** Which of the following is a valid functional interface?
```java
(a) interface A { void m1(); void m2(); }
(b) @FunctionalInterface interface B { void m1(); default void m2() {} }
(c) interface C { default void m1() {} }
(d) interface D { static void m1() {} }
```

**Q2.** Write a functional interface `StringProcessor` with method `process(String s)` returning String. Implement it using lambda to convert string to uppercase.

**Q3.** What happens if you add `@FunctionalInterface` to an interface with two abstract methods?

---

## 2. Lambda Expressions (Java 8)

### Syntax
```java
// Basic syntax
(parameters) -> expression
(parameters) -> { statements; }

// Examples
() -> 42                          // No parameter
x -> x * x                        // One parameter (parens optional)
(x, y) -> x + y                   // Multiple parameters
(String s) -> s.length()          // With type
x -> { System.out.println(x); }   // Block body
```

### Key Points
- **Anonymous function** - no name, no return type, no access modifier
- Replaces anonymous inner classes for functional interfaces
- Can access **effectively final** local variables (closure)
- Cannot modify local variables from enclosing scope
- `this` refers to enclosing class, not lambda itself

### Types of Lambda
```java
// 1. No parameter
Runnable r = () -> System.out.println("Hello");

// 2. Single parameter (type inferred)
Consumer<String> c = s -> System.out.println(s);

// 3. Multiple parameters
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;

// 4. With type declaration
Comparator<String> comp = (String s1, String s2) -> s1.compareTo(s2);

// 5. Multi-line block
Function<Integer, Integer> factorial = n -> {
    int result = 1;
    for(int i = 1; i <= n; i++) result *= i;
    return result;
};
```

### Lambda vs Anonymous Class

| Feature | Lambda | Anonymous Class |
|---------|--------|-----------------|
| **Code** | Concise | Verbose |
| **this** | Enclosing class | Anonymous class |
| **Scope** | Same as enclosing | New scope |
| **Performance** | Better (invokedynamic) | Slower |
| **Variables** | Effectively final only | Can have instance vars |

### Effectively Final
```java
int x = 10;  // effectively final
Consumer<Integer> c = n -> System.out.println(n + x); // OK
// x = 20;  // ERROR - cannot modify
```

### Exam Questions

**Q1.** Convert this anonymous class to lambda:
```java
new Thread(new Runnable() {
    public void run() {
        System.out.println("Running");
    }
}).start();
```

**Q2.** What's wrong with this code?
```java
int count = 0;
List<Integer> list = Arrays.asList(1,2,3);
list.forEach(n -> count += n);  // Error?
```

**Q3.** Write lambda expression for `Comparator<Employee>` to sort by salary in descending order.

---

## 3. Method References (Java 8)

### Syntax: `ClassName::methodName`

### Types of Method References

**1. Static Method Reference**
```java
// Lambda: x -> ClassName.staticMethod(x)
// Method Reference: ClassName::staticMethod

Function<String, Integer> parse1 = s -> Integer.parseInt(s);
Function<String, Integer> parse2 = Integer::parseInt;  // Better

BiFunction<Integer, Integer, Integer> max = Math::max;
```

**2. Instance Method Reference (Object)**
```java
// Lambda: x -> object.instanceMethod(x)
// Method Reference: object::instanceMethod

String str = "Hello";
Supplier<Integer> len1 = () -> str.length();
Supplier<Integer> len2 = str::length;  // Better

Consumer<String> print = System.out::println;
```

**3. Instance Method Reference (Class)**
```java
// Lambda: (obj, args) -> obj.instanceMethod(args)
// Method Reference: ClassName::instanceMethod

Function<String, Integer> len1 = s -> s.length();
Function<String, Integer> len2 = String::length;  // Better

BiPredicate<String, String> eq = String::equals;
// Equivalent to: (s1, s2) -> s1.equals(s2)
```

**4. Constructor Reference**
```java
// Lambda: () -> new ClassName()
// Method Reference: ClassName::new

Supplier<List<String>> list1 = () -> new ArrayList<>();
Supplier<List<String>> list2 = ArrayList::new;  // Better

Function<Integer, int[]> arr = int[]::new;  // Array constructor
```

### Quick Reference Table

| Type | Lambda | Method Ref | Example |
|------|--------|------------|---------|
| Static | `x -> Class.method(x)` | `Class::method` | `Integer::parseInt` |
| Instance (obj) | `x -> obj.method(x)` | `obj::method` | `str::length` |
| Instance (class) | `(obj,x) -> obj.method(x)` | `Class::method` | `String::length` |
| Constructor | `() -> new Class()` | `Class::new` | `ArrayList::new` |

### Exam Questions

**Q1.** Convert to method reference:
```java
(a) list.forEach(s -> System.out.println(s));
(b) list.stream().map(s -> s.toUpperCase());
(c) Arrays.sort(arr, (a, b) -> Integer.compare(a, b));
```

**Q2.** What's the difference between `String::valueOf` and `obj::toString`?

**Q3.** Write constructor reference to create `ArrayList<Integer>` from a Supplier.

---

## 4. Stream API (Java 8)

### What is Stream?
- Sequence of elements supporting sequential/parallel operations
- **NOT a data structure** - doesn't store data
- **Functional** approach to processing collections
- **Lazy evaluation** - intermediate ops not executed until terminal op

### Stream Creation
```java
// From Collection
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream1 = list.stream();

// From Array
Stream<String> stream2 = Stream.of("a", "b", "c");
Stream<Integer> stream3 = Arrays.stream(new int[]{1,2,3}).boxed();

// Using builder
Stream<String> stream4 = Stream.<String>builder().add("a").add("b").build();

// Infinite streams
Stream<Integer> infinite1 = Stream.iterate(0, n -> n + 2); // 0,2,4,6...
Stream<Double> infinite2 = Stream.generate(Math::random);

// From range
IntStream range = IntStream.range(1, 10);  // 1 to 9
IntStream rangeClosed = IntStream.rangeClosed(1, 10);  // 1 to 10
```

### Intermediate Operations (Lazy - Return Stream)

**filter(Predicate)** - Filter elements
```java
list.stream().filter(s -> s.startsWith("A"));
```

**map(Function)** - Transform elements
```java
list.stream().map(String::toUpperCase);
numbers.stream().map(n -> n * 2);
```

**flatMap(Function)** - Flatten nested streams
```java
List<List<Integer>> nested = Arrays.asList(
    Arrays.asList(1,2), Arrays.asList(3,4)
);
nested.stream().flatMap(List::stream);  // 1,2,3,4
```

**distinct()** - Remove duplicates
```java
Stream.of(1,2,2,3).distinct();  // 1,2,3
```

**sorted()** - Sort elements
```java
list.stream().sorted();
list.stream().sorted(Comparator.reverseOrder());
```

**limit(n)** - Take first n elements
```java
Stream.iterate(1, n -> n + 1).limit(10);  // 1 to 10
```

**skip(n)** - Skip first n elements
```java
list.stream().skip(2);
```

**peek(Consumer)** - Debug/observe (doesn't change stream)
```java
list.stream().peek(System.out::println).map(String::toUpperCase);
```

### Terminal Operations (Eager - Produce Result)

**forEach(Consumer)** - Iterate
```java
list.stream().forEach(System.out::println);
```

**collect(Collector)** - Collect to collection
```java
List<String> result = list.stream().collect(Collectors.toList());
Set<String> set = list.stream().collect(Collectors.toSet());
String joined = list.stream().collect(Collectors.joining(", "));

// Group by
Map<Integer, List<String>> byLength = 
    list.stream().collect(Collectors.groupingBy(String::length));

// Partition by (boolean)
Map<Boolean, List<Integer>> partition = 
    numbers.stream().collect(Collectors.partitioningBy(n -> n % 2 == 0));
```

**reduce(BinaryOperator)** - Reduce to single value
```java
// Sum
int sum = numbers.stream().reduce(0, (a, b) -> a + b);
int sum2 = numbers.stream().reduce(0, Integer::sum);

// Product
int product = numbers.stream().reduce(1, (a, b) -> a * b);

// Max
Optional<Integer> max = numbers.stream().reduce(Integer::max);
```

**count()** - Count elements
```java
long count = list.stream().count();
```

**anyMatch/allMatch/noneMatch(Predicate)** - Check conditions
```java
boolean hasEven = numbers.stream().anyMatch(n -> n % 2 == 0);
boolean allPositive = numbers.stream().allMatch(n -> n > 0);
boolean noneNegative = numbers.stream().noneMatch(n -> n < 0);
```

**findFirst/findAny()** - Find element
```java
Optional<String> first = list.stream().findFirst();
Optional<String> any = list.stream().findAny();
```

**min/max(Comparator)** - Find min/max
```java
Optional<Integer> min = numbers.stream().min(Integer::compareTo);
Optional<Integer> max = numbers.stream().max(Integer::compareTo);
```

### Primitive Streams
```java
IntStream intStream = IntStream.of(1, 2, 3);
DoubleStream doubleStream = DoubleStream.of(1.0, 2.0);
LongStream longStream = LongStream.range(1, 100);

// Special methods
int sum = IntStream.range(1, 11).sum();
OptionalDouble avg = IntStream.range(1, 11).average();
IntSummaryStatistics stats = IntStream.range(1, 11).summaryStatistics();
```

### Parallel Streams
```java
// Parallel processing
list.parallelStream().filter(...).map(...);
list.stream().parallel().forEach(...);

// Check if parallel
boolean isParallel = stream.isParallel();
```

### Exam Questions

**Q1.** Write Stream code to:
- Filter even numbers from list
- Square each number
- Sum all results

**Q2.** What's the output?
```java
Stream.of(1,2,3,4,5)
    .filter(n -> n % 2 == 0)
    .map(n -> n * n)
    .forEach(System.out::print);
```

**Q3.** Find the longest string from a list using Stream API.

**Q4.** Group list of employees by department using `collect()` and `groupingBy()`.

**Q5.** What's the difference between `map()` and `flatMap()`? Give example.

---

## 5. Default Methods (Java 8)

### Syntax
```java
interface MyInterface {
    // Abstract method
    void abstractMethod();
    
    // Default method (concrete implementation)
    default void defaultMethod() {
        System.out.println("Default implementation");
    }
}
```

### Key Points
- Allows adding new methods to interfaces **without breaking existing implementations**
- Introduced for **backward compatibility** (e.g., adding `forEach` to Collection)
- Can be **overridden** by implementing class
- Uses `default` keyword
- Can access other interface methods
- Cannot override Object class methods

### Multiple Inheritance Problem
```java
interface A {
    default void print() { System.out.println("A"); }
}

interface B {
    default void print() { System.out.println("B"); }
}

// Class must override to resolve conflict
class C implements A, B {
    @Override
    public void print() {
        A.super.print();  // Call specific interface default
        // Or provide own implementation
    }
}
```

### Rules for Default Methods
1. **Class wins** - Class method overrides interface default
2. **Subtype wins** - More specific interface wins
3. **Explicit choice** - Must override if ambiguous

### Examples
```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle starting");
    }
}

class Car implements Vehicle {
    // Can use default or override
    @Override
    public void start() {
        System.out.println("Car starting");
    }
}

// Real-world example from Java API
interface Iterable<T> {
    default void forEach(Consumer<? super T> action) {
        for (T t : this) {
            action.accept(t);
        }
    }
}
```

### Exam Questions

**Q1.** What's the purpose of default methods in interfaces?

**Q2.** Solve the diamond problem:
```java
interface A { default void m() { } }
interface B extends A { default void m() { } }
interface C extends A { }
class D implements B, C { }  // Which m() is called?
```

**Q3.** Can default method override `toString()` from Object class? Why?

---

## 6. Static Methods in Interfaces (Java 8)

### Syntax
```java
interface Utility {
    static int add(int a, int b) {
        return a + b;
    }
    
    static void print(String msg) {
        System.out.println(msg);
    }
}

// Call using interface name
int result = Utility.add(5, 3);
Utility.print("Hello");
```

### Key Points
- **Cannot be overridden** by implementing class
- Called using **interface name** (not object reference)
- Cannot use `this` keyword (no instance context)
- Used for **utility/helper methods** related to interface
- **Not inherited** by implementing classes

### Default vs Static Methods

| Feature | Default | Static |
|---------|---------|--------|
| **Access** | Through object | Through interface name |
| **Override** | Can be overridden | Cannot be overridden |
| **Inheritance** | Inherited | Not inherited |
| **this** | Can use this | Cannot use this |
| **Purpose** | Provide default behavior | Utility methods |

### Example
```java
interface Calculator {
    // Abstract method
    int calculate(int a, int b);
    
    // Default method
    default void displayResult(int result) {
        System.out.println("Result: " + result);
    }
    
    // Static utility method
    static boolean isValid(int num) {
        return num >= 0;
    }
}

class Adder implements Calculator {
    public int calculate(int a, int b) {
        if(Calculator.isValid(a) && Calculator.isValid(b)) {
            return a + b;
        }
        return 0;
    }
}
```

### Exam Questions

**Q1.** Can you call static interface method using implementing class name? Why?

**Q2.** Write an interface `MathUtil` with static method `isPrime(int n)`.

**Q3.** What's the difference between static method in interface vs abstract class?

---

## 7. Base64 Encode/Decode (Java 8)

### Basic Encoding/Decoding
```java
import java.util.Base64;

// Encode
String original = "Hello World";
String encoded = Base64.getEncoder().encodeToString(original.getBytes());
// Output: SGVsbG8gV29ybGQ=

// Decode
byte[] decoded = Base64.getDecoder().decode(encoded);
String result = new String(decoded);
// Output: Hello World
```

### Three Types of Encoders/Decoders

**1. Basic** - Standard Base64 (default)
```java
Base64.Encoder encoder = Base64.getEncoder();
Base64.Decoder decoder = Base64.getDecoder();
```

**2. URL Safe** - URL and filename safe (uses - and _ instead of + and /)
```java
Base64.Encoder urlEncoder = Base64.getUrlEncoder();
Base64.Decoder urlDecoder = Base64.getUrlDecoder();

String url = "https://example.com?param=value";
String encoded = urlEncoder.encodeToString(url.getBytes());
```

**3. MIME** - For MIME format (line length max 76, CRLF line separator)
```java
Base64.Encoder mimeEncoder = Base64.getMimeEncoder();
Base64.Decoder mimeDecoder = Base64.getMimeDecoder();
```

### Common Methods
```java
// Encoding
String encodeToString(byte[] src)
byte[] encode(byte[] src)

// Decoding  
byte[] decode(String src)
byte[] decode(byte[] src)

// Without padding (=)
Base64.Encoder encoder = Base64.getEncoder().withoutPadding();
```

### Exam Questions

**Q1.** Encode the string "Java Programming" to Base64 and then decode it back.

**Q2.** When would you use URL encoder instead of basic encoder?

**Q3.** Write code to encode a byte array without padding characters.

---

## 8. forEach Method (Java 8)

### Iterable forEach
```java
// Syntax
void forEach(Consumer<? super T> action)

// List
List<String> list = Arrays.asList("A", "B", "C");
list.forEach(item -> System.out.println(item));
list.forEach(System.out::println);  // Method reference

// Set
Set<Integer> set = new HashSet<>(Arrays.asList(1,2,3));
set.forEach(n -> System.out.println(n * 2));

// With index (workaround)
IntStream.range(0, list.size())
    .forEach(i -> System.out.println(i + ": " + list.get(i)));
```

### Map forEach
```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);

// forEach with BiConsumer
map.forEach((key, value) -> 
    System.out.println(key + " = " + value)
);

// Entry set forEach
map.entrySet().forEach(entry -> 
    System.out.println(entry.getKey() + " = " + entry.getValue())
);
```

### forEach vs for-loop

| Feature | forEach | for-loop |
|---------|---------|----------|
| **Break/Continue** | Cannot use | Can use |
| **Modify collection** | Avoid (ConcurrentModificationException) | Possible with iterator |
| **Access index** | Not directly | Easy |
| **Readability** | More concise | More flexible |
| **Performance** | Similar | Similar |

### Exam Questions

**Q1.** Print all even numbers from list using `forEach`.

**Q2.** Why can't you use `break` or `continue` in `forEach`? How to achieve early exit?

**Q3.** Print map entries in format "key: value" using `forEach`.

---

## 9. Try-with-Resources (Java 7, Enhanced Java 9)

### Java 7 Syntax
```java
// Auto-closes resources that implement AutoCloseable
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
// br is automatically closed
```

### Multiple Resources
```java
try (
    FileInputStream fis = new FileInputStream("input.txt");
    FileOutputStream fos = new FileOutputStream("output.txt")
) {
    // Use resources
    int data = fis.read();
    fos.write(data);
}
// Both auto-closed in reverse order (fos, then fis)
```

### Java 9 Enhancement - Effectively Final Variables
```java
// Java 9: Can use effectively final variables
BufferedReader br = new BufferedReader(new FileReader("file.txt"));

try (br) {  // No need to re-declare
    String line = br.readLine();
}
// br is auto-closed
```

### AutoCloseable Interface
```java
// Custom resource
class MyResource implements AutoCloseable {
    public void doSomething() {
        System.out.println("Doing something");
    }
    
    @Override
    public void close() {
        System.out.println("Closing resource");
    }
}

try (MyResource res = new MyResource()) {
    res.doSomething();
}  // close() called automatically
```

### Key Points
- Resources must implement `AutoCloseable` or `Closeable`
- `close()` called automatically in **reverse order** of creation
- Exceptions in `close()` are **suppressed** if exception occurs in try block
- Access suppressed exceptions using `getSuppressed()`
- More concise than manual `finally` blocks

### Before Try-with-Resources
```java
// Old way (verbose)
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (br != null) {
        try {
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Exam Questions

**Q1.** What interface must a class implement to be used in try-with-resources?

**Q2.** Write try-with-resources to read from one file and write to another.

**Q3.** What's the advantage of Java 9's try-with-resources over Java 7?

---

## 10. Type Annotations (Java 8)

### Before Java 8
```java
// Annotations only on declarations
@Override
public void method() { }

@Deprecated
class OldClass { }
```

### Java 8 - Annotations Anywhere
```java
// On type uses
@NonNull String str;  // Local variable
List<@NonNull String> list;  // Generic type
String @NonNull [] array;  // Array

// Type casting
String s = (@NonNull String) obj;

// instanceof
if (obj instanceof @NonNull String) { }

// Object creation
new @Interned MyObject();

// Method receiver (this)
public void method(@ReadOnly MyClass this) { }

// Throws
public void method() throws @Critical Exception { }
```

### Common Use Cases
- **Null checking**: `@NonNull`, `@Nullable`
- **Concurrency**: `@ThreadSafe`, `@Immutable`
- **Regex validation**: `@Regex`
- **Units**: `@Meters`, `@Seconds`

### ElementType.TYPE_USE
```java
import java.lang.annotation.*;

@Target(ElementType.TYPE_USE)
@interface NonNull { }

@Target(ElementType.TYPE_USE)
@interface ReadOnly { }
```

### Exam Questions

**Q1.** Where can type annotations be applied that declaration annotations cannot?

**Q2.** Write annotation `@Positive` that can be used on type uses.

**Q3.** What's the difference between `String @NonNull []` and `@NonNull String[]`?

---

## 11. Repeating Annotations (Java 8)

### Before Java 8 - Container Annotation
```java
@interface Author {
    String name();
}

@interface Authors {
    Author[] value();
}

@Authors({
    @Author(name = "John"),
    @Author(name = "Jane")
})
class Book { }
```

### Java 8 - Direct Repetition
```java
import java.lang.annotation.*;

@Repeatable(Authors.class)  // Point to container
@interface Author {
    String name();
}

@interface Authors {
    Author[] value();  // Must have value() returning array
}

// Can repeat directly
@Author(name = "John")
@Author(name = "Jane")
class Book { }
```

### Requirements for @Repeatable
1. Annotation must be marked with `@Repeatable(Container.class)`
2. Container must have `value()` method returning array of the annotation
3. Container's retention ≥ repeatable annotation's retention
4. Container's target ⊇ repeatable annotation's target

### Accessing Repeated Annotations
```java
// Get repeated annotations
Author[] authors = Book.class.getAnnotationsByType(Author.class);

for (Author author : authors) {
    System.out.println(author.name());
}

// Or get container
Authors authorsContainer = Book.class.getAnnotation(Authors.class);
```

### Complete Example
```java
@Repeatable(Schedules.class)
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface Schedule {
    String day();
    String time();
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface Schedules {
    Schedule[] value();
}

@Schedule(day = "Monday", time = "9 AM")
@Schedule(day = "Wednesday", time = "2 PM")
@Schedule(day = "Friday", time = "4 PM")
class Meeting { }
```

### Exam Questions

**Q1.** What annotation makes an annotation repeatable?

**Q2.** Write repeatable `@Test` annotation with `name` attribute and its container.

**Q3.** What are the requirements for a container annotation?

---

## 12. Java Module System (Java 9 - JPMS)

### Module Basics
- **Module** = Collection of packages
- Defined in `module-info.java` at root
- Strong encapsulation + explicit dependencies
- Replaced classpath hell

### module-info.java Syntax
```java
module com.example.myapp {
    // Export package (make public)
    exports com.example.myapp.api;
    exports com.example.myapp.utils to com.client.app;  // Qualified export
    
    // Require other module
    requires java.sql;
    requires transitive java.logging;  // Transitive dependency
    
    // Open for reflection (entire module)
    opens com.example.myapp.internal;
    opens com.example.myapp.model to com.fasterxml.jackson.databind;  // Qualified
    
    // Service provider
    provides com.example.Service with com.example.ServiceImpl;
    
    // Service consumer
    uses com.example.Service;
}
```

### Key Directives

**exports** - Make package accessible to other modules
```java
exports com.example.api;  // All modules can access
exports com.example.internal to com.friend;  // Only friend can access
```

**requires** - Depend on another module
```java
requires java.base;  // Implicit, always present
requires java.sql;
requires transitive java.logging;  // Anyone requiring this module gets logging too
```

**opens** - Allow reflection access
```java
opens com.example.model;  // Deep reflection allowed
opens com.example.entity to hibernate.core;
```

**provides...with** - Service provider
```java
provides com.example.MyService with com.example.MyServiceImpl;
```

**uses** - Service consumer
```java
uses com.example.MyService;
```

### Module Types
1. **System Modules** - JDK modules (java.base, java.sql, etc.)
2. **Application Modules** - Your modules with module-info.java
3. **Automatic Modules** - JAR without module-info (name from JAR filename)
4. **Unnamed Module** - Classpath code without module

### Benefits
- **Strong encapsulation** - Internal packages hidden
- **Reliable configuration** - Missing dependencies detected at startup
- **Smaller runtime** - Include only needed modules (jlink)
- **Better performance** - JVM optimizations

### Common JDK Modules
- `java.base` - Core (String, Object, etc.) - Always included
- `java.sql` - JDBC
- `java.xml` - XML processing
- `java.logging` - Logging
- `java.desktop` - AWT/Swing

### Exam Questions

**Q1.** Write module-info.java that:
- Exports package `com.app.api`
- Requires `java.sql`
- Opens `com.app.model` for reflection

**Q2.** What's the difference between `requires` and `requires transitive`?

**Q3.** What happens if module A requires B, and B exports package P, but A tries to access package Q from B?

---

## 13. Diamond Operator with Anonymous Inner Class (Java 9)

### Java 7 - Diamond Operator
```java
// Instead of
List<String> list = new ArrayList<String>();

// Can use
List<String> list = new ArrayList<>();  // Type inferred
```

### Java 9 Enhancement - With Anonymous Classes
```java
// Java 7/8 - ERROR
List<String> list = new ArrayList<>() {
    // anonymous class body
};

// Java 9 - OK
List<String> list = new ArrayList<>() {
    {
        add("Item 1");
        add("Item 2");
    }
};

// Another example
Comparator<String> comp = new Comparator<>() {  // Type inferred as <String>
    @Override
    public int compare(String s1, String s2) {
        return s1.length() - s2.length();
    }
};
```

### Use Cases
```java
// Custom initialization
Map<String, Integer> map = new HashMap<>() {{
    put("A", 1);
    put("B", 2);
    put("C", 3);
}};

// Custom behavior
List<Integer> list = new ArrayList<>() {
    @Override
    public boolean add(Integer e) {
        System.out.println("Adding: " + e);
        return super.add(e);
    }
};
```

### Exam Questions

**Q1.** What version of Java allows diamond operator with anonymous inner classes?

**Q2.** Is this valid in Java 9?
```java
Set<Integer> set = new HashSet<>() {
    // custom methods
};
```

**Q3.** Write an anonymous ArrayList with diamond operator that prints size when adding elements.

---

## 14. Local Variable Type Inference - var (Java 10)

### Basic Syntax
```java
// Instead of
String message = "Hello";
List<String> list = new ArrayList<>();

// Can use var
var message = "Hello";  // Type inferred as String
var list = new ArrayList<String>();  // Type inferred as ArrayList<String>
```

### Where var Can Be Used
```java
// Local variables
var name = "John";
var age = 25;
var list = new ArrayList<Integer>();

// Loop variables
for (var i = 0; i < 10; i++) { }
for (var item : list) { }

// try-with-resources
try (var br = new BufferedReader(new FileReader("file.txt"))) { }

// Lambda parameters (Java 11)
list.forEach((var item) -> System.out.println(item));
```

### Where var CANNOT Be Used
```java
// ❌ Method parameters
public void method(var param) { }  // ERROR

// ❌ Method return type
public var getValue() { }  // ERROR

// ❌ Field/Instance variable
class MyClass {
    var field = 10;  // ERROR
}

// ❌ Constructor parameters
public MyClass(var param) { }  // ERROR

// ❌ Without initializer
var x;  // ERROR - cannot infer
var y = null;  // ERROR - null has no type

// ❌ Multiple declarations
var a = 1, b = 2;  // ERROR

// ❌ Array initializer
var arr = {1, 2, 3};  // ERROR
var arr = new int[]{1, 2, 3};  // OK
```

### Best Practices
```java
// ✅ Good - Type is obvious
var message = "Hello World";
var count = 10;
var list = new ArrayList<String>();

// ⚠️ Questionable - Type not obvious
var result = calculate();  // What type?

// ❌ Bad - Loses readability
var x = getConnection();  // Connection? Stream? What?

// ✅ Better - Explicit type for clarity
Connection connection = getConnection();
```

### var with Generics
```java
// Type inferred correctly
var list = List.of("A", "B", "C");  // List<String>
var map = Map.of("key", 1);  // Map<String, Integer>

// Beware of diamond operator
var list1 = new ArrayList<>();  // ArrayList<Object> - not what you want!
var list2 = new ArrayList<String>();  // ArrayList<String> - correct
```

### Exam Questions

**Q1.** Which of the following are valid?
```java
(a) var x = 10;
(b) var list;
(c) var arr = {1,2,3};
(d) var map = new HashMap<String, Integer>();
```

**Q2.** What's the inferred type?
```java
var list = new ArrayList<>();
```

**Q3.** Can you use `var` for method parameters? Why or why not?

---

## 15. Switch Expressions (Java 12/13, Enhanced 14)

### Traditional Switch (Statement)
```java
int day = 2;
String result;
switch(day) {
    case 1:
        result = "Monday";
        break;
    case 2:
        result = "Tuesday";
        break;
    default:
        result = "Unknown";
        break;
}
```

### Switch Expression (Java 12+)
```java
int day = 2;
String result = switch(day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Unknown";
};  // Note semicolon!
```

### Arrow Syntax (->)
```java
// No fall-through, no break needed
String day = switch(num) {
    case 1 -> "One";
    case 2 -> "Two";
    case 3 -> "Three";
    default -> "Other";
};

// Multiple values
String type = switch(day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};

// Block with arrow
int result = switch(num) {
    case 1 -> {
        System.out.println("Processing one");
        yield 1 * 10;  // yield for block
    }
    case 2 -> {
        System.out.println("Processing two");
        yield 2 * 10;
    }
    default -> 0;
};
```

### Colon Syntax (Traditional)
```java
// Can still use colon, but with yield
int result = switch(num) {
    case 1:
    case 2:
        yield 10;  // Use yield, not return
    case 3:
        yield 20;
    default:
        yield 0;
};
```

### Exhaustiveness
```java
// Must be exhaustive (cover all cases or have default)
enum Day { MON, TUE, WED }

// OK - all cases covered
String s = switch(day) {
    case MON -> "Monday";
    case TUE -> "Tuesday";
    case WED -> "Wednesday";
};

// OK - has default
String s = switch(day) {
    case MON -> "Monday";
    default -> "Other day";
};

// ERROR - not exhaustive
String s = switch(day) {
    case MON -> "Monday";
};  // Missing TUE, WED
```

### Switch Expression vs Statement

| Feature | Expression | Statement |
|---------|------------|-----------|
| **Returns value** | Yes | No |
| **Arrow syntax** | Supported | Not in old Java |
| **Fall-through** | No (with ->) | Yes (with :) |
| **break** | Not needed | Needed |
| **yield** | Use for blocks | Not used |
| **Exhaustive** | Must be | Not required |

### Exam Questions

**Q1.** Convert to switch expression:
```java
int month = 5;
String season;
switch(month) {
    case 12: case 1: case 2:
        season = "Winter";
        break;
    case 3: case 4: case 5:
        season = "Spring";
        break;
    default:
        season = "Other";
}
```

**Q2.** What's wrong with this code?
```java
String result = switch(num) {
    case 1 -> "One";
    case 2 -> "Two";
};  // num could be 3
```

**Q3.** When do you use `yield` in switch expressions?

---

## 16. Yield Keyword (Java 13/14)

### Purpose
- Return value from switch expression **block**
- Alternative to `return` in switch expressions
- Similar to `return` but for switch expressions

### Syntax
```java
int result = switch(num) {
    case 1 -> {
        // Multiple statements
        int temp = num * 10;
        System.out.println("Processing: " + temp);
        yield temp;  // Return value from block
    }
    case 2 -> {
        yield num * 20;
    }
    default -> 0;
};
```

### When to Use yield

**1. With Arrow (->) and Block**
```java
String result = switch(day) {
    case "MON" -> {
        // Some processing
        yield "Monday";  // Required for block
    }
    case "TUE" -> "Tuesday";  // Simple expression, no yield
    default -> "Unknown";
};
```

**2. With Colon (:) Syntax**
```java
int value = switch(num) {
    case 1:
        System.out.println("One");
        yield 100;  // Must use yield, not break
    case 2:
        yield 200;
    default:
        yield 0;
};
```

### yield vs return

| Feature | yield | return |
|---------|-------|--------|
| **Used in** | Switch expressions | Methods |
| **Returns from** | Switch block | Entire method |
| **Syntax** | `yield value;` | `return value;` |

### Cannot Use return in Switch Expression
```java
// ❌ ERROR
int result = switch(num) {
    case 1 -> {
        return 100;  // ERROR - use yield
    }
    default -> 0;
};

// ✅ CORRECT
int result = switch(num) {
    case 1 -> {
        yield 100;
    }
    default -> 0;
};
```

### Examples
```java
// Simple calculation
int square = switch(num) {
    case 1, 2, 3 -> {
        int temp = num * num;
        yield temp;
    }
    default -> 0;
};

// With condition
String grade = switch(score) {
    case int s when s >= 90 -> {
        System.out.println("Excellent!");
        yield "A";
    }
    case int s when s >= 80 -> "B";
    default -> "F";
};
```

### Exam Questions

**Q1.** When is `yield` required in switch expressions?

**Q2.** Fix this code:
```java
int result = switch(x) {
    case 1 -> {
        int temp = x * 2;
        return temp;  // Error?
    }
    default -> 0;
};
```

**Q3.** Can you use `yield` in traditional switch statements (not expressions)?

---

## 17. Text Blocks (Java 13/14/15)

### Problem with Traditional Strings
```java
// Hard to read, lots of escaping
String html = "<html>\n" +
              "  <body>\n" +
              "    <p>Hello</p>\n" +
              "  </body>\n" +
              "</html>";

String json = "{\n" +
              "  \"name\": \"John\",\n" +
              "  \"age\": 30\n" +
              "}";
```

### Text Block Syntax
```java
// Use triple quotes """
String html = """
              <html>
                <body>
                  <p>Hello</p>
                </body>
              </html>
              """;

String json = """
              {
                "name": "John",
                "age": 30
              }
              """;
```

### Key Rules
1. Must start with `"""` followed by **newline** (not on same line)
2. End with `"""` (can be on new line or same as last line)
3. Indentation is **significant** - common indentation removed
4. Preserves formatting and line breaks
5. No need to escape quotes inside (except triple quotes)

### Opening Delimiter
```java
// ❌ WRONG - no newline after """
String wrong = """Hello""";

// ✅ CORRECT
String correct = """
                 Hello
                 """;

// ✅ ALSO CORRECT
String correct2 = """
                  Hello""";  // Closing on same line as content
```

### Incidental Whitespace
```java
// Indentation relative to closing """ is preserved
String text1 = """
               Line 1
                 Line 2
               """;
// "Line 1\n  Line 2\n"

String text2 = """
    Line 1
      Line 2
    """;
// "Line 1\n  Line 2\n"
```

### Escaping in Text Blocks
```java
// No need to escape "
String s = """
           He said "Hello"
           """;

// Need to escape """
String s = """
           Use \""" for text blocks
           """;

// \ at end of line - no newline
String s = """
           Line 1 \
           Line 2
           """;
// Result: "Line 1 Line 2\n"

// \s preserves trailing space
String s = """
           Line 1   \s
           Line 2
           """;
```

### Real-World Examples
```java
// SQL Query
String query = """
               SELECT id, name, email
               FROM users
               WHERE status = 'ACTIVE'
               ORDER BY name
               """;

// HTML Template
String template = """
                  <!DOCTYPE html>
                  <html>
                    <head>
                      <title>%s</title>
                    </head>
                    <body>
                      <h1>%s</h1>
                    </body>
                  </html>
                  """.formatted(title, heading);

// JSON
String json = """
              {
                "employees": [
                  {"name": "John", "age": 30},
                  {"name": "Jane", "age": 25}
                ]
              }
              """;
```

### Text Blocks Methods
```java
String block = """
               Hello
               World
               """;

// All String methods work
block.lines().forEach(System.out::println);
block.indent(2);  // Add indentation
block.stripIndent();  // Remove indentation
block.translateEscapes();
```

### Exam Questions

**Q1.** Which is valid?
```java
(a) String s = """Hello""";
(b) String s = """
    Hello""";
(c) String s = """ Hello
    """;
```

**Q2.** What's the output?
```java
String s = """
    Line 1
      Line 2
    """;
System.out.println(s);
```

**Q3.** Write a text block for SQL query to select all columns from "products" table where price > 100.

---

## 18. Records (Java 14/16)

### Purpose
- **Immutable data carriers** (like DTOs)
- Reduces boilerplate code
- Auto-generates constructor, getters, equals(), hashCode(), toString()

### Basic Syntax
```java
// Traditional class
class Person {
    private final String name;
    private final int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String name() { return name; }
    public int age() { return age; }
    
    @Override
    public boolean equals(Object o) { /* ... */ }
    @Override
    public int hashCode() { /* ... */ }
    @Override
    public String toString() { /* ... */ }
}

// Record - much simpler!
record Person(String name, int age) { }
```

### Auto-Generated Features
```java
record Point(int x, int y) { }

// Automatically provides:
// 1. Private final fields: x, y
// 2. Constructor: Point(int x, int y)
// 3. Accessors: x(), y() [not getX(), getY()]
// 4. equals(Object o)
// 5. hashCode()
// 6. toString() -> "Point[x=1, y=2]"

Point p = new Point(10, 20);
System.out.println(p.x());  // 10
System.out.println(p.y());  // 20
System.out.println(p);  // Point[x=10, y=20]
```

### Custom Implementations

**1. Compact Constructor**
```java
record Range(int min, int max) {
    // Compact constructor - validation
    public Range {  // No parameters!
        if (min > max) {
            throw new IllegalArgumentException("min > max");
        }
    }
}

// Canonical constructor also possible
record Range(int min, int max) {
    public Range(int min, int max) {
        if (min > max) throw new IllegalArgumentException();
        this.min = min;
        this.max = max;
    }
}
```

**2. Additional Constructors**
```java
record Person(String name, int age) {
    // Must call canonical constructor
    public Person(String name) {
        this(name, 0);  // Call canonical constructor
    }
}
```

**3. Instance Methods**
```java
record Rectangle(int width, int height) {
    // Custom methods allowed
    public int area() {
        return width * height;
    }
    
    public boolean isSquare() {
        return width == height;
    }
}
```

**4. Static Members**
```java
record Person(String name, int age) {
    static int count = 0;
    
    static Person of(String name) {
        return new Person(name, 0);
    }
}
```

### Records Restrictions
```java
// ❌ Cannot extend class (implicit extends Record)
record Person(...) extends SomeClass { }  // ERROR

// ❌ Cannot declare instance fields (only the components)
record Person(String name) {
    private int age;  // ERROR
}

// ❌ Cannot be abstract
abstract record Person(String name) { }  // ERROR

// ❌ Components are implicitly final
record Person(final String name) { }  // Redundant

// ✅ Can implement interfaces
record Person(String name) implements Comparable<Person> {
    @Override
    public int compareTo(Person other) {
        return this.name.compareTo(other.name);
    }
}

// ✅ Can have static fields/methods
record Person(String name) {
    static int count = 0;
}

// ✅ Can be generic
record Pair<T, U>(T first, U second) { }
```

### Nested Records
```java
class Outer {
    record Inner(int x) { }  // OK
}

record Outer(int x) {
    record Inner(int y) { }  // OK - implicitly static
}
```

### Use Cases
```java
// API responses
record UserResponse(String id, String name, String email) { }

// Database entities (value objects)
record Address(String street, String city, String zip) { }

// Tuple-like structures
record Pair<A, B>(A first, B second) { }

// Configuration
record DatabaseConfig(String url, String username, String password) { }
```

### Exam Questions

**Q1.** What methods are automatically generated for a record?

**Q2.** Fix this code:
```java
record Employee(String name, int salary) {
    private String department;  // Error?
}
```

**Q3.** Write a record `Book` with fields `title` and `author`. Add validation in compact constructor to ensure neither is null.

**Q4.** Can a record extend another class? Why or why not?

**Q5.** How do you access fields in a record - `getName()` or `name()`?

---

## 19. Sealed Classes (Java 15/17)

### Purpose
- **Restrict inheritance** - control which classes can extend/implement
- Better than `final` (allows some subclasses)
- Useful for exhaustive pattern matching

### Basic Syntax
```java
// Sealed class - specify permitted subclasses
public sealed class Shape
    permits Circle, Rectangle, Triangle {
    // Base class code
}

// Permitted subclasses must be: final, sealed, or non-sealed
final class Circle extends Shape { }
final class Rectangle extends Shape { }
final class Triangle extends Shape { }
```

### Three Options for Subclasses

**1. final** - Cannot be extended further
```java
sealed class Animal permits Dog, Cat { }

final class Dog extends Animal { }  // End of hierarchy
final class Cat extends Animal { }  // End of hierarchy
```

**2. sealed** - Can extend, but restrict further
```java
sealed class Animal permits Mammal, Bird { }

sealed class Mammal extends Animal permits Dog, Cat { }
final class Dog extends Mammal { }
final class Cat extends Mammal { }

final class Bird extends Animal { }
```

**3. non-sealed** - Open for extension
```java
sealed class Animal permits Dog, Cat { }

final class Dog extends Animal { }
non-sealed class Cat extends Animal { }  // Anyone can extend

class PersianCat extends Cat { }  // OK - Cat is non-sealed
```

### Sealed Interfaces
```java
public sealed interface Service
    permits DatabaseService, FileService {
    void execute();
}

final class DatabaseService implements Service {
    public void execute() { /* DB logic */ }
}

final class FileService implements Service {
    public void execute() { /* File logic */ }
}
```

### Same File Declaration
```java
// If in same file, permits can be omitted
sealed class Vehicle { }
final class Car extends Vehicle { }
final class Bike extends Vehicle { }
```

### Rules and Restrictions

**1. Permitted Subclasses Must:**
- Be in same module (or same package if unnamed module)
- Directly extend/implement the sealed class
- Be exactly one of: `final`, `sealed`, or `non-sealed`

**2. Sealed Class:**
- Must have at least one permitted subclass
- `permits` clause specifies allowed subclasses
- Can be abstract or concrete

### Use with Pattern Matching
```java
sealed interface Result permits Success, Failure { }
record Success(String data) implements Result { }
record Failure(String error) implements Result { }

// Exhaustive switch (no default needed)
String message = switch(result) {
    case Success s -> "Success: " + s.data();
    case Failure f -> "Error: " + f.error();
    // Compiler knows these are ALL possibilities
};
```

### Real-World Example
```java
// Payment system
public sealed class Payment
    permits CreditCard, DebitCard, Cash {
    
    protected double amount;
    
    public Payment(double amount) {
        this.amount = amount;
    }
}

final class CreditCard extends Payment {
    private String cardNumber;
    
    public CreditCard(double amount, String cardNumber) {
        super(amount);
        this.cardNumber = cardNumber;
    }
}

final class DebitCard extends Payment {
    private String accountNumber;
    
    public DebitCard(double amount, String accountNumber) {
        super(amount);
        this.accountNumber = accountNumber;
    }
}

final class Cash extends Payment {
    public Cash(double amount) {
        super(amount);
    }
}

// Usage - exhaustive pattern matching
public void processPayment(Payment payment) {
    switch(payment) {
        case CreditCard cc -> processCreditCard(cc);
        case DebitCard dc -> processDebitCard(dc);
        case Cash cash -> processCash(cash);
        // No default needed - compiler verifies exhaustiveness
    }
}
```

### Sealed vs Final vs Abstract

| Feature | final | sealed | abstract |
|---------|-------|--------|----------|
| **Inheritance** | None | Controlled | Open |
| **Instantiation** | Yes | Yes (if not abstract) | No |
| **Use case** | No subclasses | Limited subclasses | Must be extended |

### Exam Questions

**Q1.** What are the three modifiers a subclass of a sealed class can have?

**Q2.** Fix this code:
```java
sealed class Animal permits Dog { }
class Dog extends Animal { }  // Error?
```

**Q3.** Write a sealed interface `Status` with two permitted implementations: `Active` and `Inactive` (both final).

**Q4.** Can a sealed class be abstract? Can it have abstract methods?

**Q5.** Why are sealed classes useful with pattern matching?

---

# LAST MINUTE REVISION - 1 PAGE SUMMARY

## Functional Programming Essentials

### Functional Interface
- **ONE abstract method** only
- `@FunctionalInterface` annotation
- Built-in: `Predicate<T>`, `Function<T,R>`, `Consumer<T>`, `Supplier<T>`

### Lambda Syntax
```java
(params) -> expression
(params) -> { statements; }
```
- `x -> x * 2` (one param)
- `(a, b) -> a + b` (multiple params)
- **Effectively final** variables only

### Method References
```java
Class::staticMethod       // Integer::parseInt
object::instanceMethod    // str::length
Class::instanceMethod     // String::toUpperCase
Class::new               // ArrayList::new
```

---

## Stream API Cheat Sheet

### Creation
```java
list.stream()
Stream.of(1,2,3)
IntStream.range(1, 10)
```

### Intermediate (return Stream)
- `filter(Predicate)` - filter elements
- `map(Function)` - transform
- `flatMap()` - flatten nested
- `distinct()` - remove duplicates
- `sorted()` - sort
- `limit(n)` / `skip(n)` - take/skip n
- `peek()` - debug

### Terminal (return result)
- `forEach()` - iterate
- `collect()` - to collection
- `reduce()` - single value
- `count()` - count elements
- `anyMatch/allMatch/noneMatch()` - test
- `findFirst/findAny()` - find element
- `min/max()` - extremes

### Quick Examples
```java
// Sum even numbers
list.stream().filter(n -> n%2==0).mapToInt(Integer::intValue).sum()

// Group by length
map = list.stream().collect(Collectors.groupingBy(String::length))
```

---

## Interface Enhancements

### Default Methods (Java 8)
```java
interface I {
    default void method() { }  // Concrete implementation
}
```
- Backward compatibility
- Can be overridden
- **Class wins** over default

### Static Methods (Java 8)
```java
interface I {
    static void method() { }
}
// Call: I.method()
```
- NOT inherited
- Cannot override

---

## Modern Java Features

### var (Java 10)
```java
var name = "John";  // Type inferred
```
- ✅ Local variables, loops, try-with-resources
- ❌ Fields, method params/return, without initializer

### Switch Expression (Java 14)
```java
String result = switch(day) {
    case 1, 2, 3 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};
```
- Use `yield` for blocks
- Must be exhaustive
- No fall-through with `->`

### Text Blocks (Java 15)
```java
String html = """
              <html>
                <body>Hello</body>
              </html>
              """;
```
- Triple quotes `"""`
- Must start with newline
- Preserves formatting

### Records (Java 16)
```java
record Person(String name, int age) { }
```
**Auto-generates:** constructor, accessors (`name()` not `getName()`), `equals()`, `hashCode()`, `toString()`
- Immutable
- Cannot extend classes
- Can implement interfaces
- Components are `final`

### Sealed Classes (Java 17)
```java
sealed class Shape permits Circle, Rectangle { }
final class Circle extends Shape { }
```
- Control inheritance
- Subclass must be: `final`, `sealed`, or `non-sealed`
- Enables exhaustive pattern matching

---

## Quick Reference

### Try-with-Resources
```java
try (var br = new BufferedReader(...)) {
    // auto-closed
}
```
- Must implement `AutoCloseable`
- Java 9: can use effectively final vars

### Base64
```java
String enc = Base64.getEncoder().encodeToString(bytes);
byte[] dec = Base64.getDecoder().decode(enc);
```
- Types: Basic, URL, MIME

### forEach
```java
list.forEach(System.out::println);
map.forEach((k, v) -> print(k, v));
```

### Annotations
**Type Annotations:** Can annotate any type use
**Repeating:** `@Repeatable(Container.class)`

### Module System
```java
module com.app {
    exports com.app.api;
    requires java.sql;
    opens com.app.model;
}
```

---

## Exam Pro Tips ⚡

1. **Functional Interface** - Must have EXACTLY ONE abstract method
2. **Lambda** - Can access effectively final vars only
3. **Stream** - Intermediate ops lazy, terminal eager
4. **var** - Cannot use without initializer or with `null`
5. **Switch Expression** - Must be exhaustive (all cases or default)
6. **yield** - Use in switch blocks, NOT return
7. **Text Blocks** - Triple quotes must start new line
8. **Records** - Accessors are `field()` not `getField()`
9. **Sealed** - Subclasses must be final/sealed/non-sealed
10. **Method Reference** - `::` syntax, 4 types

---

## Common Exam Patterns

✓ Convert anonymous class → lambda → method reference
✓ Stream pipeline: filter → map → collect
✓ Identify valid/invalid var usage
✓ Convert switch statement → switch expression
✓ Write record with validation (compact constructor)
✓ Identify sealed class hierarchy errors
✓ Functional interface with custom method
✓ Try-with-resources with multiple resources

---

**REMEMBER:**
- Lambda = anonymous function
- Stream = pipeline of operations
- var = type inference (local only)
- Record = immutable data class
- Sealed = controlled inheritance
- Text blocks = multi-line strings
- Switch expression = returns value

**Good Luck!**

Brought to you by Team ZenYukti

![Footer Banner for ZenYukti - MyNotes](../../footer-image.png)