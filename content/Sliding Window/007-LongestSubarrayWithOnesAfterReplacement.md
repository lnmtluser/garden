---
title: Longest Subarray with Ones after Replacement (hard)
---

> [!example]
> Given an array containing 0s and 1s, if you are allowed to replace no more than ‘k’ 0s with 1s, find the length of the longest contiguous subarray having all 1s.<br><br>
> Example 1:<br>
> Input: Array=[0, 1, 1, 0, 0, 0, 1, 1, 0, 1, 1], k=2<br>
> Output: 6<br>
> Explanation: Replace the '0' at index 5 and 8 to have the longest contiguous subarray of 1s having length 6.<br><br>
> Example 2:<br>
> Input: Array=[0, 1, 0, 0, 1, 1, 0, 1, 1, 0, 0, 1, 1], k=3<br>
> Output: 9<br>
> Explanation: Replace the '0' at index 6, 9, and 10 to have the longest contiguous subarray of 1s having length 9.<br>

<!-- prettier-ignore-start -->
> [!note]
> Sliding window approach<br>
> 1. Iterate n times<br>
> 2. On each iteration, we keep track of the number of 1s in the current window<br>
> 3. If we take the length of the window - the number of 1s in the window, then we will get the number of 0s in the current window.<br>
> 4. Once the number of 0s in the window is greater than k, that means that we cannot flip any more 0 to make the current window all 1s, then we need to shrink the window by advancing left window<br>
> 5. When shrinking the current window, if the left window contains a 1, then we subtract 1 from the number of 1s counter<br>
> 6. On each iteration, we will also update the maximum length<br>
> 7. Return the maximum length after n iterations<br>
> O(n) time, O(1) space
<!-- prettier-ignore-end -->

```javascript
const lengthOfLongestSubarrayHavingAllOnesAfterReplacingKZeroes = (arr, k) => {
  let windowStart = 0
  let longestSubstring = 0
  let numberOfOnes = 0

  for (let windowEnd = 0; windowEnd < arr.length; windowEnd++) {
    if (arr[windowEnd] === 1) {
      numberOfOnes += 1
    }

    let length = windowEnd - windowStart + 1
    if (length - numberOfOnes > k) {
      if (arr[windowStart] === 1) {
        numberOfOnes -= 1
      }
      windowStart++
    }

    longestSubstring = Math.max(longestSubstring, windowEnd - windowStart + 1)
  }
  return longestSubstring
}
```
