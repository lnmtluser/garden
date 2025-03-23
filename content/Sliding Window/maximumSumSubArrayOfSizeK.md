---
title: Maximum Sum Subarray of Size K
---

> [!example]
> Maximum Sum Subarray of Size K<br>
> Given an array of positive numbers and a positive number ‘k’, find the maximum sum of any contiguous subarray of size ‘k’.<br><br>
> Example 1:<br>
> Input: [2, 1, 5, 1, 3, 2], k=3<br>
> Output: 9<br>
> Explanation: Subarray with maximum sum is [5, 1, 3].<br><br>
> Example 2:<br>
> Input: [2, 3, 4, 1, 5], k=2<br>
> Output: 7<br>
> Explanation: Subarray with maximum sum is [3, 4].<br>

<!-- prettier-ignore-start -->
> [!note]
> The brute force approach is to find all subarrays of size k and sum them up, while tracking the maximum sum so far, returning max sum at the end<br><br>
> Iterate from i = 0 to arr.length - k<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Iterate from j = i to j < i + k<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sum up each element<br>
> Update max<br>
> Return max<br><br>
> O(n\*n) time<br>
> O(1) space<br>
<!-- prettier-ignore-end -->

```javascript
const maximumSumOfSubarrayOfSizeK = (arr, k) => {
  let maxSum = 0
  for (let i = 0; i <= arr.length - k; i++) {
    let currentSum = 0
    for (let j = i; j < i + k; j++) {
      currentSum += arr[j]
    }
    maxSum = Math.max(maxSum, currentSum)
  }
  return maxSum
}
```
