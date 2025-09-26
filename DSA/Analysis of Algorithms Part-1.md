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



