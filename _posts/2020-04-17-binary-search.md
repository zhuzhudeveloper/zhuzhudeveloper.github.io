---
category: algorithm
tags: Binary Search
---

# Binary Search
## Characteristic
* Sequence in order
* Time Complexity O(logn)
* Space Complexity O(1)
### Perfect Code
```
        if len(nums) == 0:
            return 0
        if nums[-1] < target:
            return len(nums)
        if nums[0]>target:
            return 0
        left = 0
        right = len(nums) - 1
        while(left<right):
            mid = left + (right-left) // 2
            if(nums[mid]<target):
                left = mid + 1
            else:
                right = mid
        return left
```
### LeetCode 34: Find First and Last Position of Element in Sorted Array
Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.       
Your algorithm's runtime complexity must be in the order of O(log n).       
If the target is not found in the array, return [-1, -1].
```
        res = [-1,-1]
        if len(nums) == 0:
            return res
        if nums[-1] < target or nums[0] > target:
            return res
        left = 0
        right = len(nums)-1
        # Look for the first one
        while(left < right):
            mid = left + (right - left)//2
            if(nums[mid]<target):
                left=mid+1
            else:
                right=mid
        if(nums[left]==target):
            res[0] = left
        else: return res
        left = 0
        right = len(nums)-1
        # Look for the right one
        while(left<right):
            mid = left + (right-left)//2 + 1
            if(nums[mid]>target):
                right=mid-1
            else:
                left=mid
        res[1] = right
        return res
```
