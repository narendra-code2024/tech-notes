## Part 1: Node.js Fundamentals

### 1. Introduction to Node.js

- What is Node.js? (Event-Driven, Non-Blocking I/O)
- History (Timeline: 2009-2019)
- Overview, Node.js vs PHP
- Threading, Event Loop, npm

### 2. JS on Server

- What is a Server? (Hardware & Cloud)
- V8 JavaScript Engine, JS Engines & ECMAScript
- How Code Runs on a Machine (x86 / ARM)
- Node.js on Top of V8 (Architecture)

### 3. Let's Write Code

- First Node.js Program (using REPL)
- Running JavaScript Files with Node.js
- Global Object: `window` vs `global` vs `globalThis`

### 4. module.exports & require

- Node.js Module System (Encapsulation)
- `require()` and `module.exports`
- File Extensions & Importing Core Modules
- CommonJS (CJS) vs ES Modules (ESM)
- Nested Modules & Folder as a Module

### 5. Diving into the Node.js GitHub Repo

- IIFE (Immediately Invoked Function Expression)
- Why Module Variables Are Private
- How `require()` Works (5-Step Mechanism)

### 6. libuv & Async I/O

- Restaurant Analogy (Sync vs Async)
- Synchronous vs Asynchronous
- How Async Code Executes (V8 + libuv)
- libuv: Bridge Between Node.js and the OS

### 7. Sync, Async & setTimeout Zero

- Sync & Async Code Examples
- Blocking vs Non-Blocking I/O (`readFileSync` vs `readFile`)
- Blocking Main Thread (crypto example)
- `setTimeout(cb, 0)` Behavior

### 8. Deep Dive into V8 JS Engine

- Node.js Architecture
- Interpreted vs Compiled Languages
- V8 Code Execution Process (Parsing, JIT, Optimization)
- Garbage Collection (Orinoco, Oilpan, MCompact)

### 9. libuv Event Loop

- Event Loop Phases (Timer, Poll, Check, Close)
- Microtask Queue (`process.nextTick`, Promises)
- Node.js vs Browser Event Loop

### 10. Thread Pool in libuv

- What is a Thread Pool & When It's Used
- Default Thread Pool Size & Configuration
- Network Calls, Sockets & epoll
- Event-Driven Architecture & System Calls

### 11. Creating a Server

- How the Web Works (DNS, IP, Protocols)
- Client-Server Architecture (TCP 3-Way Handshake, HTTP)
- Streams & Buffers, URL Structure
- Creating an HTTP Server (Native `http` & Express.js)

### 12. Databases - SQL & NoSQL

- What is a Database & DBMS?
- Relational (RDBMS) vs NoSQL (Document, Key-Value, Graph)
- MongoDB & Mongoose ODM

### 13. Creating a Database with MongoDB

- MongoDB Atlas Setup (Free Tier)
- MongoDB Compass GUI
- Connecting MongoDB with Node.js
- Mongoose ODM

---

## Part 2: Building a Real-World App

### 14. Microservices vs Monolith

- Software Development Lifecycle (Roles & Phases)
- Monolith vs Microservices (Comparison Table)

### 15. Features, HLD, LLD & Planning

- Requirements & Design
- HLD: Tech Stack, Microservices, DB, Auth
- LLD: DB Design (Collections), REST API Design

### 16. Create an Express Server

- Project Initialization (`npm init`, `package.json`)
- Express.js Setup & Basics
- Semantic Versioning (`^`, `~`)
- Handling Routes with `app.use()`

### 17. Routing & Request Handlers

- Route Matching Order in Express
- `app.use()` vs `app.get()` / `app.post()`
- Route Patterns & Regex
- Query Parameters & Route Parameters

### 18. Middleware & Error Handlers

- Multiple Route Handlers & `next()`
- What is Middleware?
- Authorization Middleware
- Error Handling (4-Parameter Handler, try-catch)

### 19. Database Schema & Models (Mongoose)

- Connecting DB Before Starting Server
- Mongoose Schema & Models
- Async/Await for DB Operations

### 20. Diving into APIs

- JSON vs JavaScript Object
- `req.body` & `express.json()` Middleware

### 21. Data Sanitization & Schema Validations

- Schema-Level Validation (Mongoose)
- API-Level Validation (`validator` Package)

### 22. Encrypting Passwords

- `bcrypt` Package (Hash & Compare)

### 23. Authentication, JWT & Cookies

- JWT (JSON Web Token) — Sign & Verify
- `cookie-parser` Middleware
- Schema Methods vs Arrow Functions (`this` Keyword)

### 24. Express Router

- `express.Router()` for Modular API Routes

### 25. Logical DB Queries & Compound Indexes

- MongoDB Indexes (Single & Compound)
- When to Use & Advantages/Disadvantages

### 26. Ref, Populate & Writing APIs

- MongoDB `ref` & `populate()`
- Query Operators

### 27. Building Feed API & Pagination

- Feed API Design & Pagination
