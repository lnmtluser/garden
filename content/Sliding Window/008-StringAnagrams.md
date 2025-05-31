---
title: String Anagrams (hard)
---

> [!example]
> Given a string and a pattern, find all anagrams of the pattern in the given string.<br><br>
> Anagram is actually a Permutation of a string. For example, “abc” has the following six anagrams:<br><br>
> abc<br>
> acb<br>
> bac<br>
> bca<br>
> cab<br>
> cba<br>
> Write a function to return a list of starting indices of the anagrams of the pattern in the given string.<br><br>
> Example 1:<br>
> Input: String="ppqp", Pattern="pq"<br>
> Output: [1, 2]<br>
> Explanation: The two anagrams of the pattern in the given string are "pq" and "qp".<br><br>
> Example 2:<br>
> Input: String="abbcabc", Pattern="abc"<br>
> Output: [2, 3, 4]<br>
> Explanation: The three anagrams of the pattern in the given string are "bca", "cab", and "abc".<br>

<!-- prettier-ignore-start -->
> [!note]
> Sliding window approach<br>
> 1. Insert all elements in pattern string into a frequency map<br>
> 2. Iterate n times over str, for each iteration check if current element is in the pattern map, if so then add element's index to the returning array, subtract 1 from element's frequncy map counter, if counter is 0 for an element, increment matched by 1.<br>
> 3. If matched is equal to pattern map's size, then return true<br>
> 4. Whenever the current window is >= pattern map's size, then subtract the left window from the frequncy map, if the element in the frequncy map is 0, then subtract 1 from matched, if the left element that is being subtracted exists in the pattern map, then add the element back into the frequency map<br>
> 5. Return [] after n iterations (no anagrams exist)<br>
> O(n) time, O(n) space
<!-- prettier-ignore-end -->

```javascript
const returnListOfStartingIndicesOfAnagramsOfThePatternInGivenString = (str, pattern) => {
  let leftWindow = 0
  let matched = 0
  let resultsArr = []
  let map = new Map()

  for (let i = 0; i < pattern.length; i++) {
    let char = pattern.charAt(i)
    map.set(char, (map.get(char) || 0) + 1)
  }

  for (let rightWindow = 0; rightWindow < str.length; rightWindow++) {
    let rightChar = str.charAt(rightWindow)
    if (map.has(rightChar)) {
      map.set(rightChar, map.get(rightChar) - 1)
      resultsArr.push(rightWindow)
      if (map.get(rightChar) === 0) {
        matched += 1
      }
    }
    if (matched === map.size) {
      return resultsArr
    }

    if (rightWindow >= pattern.length - 1) {
      let leftChar = str.charAt(leftWindow)
      leftWindow++
      if (map.get(leftChar) === 0) {
        matched -= 1
      }

      if (map.has(leftChar)) {
        map.set(leftChar, map.get(leftChar) + 1)
        resultsArr.shift()
      }
    }
  }
  return []
}
```
