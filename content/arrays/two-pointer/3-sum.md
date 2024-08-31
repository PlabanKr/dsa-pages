+++
title = '3 Sum (leetcode 15)'
date = 2024-08-31T11:00:17+05:30
draft = false
+++

## Problem


Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```
Example 2:

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
```
Example 3:

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```

Constraints:
- `3 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`

## Solution

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        // first sort the array
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        for(int i = 0; i < nums.length - 2; i++) {
            // check if the next elements are not same to avoid duplicate sol
            if(i > 0 && nums[i] == nums[i-1])
                continue;

            int left = i + 1, right = nums.length - 1;
            while(left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum == 0) {
                    List<Integer> sol = new ArrayList<>();
                    sol.add(nums[i]);
                    sol.add(nums[left]);
                    sol.add(nums[right]);
                    result.add(sol);
                    left++;
                    // skip duplicates
                    while(nums[left] == nums[left-1] && left < right)
                        left++;
                } else if (sum > 0) {
                    right--;
                } else {
                    left++;
                }
            }
            
        }
        return result;
    }
}
```

> [!NOTE]
> First sort the array. Then inside follow the logic of Two Sum 2 problem.\
> When checking for duplicate solution increase the pointer and check with the previous value, this is only possible in sorted array.
