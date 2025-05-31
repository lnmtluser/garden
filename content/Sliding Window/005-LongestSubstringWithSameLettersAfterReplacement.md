---
title: Longest Substring With Same Letters After Replacement (hard)
---

> [!example]
> Given a string with lowercase letters only, if you are allowed to replace no more than ‘k’ letters with any letter, find the length of the longest substring having the same letters after replacement.<br><br>
> Example 1:<br>
> Input: String="aabccbb", k=2<br>
> Output: 5<br>
> Explanation: Replace the two 'c' with 'b' to have a longest repeating substring "bbbbb".<br><br>
> Example 2:<br>
> Input: String="abbcb", k=1<br>
> Output: 4<br>
> Explanation: Replace the 'c' with 'b' to have a longest repeating substring "bbbb".<br><br>
> Example 3:<br>
> Input: String="abccde", k=1<br>
> Output: 3<br>
> Explanation: Replace the 'b' or 'd' with 'c' to have the longest repeating substring "ccc".<br>

<!-- prettier-ignore-start -->
> [!note]
> Sliding window<br>
> 1. Iterate n times<br>
> 2. On each iteration, add the element into the hashmap, key = element, value = occurence<br>
> 3. On each iteration, we will keep track of the counter of the most frequent occurrence<br>
> 4. We will use an if statement to check to see if the length - most frequent > k, that means if after replacing k characters in the current string, there are leftover characters (more than k), then we need to subtract the leftWindow from the map and advance the left window
Update the longest substring, and finally return it after n iterations<br><br>
> O(n) time, O(26) space => O(1) space<br>
<!-- prettier-ignore-end -->

```javascript
const lengthOfLongestSubstringWithSameCharactersAfterReplacement = (str, k) => {
  let leftWindow = 0
  let mostFrequentCounter = 0
  let longestSubstring = 0
  let map = new Map()

  for (let rightWindow = 0; rightWindow < str.length; rightWindow++) {
    let leftChar = str.charAt(leftWindow)
    let rightChar = str.charAt(rightWindow)

    map.set(rightChar, (map.get(rightChar) || 0) + 1)
    mostFrequentCounter = Math.max(mostFrequentCounter, map.get(rightChar))

    let length = rightWindow - leftWindow + 1

    if (length - mostFrequentCounter > k) {
      map.set(leftChar, map.get(leftChar) - 1)
      leftWindow++
    }
    length = rightWindow - leftWindow + 1
    longestSubstring = Math.max(longestSubstring, length)
  }

  return longestSubstring
}
```
