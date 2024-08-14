#  Validate Binary Search Tree
### Problem Recap

A **Binary Search Tree (BST)** is a binary tree where:
- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be BSTs.

The task is to determine if a given binary tree satisfies the properties of a BST.

### Code Breakdown

```python
class Solution:
    def inOrderTraversal(self, node):
        if node:
            self.inOrderTraversal(node.left)
            self.result.append(node.val)
            self.inOrderTraversal(node.right)
```

#### `inOrderTraversal` function:
- This function is designed to perform an **in-order traversal** of the binary tree. In an in-order traversal, we visit the left subtree first, then the current node, and finally the right subtree.
- **Line 3:** `if node:` checks if the current node is `None`. If the node is `None`, it means we've reached a leaf node's child, so the function returns without doing anything.
- **Line 4:** `self.inOrderTraversal(node.left)` recursively calls the `inOrderTraversal` function on the left child of the current node.
- **Line 5:** `self.result.append(node.val)` appends the value of the current node to the `result` list. Since it's an in-order traversal, the `result` list will contain the node values in sorted order if the tree is a valid BST.
- **Line 6:** `self.inOrderTraversal(node.right)` recursively calls the `inOrderTraversal` function on the right child of the current node.

```python
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        if root is None:
            return True  # An empty tree is a valid BST.
```

#### `isValidBST` function:
- This is the main function that determines whether the binary tree rooted at `root` is a valid BST.
- **Line 9:** `if root is None:` checks if the tree is empty. An empty tree is considered a valid BST, so we return `True`.

```python
        self.result = []
        self.inOrderTraversal(root)
        n = len(self.result)
```

- **Line 11:** `self.result = []` initializes an empty list `result` that will store the in-order traversal of the tree.
- **Line 12:** `self.inOrderTraversal(root)` performs an in-order traversal of the tree starting from the `root` node and populates the `result` list with the node values.
- **Line 13:** `n = len(self.result)` stores the length of the `result` list in variable `n`.

```python
        # Check if the result list is sorted and has no duplicates
        for i in range(n - 1):
            if self.result[i] >= self.result[i + 1]:
                return False
        return True
```

- **Line 15-16:** The code checks if the `result` list is sorted in strictly increasing order, which is a requirement for the tree to be a valid BST.
    - **Line 15:** A `for` loop iterates through the `result` list, comparing each element with the next element.
    - **Line 16:** `if self.result[i] >= self.result[i + 1]:` checks if the current element is greater than or equal to the next element. If this condition is true, the tree is not a valid BST, and the function returns `False`.
- **Line 17:** If the loop completes without finding any violations, the function returns `True`, indicating that the tree is a valid BST.

### Summary of Approach

1. **In-order Traversal:** The code uses in-order traversal to generate a list of node values. In a valid BST, the result of in-order traversal should be a list of sorted values in strictly increasing order.
2. **Validation:** The code then checks if this list is sorted. If any value in the list is greater than or equal to the next value, the tree is not a valid BST.

### Example Walkthrough

**Example 1:** `root = [2,1,3]`
- In-order traversal of this tree gives `[1, 2, 3]`, which is sorted in increasing order.
- The function returns `True`.

**Example 2:** `root = [5,1,4,null,null,3,6]`
- In-order traversal of this tree gives `[1, 5, 3, 4, 6]`, which is **not** sorted.
- The function returns `False`.

This approach ensures that we can determine if a binary tree is a valid BST by performing an in-order traversal and then checking the sorted order of the result.
[Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/submissions/1353042546/)
