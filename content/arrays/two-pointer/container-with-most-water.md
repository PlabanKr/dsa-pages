+++
title = 'Container With Most Water (leetcode 11)'
date = 2024-08-31T10:17:08+05:30
draft = false
+++

## Problem

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.
Find two lines that together with the x-axis form a container, such that the container contains the most water.
Return the maximum amount of water a container can store.

Notice that you may not slant the container.

### Example 1:

![Container With Most Water](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
**Input:** height = [1,8,6,2,5,4,8,3,7]\
**Output:**  49\
**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.\

### Example 2:

**Input:** height = [1,1]\
**Output:**  1

## Solution

```java
class Solution {
    public int maxArea(int[] height) {
        int max = Integer.MIN_VALUE;
        int left = 0, right = height.length - 1;
        while(left < right) {
            int curr = 0;
            if(height[left] < height[right]) {
                curr = height[left] * (right - left);
                left++;
            } else {
                curr = height[right] * (right - left);
                right--;
            }
            max = Math.max(max, curr);
        }
        return max;
    }
}
```