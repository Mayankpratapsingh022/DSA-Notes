
## Finding Peak Element

### Problem Description

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

### Example 1:

```

Input: nums = [1, 2, 3, 1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.

```

### Example 2:

```

Input: nums = [1, 2, 1, 3, 5, 6, 4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

```

### Constraints:
- `1 <= nums.length <= 1000`
- `-2^31 <= nums[i] <= 2^31 - 1`
- `nums[i] != nums[i + 1]` for all valid `i`.

### Brute Force Approach

The brute force approach involves linearly traversing the entire array to find a peak element. The time complexity is `O(n)`.

#### Pseudocode for Brute Force Approach:
```plaintext
for i = 0 to n - 1:
    if (i == 0 and nums[i] > nums[i + 1]) or
       (i == n - 1 and nums[i] > nums[i - 1]) or
       (nums[i] > nums[i - 1] and nums[i] > nums[i + 1]):
        return i
return -1

```

### Explanation:

- Loop through each element (`i` from 0 to `n - 1`).
- Check if the current element is a peak:
    - If `i` is 0 and `nums[i] > nums[i + 1]`, return `i`.
    - If `i` is `n - 1` and `nums[i] > nums[i - 1]`, return `i`.
    - If `nums[i] > nums[i - 1]` and `nums[i] > nums[i + 1]`, return `i`.
- If no peak is found, return `1`.

### Optimized Approach

To achieve the `O(log n)` time complexity, we can use binary search.

### Pseudocode for Optimized Approach:

```
n = len(nums)
low = 0
high = n - 1

while low <= high:
    mid = low + (high - low) // 2
    if (mid == 0 or nums[mid] > nums[mid - 1]) and
       (mid == n - 1 or nums[mid] > nums[mid + 1]):
        return mid
    elif mid > 0 and nums[mid] < nums[mid - 1]:
        high = mid - 1
    else:
        low = mid + 1
return -1

```

### Explanation:

1. **Initialize Variables:**
    - `n = len(nums)`: Length of the array.
    - `low = 0`: Start index.
    - `high = n - 1`: End index.
2. **Binary Search Loop:**
    - While `low` is less than or equal to `high`:
        - Calculate `mid = low + (high - low) // 2`.
        - **Check if `mid` is a peak element:**
            - If `mid` is 0 or `nums[mid] > nums[mid - 1]` (left neighbor is smaller or `mid` is the first element).
            - If `mid` is `n - 1` or `nums[mid] > nums[mid + 1]` (right neighbor is smaller or `mid` is the last element).
            - If both conditions are true, return `mid`.
        - **Adjust Search Range:**
            - If `nums[mid] < nums[mid - 1]`, search the left half: `high = mid - 1`.
            - Otherwise, search the right half: `low = mid + 1`.
3. **Return `1` if no peak is found** (though by the problem's nature, there should always be a peak).

### Python Code

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        low, high = 0, n - 1

        while low <= high:
            mid = low + (high - low) // 2
            if (mid == 0 or nums[mid] > nums[mid - 1]) and (mid == n - 1 or nums[mid] > nums[mid + 1]):
                return mid
            elif mid > 0 and nums[mid] < nums[mid - 1]:
                high = mid - 1
            else:
                low = mid + 1

        return -1

```

### Explanation of the Code:

1. **Initialize Dimensions and Search Range:**
    - `n = len(nums)`: Length of the array.
    - `low = 0`: Start index of the array.
    - `high = n - 1`: End index of the array.
2. **Binary Search Loop:**
    - Calculate `mid = low + (high - low) // 2`.
    - **Check if `mid` is a peak element:**
        - If `mid` is 0 or `nums[mid] > nums[mid - 1]` (left neighbor is smaller or `mid` is the first element).
        - If `mid` is `n - 1` or `nums[mid] > nums[mid + 1]` (right neighbor is smaller or `mid` is the last element).
        - If both conditions are true, return `mid`.
    - **Adjust Search Range:**
        - If `nums[mid] < nums[mid - 1]`, search the left half: `high = mid - 1`.
        - Otherwise, search the right half: `low = mid + 1`.
3. **Return `1` if no peak is found** (though by the problem's nature, there should always be a peak).

This structured approach covers the problem description, brute force solution, optimized solution, pseudocode, and line-by-line explanation of the code.


[Find Peak Element](https://leetcode.com/problems/find-peak-element/?envType=study-plan-v2&envId=top-interview-150)
