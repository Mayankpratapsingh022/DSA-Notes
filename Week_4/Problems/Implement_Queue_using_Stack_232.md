# 232 Implement Queue using Stacks

### Explanation of the Problem

The problem is to implement a queue using two stacks. A queue follows the First-In-First-Out (FIFO) principle, whereas a stack follows the Last-In-First-Out (LIFO) principle. To achieve the functionality of a queue using two stacks, we need to carefully manage the transfer of elements between the two stacks.

## Key Functions to Implement

1. **push(x: int)**: Adds an element to the back of the queue.
2. **pop() -> int**: Removes and returns the element at the front of the queue.
3. **peek() -> int**: Returns the element at the front of the queue without removing it.
4. **empty() -> bool**: Checks if the queue is empty.

## Solution Using Two Stacks

We use two stacks, `stack1` and `stack2`, to manage the elements. Here's how we use them:

- **stack1**: Used to handle incoming elements via the `push` operation.
- **stack2**: Used to handle outgoing elements via the `pop` and `peek` operations.

### Push Operation

When an element is pushed, it is always pushed onto `stack1`.

### Pop Operation

To pop an element from the queue:

1. If `stack2` is empty, transfer all elements from `stack1` to `stack2`. This reverses the order of elements, making the oldest element (the front of the queue) the top of `stack2`.
2. Pop the top element from `stack2`.

### Peek Operation

To get the front element of the queue without removing it:

1. If `stack2` is not empty, the top element of `stack2` is the front of the queue.
2. If `stack2` is empty, the front element is the first element that was pushed onto `stack1` (stored in `self.front`).

### Empty Operation

The queue is empty if both `stack1` and `stack2` are empty.

## Detailed Python Code Explanation

Here is the Python code with detailed comments:

```python
class MyQueue:

    def __init__(self):
        # Initialize two stacks
        self.stack1 = []
        self.stack2 = []
        # Initialize a variable to keep track of the front element
        self.front = None

    def push(self, x: int) -> None:
        # If stack1 is empty, it means the queue is currently empty
        if not self.stack1:
            # Set the front element to x
            self.front = x
        # Push the element onto stack1
        self.stack1.append(x)

    def pop(self) -> int:
        # If stack2 is empty, we need to transfer elements from stack1 to stack2
        if not self.stack2:
            while self.stack1:
                # Move elements from stack1 to stack2
                self.stack2.append(self.stack1.pop())
        # Pop the top element from stack2, which is the front of the queue
        return self.stack2.pop()

    def peek(self) -> int:
        # If stack2 is not empty, the front of the queue is the top element of stack2
        if self.stack2:
            return self.stack2[-1]
        # If stack2 is empty, the front of the queue is the first element pushed onto stack1
        return self.front

    def empty(self) -> bool:
        # The queue is empty if both stack1 and stack2 are empty
        return not self.stack1 and not self.stack2

# Example usage:
# obj = MyQueue()
# obj.push(1)
# obj.push(2)
# print(obj.peek())  # Output: 1
# print(obj.pop())   # Output: 1
# print(obj.empty()) # Output: False

```

### Explanation of the Code:

1. **Initialization (`__init__` method)**:
    - `self.stack1` and `self.stack2` are initialized as empty lists.
    - `self.front` keeps track of the front element of the queue.
2. **Push (`push` method)**:
    - If `stack1` is empty, `self.front` is set to the element being pushed.
    - The element is appended to `stack1`.
3. **Pop (`pop` method)**:
    - If `stack2` is empty, elements are transferred from `stack1` to `stack2` by popping from `stack1` and pushing to `stack2`.
    - The top element of `stack2` is popped and returned.
4. **Peek (`peek` method)**:
    - If `stack2` is not empty, the top element of `stack2` is returned.
    - If `stack2` is empty, `self.front` is returned.
5. **Empty (`empty` method)**:
    - The method checks if both `stack1` and `stack2` are empty and returns `True` if they are, `False` otherwise.

This approach ensures that each operation is efficient, achieving amortized O(1) time complexity for `push`, `pop`, `peek`, and `empty` operations.

[Implement Queue using Stack LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/submissions/1348987885/)
