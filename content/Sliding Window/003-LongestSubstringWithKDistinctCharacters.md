---
title: Longest Substring With K Distinct Characters
priority: 1
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

The brute force approach is to look for all longest subarray that contains no more than k distinct characters
We will be using a hashmap to store each occurrence of characters found so far while iterating through the array

<!-- prettier-ignore-start -->
> [!note]
Iterate from i = 0 to n - 1
    Iterate from j = i to n - 1
        While iterating, store each occurrence of characters found so far in a hashmap
        If at any point, the size of the map is > k, then reset the map for next iteration, and break to go to next ith iteration
        Update the longest substring seen so far
Return the maximum subarray length

O(n*n) time, O(n) space
<!-- prettier-ignore-end -->
