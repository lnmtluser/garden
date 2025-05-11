---
title: Smallest Subarray with a given sum
---

> [!example]
> Smallest Subarray with a given sum<br><br>
> Given an array of positive numbers and a positive number ‘S’, find the length of the smallest contiguous subarray whose sum is greater than or equal
> to ‘S’<br>
> Return 0, if no such subarray exists<br><br>
> Example 1:<br>
> Input: [2, 1, 5, 2, 3, 2], S=7<br>
> Output: 2<br>
> Explanation: The smallest subarray with a sum great than or equal to '7' is [5, 2]<br><br>
> Example 2:<br>
> Input: [2, 1, 5, 2, 8], S=7<br>
> Output: 1<br>
> Explanation: The smallest subarray with a sum greater than or equal to '7' is [8]<br><br>
> Example 3:<br>
> Input: [3, 4, 1, 1, 6], S=8<br>
> Output: 3<br>
> Explanation: Smallest subarrays with a sum greater than or equal to '8' are [3, 4, 1] or [1, 1, 6]<br>

<!-- prettier-ignore-start -->
> [!note]
> The brute force approach is to find all subarrays that satisfies the condition of finding the smallest subarray whose sum is equal to or greater than the target, or 0 if none exist<br><br>
> Iterate i to n times<br>
> &nbsp;&nbsp;&nbsp;&nbsp;j = i<br>
> &nbsp;&nbsp;&nbsp;&nbsp;While current sum is less than s, and while j < arr.length<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Add each element into the sum<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Advance j<br>
> &nbsp;&nbsp;&nbsp;&nbsp;Check if current sum >= s<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If so, then update the smallest length<br>
> &nbsp;&nbsp;&nbsp;&nbsp;Reset current sum<br>
> Return smallest length<br><br>
> O(n*n) time, O(1) space
<!-- prettier-ignore-end -->

```javascript
const smallestLengthOfSubarrayWhoseSumIsGreaterThanOrEqualToTarget = (arr, s) => {
  let currentSum = 0
  let smallestLength = Number.MAX_VALUE

  for (let i = 0; i < arr.length; i++) {
    let j = i
    while (currentSum < s && j < arr.length) {
      currentSum += arr[j]
      j++
    }
    if (currentSum >= s) {
      smallestLength = Math.min(j - i, smallestLength)
    }
    currentSum = 0
  }

  return smallestLength === Number.MAX_VALUE ? 0 : smallestLength
}
```

<!-- prettier-ignore-start -->
> [!success]
> The optimal approach is to use a sliding window<br>
>
> 1. Iterate n times<br>
> 2. On each iteration, add elements into current sum<br>
> 3. While current sum >= s, update the smallest length, subtract the left side of the window, advance the left window<br>
> 4. Repeat steps 2 and 3 until end of iteration<br>
> 5. Return the smallest length<br>
> O(n) time, O(1) space
<!-- prettier-ignore-end -->

```javascript title="Optimal solution using sliding window"
const smallestLengthOfSubarrayWhoseSumIsGreaterThanOrEqualToTarget_optimal = (arr, s) => {
  let smallestLength = Number.MAX_VALUE
  let currentSum = 0
  let leftWindow = 0

  for (let rightWindow = 0; rightWindow < arr.length; rightWindow++) {
    currentSum += arr[rightWindow]
    while (currentSum >= s) {
      smallestLength = Math.min(smallestLength, rightWindow - leftWindow + 1)
      currentSum -= arr[leftWindow]
      leftWindow++
    }
  }

  return smallestLength === Number.MAX_VALUE ? 0 : smallestLength
}
```
