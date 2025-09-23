<div id="top"></div>

# Arrays

<details>

<summary>Table of contents</summary>

- [Kadane’s Algorithm](#kadanes-algorithm)

</details>

## Kadane’s Algorithm

- **Goal:** Find the maximum subarray sum in a given array (contiguous elements).
- Kadane’s Algorithm helps find the maximum sum of a contiguous subarray from a given array of integers (positive, negative, or both).

- **Logic**
  1) Initialize two variables:
    - ```maxSum = arr[0]``` → stores the maximum sum so far
    - ```currentSum = arr[0]``` → stores the current running sum

  2) Loop from second element:
      ```
      for i = 1 to n-1:
        currentSum = max(arr[i], currentSum + arr[i])
        maxSum = max(maxSum, currentSum)
      ```
  3) Return ```maxSum```

- **Example**
    ```
    Input: [-2, 1, -3, 4, -1, 2, 1, -5, 4]  
    Output: 6  
    Explanation: The subarray [4, -1, 2, 1] gives the maximum sum 6.
    ```

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>
