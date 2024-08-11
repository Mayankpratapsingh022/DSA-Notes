# Implement Queue using Stacks
### Problem Explanation

A queue is a First-In-First-Out (FIFO) data structure where the first element added is the first to be removed. However, a stack is a Last-In-First-Out (LIFO) data structure, where the last element added is the first to be removed.

The challenge here is to implement a queue using only two stacks, while ensuring that the operations (`push`, `pop`, `peek`, `empty`) behave as expected in a queue.

### Approach

To simulate a queue using two stacks, we can use the following approach:

1. **Two Stacks:** Use two stacks, `stack1` and `stack2`.
   - **`stack1`** is used for pushing elements.
   - **`stack2`** is used for popping and peeking elements.
   
2. **Push Operation:** When pushing an element, we simply push it onto `stack1`.

3. **Pop Operation:** When popping an element:
   - If `stack2` is empty, transfer all elements from `stack1` to `stack2`. This reverses the order of elements, making the oldest element in `stack1` the top element in `stack2`.
   - If `stack2` is not empty, simply pop from `stack2`.

4. **Peek Operation:** Similar to the pop operation, but we return the top element of `stack2` without removing it.

5. **Empty Operation:** The queue is empty only if both `stack1` and `stack2` are empty.

### Code Implementation

Let's go through the Python code that implements this logic step by step.

```python
class MyQueue:

    def __init__(self):
        self.stack1 = []
        self.stack2 = []
        self.front = None
```

- **`class MyQueue:`**: This defines the `MyQueue` class, which represents the queue.
- **`def __init__(self):`**: This is the constructor method, which initializes the queue.
- **`self.stack1 = []`**: Initializes `stack1` as an empty list, which will be used to push elements.
- **`self.stack2 = []`**: Initializes `stack2` as an empty list, which will be used for popping and peeking elements.
- **`self.front = None`**: Initializes `front`, which will keep track of the front element of the queue.

```python
    def push(self, x: int) -> None:
        if not self.stack1:
            self.front = x
        self.stack1.append(x)
```

- **`def push(self, x: int) -> None:`**: Defines the `push` method, which takes an integer `x` as input and returns nothing.
- **`if not self.stack1:`**: Checks if `stack1` is empty. If it is, this means we are pushing the first element, so we set `self.front` to `x`.
- **`self.front = x`**: Sets the front element to `x` if it's the first element being pushed.
- **`self.stack1.append(x)`**: Pushes `x` onto `stack1`.

```python
    def pop(self) -> int:
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        result = self.stack2.pop()
        return result
```

- **`def pop(self) -> int:`**: Defines the `pop` method, which removes and returns the front element of the queue.
- **`if not self.stack2:`**: Checks if `stack2` is empty. If `stack2` is empty, we need to transfer elements from `stack1` to `stack2` to reverse their order.
- **`while self.stack1:`**: A loop that runs while `stack1` is not empty.
- **`self.stack2.append(self.stack1.pop())`**: Pops elements from `stack1` and pushes them onto `stack2`, effectively reversing the order.
- **`result = self.stack2.pop()`**: Pops the top element from `stack2`, which is the front element of the queue.
- **`return result`**: Returns the popped element.

```python
    def peek(self) -> int:
        if self.stack2:
            return self.stack2[-1]
        return self.front
```

- **`def peek(self) -> int:`**: Defines the `peek` method, which returns the front element without removing it.
- **`if self.stack2:`**: Checks if `stack2` is not empty.
- **`return self.stack2[-1]`**: Returns the top element of `stack2`, which is the front of the queue.
- **`return self.front`**: If `stack2` is empty, returns the front element stored in `self.front`.

```python
    def empty(self) -> bool:
        return (not self.stack1 and not self.stack2)
```

- **`def empty(self) -> bool:`**: Defines the `empty` method, which checks if the queue is empty.
- **`return (not self.stack1 and not self.stack2)`**: Returns `True` if both `stack1` and `stack2` are empty, indicating that the queue is empty. Otherwise, it returns `False`.

### Usage Example

Here's how you would use the `MyQueue` class:

```python
myQueue = MyQueue()
myQueue.push(1)       # Queue is: [1]
myQueue.push(2)       # Queue is: [1, 2]
print(myQueue.peek()) # Returns 1
print(myQueue.pop())  # Returns 1, Queue is [2]
print(myQueue.empty()) # Returns False
```

- **`myQueue = MyQueue()`**: Creates a new instance of `MyQueue`.
- **`myQueue.push(1)`**: Pushes `1` into the queue. Now, the queue looks like `[1]`.
- **`myQueue.push(2)`**: Pushes `2` into the queue. Now, the queue looks like `[1, 2]`.
- **`print(myQueue.peek())`**: Returns the front element, which is `1`.
- **`print(myQueue.pop())`**: Pops and returns the front element, which is `1`. The queue is now `[2]`.
- **`print(myQueue.empty())`**: Checks if the queue is empty, which it isn’t, so it returns `False`.

### Conclusion

By using two stacks, we can effectively implement a queue that adheres to the FIFO principle. The key idea is to use one stack for pushing elements and the other for popping and peeking, ensuring that elements are processed in the correct order. The operations are efficient, with the `pop` and `peek` operations being amortized `O(1)` time.

[Implement Queue using Stack LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/submissions/1348987885/)
