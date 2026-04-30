# Java Collections Framework — Exam Notes

---

## 1. What is the Collections Framework?

A **unified architecture** for storing and manipulating groups of objects.  
Provides: **Interfaces → Implementations → Algorithms**

---

## 2. Hierarchy at a Glance

```
Iterable
  └── Collection
        ├── List       → ArrayList, LinkedList, Vector, Stack
        ├── Queue      → PriorityQueue, LinkedList
        └── Set        → HashSet, LinkedHashSet
                            └── SortedSet → TreeSet

Map (separate hierarchy)
  └── HashMap, LinkedHashMap, Hashtable
        └── SortedMap → TreeMap
```

---

## 3. Iterator Interface

Used to **traverse** any collection.

```java
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

Key methods: `hasNext()`, `next()`, `remove()`

---

## 4. Collection Interface

Root interface. Key methods:
`add()`, `remove()`, `size()`, `contains()`, `iterator()`, `clear()`

---

## 5. List Interface

**Ordered, allows duplicates, index-based access.**

### ArrayList
- Dynamic array; fast random access O(1)
- Slow insert/delete in middle O(n)

```java
ArrayList<Integer> al = new ArrayList<>();
al.add(10); al.add(20);
System.out.println(al.get(0)); // 10
```

### LinkedList
- Doubly linked list; fast insert/delete O(1)
- Slow random access O(n)
- Also implements **Queue** and **Deque**

```java
LinkedList<String> ll = new LinkedList<>();
ll.addFirst("A"); ll.addLast("B");
```

### Vector
- Like ArrayList but **synchronized** (thread-safe)
- Legacy class; prefer ArrayList unless thread-safety needed

### Stack (extends Vector)
- LIFO structure
- Methods: `push()`, `pop()`, `peek()`, `isEmpty()`

```java
Stack<Integer> s = new Stack<>();
s.push(1); s.push(2);
System.out.println(s.pop()); // 2
```

---

## 6. Queue Interface

**FIFO order.** Key methods: `offer()`, `poll()`, `peek()`

```java
Queue<Integer> q = new LinkedList<>();
q.offer(1); q.offer(2);
System.out.println(q.poll()); // 1
```

> `PriorityQueue` orders by natural ordering or Comparator.

---

## 7. Set Interface

**No duplicates allowed.**

### HashSet
- Backed by HashMap; **no order guaranteed**
- O(1) add/remove/contains

```java
HashSet<String> hs = new HashSet<>();
hs.add("A"); hs.add("A"); // duplicate ignored
System.out.println(hs.size()); // 1
```

### LinkedHashSet
- Maintains **insertion order**

### SortedSet Interface → TreeSet
- Elements stored in **sorted (natural) order**
- O(log n) operations (uses Red-Black Tree)

```java
TreeSet<Integer> ts = new TreeSet<>();
ts.add(30); ts.add(10); ts.add(20);
System.out.println(ts); // [10, 20, 30]
```

---

## 8. Map Interface

**Key-Value pairs. Keys are unique.**

### HashMap
- No order; allows one `null` key; O(1) avg
```java
HashMap<String, Integer> map = new HashMap<>();
map.put("A", 1); map.put("B", 2);
System.out.println(map.get("A")); // 1
```

### LinkedHashMap
- Maintains **insertion order**

### TreeMap
- Keys in **sorted order** (uses Red-Black Tree)
- O(log n) operations

### Hashtable
- Like HashMap but **synchronized**; no null keys/values
- Legacy class

---

## 9. Sorting

### Comparable Interface
- Class sorts **itself** → implement `compareTo()`
- `java.lang` package

```java
class Student implements Comparable<Student> {
    int marks;
    public int compareTo(Student s) {
        return this.marks - s.marks; // ascending
    }
}
Collections.sort(list);
```

### Comparator Interface
- **External** sorting logic → implement `compare()`
- `java.util` package; useful for multiple sort criteria

```java
Comparator<Student> byName = (a, b) -> a.name.compareTo(b.name);
Collections.sort(list, byName);
```

> **Key Diff:** `Comparable` = natural order (modifies class); `Comparator` = custom order (external class/lambda)

---

## 10. Properties Class

- Subclass of **Hashtable**
- Stores **String key-value** pairs (config files, `.properties`)

```java
Properties p = new Properties();
p.setProperty("user", "admin");
p.setProperty("pass", "1234");
System.out.println(p.getProperty("user")); // admin
```

---

## Quick Comparison Table

| Class | Order | Duplicates | Null | Thread-Safe |
|---|---|---|---|---|
| ArrayList | Insertion | Yes | Yes | No |
| LinkedList | Insertion | Yes | Yes | No |
| HashSet | None | No | One | No |
| LinkedHashSet | Insertion | No | One | No |
| TreeSet | Sorted | No | No | No |
| HashMap | None | Keys:No | One key | No |
| TreeMap | Sorted | Keys:No | No | No |
| Hashtable | None | Keys:No | No | **Yes** |
| Vector | Insertion | Yes | Yes | **Yes** |

---

### 5 Exam-Oriented Questions & Solutions

---

**Q1. What is the difference between ArrayList and LinkedList?**

| | ArrayList | LinkedList |
|---|---|---|
| Internal | Dynamic array | Doubly linked list |
| Access | O(1) random access | O(n) |
| Insert/Delete | O(n) (shift needed) | O(1) at ends |
| Memory | Less (no node pointers) | More |

*Use ArrayList for frequent reads; LinkedList for frequent insertions/deletions.*

---

**Q2. What is the difference between Comparable and Comparator?**

- **Comparable**: `compareTo()` inside the class itself; one sort order; `Collections.sort(list)`
- **Comparator**: `compare()` in a separate class/lambda; multiple sort orders; `Collections.sort(list, comparator)`

```java
// Comparable
class Emp implements Comparable<Emp> {
    int salary;
    public int compareTo(Emp e) { return this.salary - e.salary; }
}

// Comparator
Comparator<Emp> byName = (e1, e2) -> e1.name.compareTo(e2.name);
```

---

**Q3. Difference between HashSet, LinkedHashSet, and TreeSet?**

- **HashSet** → No order, fastest, allows one null
- **LinkedHashSet** → Maintains insertion order, allows one null
- **TreeSet** → Natural/sorted order, NO null allowed, slowest (O log n)

---

**Q4. What happens when you add a duplicate key in HashMap?**

The **old value is replaced** by the new value. The key count does NOT increase.

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("x", 10);
map.put("x", 99); // replaces 10
System.out.println(map.get("x")); // 99
System.out.println(map.size());   // 1
```

---

**Q5. How do you make an ArrayList thread-safe?**

```java
// Option 1: Collections.synchronizedList
List<String> syncList = Collections.synchronizedList(new ArrayList<>());

// Option 2: Use Vector (legacy)
List<String> v = new Vector<>();

// Option 3: CopyOnWriteArrayList (best for read-heavy)
List<String> cowList = new CopyOnWriteArrayList<>();
```

---

*Good luck on your exam!*

Brought to you by Team ZenYukti

![Footer Banner for ZenYukti - MyNotes](../../footer-image.png)