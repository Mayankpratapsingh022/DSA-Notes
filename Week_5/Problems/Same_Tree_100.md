# Same Tree
### Approach:

1. **Base Case Considerations**: 
   - If both trees are `None`, they are considered the same.
   - If one tree is `None` and the other is not, they are different.
   - If both trees have a root but the values of the roots differ, they are different.

2. **Recursive Check**:
   - If the current nodes of both trees have the same value, recursively check if their left and right subtrees are the same.
   - If both left subtrees are the same and both right subtrees are the same, then the trees are considered the same.

3. **Final Decision**:
   - If all checks pass, the trees are identical; otherwise, they are different.

### Python Code Implementation:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # Check if both trees are empty
        if p is None and q is None:
            return True
        
        # If one is empty and the other is not, return False
        elif (p is None or q is None or p.val != q.val):
            return False
        
        # Recursively check the left and right subtrees
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

### Explanation:

1. **Function Signature**:
   ```python
   def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
   ```
   - The function `isSameTree` takes two arguments, `p` and `q`, which are the roots of the two binary trees we want to compare. It returns a boolean value indicating whether the trees are the same or not.

2. **Check if Both Trees are Empty**:
   ```python
   if p is None and q is None:
       return True
   ```
   - If both `p` and `q` are `None`, the trees are empty and hence identical, so the function returns `True`.

3. **Check if Only One Tree is Empty or Values Differ**:
   ```python
   elif (p is None or q is None or p.val != q.val):
       return False
   ```
   - If either `p` or `q` is `None` (but not both), it means one tree is empty and the other is not, so they can't be the same, and the function returns `False`.
   - If the values of the current nodes `p.val` and `q.val` differ, then the trees are different, so the function returns `False`.

4. **Recursive Check on Subtrees**:
   ```python
   return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
   ```
   - If the root values of `p` and `q` are the same, the function recursively checks if the left subtrees (`p.left` and `q.left`) are the same and if the right subtrees (`p.right` and `q.right`) are the same.
   - The trees are considered the same only if both the left and right subtrees are identical.

### Summary:
- The solution is based on a recursive approach, where you compare nodes from the roots down to the leaves.
- The function efficiently checks for both structural and value-based equivalence between the two binary trees.
- The time complexity is O(n), where `n` is the number of nodes, because each node in both trees is visited once.

  [Same Tree LeetCode](https://leetcode.com/problems/same-tree/submissions/1350805380/)
