---
category: algorithm
tags: Binary Search
---

# Binary Search
## Characteristic
* Sequence in order
* Time Complexity O(logn)
* Space Complexity O(1)
## Perfect Code
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
## Python bisect
#### bisect.bisect_left(a, x, lo=0, hi=len(a))            
Locate the insertion point for x in a to maintain sorted order. The parameters lo and hi may be used to specify a subset of the list which should be considered; by default the entire list is used. If x is already present in a, the insertion point will be before (to the left of) any existing entries. The return value is suitable for use as the first parameter to list.insert() assuming that a is already sorted.                  
The returned insertion point i partitions the array a into two halves so that all(val < x for val in a[lo:i]) for the left side and all(val >= x for val in a[i:hi]) for the right side.                    

#### bisect.bisect_right(a, x, lo=0, hi=len(a)) && bisect.bisect(a, x, lo=0, hi=len(a))
Similar to bisect_left(), but returns an insertion point which comes after (to the right of) any existing entries of x in a.   
         
The returned insertion point i partitions the array a into two halves so that all(val <= x for val in a[lo:i]) for the left side and all(val > x for val in a[i:hi]) for the right side.            

#### bisect.insort_left(a, x, lo=0, hi=len(a))
Insert x in a in sorted order. This is equivalent to a.insert(bisect.bisect_left(a, x, lo, hi), x) assuming that a is already sorted. Keep in mind that the O(log n) search is dominated by the slow O(n) insertion step.               

#### bisect.insort_right(a, x, lo=0, hi=len(a)) && bisect.insort(a, x, lo=0, hi=len(a))
Similar to insort_left(), but inserting x in a after any existing entries of x.
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
### LeetCode 33: Search in Rotated Sorted Array
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.    
(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).     
You are given a target value to search. If found in the array return its index, otherwise return -1.      
You may assume no duplicate exists in the array.       
Your algorithm's runtime complexity must be in the order of O(log n).
```
        if len(nums) == 0:
            return -1
        # Binary Search to find the pivot
        left = 0
        right = len(nums) - 1
        while(left<right):
            mid = left + (right-left)//2 
            if(nums[right]<nums[mid]):
                left = mid + 1
            else:
                right = mid
        pivot = left
        # Choose one part to do binary search again, looking for the target
        if(nums[-1]>=target or pivot == 0):
            left = pivot
            right = len(nums) - 1
        else:
            left = 0
            right = pivot-1
        while(left<right):
            mid = left + (right-left)//2
            if(nums[mid]<target):
                left = mid + 1
            else:
                right = mid
        if(nums[left]==target):
            return left
        else:
            return -1
```
### LeetCode 154: Find Minimum in Rotated Sorted Array II
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.     
(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).     
Find the minimum element.           
The array may contain duplicates.
```
        while(left<right):
            mid = left + (right-left)//2
            if(nums[mid]<nums[right]):
                right = mid
            elif(nums[mid]>nums[right]):
                left = mid + 1
            else:
                right = right -1
        return nums[left]
```
### LeetCode 162: Find Peak Element   
A peak element is an element that is greater than its neighbors.                
Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.               
The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.              
You may imagine that nums[-1] = nums[n] = -∞.             
```
Analysis:
if(nums[mid]>nums[mid+1] and nums[mid]>nums[mid-1]): return mid ##pay attention to boundary
if(nums[mid]<nums[mid+1]): go right
else: go left, need test before

    def binarySearch(self, nums, left, right):
        while(left<right):
            mid = left + (right-left) // 2
            if(mid-1>0 and nums[mid]>nums[mid-1] and mid+1<len(nums) and nums[mid]>nums[mid+1]):
                return mid
            if(nums[mid]<nums[mid+1]):
                left = mid+1
                self.binarySearch(nums,left, right)
            elif(nums[mid]>nums[mid+1]):
                right = mid
                self.binarySearch(nums,left, right)
        return left
    
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        left = 0 
        right = n-1
        return self.binarySearch(nums, left, right)
```
### LeetCode 300: Longest Increasing Subsequence
Input: [10,9,2,5,3,7,101,18]                  
Output: 4                    
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.          
```
def lengthOfLIS(self, nums: List[int]) -> int:
        #scan items before i: find the item which is smaller but with largest count
        # if(len(nums)==0): return 0
        # count = []
        # for i in range(len(nums)):
        #     count.append(1)
        #     for j in range(i):
        #         if(nums[j]<nums[i]):
        #             count[i] = max(count[i], count[j]+1)
        # return max(count)
        
        dp = []
        for x in nums:
            if x not in dp:
                idex = self.binarySearch(dp, 0, len(dp), x)
                if(idex<len(dp)):
                    dp[idex]=x
                else:
                    dp.append(x)
        return len(dp)
        
    def binarySearch(self, dp, left, right, item):
        while(left<right):   
            mid = left + (right-left)//2
            if(dp[mid]==item):
                return mid
            elif(dp[mid]>item):
                right = mid
            else:
                left = mid+1
        return left
```
