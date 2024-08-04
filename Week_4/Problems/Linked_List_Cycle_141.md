# Linked List Cycle
### Problem Statement

The problem requires determining if a given singly linked list has a cycle. A cycle occurs if a node in the list can be reached again by continuously following the next pointer. The function should return `true` if there is a cycle and `false` otherwise.

### Examples

1. **Input:** head = [3, 2, 0, -4], pos = 1
   **Output:** true
   **Explanation:** There is a cycle where the tail connects to the 1st node.

2. **Input:** head = [1, 2], pos = 0
   **Output:** true
   **Explanation:** There is a cycle where the tail connects to the 0th node.

3. **Input:** head = [1], pos = -1
   **Output:** false
   **Explanation:** There is no cycle in the linked list.

### Constraints

- The number of nodes in the list is in the range [0, 10^4].
- Node values range from -10^5 to 10^5.
- `pos` is -1 or a valid index in the linked list.

### Approach

To determine if there is a cycle in the linked list, we can use Floyd's Tortoise and Hare algorithm. This approach uses two pointers, `slow` and `fast`:

1. **Initialization:** Start both `slow` and `fast` pointers at the head of the list.
2. **Traversal:** Move `slow` pointer one step at a time and `fast` pointer two steps at a time.
3. **Cycle Detection:** If there is a cycle, the `slow` and `fast` pointers will eventually meet. If `fast` reaches the end of the list (`None`), then there is no cycle.

### Pseudocode

```python
function hasCycle(head):
    if head is None:
        return False
    
    slow = head
    fast = head
    
    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False
```

### In-Depth Explanation and Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        # Initialize two pointers, slow and fast, both starting at the head
        slow = head
        fast = head
        
        # Traverse the list
        while slow and fast and fast.next:
            slow = slow.next            # Move slow pointer by 1 step
            fast = fast.next.next       # Move fast pointer by 2 steps
            
            # If slow and fast meet, it indicates a cycle
            if slow == fast:
                return True
        
        # If fast reaches the end, there is no cycle
        return False
```

#### Line-by-Line Explanation

1. **Initialization:** We start by initializing two pointers `slow` and `fast` both pointing to the head of the linked list.
   ```python
   slow = head
   fast = head
   ```

2. **Traversal:** The `while` loop continues as long as `fast` and `fast.next` are not `None`.
   ```python
   while slow and fast and fast.next:
   ```

3. **Move Pointers:** Inside the loop, move the `slow` pointer one step and the `fast` pointer two steps.
   ```python
   slow = slow.next
   fast = fast.next.next
   ```

4. **Cycle Detection:** Check if the `slow` and `fast` pointers meet. If they do, return `True` as there is a cycle.
   ```python
   if slow == fast:
       return True
   ```

5. **No Cycle:** If the loop exits, return `False` as `fast` has reached the end of the list without meeting `slow`.
   ```python
   return False
   ```

### Conclusion

Floyd's Tortoise and Hare algorithm is an efficient way to detect cycles in a linked list using O(1) space and O(n) time complexity. This approach ensures that we can detect the presence of a cycle by leveraging two pointers moving at different speeds through the list.
[Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/submissions/1344018072/)
