# Finding Missing and Repeated Elements in an Array

In this note, we'll discuss different approaches to solve the problem of finding the missing and repeated elements in an array. We'll start with a brute force solution and move on to more optimized methods, highlighting the bit manipulation (XOR) approach as the most optimized one.

## Problem Statement

Given an array of size `n` containing elements from `1` to `n`, find the missing and repeated elements.

### Example

Given array: `[1, 2, 3, 3, 4, 5]`
Missing element: `6`
Repeated element: `3`



## Approach 1: Brute Force

### Pseudocode

1. Initialize a variable `missing` to `None`.
2. Iterate through numbers from `1` to `n`.
3. For each number, check if it is in the array.
4. If a number is not found, assign it to `missing`.
5. Return the `missing` number.

### Python Code

```python
def find_missing(nums):
    n = len(nums) + 1  # Length should be n+1 because one element is missing
    missing = None

    # Iterate through numbers from 1 to n
    for i in range(1, n + 1):
        # Check if the number is in the array
        if i not in nums:
            missing = i
            break

    return missing

# Example usage
nums = [1, 2, 3, 5]
print(find_missing(nums))  # Output: 4

```

## Approach 2: Using Summation

### Pseudocode

1. Calculate the sum of the first `n` natural numbers using the formula `n * (n + 1) / 2`.
2. Calculate the sum of the elements in the array.
3. The difference between the expected sum and the actual sum is the missing number.

### Python Code

```python
def find_missing(nums):
    n = len(nums) + 1  # Length should be n+1 because one element is missing

    # Calculate the expected sum of the first n natural numbers
    total_sum = n * (n + 1) // 2

    # Calculate the sum of the elements in the array
    actual_sum = sum(nums)

    # The difference is the missing number
    missing = total_sum - actual_sum

    return missing

# Example usage
nums = [1, 2, 3, 5]
print(find_missing(nums))  # Output: 4

```

## Approach 3: Using XOR (Bit Manipulation)

### Pseudocode

1. Initialize a variable `xor1` to `0`.
2. XOR all the numbers from `1` to `n`.
3. XOR all the elements in the array.
4. The result will be the missing number since the repeated elements will cancel out.

### Python Code

```python
def find_missing(nums):
    n = len(nums) + 1  # Length should be n+1 because one element is missing
    xor1 = 0

    # XOR all numbers from 1 to n
    for i in range(1, n + 1):
        xor1 ^= i

    # XOR all elements in the array
    for num in nums:
        xor1 ^= num

    # The result is the missing number
    missing = xor1

    return missing

# Example usage
nums = [1, 2, 3, 5]
print(find_missing(nums))  # Output: 4

```

## Conclusion

In summary, the brute force solution checks each number from `1` to `n` to find the missing element, which has a time complexity of `O(n^2)`. The summation approach calculates the difference between the expected sum and the actual sum to find the missing element, which has a time complexity of `O(n)`. The XOR approach uses bit manipulation to find the missing element with a time complexity of `O(n)` and a space complexity of `O(1)`.

The XOR approach is the most efficient in terms of both time and space complexity.

[LeetCode Missing Number](https://leetcode.com/problems/missing-number/)
