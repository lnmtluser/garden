---
title: Longest Substring With K Distinct Characters
---

> [!example]
> Given a string, find the length of the longest substring in it with no more than K
> distinct characters.<br><br>
> Example 1:<br>
> Input: String="araaci", K=2<br>
> Output: 4<br>
> Explanation: The longest substring with no more than '2' distinct characters is "araa".<br><br>
> The optimal approach is to use a sliding window<br>
> Iterate in one pass<br>
> While iterating, set each element seen so far into a hashmap<br>
> If at any point, the size of the hashmap > k, then subtract the left window from the hashmap, if the value of the key is 0, delete the entry from the hashmap<br>
> Advance the left window after subtracting a value from the hashmap<br>
> Update the longest substring length<br>
> Return the longest substring length<br><br>
> O(n) time , O(n) space
