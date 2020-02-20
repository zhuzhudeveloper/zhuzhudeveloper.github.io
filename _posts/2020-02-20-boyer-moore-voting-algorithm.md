---
category: algorithm
tags: Boyer-Moore, MajorityElement
---

# Boyer-Moore Voting Algorithm
### Goal 
Find a candidate that appears more than ⌊ n/2 ⌋ times. Find one, not find all.
### Code
LeetCode 169
```python
        candidate = 0
        count = 0
        for x in nums:
            if count == 0:
                candidate = x
                count = 1
            else:
                if x==candidate:
                    count += 1
                else:
                    count -= 1
        if count > 0:
            return candidate
        else:
            return -1
```
### Main Idea
If the candidate is not the majority, the count should be subtracted to 0. It is a good time to choose next candidate, though the previous candidate can be candidate a again in the future.
### Thinking Expansion
#### Division
The array or the list can be divided to several parts.       
The array is [1,1,0,1,1,0,1,0,0].     
We devide it into two parts:      
[1,1,0,1,1] –> (candidate,count)=(1,3)       
[0,1,0,0] –> (candidate,count)=(0,2)            
Based on (1,3) and (0,2)，we get the majority element 1.
#### ⌊ n/3 ⌋
LeetCode 229: Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.
```python
        #“在任何数组中，出现次数大于该数组长度1/3的值最多只有两个。”
        candidate1 = 0
        count1 = 0
        candidate2 = 0
        count2 = 0
        for x in nums:
            if count1 == 0 and x!=candidate2:
                candidate1 = x
                count1 = 1
            elif count2 == 0 and x!=candidate1:
                candidate2 = x
                count2 = 1
            else:
                if x==candidate1:
                    count1 += 1
                elif x==candidate2:
                    count2 += 1
                else:
                    count1 -= 1
                    count2 -= 1
        result = []
        if nums.count(candidate1) > len(nums)//3:
            result.append(candidate1)
        if nums.count(candidate2) > len(nums)//3 and candidate2 != candidate1:
            result.append(candidate2)
        return result
```
### Complexity
Time Complexity: O(n)
Space Complexity: O(1)

