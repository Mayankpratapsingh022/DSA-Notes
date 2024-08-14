# Delete Node In a Linked List 237
### Problem Overview

In this problem, you are asked to delete a node from a singly linked list. However, unlike most linked list problems, you are not given the head of the list. Instead, you are given the node itself that you need to delete.

The challenge is to "delete" the node without actually having access to the head of the list. You are guaranteed that the node to be deleted is not the last node of the list.

### Approach

The key idea here is that since you can't actually remove the node from memory (because you don't have access to the previous node), you can achieve the same effect by copying the data from the next node to the current node and then bypassing the next node. 

This way, the current node effectively takes on the identity of the next node, and the next node is "deleted" by being bypassed.

### Code Explanation

```python
class Solution:
    def deleteNode(self, node):
        node.val = node.next.val
        node.next = node.next.next
```

Let's break down the code:

1. **Copy the Value of the Next Node:**
   ```python
   node.val = node.next.val
   ```
   - Here, you replace the value of the current node (`node`) with the value of the next node (`node.next`).
   - For example, if the current node has a value of `5` and the next node has a value of `1`, after this line, the current node will have the value `1`.

2. **Bypass the Next Node:**
   ```python
   node.next = node.next.next
   ```
   - In this step, you update the `next` pointer of the current node to skip the next node.
   - Essentially, the current node now points to the node after the next node. The original "next" node is now effectively removed from the linked list.
   - Continuing with the example, if the original list was `4 -> 5 -> 1 -> 9`, after these two lines, the list would become `4 -> 1 -> 9`.

### Why This Works

- **Node Value Replacement:** By copying the value from the next node, the current node "becomes" the next node in terms of data.
- **Node Removal:** By skipping the next node, you effectively remove it from the list.

### Example Walkthrough

Let's walk through the examples given in the problem statement:

1. **Example 1:**
   - **Input:** `head = [4,5,1,9]`, `node = 5`
   - **Process:**
     - Copy the value `1` (from the next node) into the node with value `5`.
     - Update the `next` pointer of the node to point to the node after the next node, which is `9`.
   - **Output:** The list becomes `4 -> 1 -> 9`.

2. **Example 2:**
   - **Input:** `head = [4,5,1,9]`, `node = 1`
   - **Process:**
     - Copy the value `9` (from the next node) into the node with value `1`.
     - Update the `next` pointer of the node to point to `None` because there's no node after `9`.
   - **Output:** The list becomes `4 -> 5 -> 9`.

### Edge Cases

- **Node is not the last node:** The problem guarantees that the node is not the last node, so this solution will always work.
- **Minimum Size List:** The smallest possible list has two nodes, and this solution works perfectly for that as well.

### Conclusion

This problem is a bit unique because it challenges you to think differently about linked list manipulation. Instead of traditional deletion, you effectively shift the problem of deletion by copying data and bypassing the node. This method is efficient and works within the problem constraints.

[Delete Node in a LinkedLIst](https://leetcode.com/problems/delete-node-in-a-linked-list/submissions/1354431711/)

