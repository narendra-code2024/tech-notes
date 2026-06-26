## Phase 1: Foundations

### 1. Introduction to Java

- Java Editions
    - Java SE (Standard Edition)
    - Jakarta EE (Enterprise Edition)
    - Java ME (Micro Edition)
- Java Features

### 2. JDK, JRE & JVM

- JAR Files
- Classpath
- JVM Architecture

### 3. Java Basics

- Program Structure
    - Hello World
    - Command-Line Arguments
- Statements, Expressions & Blocks
- Identifiers & Keywords
    - Identifiers
    - Keywords
- Comments
- Packages & Imports
    - Common Standard Packages

### 4. Variables & Data Types

- Variables
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
    - `Console` Class
- Printing Output
    - `PrintStream` Class
    - `print()` and `println()`
    - Formatted Output with `printf()`

---

## Phase 2: Common Types & Error Handling

### 8. Arrays

- Multi-Dimensional Arrays
- `Arrays` Utility Class
- Array Copying
- Varargs (Variable Arguments)

### 9. Strings

- String Immutability
- String Constant Pool
- String Comparison
- `String` Methods
- String Concatenation Internals
- String vs StringBuilder vs StringBuffer
    - `StringBuilder` Methods
- Text Blocks

### 10. Numbers, Math & Random

- `java.lang.Number`
    - Subclasses of `java.lang.Number`
- `java.lang.Math`
- `java.math.BigInteger`
- `java.math.BigDecimal`
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

- Object Creation
- Attributes
    - Compile-Time vs Runtime Constants
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

- Access Modifiers
    - private
    - protected
- Getters and Setters
- final Keyword
- Mutable vs Immutable
    - Mutable
    - Immutable
- Creating an Immutable Class
- Singleton

### 14. Inheritance & Relationships

- `super` Keyword
    - Call parent constructor
    - Access parent members
- final in Inheritance
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
- Nested Interfaces and Abstract Classes
    - Nested Interfaces
    - Nested Abstract Classes

### 18. Annotations

- Built-in Annotations
- Meta-Annotations
- Custom Annotations

### 19. Object Class

- `toString()`
- `equals()`
- `hashCode()`

### 20. Enums

- Syntax & Built-in Methods
- Fields, Constructors, and Methods
- Constant-Specific Behavior
- Enums in `switch`
- `EnumSet` and `EnumMap`
- Singleton Pattern
- Real-World Patterns
    - State Machine
    - Roles / Permissions

---

## Phase 4: Collections & Generics

### 21. Generics

- Generic Class
- Generic Method
- Generic Interface
- Bounded Type Parameters
    - Upper bound (`extends`)
    - Multiple bounds (`&`)
- Wildcards (`?`)
    - Unbounded (`?`)
    - Upper bound (`? extends T`, producer)
    - Lower bound (`? super T`, consumer)
    - PECS (Producer Extends, Consumer Super)
    - Wildcard vs named type parameter
- Type Erasure
- Arrays vs Generics
    - Generic array creation
    - Generic varargs and `@SafeVarargs`

### 22. Collection Framework

- List (Ordered, Duplicates, Index-based)
    - Key Methods
- Set (No Duplicates)
    - Key Methods
- Queue & Deque
    - Queue Operations (FIFO)
    - Deque
    - PriorityQueue
- Map (Key-Value, Unique Keys)
    - HashMap Internals
    - Key Methods
    - Iterating a Map
- Iteration
    - Under the Hood
    - Iterator (Safe Removal)
    - forEach (Java 8+)
    - ListIterator (Bidirectional, List Only)
- Collections Utility Class
- Comparable vs Comparator
- Arrays and Collections Conversions
- Bulk Operations
- Fail-Fast vs Fail-Safe Iterators
- Thread-Safe Collections
- Big-O Complexity
- Quick Decision Guide

---

## Phase 5: Modern Java (Java 8+)

### 23. Functional Programming

- Functional Interfaces
    - Built-in Interfaces (java.util.function)
    - Chaining
    - Primitive Specializations
- Lambda Expressions
- Method References
- Effectively Final Variables

### 24. Streams API

- Creating Streams
- Intermediate Operations
- Terminal Operations
    - collect
    - reduce
    - Others
- Optional
- Primitive Streams
- Parallel Streams
- Common Patterns
- Short-Circuiting Operations
- Stateless vs Stateful Operations
- Best Practices

---

## Phase 6: Concurrency, I/O & Networking

### 25. Multithreading & Concurrency

- Creating Threads
    - Extend Thread
    - Implement Runnable (preferred)
    - Implement Callable (returns a result)
    - Runnable vs Callable
- Thread Lifecycle
- Essential Thread Methods
    - Daemon vs User Threads
- Synchronization
    - synchronized
- volatile
    - Visibility and the per-core cache
- wait(), notify(), notifyAll()
- Locks (java.util.concurrent.locks)
    - ReentrantLock
    - ReadWriteLock
    - synchronized vs Lock
- Atomic Classes (java.util.concurrent.atomic)
    - High-contention counters: LongAdder
- Synchronizers (java.util.concurrent)
    - CountDownLatch (wait for N tasks, one-shot)
    - CyclicBarrier (sync N threads at a point, reusable)
    - Semaphore (cap concurrent access)
- ExecutorService (Thread Pools)
    - Submitting tasks
    - Shutting down
    - ThreadPoolExecutor (production control)
- CompletableFuture (Java 8+)
    - Combining
    - Exception handling
    - join() vs get(), and async variants
- Virtual Threads (Java 21+)
- Concurrent Collections
- Common Concurrency Problems
    - Deadlock
    - Livelock, Starvation, Race Condition

### 26. File Handling

- I/O Streams
- Reading & Writing Files
    - Character Streams (text)
    - Byte Streams (binary)
    - PrintWriter (formatted text)
- Buffered Streams
- Bridge: InputStreamReader / OutputStreamWriter
- java.nio.file (Modern File API, Java 7+)
    - Path
    - Files utility class
    - Copying streams
    - Stream-based reading (Java 8+)
    - Buffered reading/writing
- File class (Legacy, java.io)
- try-with-resources for I/O
- java.io.File vs java.nio.file

### 27. Serialization

- How to Serialize
- serialVersionUID
- transient Keyword
- static Fields and Serialization
- Inheritance and Serialization
    - Serializable parent
    - Non-serializable parent
- Custom Serialization (writeObject / readObject)
- Externalizable Interface
- Serialization and Singleton
- Security
- Modern Alternatives

### 28. Java Networking

- TCP vs UDP
- InetAddress
- TCP Sockets
    - Server
    - Client
- UDP Sockets
    - Sender
    - Receiver
- HTTP Clients
    - HttpClient (Java 11+)
    - HttpURLConnection (legacy)

---

## Phase 7: Advanced Reference

### 29. Java Modern Features

- `var`, Local Variable Type Inference (Java 10)
- Switch Expressions (Java 14)
- Text Blocks (Java 15)
- Records (Java 16)
- Pattern Matching (Java 16, `instanceof`; Java 21, `switch`)
- Sealed Classes (Java 17)
- Virtual Threads (Java 21)
- Structured Concurrency (Java 21, Preview)

### 30. JVM Architecture & Memory Model

- ClassLoader Subsystem
    - Loading
    - Linking
    - Initialization
- Runtime Data Areas
    - Method Area (Metaspace, Java 8+)
    - Heap
    - Stack (per thread)
    - PC Register and Native Method Stack (per thread)
    - Memory summary
- Execution Engine
    - Interpreter
    - JIT Compiler
    - Garbage Collector
- Object Creation Flow
- Common JVM Flags
