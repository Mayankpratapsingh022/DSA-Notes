# 225 Implement Stack using Queue

### Problem Explanation

A stack is a data structure that follows the Last-In-First-Out (LIFO) principle, where the most recently added element is the first one to be removed. In contrast, a queue follows the First-In-First-Out (FIFO) principle, where the first element added is the first one to be removed.

The challenge here is to implement a stack using only a queue. We need to ensure that the stack operations (`push`, `pop`, `top`, `empty`) behave as expected, even though we're using a queue, which inherently behaves differently.

### Approach

One common approach to implement a stack using queues is to use a single queue with a specific insertion strategy:

1. **Push Operation:** When pushing an element to the stack, we can enqueue it to the queue. However, to maintain the LIFO order, we then dequeue all the elements that were in the queue before this new element and enqueue them back. This ensures that the newest element is always at the front of the queue.
  
2. **Pop Operation:** To pop an element, simply dequeue from the queue. Since we maintained the order with the push operation, the front of the queue will always be the top of the stack.

3. **Top Operation:** The top operation can simply return the front element of the queue.

4. **Empty Operation:** To check if the stack is empty, check if the queue is empty.

### Code Implementation

Let's walk through the Python code that implements this logic.

```python
from collections import deque

class MyStack:
    def __init__(self):
        self.q = deque()
```

- **`from collections import deque`**: This imports the `deque` class, which is used to implement the queue. A `deque` is a double-ended queue that allows fast appends and pops from both ends.
- **`class MyStack:`**: This defines a new class called `MyStack`, which will represent our stack.
- **`def __init__(self):`**: This is the constructor method, which initializes the stack.
- **`self.q = deque()`**: This creates an empty deque to be used as our queue.

```python
    def push(self, x: int) -> None:
        self.q.append(x)
        for _ in range(len(self.q) - 1):
            self.q.append(self.q.popleft())
```

- **`def push(self, x: int) -> None:`**: This defines the `push` method, which takes an integer `x` as input.
- **`self.q.append(x)`**: This adds the element `x` to the end of the deque (similar to enqueueing in a queue).
- **`for _ in range(len(self.q) - 1):`**: This loop iterates through all elements in the deque except the last one (which is the new element we just added).
- **`self.q.append(self.q.popleft())`**: For each iteration, it dequeues an element from the front and enqueues it to the back, effectively rotating the elements so that the newest element is at the front.

```python
    def pop(self) -> int:
        return self.q.popleft()
```

- **`def pop(self) -> int:`**: This defines the `pop` method, which returns an integer.
- **`return self.q.popleft()`**: This removes and returns the element from the front of the deque, which corresponds to the top of the stack.

```python
    def top(self) -> int:
        return self.q[0]
```

- **`def top(self) -> int:`**: This defines the `top` method, which returns an integer.
- **`return self.q[0]`**: This returns the element at the front of the deque without removing it, corresponding to the top of the stack.

```python
    def empty(self) -> bool:
        return len(self.q) == 0
```

- **`def empty(self) -> bool:`**: This defines the `empty` method, which returns a boolean value.
- **`return len(self.q) == 0`**: This checks if the deque is empty by comparing its length to 0. If it's empty, it returns `True`; otherwise, it returns `False`.

### Usage Example

Here's how you can use the `MyStack` class to simulate stack operations:

```python
myStack = MyStack()
myStack.push(1)       # Puts 1 on the stack
myStack.push(2)       # Puts 2 on the stack
print(myStack.top())  # Shows the top item (2) without removing it
print(myStack.pop())  # Removes the top item (2) and shows it
print(myStack.empty()) # Checks if the stack is empty (False)
```

- **`myStack = MyStack()`**: This creates a new stack object.
- **`myStack.push(1)`**: This pushes `1` onto the stack.
- **`myStack.push(2)`**: This pushes `2` onto the stack.
- **`print(myStack.top())`**: This prints the top item of the stack, which is `2`.
- **`print(myStack.pop())`**: This pops the top item off the stack and prints it, so it will print `2`.
- **`print(myStack.empty())`**: This checks if the stack is empty, which it isn’t after one pop, so it prints `False`.

### Conclusion

By using a single queue and rotating the elements during the `push` operation, we can effectively implement a stack with the desired LIFO behavior. This approach ensures that both the `pop` and `top` operations are performed in constant time, making it a reasonably efficient solution.
[Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/submissions/1348955664/)
