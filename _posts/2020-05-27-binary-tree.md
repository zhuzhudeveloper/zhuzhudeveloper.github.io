# Binary Tree
## Definition for a binary tree node.
```
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
          self.val = val
          self.left = left
          self.right = right
```
## DFS
### Preoder (Root, Left, Right)
```
def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = [root]
        while stack:
            node = stack.pop()
            if node:
                res.append(node.val)
                stack.append(node.right)
                stack.append(node.left)
        return res
# O(n), O(n)
```
Recursive
```
def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.dfs(root, res)
        return res

    def dfs(self, root, res):
        if root:
            res.append(root.val)
            self.dfs(root.left, res)
            self.dfs(root.right, res)
```
