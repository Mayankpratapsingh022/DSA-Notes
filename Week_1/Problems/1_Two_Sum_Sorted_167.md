# 1 Two Sum Sorted
### Below is the pseudocode for the `twoSum` problem in a sorted array. This problem can be solved using the two-pointer technique.

### Pseudocode:

1. **Initialize Pointers:**
    - Set `low` to 0 (the start of the array).
    - Set `high` to the index of the last element in the array (`len(numbers) - 1`).
2. **Loop until the pointers meet:**
    - While `low` is less than `high`:
        - Calculate the `summation` of the elements at the `low` and `high` pointers.
        - If `summation` is equal to the `target`:
            - Return the indices `[low + 1, high + 1]` (assuming 1-based indexing).
        - If `summation` is greater than the `target`:
            - Decrease the `high` pointer by 1 (move it left).
        - Else (if `summation` is less than the `target`):
            - Increase the `low` pointer by 1 (move it right).
3. **Return Not Found:**
    - If no such pair is found, return `[-1, -1]`.

### Detailed Pseudocode:

```
FUNCTION twoSum(numbers, target):
    SET low to 0
    SET high to length of numbers - 1

    WHILE low is less than high:
        SET summation to numbers[low] + numbers[high]

        IF summation is equal to target:
            RETURN [low + 1, high + 1]  // Return 1-based indices

        ELSE IF summation is greater than target:
            DECREMENT high by 1  // Move the high pointer left

        ELSE:
            INCREMENT low by 1  // Move the low pointer right

    RETURN [-1, -1]  // If no solution is found

```





This pseudocode outlines the step-by-step process of solving the two-sum problem for a sorted array using the two-pointer technique. It efficiently narrows down the search space by adjusting the pointers based on the comparison of the current sum with the target.



```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        low,high = 0 , len(numbers) -1
        while low<high:
            summation = numbers[low] + numbers[high]
            if sumamation ==target:
                return [low+1,high+1]
            elif summation> target:
                high -= 1
            else:
                low += 1
        return [-1,-1]


````


#### My Solution on LeetCode

[Two Sum II - Input Array Is Sorted - LeetCode](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/submissions/1326224716/)
