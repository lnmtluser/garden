---
title: Maximum Sum Subarray of Size K
---

> [!example]
> Maximum Sum Subarray of Size K<br><br>
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

```javascript title="Alternative solution using slice and reduce"
const maximumSumOfSubarrayOfSizeK = (arr, k) => {
  let maxSum = 0

  for (let i = 0; i <= arr.length - k; i++) {
    let sections = arr.slice(i, i + k)
    let sum = sections.reduce((accum, value) => {
      return accum + value
    }, 0)
    maxSum = Math.max(maxSum, sum)
  }

  return maxSum
}
```

<!-- prettier-ignore-start -->
> [!success]
> The idea behind the sliding window approach is to maintain a window frame that will extend/shrink based on certain conditions while performing at O(n) time complexity.<br><br>
> In this example of finding the maximum subarray of size k, we can use the sliding window approach:<br>
> 1. The left side of the window starts at index 0<br>
> 2. We will sum up all the values in the array while updating the max sum<br>
> 3. Once the kth index is reached, we will remove the left window from the current sum and advance the left window<br>
> 4. Repeat steps 2 and 3 until the end of the window has been reached<br>
> 5. Return max sum<br>
> O(n) time, O(1) space<br><br>
>    [2,1,5,1,3,2]<br>
>    iteraton 1:<br>
>    if (0 >= 3) -> no<br>
>    current sum: 2<br><br>
>    iteration 2:<br>
>    if (1 >=3) -> no<br>
>    current sum: 2+1 = 3<br><br>
>    iteration 3:<br>
>    if (2 >= 3) -> no<br>
>    current sum: 2+1+5 = 8<br><br>
>    iteration 4:<br>
>    if (3 >= 3) -> yes<br>
>    maxSum = Math.max(8, 0) => 8<br>
>    currrentSum = 8 - 2 = 6<br>
>    left window = 1<br>
>    currentSum = 6+1 = 7<br><br>
>    iteration 5:<br>
>    if(4 >= 3) -> yes<br>
>    maxSum = Math.max(8, 7) => 8<br>
>    currentSum = 7 - 1 - 6<br>
>    left window = 2<br>
>    current sum = 6 + 3 = 9<br><br>
>    iteration 6:<br>
>    if ( 5 >= 3) -> yes<br>
>    maxSum = Math.max(9, 8) => 9<br>
>    current sum = 9 - 5 = 4<br>
>    left window = 3<br>
>    current sum = 4 + 2 = 6<br><br>
>    Return 9<br>
<!-- prettier-ignore-end -->

```javascript title="Optimal solution using sliding window"
const maximumSumOfSubarrayOfSizeK_optimal = (arr, k) => {
  let leftWindow = 0
  let currentSum = 0
  let maxSum = 0

  for (let rightWindow = 0; rightWindow < arr.length; rightWindow++) {
    if (rightWindow >= k) {
      currentSum -= arr[leftWindow]
      leftWindow++
    }
    currentSum += arr[rightWindow]
    maxSum = Math.max(currentSum, maxSum)
  }

  return maxSum
}
```
