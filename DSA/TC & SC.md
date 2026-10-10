# Time & Space Complexity — Quick Reference

> **Purpose:** Architectural reference for recursion trees and recurrence analysis.
> Memorize the mechanical laws — not the final answers.

---

## Part 1 — Common Collisions (Know These Cold)

### Collision 1: Sum vs. Multiply

Use **(work at one level) × (number of levels)** **only** when work is **identical at every level**.

> **Example:** Level 0 does $n$, Level 1 does $n$, Level 2 does $n$ → Total $= n \times \text{depth}$

If the work per level is **changing** (growing or shrinking), you must:
1. Write out the series explicitly.
2. Apply the **Geometric Progression (GP) formula**.

> **Critical Rule:** The GP formula gives the total sum of the entire tree — **you are done once you have it.**
> ❌ Never multiply the GP result by levels again — the formula already summed all levels.

---

### Collision 2: Width ($2^k$) vs. Depth ($k$) — The Axis Isolation Law

These two are driven by **entirely separate axes** of the recurrence:

| Axis | What to Look At | What it Gives You |
|------|-----------------|-------------------|
| **Vertical (Depth)** | The parameter *inside* $T(\cdots)$ | How deep the tree goes |
| **Horizontal (Width)** | The coefficient *outside* $T$ | How many nodes at level $k$ |

#### Division: $T(n) = 2T(n/2)$

- Input shrinks by dividing: $n \to \dfrac{n}{2} \to \dfrac{n}{4} \to \cdots \to \dfrac{n}{2^k}$
- Base case: $\dfrac{n}{2^k} = 1 \implies 2^k = n \implies$ **Depth $= \log_2 n$**

#### Subtraction: $T(n) = 2T(n-1)$

- Input shrinks by subtracting: $n \to n-1 \to n-2 \to \cdots \to n-k$
- Base case: $n - k = 0 \implies$ **Depth $= n$**

> **Rule:** When finding depth → look **only** at the parameter inside the parentheses.
> $2^k$ is **horizontal width** on level $k$ — it has nothing to do with depth in the $n-1$ pattern.

---

## Part 2 — The Mathematical Engine

### 2.1 Geometric Progression (GP) Sums

| Condition | Formula | Intuition |
|-----------|---------|-----------|
| **Growing** ($r > 1$) | $S = a \cdot \dfrac{r^k - 1}{r - 1}$ | Bottom of tree dominates |
| **Shrinking** ($r < 1$) | $S = a \cdot \dfrac{1 - r^k}{1 - r}$ | Top of tree dominates |
| **Infinite converging** ($r < 1$) | $S = \dfrac{a}{1 - r}$ | Total bounded by $O(a)$ — root cost |

> **Shrinking shortcut:** If work strictly decreases each level, total work is $O(\text{root node cost})$ — no need to calculate tree depth.

---

### 2.2 Logarithmic Identities

| Identity | Application |
|----------|-------------|
| $b^{\log_b(n)} = n$ | **Leaf count:** Depth $= \log_2 n$, branching $= 2$ → Leaves $= 2^{\log_2 n} = n$ |
| $a^{\log_b n} = n^{\log_b a}$ | **Change of base for leaf count** in growing GPs |

---

### 2.3 Depth Formula Reference

| Recurrence Type | Depth |
|-----------------|-------|
| $T(n/b)$ | $\log_b n$ — solves $n/b^k = 1$ |
| $T(n - c)$ | $n/c$ — solves $n - kc = 0$ |

---

## Part 3 — Execution Patterns (The Blueprint)

### Pattern 1 — Shrinking Search Space (Single Branch)

The tree has **width = 1** at every level. CPU takes one path down.

**Master Example:** $T(n) = T(n/2) + O(1)$ ← Binary Search
- Depth: $\log_2 n$ | Work/level: $1$ | **Total: $O(\log n)$**

| Recurrence | Answer | Reasoning |
|------------|--------|-----------|
| $T(n) = T(n/5) + O(1)$ | $O(\log n)$ | Log base drops asymptotically |
| $T(n) = T(n-1) + O(n)$ | $O(n^2)$ | Width $=1$, Depth $=n$, sum: $n+(n-1)+\cdots = n(n+1)/2$ |
| $T(n) = T(n/2) + O(n)$ | $O(n)$ | Shrinking GP: $n+n/2+n/4+\cdots$ converges to $2n$ |

---

### Pattern 2 — Divide and Conquer (Balanced / Growing Work)

CPU spawns a **widening tree**; input shrinks by division.

**Master Example:** $T(n) = 2T(n/2) + O(n)$ ← Merge Sort
- Width: $2^k$ | Depth: $\log_2 n$ | Work/level: $n$ (perfectly balanced) | **Total: $O(n \log n)$**

| Recurrence | Answer | Reasoning |
|------------|--------|-----------|
| $T(n) = 3T(n/2) + O(n)$ | $O(n^{\log_2 3})$ | Growing GP ($r=3/2$). Leaves $= 3^{\log_2 n} = n^{\log_2 3}$ |
| $T(n) = 8T(n/2) + O(1)$ | $O(n^3)$ | Growing GP. Leaves $= 8^{\log_2 n} = n^{\log_2 8} = n^3$ |
| $T(n) = 2T(n/2) + O(n^2)$ | $O(n^2)$ | Shrinking GP ($r=1/2$). Root node cost dominates |

---

### Pattern 3 — Exponential Attrition (Branching + Subtraction) ⚠️

CPU spawns a widening tree, but input shrinks **linearly** — the danger zone.

**Master Example:** $T(n) = 2T(n-1) + O(1)$ ← Naive Fibonacci
- Width: $2^k$ | Depth: $n$ | Work/level: $2^k$ | **Total: $O(2^n)$**

| Recurrence | Answer | Reasoning |
|------------|--------|-----------|
| $T(n) = 3T(n-1) + O(1)$ | $O(3^n)$ | Width $=3^k$, Depth $=n$. GP sum → $3^{n+1}$ |
| $T(n) = 2T(n-2) + O(1)$ | $O(2^{n/2})$ | Width $=2^k$, Depth $=n/2$ (input shrinks by 2). Leaves $= 2^{n/2}$ |
| $T(n) = T(n-1) + T(n-2) + O(1)$ | $O(2^n)$ | Lopsided tree. Left branch drives depth $=n$. Bounded by full binary tree of depth $n$ |

---

## Part 4 — Pattern Recognition Cheatsheet

> **Read the recurrence → identify the pattern → apply the right law.**

| Recurrence Form | Width | Depth | Typical Result |
|-----------------|-------|-------|----------------|
| $T(n/b) + O(1)$ | $1$ | $\log_b n$ | $O(\log n)$ |
| $T(n-1) + O(n)$ | $1$ | $n$ | $O(n^2)$ |
| $T(n/2) + O(n)$ | $1$ | $\log n$ | $O(n)$ — shrinking GP |
| $2T(n/2) + O(n)$ | $2^k$ | $\log_2 n$ | $O(n \log n)$ |
| $aT(n/b) + O(n)$, $a > b$ | $a^k$ | $\log_b n$ | $O(n^{\log_b a})$ — leaves dominate |
| $aT(n/b) + O(n)$, $a < b$ | $a^k$ | $\log_b n$ | $O(n)$ — root dominates |
| $2T(n-1) + O(1)$ | $2^k$ | $n$ | $O(2^n)$ |
| $aT(n-1) + O(1)$ | $a^k$ | $n$ | $O(a^n)$ |

---

## Part 5 — Decision Flowchart

```
Given T(n) = aT(...) + f(n)
        │
        ├─ Inside T: n/b? ──→ Depth = log_b(n)
        │           n-c? ──→ Depth = n/c
        │
        ├─ Outside T: coefficient a ──→ Width at level k = a^k
        │
        └─ Work per level: constant across all levels?
                │
                ├─ YES ──→ Multiply: (work/level) × depth
                │
                └─ NO  ──→ Is it growing (r > 1) or shrinking (r < 1)?
                            ├─ Growing  ──→ Bottom of tree dominates → leaf count
                            └─ Shrinking ──→ Top of tree dominates → root cost
```
