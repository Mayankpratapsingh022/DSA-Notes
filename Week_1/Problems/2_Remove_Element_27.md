## Remove Element

### Problem Explanation

Given an integer array `nums` and an integer `val`, you need to remove all occurrences of `val` in `nums` in-place. The order of the elements can be changed. After removal, return the number of elements in `nums` which are not equal to `val`.

### Example

**Example 1:**

- **Input:** `nums = [3, 2, 2, 3]`, `val = 3`
- **Output:** `2`, `nums = [2, 2, _, _]`
- **Explanation:** The function returns `k = 2`, with the first two elements of `nums` being 2. It does not matter what you leave beyond the returned `k`.

**Example 2:**

- **Input:** `nums = [0, 1, 2, 2, 3, 0, 4, 2]`, `val = 2`
- **Output:** `5`, `nums = [0, 1, 4, 0, 3, _, _, _]`
- **Explanation:** The function returns `k = 5`, with the first five elements of `nums` containing 0, 1, 4, 0, and 3. Note that the five elements can be returned in any order.

### Constraints

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

### Approach

To solve this problem, we use a two-pointer approach:

1. One pointer (`current`) traverses the entire array.
2. Another pointer (`insert_index`) keeps track of where to insert the next non-`val` element.

### Pseudocode

1. Initialize `insert_index` to `0`.
2. Loop through each element in `nums` with a pointer `current`.
3. If `nums[current]` is not equal to `val`:
    - Set `nums[insert_index]` to `nums[current]`.
    - Increment `insert_index`.
4. After the loop, `insert_index` will be the number of elements not equal to `val`.
5. Return `insert_index`.

### Detailed Steps with Visual Representation

1. **Initialize:**
    - `nums = [3, 2, 2, 3]`
    - `val = 3`
    - `insert_index = 0`
2. **Iteration 1:**
    - `current = 0`
    - `nums[current] = 3` (equals `val`)
    - Do nothing.
3. **Iteration 2:**
    - `current = 1`
    - `nums[current] = 2` (not equal to `val`)
    - `nums[insert_index] = nums[current]` → `nums[0] = 2`
    - Increment `insert_index` → `insert_index = 1`
    
    **Array State:** `[2, 2, 2, 3]`
    
4. **Iteration 3:**
    - `current = 2`
    - `nums[current] = 2` (not equal to `val`)
    - `nums[insert_index] = nums[current]` → `nums[1] = 2`
    - Increment `insert_index` → `insert_index = 2`
    
    **Array State:** `[2, 2, 2, 3]`
    
5. **Iteration 4:**
    - `current = 3`
    - `nums[current] = 3` (equals `val`)
    - Do nothing.
6. **Result:**
    - `insert_index = 2`
    - `nums` modified to `[2, 2, _, _]`

**Time Complexity:** \( O(n) \) - We traverse the array once.
**Space Complexity:** \( O(1) \) - We do not use extra space.

### Python Code Implementation

```python
def removeElement(nums, val):
    insert_index = 0
    for current in range(len(nums)):
        if nums[current] != val:
            nums[insert_index] = nums[current]
            insert_index += 1
    return insert_index

```

### Visual Diagram

```
Initial Array:   [3, 2, 2, 3]
Value to remove: 3

Step 1:
  Current = 0, Insert Index = 0
  3 == 3, so do nothing.

Step 2:
  Current = 1, Insert Index = 0
  2 != 3, nums[0] = 2, Increment Insert Index.
  Array: [2, 2, 2, 3]

Step 3:
  Current = 2, Insert Index = 1
  2 != 3, nums[1] = 2, Increment Insert Index.
  Array: [2, 2, 2, 3]

Step 4:
  Current = 3, Insert Index = 2
  3 == 3, so do nothing.

Final:
  Insert Index = 2
  Resultant Array: [2, 2, _, _]

```

### Tips for Approaching Similar Questions

1. **Understand the problem constraints:** Determine if you can use extra space or if you need an in-place solution.
2. **Think about edge cases:** Consider cases like an empty array or all elements being the value to remove.
3. **Use two-pointer technique:** This is often useful for in-place modifications when you need to retain order or modify the array in specific ways.
4. **Test thoroughly:** Ensure to test your solution with different inputs to cover all possible edge cases.

By following these steps and understanding the problem deeply, you can approach similar array manipulation problems effectively.
[Remove Element Leetcode](https://leetcode.com/problems/remove-element/)
