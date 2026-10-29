<div id="top"></div>

# 🟢 Node.js — Quick Reference

A quick-reference stub for Node.js fundamentals. More notes will be added here as learning progresses.

<details>
<summary>Table of contents</summary>

- [Node.js Basics](#-nodejs-basics)
- [Architecture & Under the Hood](#-architecture--under-the-hood)
- [Single vs. Multi-Threading](#-single-vs-multi-threading)
- [Event Loop & Priority (The Simple Mental Model)](#-event-loop--priority-the-simple-mental-model)

</details>

---

## 🧠 Node.js Basics

* **Node.js** is a runtime environment that allows you to run JavaScript on the server side (outside the browser).
* **Express** is a web framework built on top of Node.js — makes building servers and handling HTTP requests easier.

```bash
# Initialize a new Node project
npm init
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## ⚙️ Architecture & Under the Hood

Node.js binds the **Google V8 engine** with the **libuv C++ library** to execute JavaScript asynchronously on a single main thread.

```
┌─────────────────────────────────────────────────────────┐
│                     Node.js Runtime                     │
│  ┌─────────────────────────┐   ┌─────────────────────┐  │
│  │     V8 Engine (C++)     │   │     libuv (C++)     │  │
│  │  - Call Stack           │   │  - Event Loop       │  │
│  │  - Memory Heap          │   │  - Worker Pool      │  │
│  │  - JS Code Execution    │   │  - Non-blocking I/O │  │
│  └─────────────────────────┘   └─────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### Execution Flow

```
JS Code ──> Call Stack (V8)
                 │
  ┌──────────────┴──────────────┐
  ▼ (Sync)                      ▼ (Async)
Executed immediately       Offloaded to libuv / OS
                                │
                 ┌──────────────┴──────────────┐
                 ▼                             ▼
          OS Kernel (Async)          Worker Thread Pool (libuv)
          - Network sockets (HTTP)   - File I/O (`fs`)
          - epoll / kqueue / IOCP    - Crypto (`crypto`)
                 │                   - Compression (`zlib`)
                 │                   - DNS lookup (`dns.lookup`)
                 └──────────────┬──────────────┘
                                ▼
                       Callback / Event Queues
                                │
                                ▼ (Pushed when Call Stack is empty)
                           Call Stack
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 🧵 Single vs. Multi-Threading

* **JavaScript Execution is Single-Threaded:** Only **one** Call Stack exists. All synchronous code runs sequentially on the main thread.
* **Node Runtime is Multi-Threaded:** libuv maintains a background C++ **Worker Thread Pool** (default: 4 threads, configurable via `UV_THREADPOOL_SIZE`).

| Task Category | How It Runs | Handled By | Thread Used? |
|---|---|---|---|
| **Sync JS execution** | Synchronous line-by-line | V8 Call Stack | Main thread |
| **Network I/O** (HTTP, TCP, UDP) | Non-blocking system calls | OS Kernel (`epoll` / `kqueue`) | No threads (OS async) |
| **File System** (`fs`) | Thread pool worker | libuv Worker Pool | 1 worker thread per task |
| **Crypto & Hashing** (`pbkdf2`, `scrypt`) | Thread pool worker | libuv Worker Pool | 1 worker thread per task |
| **Compression** (`zlib`) | Thread pool worker | libuv Worker Pool | 1 worker thread per task |

> ⚠️ **The Golden Rule:** *"Don't block the Event Loop."*  
> Heavy CPU work (e.g. complex regex, large JSON parsing, image processing, blocking loops) freezes the single main thread, stalling requests for all concurrent users.

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 🔄 Event Loop & Priority (The Simple Mental Model)

The Event Loop only does one job: **Wait for the Call Stack to be empty, then push queued callbacks onto it.**

### 3-Step Execution Priority

```
1. Synchronous Code  ──> Runs immediately on the Call Stack
         │ (when stack is empty)
         ▼
2. Microtask Queue   ──> High priority: Promises (`.then`), `process.nextTick`
         │ (when microtasks are drained)
         ▼
3. Macrotask Queue   ──> Low priority: `setTimeout`, `setInterval`, `setImmediate`, I/O
```

| Order | Queue Type | Examples | Rule |
|---|---|---|---|
| **1** | **Call Stack** | `console.log()`, functions, loops | Runs first; blocks everything if slow |
| **2** | **Microtasks** | `process.nextTick()`, `Promise.then()` | Runs immediately after sync code; drains completely |
| **3** | **Macrotasks** | `setTimeout()`, `setImmediate()`, I/O | Runs after microtasks finish |

### Quick Recall Code Snippet

```js
console.log("1: Sync");

setTimeout(() => console.log("4: Timeout (Macrotask)"), 0);
Promise.resolve().then(() => console.log("3: Promise (Microtask)"));
process.nextTick(() => console.log("2: nextTick (Microtask VIP)"));

// Output:
// 1: Sync
// 2: nextTick (Microtask VIP)
// 3: Promise (Microtask)
// 4: Timeout (Macrotask)
```

> 💡 **The Only 2 Things You Actually Need for Interviews:**
> 1. **Microtasks beat Macrotasks:** Promises always run before `setTimeout(..., 0)`.
> 2. **`nextTick` vs `setImmediate`:** `process.nextTick()` jumps to the front of microtasks; `setImmediate()` waits for the next macrotask cycle.

<p align="right">(<a href="#top">back to top</a>)
<hr/>
