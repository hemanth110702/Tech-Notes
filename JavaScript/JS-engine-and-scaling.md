# JS Engine Mechanics & System Scaling — Quick Reference

---

## 1. V8 Engine & The Event Loop

JavaScript is **single-threaded** but handles concurrency by offloading heavy tasks to **libuv** (Node) / **Web APIs** (browser).

| Component | Role |
|---|---|
| **Call Stack** | Executes JS code line by line |
| **Web APIs / libuv** | Handles async tasks off-thread (timers, I/O, fetch) |
| **Microtask Queue** | High-priority — `Promise.then`, `queueMicrotask` |
| **Macrotask Queue** | Lower-priority — `setTimeout`, `setInterval`, I/O callbacks |

**Golden Rule:** The Event Loop empties the **entire Microtask Queue** before picking the next Macrotask.

```
Call Stack → (empty?) → drain Microtask Queue → pick next Macrotask → repeat
```

```js
console.log("1");
setTimeout(() => console.log("2"), 0);          // Macrotask
Promise.resolve().then(() => console.log("3")); // Microtask
console.log("4");
// Output: 1 → 4 → 3 → 2
```

---

## 2. System Architecture — Scaling a Node.js App

| Strategy | What It Does | Tool / Example |
|---|---|---|
| **Process Forking** | Run multiple Node processes on one machine | `cluster` module, PM2 |
| **Horizontal Scaling** | Deploy across multiple servers | Cloud VMs, containers |
| **Load Balancing** | Distribute incoming traffic across instances | NGINX, AWS ALB |
| **Caching** | Serve frequently-used data without hitting DB | Redis |

### Why Each Matters

- **Process Forking** — Node is single-threaded; forking lets you use all CPU cores. One process per core is typical.
- **Horizontal Scaling** — When one machine hits its limit, you add more machines instead of upgrading a single one (vertical scaling). More resilient, cheaper at scale.
- **Load Balancer (NGINX/ALB)** — Sits in front of all instances, routes each request to the least-busy server. Also handles SSL termination.
- **Redis** — In-memory store. DB queries for hot data (user sessions, leaderboards) get replaced by Redis lookups — microseconds instead of milliseconds.

---

## 3. Quick Summary

| Concept | Key Takeaway |
|---|---|
| Event Loop | Microtasks drain before Macrotasks run |
| Promise vs setTimeout | Promise wins — microtask queue has higher priority |
| Process Forking | Leverage all CPU cores on one machine |
| Horizontal Scaling | Scale out (more machines), not just up |
| NGINX / ALB | Load balancer + reverse proxy |
| Redis | In-memory cache for high-frequency reads |