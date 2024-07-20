## Solving Fibonacci Sequence Using Recursion

The Fibonacci sequence is a series of numbers where each number is the sum of the two preceding ones. This sequence starts with 0 and 1. The problem can be described as follows:

- **Base Cases:**
    - \( F(0) = 0 \)
    - \( F(1) = 1 \)
- **Recursive Case:**
    - \( F(n) = F(n - 1) + F(n - 2) \) for \( n > 1 \)

### Example Calculations

- **Example 1:**
    - Input: \( n = 2 \)
    - Output: \( F(2) = F(1) + F(0) = 1 + 0 = 1 \)
- **Example 2:**
    - Input: \( n = 3 \)
    - Output: \( F(3) = F(2) + F(1) = 1 + 1 = 2 \)
- **Example 3:**
    - Input: \( n = 4 \)
    - Output: \( F(4) = F(3) + F(2) = 2 + 1 = 3 \)

### Pseudocode

1. **Function Definition:**
    - Define a function `fib(n)` that calculates the Fibonacci number for a given `n`.
2. **Base Cases:**
    - If `n` is 0, return 0.
    - If `n` is 1, return 1.
3. **Recursive Case:**
    - Return the sum of `fib(n-1)` and `fib(n-2)`.

### Pseudocode Representation

```
function fib(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    return fib(n-1) + fib(n-2)

```

### Python Code

```python
class Solution:
    def fib(self, n: int) -> int:
        # BASE CASES
        if n == 0:
            return 0
        if n == 1:
            return 1

        # RECURSIVE CASE
        return self.fib(n - 1) + self.fib(n - 2)

```

### Explanation of the Code

1. **Function Definition:**
    - `def fib(self, n: int) -> int:`: This line defines a method `fib` within the `Solution` class, which takes an integer `n` and returns an integer.
2. **Base Cases:**
    - `if n == 0: return 0`: If the input `n` is 0, the function returns 0.
    - `if n == 1: return 1`: If the input `n` is 1, the function returns 1.
3. **Recursive Case:**
    - `return self.fib(n - 1) + self.fib(n - 2)`: For any other value of `n`, the function calls itself with the arguments `n - 1` and `n - 2`, sums the results, and returns the sum. This is based on the Fibonacci recurrence relation.

### Detailed Line-by-Line Explanation

```python
class Solution:                          # Define the Solution class.
    def fib(self, n: int) -> int:        # Define the fib method, which takes an integer n and returns an integer.
        if n == 0:                       # Check if n is 0.
            return 0                     # If true, return 0.
        if n == 1:                       # Check if n is 1.
            return 1                     # If true, return 1.
        return self.fib(n - 1) + self.fib(n - 2)  # If n is neither 0 nor 1, recursively call fib with n-1 and n-2, sum the results, and return the sum.

```

### Notes

- **Base Cases:** The base cases handle the simplest inputs directly, which stops the recursion from continuing indefinitely.
- **Recursive Case:** The recursive case builds on smaller instances of the problem, reducing the size of the input each time until it reaches the base cases.
- **Efficiency Considerations:** While this recursive approach is straightforward, it has exponential time complexity \(O(2^n)\) due to repeated calculations. For larger values of `n`, consider using dynamic programming or memoization to optimize the solution.

This approach outlines the fundamental steps to solve Fibonacci sequence problems using recursion and provides a detailed explanation of the code and logic involved.


      
[Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
