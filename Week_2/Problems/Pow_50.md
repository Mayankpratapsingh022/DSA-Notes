## Power of a Number using Recursion

We need to compute the power of a given number raised to a specified exponent using recursion. Let's consider the example where \( a = 2 \) and \( n = 8 \). The task is to compute \( 2^8 \).

### Approach 1: Simple Recursion

In this approach, we break down the power calculation step by step.

### Steps

1. **Base Case:** 
    - If the exponent \( n \) is 0, return 1. (Since any number to the power of 0 is 1)
    - If the exponent \( n \) is 1, return \( a \). (Since any number to the power of 1 is the number itself)
2. **Recursive Case:** 
    - For \( n > 1 \), the power \( a^n \) can be expressed as \( a \times a^{n-1} \). We use recursion to compute \( a^{n-1} \) and then multiply by \( a \).

### Pseudocode

```
function power(a, n):
    if n == 0:
        return 1
    if n == 1:
        return a
    return a * power(a, n-1)
```

### Python Code

```python
def power(a, n):
    if n == 0:
        return 1
    if n == 1:
        return a
    return a * power(a, n - 1)
```

### Line-by-Line Explanation of Python Code

1. **Function Definition:** `def power(a, n):` defines the function `power` that takes a base `a` and an exponent `n` as inputs.
2. **Base Case for Zero:** `if n == 0:` checks if the exponent is 0.
3. **Return for Zero Exponent:** `return 1` returns 1 since any number raised to the power of 0 is 1.
4. **Base Case for One:** `if n == 1:` checks if the exponent is 1.
5. **Return for One Exponent:** `return a` returns the base \( a \) since any number raised to the power of 1 is the number itself.
6. **Recursive Case:** `return a * power(a, n - 1)` calculates \( a \times a^{n-1} \) by recursively calling the `power` function with the exponent decreased by 1.

## Approach 2: Optimized Power Calculation (Divide and Conquer)

This approach optimizes the power calculation using the divide-and-conquer strategy, which reduces the number of multiplications.

### Steps

1. **Base Case:** 
    - If the exponent \( n \) is 0, return 1.
    - If the exponent \( n \) is 1, return \( a \).
2. **Recursive Case:** 
    - Calculate the midpoint \( \text{mid} = n // 2 \).
    - Recursively compute \( \text{result} = \text{pow}(a, \text{mid}) \).
    - Square the result to get \( \text{finalresult} = \text{result} \times \text{result} \).
    - If \( n \) is even, return \( \text{finalresult} \).
    - If \( n \) is odd, return \( a \times \text{finalresult} \).

### Pseudocode

```
function pow(a, n):
    if n == 0:
        return 1
    if n == 1:
        return a
    mid = n // 2
    result = pow(a, mid)
    finalresult = result * result
    if n % 2 == 0:
        return finalresult
    else:
        return a * finalresult
```

### Python Code

```python
def pow(a, n):
    if n == 0:
        return 1
    if n == 1:
        return a
    mid = n // 2
    result = pow(a, mid)
    finalresult = result * result
    if n % 2 == 0:
        return finalresult
    else:
        return a * finalresult
```

### Line-by-Line Explanation of Python Code

1. **Function Definition:** `def pow(a, n):` defines the function `pow` that takes a base `a` and an exponent `n` as inputs.
2. **Base Case for Zero:** `if n == 0:` checks if the exponent is 0.
3. **Return for Zero Exponent:** `return 1` returns 1 since any number raised to the power of 0 is 1.
4. **Base Case for One:** `if n == 1:` checks if the exponent is 1.
5. **Return for One Exponent:** `return a` returns the base \( a \) since any number raised to the power of 1 is the number itself.
6. **Calculate Midpoint:** `mid = n // 2` calculates the midpoint of the exponent.
7. **Recursive Call:** `result = pow(a, mid)` calls the function recursively with the base \( a \) and the midpoint \( \text{mid} \).
8. **Square Result:** `finalresult = result * result` squares the result of the recursive call.
9. **Check Even Exponent:** `if n % 2 == 0:` checks if the exponent is even.
10. **Return for Even Exponent:** `return finalresult` returns the squared result if the exponent is even.
11. **Odd Exponent Case:** `else:` handles the case where the exponent is odd.
12. **Multiply Base for Odd Exponent:** `return a * finalresult` multiplies the squared result by the base \( a \) if the exponent is odd.

### Handling Negative Exponents

To handle negative exponents, we need to adjust our approach to compute the power of the reciprocal of the base.

### Steps

1. **Check for Negative Exponent:** 
    - If the exponent \( n \) is negative, convert the base \( a \) to its reciprocal and change the exponent \( n \) to its absolute value.
2. **Proceed with Existing Logic:** 
    - Use the existing logic for positive exponents to compute the result.

### Pseudocode

```
function pow(a, n):
    if n == 0:
        return 1
    if n == 1:
        return a
    if n < 0:
        a = 1 / a
        n = -n
    mid = n // 2
    result = pow(a, mid)
    finalresult = result * result
    if n % 2 == 0:
        return finalresult
    else:
        return a * finalresult
```

### Python Code

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        if n == 1:
            return x
        if n < 0:
            x = 1 / x
            n = -n
        mid = n // 2
        result = self.myPow(x, mid)
        finalresult = result * result
        if n % 2 == 0:
            return finalresult
        else:
            return x * finalresult
```

### Line-by-Line Explanation of Python Code

1. **Class Definition:** `class Solution:` defines the class `Solution`.
2. **Function Definition:** `def myPow(self, x: float, n: int) -> float:` defines the function `myPow` that takes a base `x` and an exponent `n` as inputs.
3. **Base Case for Zero:** `if n == 0:` checks if the exponent is 0.
4. **Return for Zero Exponent:** `return 1` returns 1 since any number raised to the power of 0 is 1.
5. **Base Case for One:** `if n == 1:` checks if the exponent is 1.
6. **Return for One Exponent:** `return x` returns the base \( x \) since any number raised to the power of 1 is the number itself.
7. **Negative Exponent Case:** `if n < 0:` checks if the exponent is negative.
8. **Convert Base and Exponent:** `x = 1 / x` and `n = -n` convert the base to its reciprocal and the exponent to its absolute value.
9. **Calculate Midpoint:** `mid = n // 2` calculates the midpoint of the exponent.
10. **Recursive Call:** `result = self.myPow(x, mid)` calls the function recursively with the base \( x \) and the midpoint \( \text{mid} \).
11. **Square Result:** `finalresult = result * result` squares the result of the recursive call.
12. **Check Even Exponent:** `if n % 2 == 0:` checks if the exponent is even.
13. **Return for Even Exponent:** `return finalresult` returns the squared result if the exponent is even.
14. **Odd Exponent Case:** `else:` handles the case where the exponent is odd.
15. **Multiply Base for Odd Exponent:** `return x * finalresult` multiplies the squared result by the base \( x \) if the exponent is odd.

### Complexity Analysis

The time complexity of this optimized approach is \( O(\log n) \) because the exponent is halved at each step. Here's the detailed analysis:

- **Recurrence Relation:** \( T(n) = T

(n/2) + c \), where \( c \) is a constant time operation.
- **Base Case:** \( T(1) = 1 \)
- **Substitution Method:**
    - \( T(n) = T(n/2) + c \)
    - \( T(n/2) = T(n/2^2) + c \)
    - \( T(n) = T(n/2^2) + 2c \)
    - \( T(n) = T(n/2^3) + 3c \)
    - ...
    - \( T(n) = T(n/2^k) + kc \)
- When \( n/2^k = 1 \):
    - \( k = \log_2(n) \)
- Final time complexity:
    - \( T(n) = O(\log n) \)

This logarithmic time complexity is better than the linear time complexity of a naive approach, making it a more efficient solution for calculating powers. The space complexity is also \( O(\log n) \) due to the depth of the recursion stack.
[Pow Leetcode](https://leetcode.com/problems/powx-n/)
