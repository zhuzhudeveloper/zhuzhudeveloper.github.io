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
### LeetCode 354: Russian Doll Envelopes
You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? (put one inside other)

Note:
Rotation is not allowed.

Example:

Input: [[5,4],[6,4],[6,7],[2,3]]
Output: 3 
Explanation: The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```
# First Element: Increasing
# If same first elements: Second Element goes decreasing
# Longest increasing sequence
import bisect
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:
        def lis(nums):
            dp = []
            for num in nums:
                idx = bisect_left(dp, num)
                if(idx<len(dp)):
                    dp[idx] = num
                else:
                    dp.append(num)
            return len(dp)
        envelopes.sort(key = lambda x: (x[0], -x[1]))
        return lis([i[1] for i in envelopes])
```
### LeetCode 315: Count of Smaller Numbers After Self
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].           
Example:            
Input: [5,2,6,1]           
Output: [2,1,1,0]               
Explanation:            
To the right of 5 there are 2 smaller elements (2 and 1).         
To the right of 2 there is only 1 smaller element (1).          
To the right of 6 there is 1 smaller element (1).        
To the right of 1 there is 0 smaller element.          
```
def countSmaller(self, nums: List[int]) -> List[int]:
        import bisect
        res = []
        sortedqueue = []
        for num in nums[::-1]:
            position = bisect.bisect_left(sortedqueue,num)
            res.append(position)
            sortedqueue.insert(position, num)
        return res[::-1]
```
Other four solutions for this problem
```
思路二：归并排序

因为归并排序，在合并的时候，可以判断出右边比它小的个数

时间复杂度：$O(nlogn)$

class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        arr = []
        res = [0] * len(nums)
        for idx, num in enumerate(nums):
            arr.append((idx, num))

        def merge_sort(arr):
            if len(arr) <= 1:
                return arr
            mid = len(arr) // 2
            left = merge_sort(arr[:mid])
            right = merge_sort(arr[mid:])
            # print(left, right)
            return merge(left, right)

        def merge(left, right):
            tmp = []
            i = 0
            j = 0
            while i < len(left) or j < len(right):
                if j == len(right) or i < len(left) and left[i][1] <= right[j][1]:
                    tmp.append(left[i])
                    res[left[i][0]] += j
                    i += 1
                else:
                    tmp.append(right[j])
                    j += 1
            return tmp

        merge_sort(arr)
        return res
思路三：树状数组

class BinaryIndexedTree:
    def __init__(self, nums):

        self.BIT_arr = [0] * (len(nums) + 1)
        # O(nlogn)
        # for i in range(len(nums)):
        #     self.updata(i, nums[i])
        # O(n)
        for i in range(len(nums)):
            self.BIT_arr[i + 1] = nums[i]
        for i in range(1, len(self.BIT_arr)):
            j = i + (i & -i)
            if j < len(self.BIT_arr):
                self.BIT_arr[j] += self.BIT_arr[i]
	# 更新,是指在i位置上加上 val
    def updata(self, i, delta):
        i += 1
        while i < len(self.BIT_arr):
            self.BIT_arr[i] += delta
            i += (i & (-i))
	# 重新赋值, 在i位置为val
    def setVal(self, i, val):
        i += 1
        self.updata(i, val - self.BIT_arr[i])

    def prefix(self, i):
        i += 1
        res = 0
        while i > 0:
            res += self.BIT_arr[i]
            i -= (i & (-i))
        return res


class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        hashTable = {v: i for i, v in enumerate(sorted(set(nums)))}
        # print(hashTable)
        tree = BinaryIndexedTree([0] * len(hashTable))
        res = []
        for i in range(len(nums) - 1, -1, -1):
            res.append(tree.prefix(hashTable[nums[i]] - 1))
            tree.updata(hashTable[nums[i]] , 1)
        
        return res[::-1]
思路四：线段树

class SegmentTree(object):

    def __init__(self, nums):
        self.l = len(nums)
        self.tree = [0] * self.l + nums
        for i in range(self.l - 1, 0, -1):
            self.tree[i] = self.tree[i << 1] + self.tree[i << 1 | 1]
    # 重新赋值, 在i位置为val
    def setVal(self, i, val):
        n = self.l + i
        self.tree[n] = val
        while n > 1:
            self.tree[n >> 1] = self.tree[n] + self.tree[n ^ 1]
            n >>= 1
    # 更新,是指在i位置上加上 val
    def updata(self, i, val):
        n = self.l + i
        tmp = self.tree[n]
        self.setVal(i, tmp + val)

    def sumRange(self, i: int, j: int) -> int:
        m = self.l + i
        n = self.l + j
        res = 0
        while m <= n:
            if m & 1:
                res += self.tree[m]
                m += 1
            m >>= 1
            if n & 1 == 0:
                res += self.tree[n]
                n -= 1
            n >>= 1
        return res


class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        hashTable = {v: i for i, v in enumerate(sorted(set(nums)))}
        tree, r = SegmentTree(len(hashTable) * [0]), []
        for i in range(len(nums) - 1, -1, -1):
            r.append(tree.sumRange(0, hashTable[nums[i]] - 1))
            tree.updata(hashTable[nums[i]], 1)
        return r[::-1]
思路五：二叉搜索树

class Node():
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.leftSum = 0
        self.dup = 0


class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:
        def insert(node, val):
            Sum = 0
            while node.val != val:
                if node.val > val:
                    if node.left == None:
                        node.left = Node(val)
                    node.leftSum += 1
                    node = node.left
                else:
                    Sum += node.leftSum + node.dup
                    if node.right == None:
                        node.right = Node(val)
                    node = node.right
            node.dup += 1
            return Sum + node.leftSum
        if not nums: return []
        res = [0] * len(nums)
        root = Node(nums[-1])
        for i in range(len(nums) - 1, -1, -1):
            res[i] = insert(root, nums[i])
        return res
```
