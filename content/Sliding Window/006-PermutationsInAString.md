---
title: Permutations In A String (hard)
---

> [!example]
> Given a string and a pattern, find out if the string contains any permutation of the pattern.<br><br>
> Permutation is defined as the re-arranging of the characters of the string. For example, “abc” has the following six permutations:<br><br>
> abc<br>
> acb<br>
> bac<br>
> bca<br>
> cab<br>
> cba<br><br>
> If a string has ‘n’ distinct characters it will have n! permutations.<br><br>
> Example 1:<br>
> Input: String="oidbcaf", Pattern="abc"<br>
> Output: true<br>
> Explanation: The string contains "bca" which is a permutation of the given pattern.<br><br>
> Example 2:<br>
> Input: String="odicf", Pattern="dc"<br>
> Output: false<br>
> Explanation: No permutation of the pattern is present in the given string as a substring.<br><br>
> Example 3:<br>
> Input: String="bcdxabcdy", Pattern="bcdyabcdx"<br>
> Output: true<br>
> Explanation: Both the string and the pattern are a permutation of each other.<br><br>
> Example 4:<br>
> Input: String="aaacb", Pattern="abc"<br>
> Output: true<br>
> Explanation: The string contains "acb" which is a permutation of the given pattern.<br>

<!-- prettier-ignore-start -->
> [!note]
> Sliding window approach<br>
> 1. Initialize a map that stores each Key:Value as element:occurence for the given string<br>
> 2. Initialize a pattern map that will take values of the map above<br>
> 3. Iterate n times, on each iteration, check to see if current element in the str exists in the pattern map, if so, subtract its value by 1 from the pattern map, and if 0, remove its entry from the pattern map. Inside of this check, add another check for if pattern map is size 0, then return true as all matches have been found<br>
> 4. If the pattern map does not contain the current element, then we have to check if previous matches were found, if so, then we need to restore the pattern map to its default state<br>
> 5. Return false after n iterations (no matches found)<br>
> O(n) time, O(n) space
<!-- prettier-ignore-end -->

```javascript
const stringContainsPermutation = (str, pattern) => {
  let leftWindow = 0
  let map = new Map()
  let matched = 0

  for (let i = 0; i < pattern.length; i++) {
    map.set(pattern.charAt(i), (map.get(pattern.charAt(i)) || 0) + 1)
  }

  for (let windowEnd = 0; windowEnd < str.length; windowEnd++) {
    const rightChar = str[windowEnd]
    if (map.has(rightChar)) {
      map.set(rightChar, map.get(rightChar) - 1)
      if (map.get(rightChar) === 0) {
        matched += 1
      }
    }

    if (matched === map.size) {
      return true
    }

    if (windowEnd >= pattern.length - 1) {
      const leftChar = str[leftWindow]
      leftWindow++
      if (map.has(leftChar)) {
        if (map.get(leftChar) === 0) {
          matched -= 1
        }
        map.set(leftChar, map.get(leftChar) + 1)
      }
    }
  }
  return false
}
```
