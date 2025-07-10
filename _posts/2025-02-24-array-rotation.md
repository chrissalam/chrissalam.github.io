---
layout: post
title: Rotate an array
---

I thought this was going to be similar to matrix rotation but it's shape is very different. You can go about this three ways (it's personally hard for me to find one that's clearly the most legible so maybe there's value in showing all three strategies.).

1. Make an empty array that's the same size and fill in the numbers
2. Swap full sections
3. Reverse the full array, and then reverse 0 - K and K to n - 1. 

I'm going to do the last because it's the most obvious to me.

```
Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
Example 2:

Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]

```

All three problems rely heavily on the modulus operator (%), because if you need an array of 7 units rotated by 8, you really just want it rotated by 1 slot. So each k will be operated on and it's not typical for me to use this function when the first number is smaller than the second number, so it threw me off initially but think of it as a remainder. 3 % 7 -> the remainder is 3. So this start is in all three of our solutions.

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        n = len(nums)
        k = k % n
        if k == 0:
            return

```
Reversing twice (or reversing once and then reversing in sections), is the same as rotation.

In a tiny example, we can see it pretty easily.
```python
k = 1

[1, 2, 3] -> [3, 2, 1] -> [3] + [1, 2]

or 

k = 2

[1, 2, 3, 4, 5] -> [5, 4, 3, 2, 1] -> [4, 5] + [1, 2, 3]
```

Ok... so let's see it in code.

```python
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k % n
        if k == 0:
            return
        
        def reverse(start, end):
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1
        # Reverse entire array
        reverse(0, n - 1)
        # Reverse first k elements
        reverse(0, k - 1)
        # Reverse remaining elements
        reverse(k, n - 1)
```
