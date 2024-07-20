


# Search a 2D Matrix

### Problem Description

You are given an `m x n` integer matrix `matrix` with the following properties:
- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` is in `matrix` or `false` otherwise.

You must write a solution with `O(log(m * n))` time complexity.

### Example 1:
```
Input: matrix = [[1, 3, 5, 7], [10, 11, 16, 20], [23, 30, 34, 60]], target = 3
Output: true
```

### Example 2:
```
Input: matrix = [[1, 3, 5, 7], [10, 11, 16, 20], [23, 30, 34, 60]], target = 13
Output: false
```

### Constraints:
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-10^4 <= matrix[i][j], target <= 10^4`

### Brute Force Approach

The brute force approach involves linearly traversing the entire matrix to find the target value. The time complexity is `O(m * n)`.

#### Pseudocode for Brute Force Approach:
```plaintext
for i = 0 to m:
    for j = 0 to n:
        if matrix[i][j] == target:
            return true
return false
```

#### Explanation:
- Loop through each row (`i` from 0 to `m`).
- Within each row, loop through each column (`j` from 0 to `n`).
- If the current element `matrix[i][j]` is equal to `target`, return `true`.
- If the loop completes without finding the `target`, return `false`.

### Optimized Approach

To achieve the `O(log(m * n))` time complexity, we can treat the 2D matrix as a virtual 1D array and apply binary search.

#### Steps to Convert 2D Index to 1D Index:
- Let `n` be the number of columns.
- `row_idx = index // n` (integer division)
- `col_idx = index % n` (modulus)

#### Pseudocode for Optimized Approach:
```plaintext
m = len(matrix)
n = len(matrix[0])
low = 0
high = m * n - 1

while low <= high:
    mid = low + (high - low) // 2
    row_idx = mid // n
    col_idx = mid % n
    midElement = matrix[row_idx][col_idx]
    
    if target == midElement:
        return true
    elif target < midElement:
        high = mid - 1
    else:
        low = mid + 1

return false
```

#### Explanation:
1. **Initialize Variables:**
    - `m = len(matrix)`: Number of rows.
    - `n = len(matrix[0])`: Number of columns.
    - `low = 0`: Start of the virtual array.
    - `high = m * n - 1`: End of the virtual array.

2. **Binary Search Loop:**
    - While `low` is less than or equal to `high`:
        - Calculate `mid = low + (high - low) // 2`.
        - Convert `mid` to 2D indices: `row_idx = mid // n`, `col_idx = mid % n`.
        - Get the middle element: `midElement = matrix[row_idx][col_idx]`.
        
        - If `target == midElement`, return `true`.
        - If `target < midElement`, adjust `high = mid - 1` to search the left half.
        - If `target > midElement`, adjust `low = mid + 1` to search the right half.

3. **Return `false` if the loop completes without finding the `target`.**

### Python Code
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m = len(matrix)
        n = len(matrix[0])
        low = 0
        high = m * n - 1
        
        while low <= high:
            mid = low + (high - low) // 2
            row_idx = mid // n
            col_idx = mid % n
            midElement = matrix[row_idx][col_idx]
            
            if target == midElement:
                return True
            elif target < midElement:
                high = mid - 1
            else:
                low = mid + 1
        
        return False
```

#### Explanation of the Code:
1. **Initialize Dimensions and Search Range:**
    - `m = len(matrix)`: Number of rows.
    - `n = len(matrix[0])`: Number of columns.
    - `low = 0`: Start index of the virtual array.
    - `high = m * n - 1`: End index of the virtual array.

2. **Binary Search Loop:**
    - Calculate `mid = low + (high - low) // 2`.
    - Convert `mid` to 2D indices: `row_idx = mid // n`, `col_idx = mid % n`.
    - Retrieve the middle element: `midElement = matrix[row_idx][col_idx]`.
    
    - If `target == midElement`, return `True`.
    - If `target < midElement`, adjust `high = mid - 1`.
    - If `target > midElement`, adjust `low = mid + 1`.

3. **Return `False` if `target` is not found.**



[Search of a 2D Matrix Leetcode](https://leetcode.com/problems/search-a-2d-matrix/?envType=study-plan-v2&envId=top-interview-150)
