### Problem Statement

The problem requires reversing a singly linked list. Given the head of a singly linked list, we need to reverse the list and return the new head of the reversed list.

### Examples

1. **Input:** head = [1, 2, 3, 4, 5]
   **Output:** [5, 4, 3, 2, 1]

2. **Input:** head = [1, 2]
   **Output:** [2, 1]

3. **Input:** head = []
   **Output:** []

### Constraints

- The number of nodes in the list is in the range [0, 5000].
- Node values range from -5000 to 5000.

### Approaches

The linked list can be reversed either iteratively or recursively. Below, I'll explain both approaches.

### Iterative Approach

#### Explanation

1. **Initialization:** Start with three pointers: `prev`, `curr`, and `nextPtr`.
   - `prev` will be initialized to `None` because initially, there is no previous node.
   - `curr` will be initialized to the head of the list.
   - `nextPtr` will be used to temporarily store the next node in the list during the reversal process.

2. **Iterate through the list:**
   - While `curr` is not `None` (i.e., we have not reached the end of the list):
     - Store the next node (`curr.next`) in `nextPtr`.
     - Reverse the current node's pointer by setting `curr.next` to `prev`.
     - Move `prev` to `curr`.
     - Move `curr` to `nextPtr`.

3. **Return the new head:** At the end of the loop, `prev` will point to the new head of the reversed list.

#### Pseudocode

```python
function reverseList(head):
    prev = None
    curr = head
    nextPtr = None

    while curr is not None:
        nextPtr = curr.next  # Store next node
        curr.next = prev     # Reverse current node's pointer
        prev = curr          # Move prev to current node
        curr = nextPtr       # Move to next node

    return prev  # New head of the reversed list
```

#### Line-by-Line Explanation

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None              # Initialize previous node as None
        curr = head              # Start with the head of the list
        nextPtr = None           # Temporary pointer for the next node
        
        while curr:              # Traverse until curr is None
            nextPtr = curr.next  # Store the next node
            curr.next = prev     # Reverse the current node's pointer
            prev = curr          # Move prev to the current node
            curr = nextPtr       # Move to the next node in the list
        
        head = prev              # Update head to the new first node
        return head              # Return the new head of the reversed list
```

### Recursive Approach (Alternative)

#### Explanation

1. **Base Case:** If `head` is `None` or `head.next` is `None`, return `head`. This means we've reached the end of the list.

2. **Recursive Case:** Reverse the rest of the list and fix the current node.
   - Recursively call `reverseList` for the next node.
   - Once the recursive call returns, set the next node's next pointer to the current node.
   - Set the current node's next pointer to `None`.

3. **Return the new head:** The result of the recursive call is the new head of the reversed list.

#### Pseudocode

```python
function reverseList(head):
    if head is None or head.next is None:
        return head
    
    newHead = reverseList(head.next)  # Reverse the rest of the list
    head.next.next = head             # Fix the current node
    head.next = None                  # Set current node's next to None
    
    return newHead                    # Return the new head
```

### Conclusion

Both iterative and recursive approaches achieve the goal of reversing the linked list. The iterative approach is typically easier to understand and implement, especially for beginners.
[Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/submissions/1343979862/)
