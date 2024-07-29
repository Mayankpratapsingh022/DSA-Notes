
# Palindrome Number

### Using String Conversion

The simplest way to check if a number is a palindrome is to convert the number to a string and check if the string reads the same forwards and backwards.

Here’s the step-by-step solution:

1. **Convert the integer to a string**.
2. **Reverse the string**.
3. **Compare the original string with the reversed string**.

Here's the code:

```python
def isPalindrome(x: int) -> bool:
    # Convert the number to a string
    str_x = str(x)
    # Reverse the string
    reversed_str_x = str_x[::-1]
    # Check if the original string is equal to the reversed string
    return str_x == reversed_str_x

# Test cases
print(isPalindrome(121))  # Output: True
print(isPalindrome(-121)) # Output: False
print(isPalindrome(10))   # Output: False

```

### Without String Conversion

To solve the problem without converting the integer to a string, you can follow these steps:

1. **Handle negative numbers**: A negative number cannot be a palindrome because of the minus sign.
2. **Reverse half of the number**: Compare the reversed second half with the first half.

Here's the step-by-step explanation:

1. **Check if the number is negative**: If `x` is negative, return `false` immediately.
2. **Initialize variables**: Use a variable to store the reversed number (initialize it to 0).
3. **Iterate to reverse half of the number**: Use a loop to build the reversed second half of the number.
4. **Compare the original number and the reversed number**: If they are the same or if the original number without the last digit (in case of odd length) is equal to the reversed number, it is a palindrome.

Here's the code:

```python
def isPalindrome(x: int) -> bool:
    # If x is negative or if the last digit is 0 (but x is not 0), it can't be a palindrome
    if x < 0 or (x % 10 == 0 and x != 0):
        return False

    # Initialize reversed number to 0
    reversed_half = 0
    while x > reversed_half:
        # Add the last digit of x to reversed_half
        reversed_half = reversed_half * 10 + x % 10
        # Remove the last digit from x
        x //= 10

    # If the length is an odd number, we can get rid of the middle digit by reversed_half//10
    # For example, when the input is 12321, at the end of the while loop we get x = 12, reversed_half = 123,
    # since the middle digit doesn't matter in palindrome(it will always equal to itself), we can simply get rid of it.
    return x == reversed_half or x == reversed_half // 10

# Test cases
print(isPalindrome(121))  # Output: True
print(isPalindrome(-121)) # Output: False
print(isPalindrome(10))   # Output: False

```

### Explanation of the optimized approach

1. **Negative check**: A negative number or a number ending in 0 (but not 0 itself) cannot be a palindrome.
2. **Reverse the second half**: We reverse the second half of the number and compare it to the first half.
3. **Odd length numbers**: For numbers with an odd number of digits, we discard the middle digit by dividing the reversed number by 10.

By following these steps, you can determine whether a given integer is a palindrome without converting it to a string.

[Palindrome Number](https://leetcode.com/problems/palindrome-number/submissions/1337271068/)
