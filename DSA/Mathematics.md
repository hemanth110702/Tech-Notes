<div id="top"></div>

# Mathematics

<details>
<summary>Table of contents</summary>

- [Key notes](#key-notes)
- [GCD - Euclidean Algorithm](#gcd---euclidean-algorithm)
- [Check for Prime](#check-for-prime) 

</details>

<hr/>

## Key notes

- To find number of digits in a number: $\lfloor logn\rfloor$ + 1
- Relation between GCD and LCM
```java
(a * b) = lcm(a,b) * gcd(a,b)
```

<hr/>

## GCD - Euclidean Algorithm

The **Euclidean Algorithm** efficiently computes the **Greatest Common Divisor (GCD)** of two numbers.

### Key Property

\[
gcd(a,b) = gcd(b, a \bmod b)
\]

This means the GCD **does not change** if we replace `(a, b)` with `(b, a % b)`.

```java
class Solution {
    public static int gcd(int a, int b) {
        if(b == 0) return a;
        return gcd(b, a % b);
    }
}

ex:
gcd(48,18) = gcd(18,12) // common divisors won't change
gcd(18,12)
gcd(12,6)
gcd(6,0)
//Result
GCD = 6

Time-Complexity: O(log(min(a,b)))
```

<p align="right"><a href="#top">⬆️ Back to Top</a></p>

<hr/>


## Check for Prime

- Most efficient
```java
class Solution {
    public int isPrime(int N) {
        // code here
        if(N==1) return 0;
        if(N==2||N==3)return 1;
        if(N%2==0 || N%3==0)return 0;
        for(int i=5; i<=Math.sqrt(N); i+=6) {
            if(N%i==0 || N%(i+2) == 0)return 0;
        }
        return 1;
    }
}
```