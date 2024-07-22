### Problem Statement Explanation

Given an integer array `nums`, the task is to return an array `answer` where `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`. We need to solve this problem without using the division operation and in O(n) time complexity.

### Key Points
1. **No Division Allowed**: We cannot use division to solve this problem.
2. **Time Complexity**: The algorithm must run in O(n) time.
3. **Space Complexity**: Aim for O(1) extra space complexity, meaning we should not use additional space beyond the output array.

### Approach

To achieve this, we can use a two-pass approach:
1. **Left Pass**: Compute the product of all elements to the left of each index.
2. **Right Pass**: Compute the product of all elements to the right of each index.

#### Step-by-Step Plan
1. **Initialize the Output Array**: Start with an array `answer` initialized to 1.
2. **Compute Left Products**: Traverse the array from left to right, calculating the running product of all elements to the left of each element and store it in the corresponding position in `answer`.
3. **Compute Right Products**: Traverse the array from right to left, calculating the running product of all elements to the right of each element and multiply it with the corresponding element in `answer`.

### Pseudocode
```plaintext
function productExceptSelf(nums):
    n = length of nums
    answer = array of size n initialized to 1
    
    # Compute the left products and store in answer
    left_product = 1
    for i from 0 to n-1:
        answer[i] = left_product
        left_product *= nums[i]
    
    # Compute the right products and update answer
    right_product = 1
    for i from n-1 to 0:
        answer[i] *= right_product
        right_product *= nums[i]
    
    return answer
```

### Explanation Line-by-Line
1. **Initialization**:
   ```plaintext
   n = length of nums
   answer = array of size n initialized to 1
   ```
   We initialize the length of `nums` and create an `answer` array filled with 1s, as the product of no numbers is 1.

2. **Compute Left Products**:
   ```plaintext
   left_product = 1
   for i from 0 to n-1:
       answer[i] = left_product
       left_product *= nums[i]
   ```
   - `left_product` starts at 1.
   - For each element in `nums`, we set `answer[i]` to the current `left_product`.
   - We then update `left_product` by multiplying it with `nums[i]`.

3. **Compute Right Products and Update Answer**:
   ```plaintext
   right_product = 1
   for i from n-1 to 0:
       answer[i] *= right_product
       right_product *= nums[i]
   ```
   - `right_product` starts at 1.
   - For each element in `nums` from right to left, we multiply `answer[i]` by the current `right_product`.
   - We then update `right_product` by multiplying it with `nums[i]`.

4. **Return the Result**:
   ```plaintext
   return answer
   ```

### Example Walkthrough
#### Example 1: `nums = [1, 2, 3, 4]`
1. **Left Products**:
   - `answer = [1, 1, 1, 1]` (initial)
   - After left pass: `answer = [1, 1, 2, 6]`

2. **Right Products**:
   - `answer = [24, 12, 8, 6]` after updating with right products

Final `answer = [24, 12, 8, 6]`.

#### Example 2: `nums = [-1, 1, 0, -3, 3]`
1. **Left Products**:
   - `answer = [1, 1, 1, 1, 1]` (initial)
   - After left pass: `answer = [1, -1, -1, 0, 0]`

2. **Right Products**:
   - `answer = [0, 0, 9, 0, 0]` after updating with right products

Final `answer = [0, 0, 9, 0, 0]`.

### Python Code Implementation
```python
def productExceptSelf(nums):
    n = len(nums)
    answer = [1] * n
    
    # Compute the left products and store in answer
    left_product = 1
    for i in range(n):
        answer[i] = left_product
        left_product *= nums[i]
    
    # Compute the right products and update answer
    right_product = 1
    for i in range(n-1, -1, -1):
        answer[i] *= right_product
        right_product *= nums[i]
    
    return answer

# Example usage:
nums1 = [1, 2, 3, 4]
print(productExceptSelf(nums1))  # Output: [24, 12, 8, 6]

nums2 = [-1, 1, 0, -3, 3]
print(productExceptSelf(nums2))  # Output: [0, 0, 9, 0, 0]
```

This Python implementation follows the same logic described earlier, ensuring it runs in O(n) time complexity and uses O(1) extra space complexity.

[Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)
