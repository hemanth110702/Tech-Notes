<div id="top"></div>

# Tricks

<details>

<summary>Table of contents</summary>

- [In-Place Two-Number Encoding Trick in Arrays](#in-place-two-number-encoding-trick-in-arrays)

</details>

## In-Place Two-Number Encoding Trick in Arrays

- A DSA trick to store two numbers in a single array index using mathematical encoding. This helps to reduce space usage without using extra memory (auxiliary space = O(1)).
-We use one number as a base multiplier (usually array length n or max_val+1) and encode two values:

```
arr[i] = original_value + n * value_to_store
original = arr[i] % n
stored   = arr[i] // n
```


<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

