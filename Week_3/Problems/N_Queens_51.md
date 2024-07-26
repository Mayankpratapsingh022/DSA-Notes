# N-Queens problem

Problem Explanation

Imagine you have a big square board like a checkerboard. You also have some special pieces called queens, which you want to place on this board. The queens are very special because they can move in any direction: up, down, left, right, and diagonally. Your goal is to place the queens on the board in such a way that no queen can "see" or attack another queen.

### Example

If you have a 4x4 board (4 rows and 4 columns), you need to place 4 queens. But remember, each queen should be placed in such a way that it doesn't share the same row, column, or diagonal with another queen. This is a bit tricky, so we need to find all possible ways to do this.

Let's see a picture to understand it better (you can imagine this as if it were like a picture book explanation):

![Chessboard image](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

### Solutions

For a 4x4 board, there are two ways to place the 4 queens so that they don't attack each other:

1. **First Way:**
    - Place a queen in the second box of the first row (row 1, column 2).
    - Place a queen in the fourth box of the second row (row 2, column 4).
    - Place a queen in the first box of the third row (row 3, column 1).
    - Place a queen in the third box of the fourth row (row 4, column 3).
2. **Second Way:**
    - Place a queen in the third box of the first row (row 1, column 3).
    - Place a queen in the first box of the second row (row 2, column 1).
    - Place a queen in the fourth box of the third row (row 3, column 4).
    - Place a queen in the second box of the fourth row (row 4, column 2).

### Summary

- **Objective:** Place `n` queens on an `n x n` board.
- **Rule:** No two queens should be in the same row, column, or diagonal.
- **Output:** All possible ways to place the queens without them attacking each other.

If you understood the example for 4 queens, you can apply the same idea to boards of different sizes, like a 5x5 board with 5 queens, a 6x6 board with 6 queens, and so on. Each size will have its own unique solutions!

### Explanation

1. **Initialization**:
    
    ```python
    board = []
    for i in range(n):
        row = '.' * n
        board.append(row)
    
    ```
    
    We start by creating an empty chess board of size `n x n`. Each cell on the board is represented by a dot ('.').
    
2. **Result Storage**:
    
    ```python
    result = []
    
    ```
    
    We initialize an empty list called `result` to store the possible solutions.
    
3. **Helper Function - isValid**:
    
    ```python
    def isValid(board, row, col):
        # Check if there's a queen in the same row or column
        for i in range(n):
            if (i != col and board[row][i] == "Q") or (i != row and board[i][col] == "Q"):
                return False
    
    ```
    
    This function checks if placing a queen at position (row, col) is valid. It first checks if there's already a queen in the same row or column.
    
4. **Diagonal Checks**:
    
    ```python
        # Check the diagonals for any other queens
        # southeast diagonal
        r, c = row - 1, col - 1
        while r >= 0 and c >= 0:
            if board[r][c] == "Q":
                return False
            r -= 1
            c -= 1
    
        # northeast diagonal
        r, c = row + 1, col + 1
        while r < n and c < n:
            if board[r][c] == "Q":
                return False
            r += 1
            c += 1
    
        # southwest diagonal
        r, c = row - 1, col + 1
        while r >= 0 and c < n:
            if board[r][c] == "Q":
                return False
            r -= 1
            c += 1
    
        # northwest diagonal
        r, c = row + 1, col - 1
        while r < n and c >= 0:
            if board[r][c] == "Q":
                return False
            r += 1
            c -= 1
    
        return True
    
    ```
    
    The function continues to check if there are any queens on the diagonals (southeast, northeast, southwest, northwest). If any queen is found on these diagonals, the function returns `False`. If all checks pass, it returns `True`.
    
5. **Main Recursive Function - solve**:
    
    ```python
    def solve(board, row):
        # If all queens are placed
        if row == n:
            result.append(board.copy())
            return
    
    ```
    
    The `solve` function tries to place queens row by row. If all queens are placed (`row == n`), it adds the current board configuration to the result list.
    
6. **Placing Queens**:
    
    ```python
        # Place queen at every column in the current row, and recur for the next row
        for col in range(n):
            if isValid(board, row, col):
                # Place queen
                board[row] = board[row][:col] + "Q" + board[row][col + 1 :]
                # Recur for the next row
                solve(board, row + 1)
                # Backtrack and remove the queen from current position
                board[row] = board[row][:col] + "." + board[row][col + 1 :]
    
    ```
    
    For each row, the function tries to place a queen in each column. If placing a queen is valid, it places the queen (`Q`), calls the `solve` function recursively for the next row, and then backtracks by removing the queen (`.`).
    
7. **Start the Algorithm**:
    
    ```python
    solve(board, 0)
    return result
    
    ```
    
    Finally, the `solve` function is called with the initial board and starting row 0. The function returns the list of all possible solutions.
    

### Pseudocode

Here's a simplified pseudocode for better understanding:

```
1. Create an empty n x n board filled with dots (.)
2. Initialize an empty list to store the results

3. Define a function isValid(board, row, col):
    a. Check if there's a queen in the same row or column
    b. Check all diagonals for any queens
    c. If all checks pass, return True

4. Define a function solve(board, row):
    a. If row equals n, add the current board configuration to the results
    b. For each column in the current row:
        i.   If placing a queen at (row, col) is valid:
        ii.  Place a queen at (row, col)
        iii. Recur to place queens in the next row
        iv.  Remove the queen (backtrack)

5. Call solve(board, 0) to start placing queens from the first row
6. Return the list of results

```

### Explanation

1. **Setup the Board**:
We start by making a chessboard with `n` rows and `n` columns. Each square on the board is empty (represented by a dot).
2. **Check Valid Placement**:
We need a way to check if placing a queen on the board is safe. We make sure no other queens are in the same row, column, or diagonal.
3. **Place Queens**:
We try to put queens on the board one row at a time. For each row, we try every column. If it’s safe to place a queen, we do it and move to the next row. If placing a queen there eventually leads to a solution, great! If not, we remove the queen and try the next column (this is called backtracking).
4. **Store Solutions**:
When all queens are placed safely, we save this board configuration as a solution.
5. **Start the Process**:
We begin by placing queens starting from the first row and continue the process until we've tried all possibilities. Finally, we return all the solutions we found.

#### Full Code

```python
from typing import List

class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        # Initialize an empty chess board
        board = []
        for i in range(n):
            row = '.' * n
            board.append(row)
        result = []

        def isValid(board, row, col):
            # Check if there's a queen in the same row or column
            for i in range(n):
                if (i != col and board[row][i] == "Q") or (i != row and board[i][col] == "Q"):
                    return False

            # Check the diagonals for any other queens
            # southeast diagonal
            r, c = row - 1, col - 1
            while r >= 0 and c >= 0:
                if board[r][c] == "Q":
                    return False
                r -= 1
                c -= 1

            # northeast diagonal
            r, c = row + 1, col + 1
            while r < n and c < n:
                if board[r][c] == "Q":
                    return False
                r += 1
                c += 1

            # southwest diagonal
            r, c = row - 1, col + 1
            while r >= 0 and c < n:
                if board[r][c] == "Q":
                    return False
                r -= 1
                c += 1

            # northwest diagonal
            r, c = row + 1, col - 1
            while r < n and c >= 0:
                if board[r][c] == "Q":
                    return False
                r += 1
                c -= 1

            return True

        def solve(board, row):
            # If all queens are placed
            if row == n:
                result.append(board.copy())
                return

            # Place queen at every column in the current row, and recur for the next row
            for col in range(n):
                if isValid(board, row, col):
                    # Place queen
                    board[row] = board[row][:col] + "Q" + board[row][col + 1 :]
                    # Recur for the next row
                    solve(board, row + 1)
                    # Backtrack and remove the queen from current position
                    board[row] = board[row][:col] + "." + board[row][col + 1 :]

        # Start the algorithm to solve the n-queens problem
        solve(board, 0)
        return result

# Example usage:
# solution = Solution()
# print(solution.solveNQueens(4))

```

[N Queens Leetcode](https://leetcode.com/problems/n-queens/submissions/1326224716/)
