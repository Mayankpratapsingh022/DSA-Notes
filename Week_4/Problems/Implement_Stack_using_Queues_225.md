# 225 Implement Stack using Queues 
 
### Question Explanation

We need to create a stack using only two queues. A stack is like a pile of books where you can only take the top book off or put a new book on the top. The stack should support these actions:

- **push**: Add an item to the top of the stack.
- **pop**: Remove the item from the top of the stack and return it.
- **top**: Look at the item on the top without removing it.
- **empty**: Check if the stack is empty.

### Code Explanation

Let's go through the code step by step.

```python
from collections import deque

class MyStack:
    def __init__(self):
        self.q = deque()

```

- **`from collections import deque`**: This line imports the `deque` class from the `collections` module. A `deque` is like a list but optimized for adding and removing items from both ends.
- **`class MyStack:`**: This line defines a new class called `MyStack`. A class is like a blueprint for creating objects.
- **`def __init__(self):`**: This line defines the constructor method, which is a special function that runs when we create a new `MyStack` object.
- **`self.q = deque()`**: This line creates a new, empty deque and stores it in `self.q`. This deque will act like our queue.

```python
    def push(self, x: int) -> None:
        self.q.append(x)

```

- **`def push(self, x: int) -> None:`**: This line defines a new method called `push` that takes an integer `x` as input and returns nothing (`None`).
- **`self.q.append(x)`**: This line adds the item `x` to the end of the deque `self.q`. This is like putting a book on top of the stack.

```python
    def pop(self) -> int:
        for i in range(len(self.q)-1):
            self.push(self.q.popleft())
        return self.q.popleft()

```

- **`def pop(self) -> int:`**: This line defines a new method called `pop` that returns an integer.
- **`for i in range(len(self.q)-1):`**: This line starts a loop that will run for each item in the deque except the last one.
- **`self.push(self.q.popleft())`**: Inside the loop, this line removes the item from the front of the deque (`popleft()`) and immediately adds it to the back (`push()`). This effectively moves all items except the last one to the back of the deque.
- **`return self.q.popleft()`**: After the loop, this line removes the last item from the front of the deque and returns it. This is like taking the top book off the stack.

```python
    def top(self) -> int:
        return self.q[-1]

```

- **`def top(self) -> int:`**: This line defines a new method called `top` that returns an integer.
- **`return self.q[-1]`**: This line returns the last item in the deque (`self.q[-1]`) without removing it. This is like looking at the top book without taking it off.

```python
    def empty(self) -> bool:
        return len(self.q) == 0

```

- **`def empty(self) -> bool:`**: This line defines a new method called `empty` that returns a boolean (`True` or `False`).
- **`return len(self.q) == 0`**: This line checks if the length of the deque is 0. If it is, it returns `True` (the stack is empty); otherwise, it returns `False`.

### Usage Example

Here's how you would use the `MyStack` class:

```python
myStack = MyStack()
myStack.push(1)       # Puts 1 on the stack
myStack.push(2)       # Puts 2 on the stack
print(myStack.top())  # Shows the top item (2) without removing it
print(myStack.pop())  # Removes the top item (2) and shows it
print(myStack.empty()) # Checks if the stack is empty (False)

```

This creates a stack, adds 1 and 2 to it, shows the top item, removes the top item, and checks if the stack is empty.

[Implement Stack using Queues LeetCode](https://leetcode.com/problems/implement-stack-using-queues/submissions/1348955664/)
