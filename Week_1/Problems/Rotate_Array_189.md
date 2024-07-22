### Problem Statement Explanation

Given an integer array `nums`, we need to rotate the array to the right by `k` steps. The rotation means shifting each element of the array to the right by `k` positions. If an element is moved past the end of the array, it wraps around to the beginning.

### Key Points
1. **Rotation**: Moving elements in the array to the right by `k` steps.
2. **Wrapping Around**: Elements that move past the end of the array should appear at the beginning.
3. **In-Place**: Perform the rotation without using extra space (in-place with O(1) extra space).

### Examples
1. `nums = [1, 2, 3, 4, 5, 6, 7]`, `k = 3`
   - Rotate right by 1 step: `[7, 1, 2, 3, 4, 5, 6]`
   - Rotate right by 2 steps: `[6, 7, 1, 2, 3, 4, 5]`
   - Rotate right by 3 steps: `[5, 6, 7, 1, 2, 3, 4]`

2. `nums = [-1, -100, 3, 99]`, `k = 2`
   - Rotate right by 1 step: `[99, -1, -100, 3]`
   - Rotate right by 2 steps: `[3, 99, -1, -100]`

### Approach

We can use the reversal algorithm to solve this problem in-place with O(1) extra space. The idea is to reverse parts of the array to achieve the desired rotation.

### Steps
1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the remaining `n-k` elements.

### Pseudocode
```plaintext
function reverse(array, start, end):
    while start < end:
        swap array[start] and array[end]
        start += 1
        end -= 1

function rotate(array, k):
    n = length of array
    k = k % n  # In case k is larger than the length of array

    reverse(array, 0, n-1)
    reverse(array, 0, k-1)
    reverse(array, k, n-1)
```

### Python Code Implementation with Line-by-Line Explanation
```python
class Solution:
    def reverse(self, nums, low, high):
        # Reverse the elements between indices low and high
        while low < high:
            # Swap the elements at indices low and high
            nums[low], nums[high] = nums[high], nums[low]
            low += 1
            high -= 1
        
    def rotate(self, nums: List[int], k: int) -> None:
        n = len(nums)
        k = k % n  # Handle the case where k is larger than the length of nums

        # Step 1: Reverse the entire array
        self.reverse(nums, 0, n-1)
        
        # Step 2: Reverse the first k elements
        self.reverse(nums, 0, k-1)
        
        # Step 3: Reverse the remaining n-k elements
        self.reverse(nums, k, n-1)

# Example usage:
sol = Solution()
nums1 = [1, 2, 3, 4, 5, 6, 7]
k1 = 3
sol.rotate(nums1, k1)
print(nums1)  # Output: [5, 6, 7, 1, 2, 3, 4]

nums2 = [-1, -100, 3, 99]
k2 = 2
sol.rotate(nums2, k2)
print(nums2)  # Output: [3, 99, -1, -100]
```

### Line-by-Line Explanation
1. **reverse Function**:
   ```python
   def reverse(self, nums, low, high):
       while low < high:
           nums[low], nums[high] = nums[high], nums[low]
           low += 1
           high -= 1
   ```
   - This function reverses the elements in `nums` between indices `low` and `high`.
   - It uses a while loop to swap elements at the `low` and `high` indices and then moves `low` up and `high` down until they meet.

2. **rotate Function**:
   ```python
   def rotate(self, nums: List[int], k: int) -> None:
       n = len(nums)
       k = k % n  # Handle the case where k is larger than the length of nums
   ```
   - `n` is the length of the array `nums`.
   - `k = k % n` ensures that `k` is within the bounds of the array's length, handling cases where `k` is larger than `n`.

   ```python
       self.reverse(nums, 0, n-1)
   ```
   - Step 1: Reverse the entire array.

   ```python
       self.reverse(nums, 0, k-1)
   ```
   - Step 2: Reverse the first `k` elements.

   ```python
       self.reverse(nums, k, n-1)
   ```
   - Step 3: Reverse the remaining `n-k` elements.

By following these steps, the array `nums` is rotated to the right by `k` steps in-place with O(1) extra space complexity.

[Rotate Array Leetcode](https://leetcode.com/problems/rotate-array/description/)
