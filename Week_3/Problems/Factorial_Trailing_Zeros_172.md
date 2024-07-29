# Factorial Trailing Zeros
### Brute Force Approach

The brute force approach involves calculating the factorial of \( n \) and then counting the number of trailing zeroes. However, this approach is impractical for large values of \( n \) due to the rapid growth of the factorial number.

1. **Calculate the Factorial**: Compute \( n! \).
2. **Count Trailing Zeroes**: Count how many times 10 divides into \( n! \).

Here’s the brute force approach in Python:

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

def count_trailing_zeroes(n):
    fact = factorial(n)
    count = 0
    while fact % 10 == 0:
        count += 1
        fact //= 10
    return count

# Example usage
n = 10
print(count_trailing_zeroes(n))  # Output: 2

```

**Explanation**:

- The `factorial` function calculates \( n! \) recursively.
- The `count_trailing_zeroes` function counts the number of trailing zeroes by repeatedly dividing the factorial by 10.

### Optimized Approach

The optimized approach leverages the fact that trailing zeroes are created by factors of 10 in the factorial. Since \( 10 = 2 \times 5 \), we only need to count the number of times 5 appears as a factor in the numbers from 1 to \( n \). This is because there are usually more factors of 2 than factors of 5.

**Steps**:

1. Count the multiples of 5, 25, 125, etc., up to \( n \).
2. Sum these counts to get the number of trailing zeroes.

Here’s the optimized approach in Python:

```python
def count_trailing_zeroes_optimized(n):
    count = 0
    i = 5
    while n // i > 0:
        count += n // i
        i *= 5
    return count

# Example usage
n = 10
print(count_trailing_zeroes_optimized(n))  # Output: 2

```

**Explanation**:

1. **Initialize** `count` to 0 and `i` to 5.
2. **Loop**: While \( n // i \) is greater than 0, add \( n // i \) to `count` and multiply `i` by 5.
3. **Return** `count`.

**Line-by-Line Guide**:

- `def count_trailing_zeroes_optimized(n):`: Define the function to count trailing zeroes.
- `count = 0`: Initialize the count of trailing zeroes to 0.
- `i = 5`: Start with the first power of 5.
- `while n // i > 0:`: Loop as long as there are multiples of \( i \) (5, 25, 125, etc.) in the factorial.
- `count += n // i`: Add the number of multiples of \( i \) to `count`.
- `i *= 5`: Move to the next power of 5.
- `return count`: Return the total count of trailing zeroes.

### Example

For \( n = 10 \):

- \( 10! = 3628800 \)
- Trailing zeroes: 2 (as 10 and 5 contribute to the trailing zeroes)

For \( n = 25 \):

- Count the multiples of 5: \( 25 // 5 = 5 \)
- Count the multiples of 25: \( 25 // 25 = 1 \)
- Total trailing zeroes: \( 5 + 1 = 6 \)

This optimized solution runs in logarithmic time complexity, making it efficient for large values of \( n \).

[Factorial Trailing Zeros](https://leetcode.com/problems/factorial-trailing-zeroes/submissions/1337184389/)
