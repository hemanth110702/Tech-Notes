<div id="top"></div>

# Analysis of Algorithms Part-1

## Topics

  -   [The Role of Algorithm](./Analysis%20of%20Algorithms%20Part-1.md#the-role-of-algorithm)
  -   [Asymptotic Complexity](./Analysis%20of%20Algorithms%20Part-1.md#asymptotic-complexity)
  -   [Asymptotic NOtation & Growth of Functions](./Analysis%20of%20Algorithms%20Part-1.md#asymptotic-notation-growth-of-functions)
  -   [Comparing of two functions](./Analysis%20of%20Algorithms%20Part-1.md#comparing-of-two-functions)
  -   [Order of Growth](./Analysis%20of%20Algorithms%20Part-1.md#order-of-growth)

## The Role of Algorithm 

### Factors Affecting Program Performance

1.  **Data Structures & Algorithms (DS & Algo)**
2.  **Hardware (H/W)**: e.g., desktop vs. desktop
3.  **Compiler**: e.g., 4-6 cycle optimization
4.  **Operating System (OS)**: e.g., how it links system libraries
5.  **Programming Language (Prog. Lang)**: e.g., Microsoft Visual C++ vs. GCC

> **Note:** Items 2-5 are considered secondary factors. None of these give a 100 times better result for program performance.

### The Power of Algorithms

A good algorithm can make a significant difference in performance.

* **Merge Sort:** Has a time complexity of $O(n \log n)$.
* **Insertion Sort:** Has a time complexity of $O(n^2)$.

**Calculation of Speedup:**

* Merge Sort Speedup = $\frac{O(n^2)}{O(n \log n)} = \frac{n}{\log n}$

* **For an input size $n = 1000$:**
    * Speedup = $\frac{1000}{\log_2(1000)} \approx \frac{1000}{10} \approx 100$

This shows that Merge Sort is approximately **100 times faster** than Insertion Sort for an input size of 1000, highlighting the importance of choosing the right algorithm.

---

## Asymptotic Complexity

<img width="1132" height="406" alt="cycles" src="https://github.com/user-attachments/assets/8b969d96-16a8-4f2f-a767-37db7f2384cc" />

* **Limitations of Asymptotic Notation**
    * We don't account for **memory** and **caching**.
    * We assume all operations take the same amount of time in our **model**.
    * We ignore **constants** and **lower-order terms** because they become insignificant for large input sizes.
        * **Example:** For a function $t(n) = 4n^2 + 6n + 16$, the term $4n^2$ will dominate as $n$ becomes large. Therefore, the complexity is $O(n^2)$.

* **Real-world Performance Example**
    * A 1-GHz processor can perform **$10^9$ cycles per second**.
    * Assuming an average operation takes 10 cycles, the processor can execute $\frac{10^9}{10} = 10^8$ operations per second.
    * **Case 1: $O(n)$ algorithm**
        * For an input size $n = 10^5$, the time taken is $\frac{10^5 \text{ operations}}{10^8 \text{ ops/sec}} = 10^{-3} \text{ seconds}$, or 1 millisecond.
    * **Case 2: $O(n^2)$ algorithm**
        * For an input size $n = 10^5$, the number of operations is $(10^5)^2 = 10^{10}$.
        * The time taken is $\frac{10^{10} \text{ operations}}{10^8 \text{ ops/sec}} = 10^2 \text{ seconds}$, or **100 seconds**.
        * This demonstrates why an asymptotically worse algorithm can become impractical for large inputs, even on a fast machine.



* **Consider an $O(2^n)$ exponential algorithm running on a machine that can execute $10^8$ operations/second.**

    ### Some Terms to Remember

    * **1K** = $2^{10} \approx 10^3$
    * **1M** = $2^{20} \approx 10^6$
    * **1G** = $2^{30} \approx 10^9$

    * **For $n = 50$:**
        * Time taken, $t = \frac{\text{no. of ops}}{\text{speed}} = \frac{2^{50}}{10^8}$
        * $\frac{2^{50}}{10^8} = \frac{(10^3)^5}{10^8} = \frac{10^{15}}{10^8} = 10^7 \text{ seconds}$
        * $10^7 \text{ seconds} \approx 0.317$ years

    * **For $n = 100$:**
        * Time taken, $t = \frac{2^{100}}{10^8} = \frac{2^{50} \cdot 2^{50}}{10^8} = \frac{2^{50}}{10^8} \cdot 2^{50} \approx 0.317 \text{ years} \cdot 2^{50}$
        * $2^{50}$ is an incredibly large number, so the time taken would be billions of years, even on a supercomputer.

* This demonstrates that even with a significant increase in hardware speed, for a highly inefficient algorithm, the increase in input size from 50 to 100 makes the problem practically unsolvable. Therefore, **we need to use efficient algorithms.**

### Problem Solving Example

**Problem:**

* Consider an algorithm with an asymptotic complexity of $O(n^2)$.
* If the algorithm takes 3 seconds to process an input of size $10^4$, how much time will it take to process an input of size $10^5$ on the same machine?

**Hint:**
* $Time = \frac{\text{no. of ops}}{\text{speed}}$

**Solution:**

* Let $t_1$ be the time taken for input size $n_1$, and $t_2$ be the time for input size $n_2$.
* We know that the number of operations for an $O(n^2)$ algorithm is proportional to $n^2$. Let the speed of the machine be constant.

* $t_1 = \frac{n_1^2}{\text{speed}}$  (1)
* $t_2 = \frac{n_2^2}{\text{speed}}$  (2)

* **By dividing equation (2) by (1), we get:**
    * $\frac{t_2}{t_1} = \frac{n_2^2 / \text{speed}}{n_1^2 / \text{speed}} = \left(\frac{n_2}{n_1}\right)^2$

* **Now, substitute the given values:**
    * $t_2 = \left(\frac{n_2}{n_1}\right)^2 \times t_1$
    * $t_2 = \left(\frac{10^5}{10^4}\right)^2 \times 3 \text{ seconds}$
    * $t_2 = (10)^2 \times 3 \text{ seconds}$
    * $t_2 = 100 \times 3 \text{ seconds}$
    * $t_2 = 300 \text{ seconds}$

**Answer:** It will take **300 seconds** (or 5 minutes) to process the larger input.

<p align="right"><a href="#top">⬆️ Back to Top</a></p>

---

## Asymptotic NOtation & Growth of Functions

* **Lucky - Best Case:** Input already sorted
    * $T_{BC}(n) = \theta(n)$
* **Unlucky - Worst Case:** Input sorted in reverse order
    * **Lower Bound:** Order $n$
        * $T(n) = \Omega(n)$
    * **Upper Bound:** Order $n^2$
        * $T(n) = O(n^2)$
    * **Tight Bound:** Order $n^2$
        * $T(n) = \frac{n(n-1)}{2} = \theta(n^2)$

* $O$: upper bound $\le$
* $\Omega$: lower bound $\ge$
* $\theta$: tight asymptotic bound $=$
* $O$:** exclusive upper bound $<$
* $\omega$: exclusive lower bound $>$

---

## Comparing of two functions

Given two functions $f(n)$ and $g(n)$:

### Case-1

* **If $\lim_{n\to\infty} \frac{f(n)}{g(n)} = \text{zero}$:**
    * $f(n) = o(g(n))$ [most precise] - implicits $f(n) < o(g(n))$
    * $g(n) = \omega(f(n))$ [most precise] - implicits$g(n) $>$ (f(n))$ 
    * $f(n) = O(g(n))$   - implicits $f(n) \le (g(n))$
    * $g(n) = \Omega(f(n))$ - implicits $g(n) \ge (f(n))$

    #### Example

    **Given two functions:** $f(n) = n$ and $g(n) = 2n^2$

    **The limit as $n$ approaches infinity:**
    $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \lim_{n \to \infty} \frac{n}{2n^2} = \lim_{n \to \infty} \frac{1}{2n} = 0$


    Since the limit is zero, it implies that $f(n)$ grows strictly slower than $g(n)$. Therefore, the following relationships hold:

    * **$f(n) = o(g(n))$**
        * This is the most precise answer. It states that $f(n)$ is a "little-o" of $g(n)$, meaning $f(n)$ grows strictly slower than $g(n)$.

    * **$g(n) = \omega(f(n))$**
        * This is also a precise answer. It states that $g(n)$ is a "little-omega" of $f(n)$, meaning $g(n)$ grows strictly faster than $f(n)$.

    * **$f(n) = O(g(n))$**
        * This is a correct, but less precise, answer. The Big-O notation indicates that $f(n)$ grows at a rate that is less than or equal to $g(n)$, which is true since it grows strictly slower.

    * **$g(n) = \Omega(f(n))$**
        * This is also a correct, but less precise, answer. The Big-Omega notation indicates that $g(n)$ grows at a rate that is greater than or equal to $f(n)$, which is true since it grows strictly faster.

### Case-2

* **If $\lim_{n\to\infty} \frac{f(n)}{g(n)} = k$ (a non-zero constant):**
    * $f(n) = \theta(g(n))$ [most precise] - implicits $f(n) = (g(n))$ 
    * $f(n) = O(g(n))$ [ precise ]
    * $f(n) = \Omega(g(n))$ [ precise ]

    #### Example

    **Given two functions:** $f(n) = n^2$ and $g(n) = 4n^2$

    **The limit as $n$ approaches infinity:**
    $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \lim_{n \to \infty} \frac{n^2}{4n^2} = \frac{1}{4}$

    Since the limit of $\frac{f(n)}{g(n)}$ as $n$ approaches infinity is a non-zero constant, it implies that both functions grow at the same rate. Therefore, the following relationships hold:

    * **$f(n) = \theta(g(n))$**
        * This is the **most precise** answer. The Big-Theta notation signifies that $f(n)$ and $g(n)$ have the same asymptotic growth rate, meaning they are tightly bound to each other.

    * **$f(n) = O(g(n))$**
        * This is also a correct answer. The Big-O notation indicates that $f(n)$ grows at a rate that is less than or equal to $g(n)$, which is true since they grow at the same rate.

    * **$f(n) = \Omega(g(n))$**
        * This is also a correct answer. The Big-Omega notation indicates that $f(n)$ grows at a rate that is greater than or equal to $g(n)$, which is also true since they grow at the same rate.

### Case-3

* **If $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty$**:
    * $f(n) = \omega(g(n))$
    * $g(n) = o(f(n))$
    * $f(n) = \Omega(g(n))$
    * $g(n) = O(f(n))$

<p align="right"><a href="#top">⬆️ Back to Top</a></p>

---

## Order of Growth

<img width="337" height="246" alt="oog graph" src="https://github.com/user-attachments/assets/46b3f62a-c0f0-4e48-8684-fc3d1f7ae6fd" />

<img width="673" height="682" alt="oog final" src="https://github.com/user-attachments/assets/5bdb8736-254b-4f6d-807f-51a92bd3fa42" />

---

## Asymptotic Complexity - Examples

### Example-1
```c
for (i = 3; i <= n; i++)
    op;                     
```
$$T(n)= $\theta(n)$$
(step is constant)

### Example-2 
```c
for (i = 3; i <= 2*n(bound); i++)
    op;                     
```
$$T(n) = \theta(n)$$ 
(step is constant)

### Example-3
```c
for (i = 3; i <= n; i*=2 (Step)) 
    op;                     
```
$$x = \log_2 n + 1$$
$$T(n) = \theta(\log n)$$
(step is not constant, it grows)

### Example-4
```c
for (i = 3; i <= n; i+=2) 
    op;                     
```
$$T(n) = \theta(n) $$
(step is constant)

### 📝 Note on Logarithm Base in Asymptotic Notation

**Core Principle:** In Asymptotic Notation ($O, \Omega, \theta$), the base of the logarithm is **not required** and is conventionally dropped.

**Mathematical Proof (Change of Base Formula):**
The change of base formula for logarithms is:
$$\log_a x = \frac{\log_b x}{\log_b a}$$

**Application to Complexity:**
If we have an algorithm running in $O(\log_2 n)$ time, and we want to change the base to $10$:
$$\log_2 n = \frac{\log_{10} n}{\log_{10} 2}$$

Since $\log_{10} 2$ is a **constant** value (approximately 0.301), the expression becomes:
$$\log_2 n = (\text{Constant}) \times \log_{10} n$$

In asymptotic analysis, we discard all constant factors. Therefore, $O(\log_2 n)$ is equivalent to $O(\log_{10} n)$, and both are simply written as $O(\log n)$.


### Example - 5
```c
for (i=1 ; i<=n ; i++)  // -> θ(n)
    for (j=1 ; j<=10 ; j++)  // -> θ(1)
        if (cond)
            op
        else
            break
```
$$T(n)  = \theta(n) \times \theta(1) = \theta(n)$$

### Example - 6
```c
for (i=1 ; i<=n ; i++)  // -> θ(n)
    for (j=1 ; j<=n*n ; j++)  // -> θ(n^2)
        if (cond)
            op
        else
            break
```
$$T(n) = \theta(n) \times \theta(n^2) = \theta(n^3)$$

### Example - 7
```c
for (i=1 ; i<=n ; i++)  // -> θ(n)
    for (j=i ; j<=i+3 ; j++)  // -> θ(4) -> θ(1)
        if (cond)
            op
```
$$T(n) = \theta(n) \times \theta(1) = \theta(n)$$

### Example - 8
```c
for (i=1 ; i<=n ; i++)  // -> θ(n)
    for (j=1 ; j<=n*n ; j*=2)  // -> θ(log_2 n^2)
        if (cond)
            op
        else
            break
```
$$\log_2 n^2 = 2 \log_2 n = \theta(\log n)$$
$$T(n) = \theta(\log n) \times \theta(n) = \theta(n \log n)$$

### Example - 9
```c
// Section 1: Nested Loops
for (i=1 ; i<=n ; i++) 
    for (j=1 ; j<=n ; j+=5)
        op
// Section 2: Sequential Loop
for (k=1 ; k<=n/2 ; k++)
    op
```
$$T(n) = \theta(n^2) + \theta(n) = \theta(n^2)$$

### Example - 10
### Problem Solving Example (Re-visiting $O(n^2)$)

**Problem:**

* Consider an algorithm with an asymptotic complexity of $\theta(n^2)$.
* If the algorithm takes **3 seconds** to process an input of size **$10^4$**, how much time will it take to process an input of size **$10^5$** on the same machine?

**Core Principle:**
$$ \text{Time} = \frac{\text{# of ops}}{\text{speed}} $$

**Setup (Since $\text{speed}$ is constant):**

1.  $$ t_1 = \frac{n_1^2}{\text{speed}} \quad (1) $$
2.  $$ t_2 = \frac{n_2^2}{\text{speed}} \quad (2) $$

**Calculation (Divide (2) by (1)):**

$$ \frac{t_2}{t_1} = \frac{n_2^2}{n_1^2} = \left(\frac{n_2}{n_1}\right)^2 $$

**Substituting values:**

$$ t_2 = t_1 \times \left(\frac{n_2}{n_1}\right)^2 $$
$$ t_2 = 3 \text{ seconds} \times \left(\frac{10^5}{10^4}\right)^2 $$
$$ t_2 = 3 \times (10)^2 $$
$$ t_2 = 3 \times 100 $$
$$ t_2 = 300 \text{ seconds} $$

### Example - 11
### Asymptotic Comparison of $f(n)$ and $g(n)$

**Given Functions:**

* $f(n) = n^2 + n + 5$
* $g(n) = 5n^3 + 2$

**Analysis:**

As $n$ approaches infinity, the term with the highest exponent dominates.
* For $f(n)$, the dominant term is $n^2$.
* For $g(n)$, the dominant term is $5n^3$.

Since $n^3$ grows asymptotically larger than $n^2$, $g(n)$ is asymptotically larger than $f(n)$.

$$\lim_{n\to\infty} \frac{f(n)}{g(n)} = \lim_{n\to\infty} \frac{n^2}{5n^3} = \lim_{n\to\infty} \frac{1}{5n} = 0$$

Since the limit is **zero**, the following asymptotic relationships hold:

| Relationship | Notation | Implication |
| :--- | :--- | :--- |
| **$f(n)$ is Little-o of $g(n)$** | $f(n) = o(g(n))$ | $f(n)$ is **strictly less than** $g(n)$ |
| **$f(n)$ is Big-O of $g(n)$** | $f(n) = O(g(n))$ | $f(n)$ is **less than or equal to** $g(n)$ |
| **$g(n)$ is Little-omega of $f(n)$** | $g(n) = \omega(f(n))$ | $g(n)$ is **strictly greater than** $f(n)$ |
| **$g(n)$ is Big-Omega of $f(n)$** | $g(n) = \Omega(f(n))$ | $g(n)$ is **greater than or equal to** $f(n)$ |


# Worksheet 1.1: Growth of Functions and Run-Time Estimation

## Question 1: Asymptotic Relations

**Question 1:** For each pair of functions below, first determine which function grows asymptotically faster, and then express the relation between the two functions using all the asymptotic notations (θ, O, Ω, o and ω) that apply. Only give the relations in which f(n) appears on the left-hand side. Justify your answer, and use the limit definition if necessary.                                       
1) $f(n) = n^2 + (\log n)^3$ vs. $g(n) = n^2 \log n$
No justification is required                                                 

2) $f(n) = 4^n$ vs. $g(n) = 3^n + n$   
Justify your answer using the limit definition. Show your work.

### (1) $f(n) = n^2 + (\log n)^3$ vs. $g(n) = n^2 \log n$

**Justification:** We compare the highest-order terms of the functions.
* $f(n)$'s dominant term is $n^2$.
* $g(n)$'s dominant term is $n^2 \log n$.

Since $\log n$ grows slower than any positive polynomial, but faster than $O(1)$, $n^2 \log n$ is asymptotically larger than $n^2$.

$$\lim_{n\to\infty} \frac{f(n)}{g(n)} = \lim_{n\to\infty} \frac{n^2 + (\log n)^3}{n^2 \log n} = \lim_{n\to\infty} \left(\frac{1}{\log n} + \frac{(\log n)^2}{n^2}\right) = 0$$

Since the limit is **zero**, $g(n)$ grows strictly faster than $f(n)$.

**Conclusion:** **$g(n)$ grows asymptotically faster.**

| Notation | Relation | Implication |
| :--- | :--- | :--- |
| **Little-o (o)** | $f(n) = o(g(n))$ | $f(n)$ grows strictly slower than $g(n)$ (Most precise) |
| **Big-O (O)** | $f(n) = O(g(n))$ | $f(n)$ is bounded above by $g(n)$ |

### (2) $f(n) = 4^n$ vs. $g(n) = 3^n + n$

**Justification:** We must use the limit definition as the base of the exponential term is different.

$$\lim_{n\to\infty} \frac{f(n)}{g(n)} = \lim_{n\to\infty} \frac{4^n}{3^n + n}$$

We can simplify the fraction by dividing the numerator and denominator by the highest-growing term in the denominator, which is $3^n$:

$$= \lim_{n\to\infty} \frac{(4/3)^n}{1 + n/3^n}$$

We know that:
* $\lim_{n\to\infty} (4/3)^n = \infty$ (since $4/3 > 1$)
* $\lim_{n\to\infty} \frac{n}{3^n} = 0$ (exponentials grow faster than polynomials)

$$= \frac{\infty}{1 + 0} = \infty$$

Since the limit is **infinity**, $f(n)$ grows strictly faster than $g(n)$.

**Conclusion:** **$f(n)$ grows asymptotically faster.**

| Notation | Relation | Implication |
| :--- | :--- | :--- |
| **Little-omega ($\omega$)** | $f(n) = \omega(g(n))$ | $f(n)$ grows strictly faster than $g(n)$ (Most precise) |
| **Big-Omega ($\Omega$)** | $f(n) = \Omega(g(n))$ | $f(n)$ is bounded below by $g(n)$ |

---

## Question 2: Possible Running Time $T(n)$

**Question 2:** If we know that the running time T(n) of some algorithm satisfies the relations:
$T(n) = o(n^{2.5} \log n)$ and $T(n) = \Omega(n (\log n)^3)$, 
which of the following functions can T(n) possibly be? Circle all that apply.                                                                                                                                                                                  
* $n^{2.5} \log n$
* $n (\log n)^3$
* $n(\log n)^5$
* $n^{1.01}$
* $n^{2.6}$
                 

If $T(n)$ satisfies the relations: $T(n) = o(n^{2.5} \log n)$ and $T(n) = \Omega(n (\log n)^3)$.

This means $T(n)$ must satisfy:
1.  **Upper Bound (Strictly Less Than):** $T(n)$ must grow strictly slower than $n^{2.5} \log n$.
2.  **Lower Bound (Greater Than or Equal To):** $T(n)$ must grow at a rate equal to or faster than $n (\log n)^3$.

Let $T_{UB} = n^{2.5} \log n$ and $T_{LB} = n (\log n)^3$.

| Candidate Function | Comparison with $T_{UB}$ ($< T_{UB}$?) | Comparison with $T_{LB}$ ($\ge T_{LB}$?) | Result |
| :--- | :--- | :--- | :--- |
| **$n^{2.5} \log n$** | No (Grows at the same rate: $T(n) \not< T_{UB}$) | Yes | Fails $o()$ constraint |
| **$n (\log n)^3$** | Yes | Yes (Grows at the same rate: $T(n) = T_{LB}$) | **Possible** |
| **$n (\log n)^5$** | Yes | Yes (Grows faster than $T_{LB}$) | **Possible** |
| **$n^{1.01}$** | Yes | Yes (Grows faster than $T_{LB}$) | **Possible** |
| **$n^{2.6}$** | No (Grows faster than $T_{UB}$) | Yes | Fails $o()$ constraint |

**Possible Functions:** $n (\log n)^3$, $n (\log n)^5$, $n^{1.01}$

---

## Question 3: Machine Speed Comparison

**Question 3:** Consider two algorithms for solving a certain problem: Algorithm X with an asymptotic complexity of θ(n2logn) and Algorithm Y with an asymptotic complexity of θ(n3). Algorithm X is run on a machine that can execute 107 operation per second. Compute the speed of the machine that we need to run Algorithm Y on in order to get the same execution time as Algorithm X for an input of size one million. Assume base 2 for the log. Compute the best possible approximation without using a calculator. Show your work


We need to find the speed of the machine running Algorithm Y ($S_Y$) such that the execution time is the same as Algorithm X ($t_X = t_Y$) for input $n = 10^6$.

### Given Information

* Input size: $n = 1,000,000 = 10^6$
* Algorithm X Complexity: $T_X(n) = \theta(n^2 \log_2 n)$
* Algorithm Y Complexity: $T_Y(n) = \theta(n^3)$
* Machine X Speed: $S_X = 10^7$ operations/second

### Step 1: Approximate $\log_2 n$

For $n = 10^6$:
$$\log_2(10^6) = \log_2((10^3)^2) = 2 \log_2(10^3)$$

We use the common approximation: $2^{10} \approx 10^3$.
Therefore, $\log_2(10^3) \approx 10$.

$$ \log_2(10^6) \approx 2 \times 10 = 20 $$

### Step 2: Set Execution Times Equal

The time taken is $t = \frac{\text{Ops}}{\text{Speed}}$. Since $t_X = t_Y$:
$$ \frac{\text{Ops}_X}{\text{Speed}_X} = \frac{\text{Ops}_Y}{\text{Speed}_Y} $$

We are using the dominant terms for operations:
$$ \frac{n^2 \log_2 n}{S_X} = \frac{n^3}{S_Y} $$

### Step 3: Solve for $S_Y$

$$ S_Y = S_X \times \frac{n^3}{n^2 \log_2 n} $$
$$ S_Y = S_X \times \frac{n}{\log_2 n} $$

### Step 4: Substitute Values

$$ S_Y \approx 10^7 \times \frac{10^6}{20} $$

### Step 5: Final Calculation

$$ S_Y \approx 10^7 \times \frac{10^6}{2 \times 10} $$
$$ S_Y \approx 10^7 \times \frac{1}{2} \times 10^5 $$
$$ S_Y \approx 0.5 \times 10^{12} $$
$$ S_Y \approx 5 \times 10^{11} \text{ operations/second} $$

**Answer:** The machine running Algorithm Y must have a speed of approximately **$5 \times 10^{11}$ operations/second** (or 500 Giga-operations/second).

---


# Worksheet 1.2: Lecture 4 — Asymptotic Complexity

Find the asymptotic complexity of each of the following algorithms. Assume that the input size is n and that Op is a constant-time operation. Show your analysis. If it is possible to analyze each loop separately, you must give the asymptotic complexity for each loop, and then show how you combine them to compute the asymptotic complexity for the whole algorithm.                                                     

**Notation / assumptions**
- `Op` is a constant-time operation.  
- `log n` means logarithm in any constant base (Θ same).  
- **Assumption:** in the first algorithm the missing bound `for (j=1; j< ; j*=4)` is assumed to be `for (j=1; j < n; j*=4)`.

---

## (1)
```c
for (i=1; i < n/2; i+=3) {
    for (j=1; j < n; j*=4)      // assumed j < n
        Op;
    for (k=3; k < n*n; k+=2)
        for (m=k-2; m <= k+2; m++)
            Op;
}
```

**Analysis:**
- Outer `i` loop → Θ(n).  
- Inner `j` loop → Θ(log n).  
- `k` loop → Θ(n²).  
- `m` loop → Θ(1).  
- `k`–`m` pair → Θ(n²).  
- Per `i` iteration → Θ(n²).  
- Total = Θ(n³).

**Answer:** **Θ(n³)**.

---

## (2)
```c
for (i=1; i < 4*n; i+=2) {
    for (j=i+5; j >= i; j--)
        Op;
}
for (k=1; k < n*n*n; k*=5) {
    for (m=1; m < logn; m++)
        Op;
}
```

**Analysis:**
- First double loop: `i` → Θ(n), `j` → Θ(1) ⇒ Θ(n).  
- Second double loop: `k` → Θ(log n), `m` → Θ(log n) ⇒ Θ((log n)²).  
- Sequential total: Θ(n) + Θ((log n)²) = Θ(n).

**Answer:** **Θ(n)**.

---

## (3)
```c
for (i=3; i < n; i++) {
    for (j=i; j <= 2*n; j++)
        Op;
}
```

**Exact formula:**
\[
T(n) = \sum_{i=3}^{n-1} (2n - i + 1)
= \frac{3n^2 - 9n}{2}.
\]

**Asymptotic:** leading term \(\tfrac{3}{2}n^2\) ⇒ Θ(n²).

**Answer:** Exact \(T(n)=\tfrac{3n^2-9n}{2}\), asymptotic = **Θ(n²)**.

---

## (4) InsertionSort on Alternating Input
Array of size `n` (even):  
`<3, 8, 3, 8, … , 3, 8>`

```c
InsertionSort(A, n) {
  for (i=1; i < n; i++) {
    key = A[i];
    for (j=i-1; j>=0 && A[j] > key; j--)
       A[j+1] = A[j];
    A[j+1] = key;
  }
}
```

**Pattern:**
- Odd `i` (keys = 8) → 0 shifts.  
- Even `i=2t` (keys = 3) → exactly `t` shifts.  

**Total shifts:**
\[
1+2+3+...+(n/2 - 1) = \frac{n^2 - 2n}{8}.
\]

**Total comparisons:**
\[
\frac{n^2}{8} + \frac{3n}{4} - 1.
\]

**Asymptotic runtime:** Θ(n²).

**Answer:**  
- Shifts = \(\dfrac{n^2 - 2n}{8}\).  
- Comparisons = \(\dfrac{n^2}{8} + \dfrac{3n}{4} - 1\).  
- Overall = **Θ(n²)**.

---

# Worksheet 1.2: Lecture 4 — Asymptotic Complexity (Variant)

Find the asymptotic complexity of each of the following algorithms. Assume that the input size is n and that Op is a constant-time operation. Show your analysis. If it is possible to analyze each loop separately, you must give the asymptotic complexity for each loop, and then show how you combine them to compute the asymptotic complexity for the whole algorithm. 

**Notation / assumptions**
- `Op` is a constant-time operation.
- `log n` means logarithm in any constant base (Θ same).
- `sqrt(n)` denotes the square root of n.

---

## (1)
```c
for (i=1; i < n/2; i+=3) {
    for (j=1; j < sqrt(n); j*=4)
        Op;
    for (k=3; k < n*n; k+=2)
        for (m=k-2; m <= k+2; m++)
            Op;
}
```

**Analysis (per loop):**
- `i` loop: iterations ≈ (n/2)/3 = Θ(n).
- `j` loop: geometric by ×4 until < sqrt(n) → iterations = Θ(log_4 sqrt(n)) = Θ(log n).
- `k` loop: Θ(n²).
- `m` loop: constant 5 iterations = Θ(1).
- `k`–`m` pair: Θ(n²).

Per `i` iteration cost = Θ(log n) + Θ(n²) = Θ(n²).  
Total = Θ(n) * Θ(n²) = **Θ(n³)**.

**Answer:** **Θ(n³)**.

---

## (2)
```c
for (i=1; i < 4*n; i+=2) {
    for (j=i+5; j >= i; j--)
        Op;
}
for (k=1; k < n*n*n; k*=5) {
    for (m=1; m < logn; m++)
        Op;
}
```

**Analysis:**
- First double loop: `i` → Θ(n), inner `j` fixed 6 iterations → Θ(1) ⇒ Θ(n).
- Second double loop: `k` geometric to n^3 → Θ(log n), `m` → Θ(log n) ⇒ Θ((log n)²).
- Combined: Θ(n) + Θ((log n)²) = **Θ(n)**.

**Answer:** **Θ(n)**.

---

## (3)
```c
for (i=3; i < n; i++) {
    for (j=i; j <= 2*n; j++)
        Op;
}
```

**Exact formula (count of `Op`):**
For `i = 3..n-1`, inner loop runs `2n - i + 1` times. So
\[
T(n) = \sum_{i=3}^{n-1} (2n - i + 1) = \frac{3n^2 - 9n}{2}.
\]

**Asymptotic:** Θ(n²).

**Answer:** Exact \(T(n)=\tfrac{3n^2-9n}{2}\), asymptotic = **Θ(n²)**.

---

## (4) InsertionSort on Alternating Input
Array of size `n` (even):  
`<3, 8, 3, 8, … , 3, 8>`

```c
InsertionSort(A, n) {
  for (i=1; i < n; i++) {
    key = A[i];
    for (j=i-1; j>=0 && A[j] > key; j--)
       A[j+1] = A[j];
    A[j+1] = key;
  }
}
```

**Pattern (inspect first i):**
- `i=1` (8): 0 shifts.
- `i=2` (3): 1 shift.
- `i=3` (8): 0 shifts.
- `i=4` (3): 2 shifts.
- So even `i=2t` → `t` shifts; odd `i` → 0 shifts.

**Total shifts:**
\[
1+2+...+(n/2 - 1) = \frac{n^2 - 2n}{8}.
\]

**Total comparisons:** Θ(n²) (exact expression equals \(\frac{n^2}{8} + \frac{3n}{4} - 1\)).

**Asymptotic runtime:** **Θ(n²)**.

**Answer:** Shifts = \(\dfrac{n^2 - 2n}{8}\); Comparisons ≈ \(\dfrac{n^2}{8} + \dfrac{3n}{4} - 1\); Overall = **Θ(n²)**.

---