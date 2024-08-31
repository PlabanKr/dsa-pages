+++
title = 'Longest Palindromic Substring (leetcode 5)'
date = 2024-08-31T11:27:15+05:30
draft = false
+++

## Problem

Given a string s, return the longest palindromic substring in `s`.

Example 1:
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```
Example 2:
```
Input: s = "cbbd"
Output: "bb"
```
Constraints:
- `1 <= s.length <= 1000`
- s consist of only digits and English letters.

## Solution

```java
class Solution {
    public String longestPalindrome(String s) {
        String result = "";
        int maxLength = 0;
        for(int i = 0; i < s.length(); i++) {
            // Odd length
            int left = i, right = i;
            while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                int currLength = right - left + 1;
                if(currLength > maxLength) {
                    result = s.substring(left, right+1);
                    maxLength = currLength;
                }
                left--;
                right++;
            }
            // Even length
            left = i;
            right = i+1;
            while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                int currLength = right - left + 1;
                if(currLength > maxLength) {
                    result = s.substring(left, right+1);
                    maxLength = currLength;
                }
                left--;
                right++;
            }
        }

        return result;
    }
}
```
> [!TIP]
> In normal palindrome problem we take left and right pointer at the extreme left and right end of the string and in each iteration make come towards each other.\
> But here the idea is to expand left and right pointer from the current index and see if the substring is palindrome or not. So loop through until left or right pointer goes out of bound or the character at left and right doesn't match in other words we encounter a non palindromic string.\
> In side the loop check the length of current palindrome. If the length of current palidrome is large than the max then change the longest palindrome. 

> [!CAUTION]
> If we carefully see then the above method only works for the odd length palindrome. The above method won't work for the example 2. So we need to add a edge case for even length string.

