---
category: algorithm
tags: prefix sum
---
# Prefix Sum
## Characteristics and Main Thoughts
Characteristics: Subarray, Sum to target                      
Main Thoughts: Calculate sum for each element -> Generate a hashmap (key: sum; value: count). Then check if (currentSum - target) in hashmap.
## LeetCode
### LeetCode 437: Path Sum III
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

Example:

root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```
    def pathSum(self, root: TreeNode, sum: int) -> int:
        res = 0
        hashmap = collections.defaultdict(int)
        # Should set 0 for a good start
        hashmap[0] = 1
        def checkSum(root, cursum):
            nonlocal res
            if not root:
                return
            cursum += root.val
            key = cursum - sum
            if key in hashmap:
                res += hashmap[key]
            hashmap[cursum] = hashmap[cursum] + 1
            if root.left:
                checkSum(root.left, cursum)
            if root.right:
                checkSum(root.right, cursum)
            # Can't del it here. +1 -> -1, not delete
            hashmap[cursum] = hashmap[cursum] - 1
        checkSum(root, 0)
        return res
```

