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

test
