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
## BFS
```
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res = []
        level = [root]
        while root and level:
            currentlevelres = []
            nextlevel = []
            for node in level:
                currentlevelres.append(node.val)
                if node.left:
                    nextlevel.append(node.left)
                if node.right:
                    nextlevel.append(node.right)
            res.append(currentlevelres)
            level = nextlevel
        return res
```
Recursive
```
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res = []
        if not root:
            return res
        self.levelOrderHelper(root, 0, res)
        return res
    
    def levelOrderHelper(self, node, levelnum, res):
        if len(res) == levelnum:
            res.append([])
        res[levelnum].append(node.val)
        if node.left:
            self.levelOrderHelper(node.left, levelnum+1, res)
        if node.right:
            self.levelOrderHelper(node.right, levelnum+1, res)
```
## LeetCode 110: Balanced Binary Tree
Given a binary tree, determine if it is height-balanced. For this problem, a height-balanced binary tree is defined as: a binary tree in which the left and right subtrees of every node differ in height by no more than 1.
```
    def height(self, root):
        if not root:
            return -1
        return 1+max(self.height(root.left), self.height(root.right))
    def isBalanced(self, root: TreeNode) -> bool:
        if not root:
            return True
        return abs(self.height(root.left) - self.height(root.right))<2 and self.isBalanced(root.left) and self.isBalanced(root.right)
```
Time Complexity: O(nlogn); Space Complexity: O(n)
```
    def isBalancedHelper(self, root: TreeNode) -> (bool, int):
        # An empty tree is balanced and has height -1
        if not root:
            return True, -1
        
        # Check subtrees to see if they are balanced. 
        leftIsBalanced, leftHeight = self.isBalancedHelper(root.left)
        if not leftIsBalanced:
            return False, 0
        rightIsBalanced, rightHeight = self.isBalancedHelper(root.right)
        if not rightIsBalanced:
            return False, 0
        
        # If the subtrees are balanced, check if the current tree is balanced
        # using their height
        return (abs(leftHeight - rightHeight) < 2), 1 + max(leftHeight, rightHeight)
        
    def isBalanced(self, root: TreeNode) -> bool:
        return self.isBalancedHelper(root)[0]
```
Time Complexity: O(n); Space Compelexity: O(n)
```
