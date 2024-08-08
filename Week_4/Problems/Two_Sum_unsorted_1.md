# 1 Two Sum
### Problem Explanation

Given an array of integers `nums` and an integer `target`, you need to find two indices of the numbers in the array such that they add up to the `target`. The solution assumes that there is exactly one solution and that the same element cannot be used twice.

### Solution Strategy

We can use a dictionary to store the numbers and their indices as we iterate through the array. For each number, we check if the complement (i.e., `target - num`) exists in the dictionary. If it does, we have found the two numbers that add up to the target. If not, we add the current number and its index to the dictionary.

Here is the solution implemented in Python:

```python
pythonCopy code
from typing import List

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}  # Dictionary to store numbers and their indices

        for i, num in enumerate(nums):
            complement = target - num  # Find the complement of the current number
            if complement in seen:
                return [seen[complement], i]  # Return the indices of the two numbers
            seen[num] = i  # Add the current number and its index to the dictionary

        # If no solution is found, return an empty list (though the problem guarantees a solution exists)
        return []

# Example usage:
solution = Solution()
print(solution.twoSum([2, 7, 11, 15], 9))  # Output: [0, 1]
print(solution.twoSum([3, 2, 4], 6))       # Output: [1, 2]
print(solution.twoSum([3, 3], 6))          # Output: [0, 1]

```

### Explanation

1. **Initialization**:
    - A dictionary `seen` is initialized to keep track of the numbers and their corresponding indices.
2. **Iteration**:
    - We iterate through the list `nums` using `enumerate` to get both the index `i` and the number `num`.
    - For each number, we calculate its complement (`target - num`).
3. **Check for Complement**:
    - If the complement is already in the dictionary `seen`, it means we have found the two numbers that add up to the `target`.
    - We return the indices of the complement and the current number.
4. **Update Dictionary**:
    - If the complement is not found, we add the current number and its index to the dictionary.
5. **Return Result**:
    - If no solution is found during the iteration (which theoretically should not happen as per the problem constraints), we return an empty list.

### Time Complexity

- **Time Complexity**: O(n) because we are iterating through the list once and dictionary operations (insert and lookup) are on average O(1).
    
    O(n)O(n)
    
    O(1)O(1)
    
- **Space Complexity**: O(n) for storing the elements and their indices in the dictionary.
    
    O(n)O(n)
    

This approach ensures that we efficiently find the indices of the two numbers that add up to the target, meeting the problem's constraints and requirements.

[Two Sum Leetcode -My sol](https://leetcode.com/problems/two-sum/submissions/1348788823/)
