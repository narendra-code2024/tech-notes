## Phase 1: Foundations

### 1. Introduction to Java

- Overview
- Java Editions
    - Java SE
    - Jakarta EE
    - Java ME
- Java Features
    - Object-Oriented
    - Platform Independent
    - Secured
    - Multithreaded
    - Compiled & Interpreted

### 2. JDK, JRE & JVM

- JDK vs JRE vs JVM
    - Compilation Flow
    - "Write Once, Run Anywhere"
- JAR Files
- Classpath
- JVM Architecture
    - ClassLoader Subsystem
    - Runtime Data Areas
    - Execution Engine

### 3. Java Basics

- Program Structure
    - Hello World
    - Command-Line Arguments
- Statements, Expressions & Blocks
- Identifiers & Keywords
- Comments
- Packages & Imports
    - Common Standard Packages

### 4. Variables & Data Types

- Variables
    - Declaration and Initialization
    - Scope and Lifetime
    - `final` Keyword
    - `var` Keyword (Java 10+)
- Primitive Data Types
- Literals
    - Escape Sequences
    - Underscore Separators (Java 7+)
- Wrapper Classes
- Non-Primitive Data Types

### 5. Operators & Type System

- Operators
    - Basic Operators
    - Ternary
    - Bitwise
    - Shift
    - `instanceof`
- Type Conversion
    - Typecasting
    - Type Promotion
- Boxing & Unboxing

### 6. Control Statements

- Conditional Statements
    - `if` / `if-else` / `else-if`
    - `switch` Statement
    - `switch` Expressions (Java 14+)
    - `switch` Statement vs `switch` Expression
- Iterative Statements
    - `for`
    - `while`
    - `do-while`
    - Enhanced `for-each` (Java 5+)
- Branching Statements
    - `break`
    - `continue`
    - `return`
    - Labeled Loops

### 7. Java I/O Basics

- Reading Input
    - `Scanner` Class
        - Common Scanner Methods
        - Scanner Newline Trap
        - Parsing Input with Wrapper Classes
    - `Console` Class
- Printing Output
    - `PrintStream` Class
    - `print()` and `println()`
    - Formatted Output with `printf()`

---

## Phase 2: Common Types & Error Handling

### 8. Arrays

- Declaration & Initialization
- Multi-Dimensional Arrays
- `Arrays` Utility Class
- Array Copying
- Varargs

### 9. Strings

- String Basics
- String Immutability
- String Constant Pool
- String Comparison
- `String` Methods
- String Concatenation Internals
- String vs StringBuilder vs StringBuffer
    - `StringBuilder` Methods
- Text Blocks (Java 15+)

### 10. Numbers, Math & Random

- `java.lang.Number`
- `java.lang.Math`
- `BigInteger`
- `BigDecimal`
- Number Parsing & Formatting
- Random Number Generation

### 11. Exception Handling

- Exception Hierarchy
- Checked vs Unchecked Exceptions
- try-catch-finally
    - Multiple catch blocks
    - Multi-catch (Java 7+)
- Exception Methods
- try-with-resources (Java 7+)
    - Suppressed Exceptions
    - AutoCloseable vs Closeable
- throw vs throws
- Custom Exceptions
- Exception Chaining
- Exception Handling with Inheritance

---

## Phase 3: OOP

### 12. OOP Foundations

- Class and Object
- Object Creation
- Attributes
- Methods
    - Instance vs Static Methods
- Blocks
    - Instance Block
    - Static Block
    - Execution Order
- Constructors
    - Constructor Chaining
    - Constructor vs Method
- `this` Keyword
- Four Pillars of OOP

### 13. Encapsulation & Access Control

- Encapsulation Basics
- Access Modifiers
- Getters and Setters
- Mutable vs Immutable
- Creating an Immutable Class
- Singleton

### 14. Inheritance & Relationships

- Inheritance Basics
- `super` Keyword
    - Call parent constructor
    - Access parent members
- Types of Inheritance
- Generalization and Specialization
- HAS-A

### 15. Polymorphism

- Method Overloading
    - Resolution Order
- Method Overriding
- Method Hiding
- Polymorphic Member Resolution

### 16. Abstraction & Interfaces

- Abstract Class
- Interface
- Concrete Methods in Interface
    - Default Methods
    - Static Methods
    - Private Methods
- Default Method Conflicts
- Marker Interfaces
- Class vs Abstract Class vs Interface

### 17. Nested Classes & Interfaces

- Static Nested Class
- Non-Static Inner Class
    - Non-Static Inner vs Static Nested Classes
- Local Inner Class
- Anonymous Inner Class
    - Anonymous Class vs Lambda
- Nested Interfaces
- Nested Abstract Classes

### 18. Annotations

- Built-in Annotations
- Meta-Annotations
- Custom Annotations

### 19. Object Class

- Object Methods
- `toString()`
- `equals()`
    - `==` vs `.equals()`
- `hashCode()`

### 20. Enums

- Declaration & Basics
- Built-in methods (`values()`, `valueOf()`, `name()`, `ordinal()`)
- Enums with Fields, Constructors, and Methods
- Abstract Methods per Constant (Strategy Pattern)
- Implementing Interfaces
- Enums in `switch` (including pattern matching in Java 21+)
- `EnumSet` and `EnumMap` (high-performance collections)
- Enum as Singleton (Effective Java pattern)
- Real-World Patterns (state, roles/permissions, feature flags, log levels)

---

## Phase 4: Collections & Generics

### 21. Generics

- Generic Class
- Generic Method
- Bounded Type Parameters (upper bound `extends`, multiple bounds with `&`)
- Wildcards (`?`, `? extends T`, `? super T`)
    - PECS, Producer Extends, Consumer Super
- Wildcards vs Bounded Type Parameters
- Type Erasure
- Arrays vs Generics (Covariance vs Invariance)
    - Generic Array Creation Restriction
    - Generic Varargs and `@SafeVarargs`
- Generic Interface
- Generic Constructor

### 22. Collection Framework

- Hierarchy Overview
- List (`ArrayList`, `LinkedList`, `Vector`, `Stack`)
- Set (`HashSet`, `LinkedHashSet`, `TreeSet`)
- Queue & Deque (`PriorityQueue`, `ArrayDeque`)
- Map (`HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable`, `ConcurrentHashMap`)
    - `HashMap` Internal Working
- Iteration Techniques (`Iterator`, for-each, `forEach()`, `ListIterator`)
- `Collections` Utility Class (sort, reverse, shuffle, fill, binarySearch)
- `Comparable` vs `Comparator`
- Arrays ↔ Collections Conversions
- Bulk Operations (`addAll`, `removeAll`, `retainAll`, `removeIf`)
- Fail-Fast vs Fail-Safe Iterators
- Thread-Safe Collections (`ConcurrentHashMap`, `CopyOnWriteArrayList`, `BlockingQueue`)
- Big-O Cheat Sheet
- Quick Decision Guide

---

## Phase 5: Modern Java (Java 8+)

### 23. Functional Programming (Java 8+)

- Functional Interfaces
    - Built-in (`Predicate`, `Function`, `Consumer`, `Supplier`, Bi/Unary/Binary variants)
    - Chaining Functional Interfaces
    - Primitive Specialized Functional Interfaces (`IntPredicate`, `LongFunction`, etc.)
- Lambda Expressions
- Method References (static, instance-specific, instance-any, constructor)
- Effectively Final Variables

### 24. Streams API (Java 8+)

- Creating Streams (`stream()`, `of()`, `generate()`, `iterate()`)
- Intermediate Operations (`filter`, `map`, `flatMap`, `sorted`, `distinct`, `limit`, `skip`)
- Terminal Operations (`collect`, `forEach`, `reduce`, `count`, `findFirst`, `anyMatch`)
- Optional (Companion to Streams)
- Primitive Streams (`IntStream`, `LongStream`, `DoubleStream`)
- Parallel Streams
- Common Stream Patterns
- Stream Pipeline Order Matters
- Short-Circuiting Operations
- Stateless vs Stateful Operations
- Stream Best Practices

---

## Phase 6: Concurrency, I/O & Networking

### 25. Multithreading & Concurrency

- Creating Threads (`Thread`, `Runnable`, `Callable`)
- Thread Lifecycle (NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED)
- Essential Thread Methods (`start`, `sleep`, `join`, `interrupt`, `yield`)
    - Daemon vs User Threads
- Synchronization, `synchronized` Keyword
- `volatile` Keyword
- `wait()`, `notify()`, `notifyAll()`
- Locks (`ReentrantLock`, `ReadWriteLock`)
- Atomic Classes (`AtomicInteger`, `LongAdder`, `LongAccumulator`)
- Synchronizers (`CountDownLatch`, `CyclicBarrier`, `Semaphore`)
- ExecutorService (Thread Pools)
    - `ThreadPoolExecutor` (production-grade)
- `CompletableFuture` (Java 8+)
- Virtual Threads (Java 21+)
- Concurrent Collections
- Common Concurrency Problems (Deadlock, Livelock, Starvation, Race Condition)

### 26. File Handling

- I/O Streams (byte vs character)
- Reading & Writing Files
    - Character Streams (`FileReader`, `FileWriter`, `PrintWriter`)
    - Byte Streams (`FileInputStream`, `FileOutputStream`)
- Buffered Streams (`BufferedReader`, `BufferedWriter`)
- `java.nio.file` (Modern File API, Java 7+)
    - `Path` and `Paths`
    - `Files` Utility Class (`readString`, `readAllLines`, `write`, `copy`, `move`, `delete`)
    - Stream-based File Reading (`Files.lines`, `Files.walk`)
    - Modern Buffered Reading/Writing (`Files.newBufferedReader`, `Files.newBufferedWriter`)
- `File` class (Legacy, `java.io`)
- `try-with-resources` for I/O
- `InputStreamReader` / `OutputStreamWriter` (Bridge)
- Common I/O Patterns
- `java.io.File` vs `java.nio.file`

### 27. Serialization

- How to Serialize (`Serializable`, `ObjectOutputStream`, `ObjectInputStream`)
- `serialVersionUID`
- `transient` Keyword (excluding fields from serialization)
- `static` Fields and Serialization
- Inheritance and Serialization
- Custom Serialization (`writeObject()`, `readObject()`)
- `Externalizable` Interface
- Serialization and Singleton (`readResolve`, enum singleton)
- Modern Alternatives (JSON, Protobuf, Avro, Kryo)

### 28. Java Networking

- `java.net` Package Overview
- `InetAddress`
- TCP Sockets (`Socket`, `ServerSocket`)
- UDP Sockets (`DatagramSocket`, `DatagramPacket`)
- `URL` and `HttpURLConnection` (legacy)
- Modern HTTP Client (Java 11+), `java.net.http.HttpClient`

---

## Phase 7: Advanced Reference

### 29. Java Modern Features

- Local Variable Type Inference (`var`)
- Records
- Pattern Matching for `instanceof`
- Sealed Classes
- Virtual Threads
- Structured Concurrency
- Text Blocks
- Switch Expressions

### 30. JVM Architecture & Memory Model

- ClassLoader Subsystem
    - Loading (Bootstrap, Extension/Platform, Application/System)
    - Linking (Verification, Preparation, Resolution)
    - Initialization
    - Parent-first delegation model
- Runtime Data Areas (Memory)
    - Method Area / Metaspace (class metadata, static vars)
    - Heap
        - Young Generation (Eden, Survivor S0/S1)
        - Old Generation
        - String Constant Pool (in Heap since Java 7)
    - Stack (per thread, local vars, frames)
    - PC Register (per thread)
    - Native Method Stack (per thread)
- Execution Engine
    - Interpreter vs JIT
    - Tiered Compilation (C1 + C2)
    - Garbage Collector
        - Reachability analysis from GC Roots
        - GC types: Serial, Parallel, G1 (default Java 9+), ZGC (Java 15+)
        - Minor GC vs Major/Full GC
        - Stop-The-World pauses
        - `System.gc()` is a hint, `finalize()` deprecated
- Object Creation Flow (class load → heap alloc → default init → constructor → stack reference)
- String Memory (literal pool vs `new String(...)`)
- JVM Flags (`-Xms`, `-Xmx`, `-Xss`, GC selection, heap dump on OOM)
- Technical Notes
    - Stack vs Heap confusion
    - PermGen vs Metaspace
    - `OutOfMemoryError` variants (heap, metaspace, native thread, GC overhead)
    - JIT warmup
    - Memory leak causes

