
# Matrix Diagonal Sum

## Problem Explanation

You are given a square matrix (a 2D array) where the number of rows is equal to the number of columns. The task is to find the sum of the elements on both the primary diagonal and the secondary diagonal. However, if an element belongs to both diagonals (which only happens in the middle of the matrix when the matrix size is odd), it should be counted only once.

### Steps to Approach the Problem

1. **Primary Diagonal**: This consists of elements where the row index is equal to the column index, i.e., `mat[i][i]`.
2. **Secondary Diagonal**: This consists of elements where the row index and column index sum up to `n-1`, i.e., `mat[i][n-1-i]`.
3. **Avoid Double Counting**: If the matrix size `n` is odd, the middle element belongs to both diagonals and should be subtracted once.

### Pseudocode

1. Initialize `res` to store the sum of the diagonals.
2. Calculate the size of the matrix `n`.
3. Loop through each row `i` from 0 to `n-1`.
    - Add the element of the primary diagonal `mat[i][i]` to `res`.
    - Add the element of the secondary diagonal `mat[i][n-1-i]` to `res`.
4. If `n` is odd, subtract the middle element `mat[n//2][n//2]` from `res` to avoid double counting.
5. Return `res`.

### Pseudocode with Line-by-Line Explanation

```
function diagonalSum(mat):
    initialize res to 0                  # Step 1: Initialize the result variable
    n = length of mat                    # Step 2: Get the size of the matrix

    for i from 0 to n-1:                 # Step 3: Loop through each row
        res = res + mat[i][i]            # Add primary diagonal element
        res = res + mat[i][n-1-i]        # Add secondary diagonal element

    if n % 2 == 1:                       # Step 4: Check if n is odd
        res = res - mat[n//2][n//2]      # Subtract the middle element if it was added twice

    return res                           # Step 5: Return the result

```

### Python Code

```python
from typing import List

class Solution:
    def diagonalSum(self, mat: List[List[int]]) -> int:
        res = 0
        n = len(mat)

        for i in range(n):
            res += mat[i][i]               # Add primary diagonal element
            res += mat[i][n-1-i]           # Add secondary diagonal element

        if n % 2 == 1:                     # Check if n is odd
            res -= mat[n//2][n//2]         # Subtract the middle element if it was added twice

        return res

```

### Line-by-Line Explanation of Python Code

1. **Import List**: `from typing import List` allows us to use `List` for type hints.
2. **Define Class and Method**: The `Solution` class contains the method `diagonalSum`.
3. **Initialize Result**: `res = 0` initializes the result variable to store the sum.
4. **Matrix Size**: `n = len(mat)` gets the size of the matrix.
5. **Loop through Rows**: `for i in range(n):` iterates through each row of the matrix.
    - **Primary Diagonal**: `res += mat[i][i]` adds the primary diagonal element to `res`.
    - **Secondary Diagonal**: `res += mat[i][n-1-i]` adds the secondary diagonal element to `res`.
6. **Check for Odd Size**: `if n % 2 == 1:` checks if the matrix size is odd.
    - **Subtract Middle Element**: `res -= mat[n//2][n//2]` subtracts the middle element to avoid double counting.
7. **Return Result**: `return res` returns the final sum.

This approach ensures that we correctly calculate the sum of both diagonals, taking care to avoid double-counting the center element when the matrix size is odd.
[Matrix Diagonal Sum](https://leetcode.com/problems/matrix-diagonal-sum/submissions/1339514750/)
