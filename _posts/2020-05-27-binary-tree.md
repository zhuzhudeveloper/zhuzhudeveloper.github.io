---
category: algorithm
tags: Binary Tree
---
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
### Inorder (Left, Root, Right)
```
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = []
        while True:
            while root:
                stack.append(root)
                root = root.left
            if not stack:
                return res
            node = stack.pop()
            res.append(node.val)
            root = node.right
```
Recursive
```
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.inorderHelper(root, res)
        return res
    def inorderHelper(self, root, res):
        if root:
            self.inorderHelper(root.left, res)
            res.append(root.val)
            self.inorderHelper(root.right, res)
```
### Postorder (Left, Right, Root)
Stack: Remember the visited status
```
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = [(root, False)]
        while stack:
            node, visited = stack.pop()
            if node:
                if visited:
                    res.append(node.val)
                else:
                    stack.append((node, True))
                    stack.append((node.right, False))
                    stack.append((node.left, False))
        return res
```
Preorder Method can also be used here. [::-1]result
```
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = [root]
        while stack:
            node = stack.pop()
            if node:
                res.append(node.val)
                stack.append(node.left)
                stack.append(node.right)
        return res[::-1]
```
Recursive
```
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.postorderHelper(root, res)
        return res
    def postorderHelper(self, root, res):
        if root:
            self.postorderHelper(root.left, res)
            self.postorderHelper(root.right, res)
            res.append(root.val)
```
