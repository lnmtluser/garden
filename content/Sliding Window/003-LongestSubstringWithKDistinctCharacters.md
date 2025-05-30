---
title: Longest Substring With K Distinct Characters
---

> [!example]
> Given a string, find the length of the longest substring in it with no more than K distinct characters.<br><br>
> Example 1:<br>
> Input: String="araaci", K=2<br>
> Output: 4<br>
> Explanation: The longest substring with no more than '2' distinct characters is "araa".<br><br>
> Example 2:<br>
> Input: String="araaci", K=1<br>
> Output: 2<br>
> Explanation: The longest substring with no more than '1' distinct > characters is "aa".<br><br>
> Example 3:<br>
> Input: String="cbbebi", K=3<br>
> Output: 5<br>
> Explanation: The longest substrings with no more than '3' distinct characters are "cbbeb" & "bbebi".<br>

<!-- prettier-ignore-start -->
> [!note]
> The brute force approach is to look for all longest subarray that contains no more than k distinct characters<br>
> We will be using a hashmap to store each occurrence of characters found so far while iterating through the array<br><br>
> Iterate from i = 0 to n - 1<br>
> &nbsp;&nbsp;&nbsp;&nbsp;Iterate from j = i to n - 1<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;While iterating, store each occurrence of characters found so far in a hashmap<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If at any point, the size of the map is > k, then reset the map for next iteration, and break to go to next ith iteration<br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Update the longest substring seen so far<br>
> Return the maximum subarray length<br>
> O(n*n) time, O(n) space<br>
<!-- prettier-ignore-end -->

```javascript
const findLengthOfLongestSubstringWithNoMoreThanKDistinctCharacters = (arr, k) => {
  let longestSubstring = 0
  let map = new Map()

  for (let i = 0; i < arr.length; i++) {
    for (let j = i; j < arr.length; j++) {
      map.set(arr[j], (map.get(arr[j]) || 0) + 1)
      if (map.size > k) {
        map = new Map()
        break
      }
      longestSubstring = Math.max(longestSubstring, j - i + 1)
    }
  }

  return longestSubstring
}
```

<!-- prettier-ignore-start -->
> [!success]
> The optimal approach is to use a sliding window<br>
> 1. Iterate in one pass<br>
> 2. While iterating, set each element seen so far into a hashmap<br>
> 3. If at any point, the size of the hashmap > k, then subtract the left window from the hashmap, if the value of the key is 0, delete the entry from the hashmap<br>
> 4. Advance the left window after subtracting a value from the hashmap<br>
> 5. Update the longest substring length<br>
> 6. Return the longest substring length<br><br>
> O(n) time , O(n) space<br>
<!-- prettier-ignore-end -->

```javascript title="Optimal solution using sliding window"
const findLengthOfLongestSubstringWithNoMoreThanKDistinctCharacters_optimal = (arr, k) => {
  let leftWindow = 0
  let longestSubstring = 0
  let map = new Map()

  for (let rightWindow = 0; rightWindow < arr.length; rightWindow++) {
    map.set(arr[rightWindow], (map.get(arr[rightWindow]) || 0) + 1)
    while (map.size > k) {
      map.set(arr[leftWindow], map.get(arr[leftWindow]) - 1)
      if (map.get(arr[leftWindow]) === 0) {
        map.delete(arr[leftWindow])
      }
      leftWindow++
    }
    longestSubstring = Math.max(rightWindow - leftWindow + 1, longestSubstring)
  }

  return longestSubstring
}
```
