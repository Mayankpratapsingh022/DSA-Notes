### 1985. Find the Kth Largest Integer in the Array

#### Problem Statement
You are given an array of strings `nums` and an integer `k`. Each string in `nums` represents an integer without leading zeros. You need to return the string that represents the `k`th largest integer in `nums`.

**Note**: Duplicate numbers should be counted distinctly. For example, if `nums` is `["1", "2", "2"]`, `"2"` is the first largest integer, `"2"` is the second-largest integer, and `"1"` is the third-largest integer.

#### Example 1:
**Input**: `nums = ["3", "6", "7", "10"], k = 4`  
**Output**: `"3"`  
**Explanation**:  
The numbers in `nums` sorted in non-decreasing order are `["3", "6", "7", "10"]`.  
The 4th largest integer in `nums` is `"3"`.

#### Example 2:
**Input**: `nums = ["2", "21", "12", "1"], k = 3`  
**Output**: `"2"`  
**Explanation**:  
The numbers in `nums` sorted in non-decreasing order are `["1", "2", "12", "21"]`.  
The 3rd largest integer in `nums` is `"2"`.

#### Example 3:
**Input**: `nums = ["0", "0"], k = 2`  
**Output**: `"0"`  
**Explanation**:  
The numbers in `nums` sorted in non-decreasing order are `["0", "0"]`.  
The 2nd largest integer in `nums` is `"0"`.

#### Constraints:
- `1 <= k <= nums.length <= 10^4`
- `1 <= nums[i].length <= 100`
- `nums[i]` consists of only digits.
- `nums[i]` will not have any leading zeros.

---

### Solution Approaches

#### 1. **Sorting**
This is the simplest approach:
- Convert each string in `nums` to an integer.
- Sort the list of integers in descending order.
- Return the `k`th element in the sorted list.

```python
class Solution:
    def kthLargestNumber(self, nums: List[str], k: int) -> str:
        nums_int = [int(num) for num in nums]  # Convert all elements to integers
        nums_int.sort(reverse=True)            # Sort the integers in descending order
        kth_largest_int = nums_int[k-1]        # Select the kth largest integer
        return str(kth_largest_int)            # Convert back to string and return
```

**Time Complexity**: \(O(n \log n)\) for sorting the list, where `n` is the number of elements in `nums`.  
**Space Complexity**: \(O(n)\) for the space used in converting strings to integers.

#### 2. **Using a Min-Heap**
This approach maintains a heap of size `k`:
- Convert each string in `nums` to an integer.
- Push elements into a min-heap (which maintains the smallest of the `k` largest elements at the root).
- The root of the heap will be the `k`th largest element.

```python
import heapq

class Solution:
    def kthLargestNumber(self, nums: List[str], k: int) -> str:
        nums = [int(num) for num in nums]  # Convert all elements to integers
        heapq.heapify(nums)                # Convert list into a heap
        kth_largest_num = None
        for _ in range(len(nums) - k + 1):
            kth_largest_num = heapq.heappop(nums)  # Pop the smallest element len(nums) - k + 1 times
        return str(kth_largest_num)        # Convert back to string and return
```

**Time Complexity**: \(O(n + k \log n)\), where \(O(n)\) for heapify and \(O(k \log n)\) for extracting the elements.  
**Space Complexity**: \(O(n)\) for the space used by the heap.

#### 3. **Using a Max-Heap**
In this approach, we convert the problem to finding the smallest `k`th element by using a max-heap:
- Convert each string in `nums` to an integer.
- Push the negative of these integers into a max-heap (Python’s `heapq` is a min-heap by default, so we push negative values).
- Pop `k` elements from the max-heap, and the last popped element is the `k`th largest element.

```python
import heapq

class Solution:
    def kthLargestNumber(self, nums: List[str], k: int) -> str:
        nums = [-int(num) for num in nums]   # Convert elements to negative integers for max-heap
        heapq.heapify(nums)                  # Convert list into a heap
        k_largest_num = None
        for _ in range(k):
            k_largest_num = -heapq.heappop(nums)  # Pop the smallest negative, convert back to positive
        return str(k_largest_num)            # Convert back to string and return
```

**Time Complexity**: \(O(n + k \log n)\), where \(O(n)\) for heapify and \(O(k \log n)\) for extracting the elements.  
**Space Complexity**: \(O(n)\) for the space used by the heap.

---

### Conclusion
- The **Sorting** method is straightforward and works well for moderate-sized arrays.
- The **Min-Heap** and **Max-Heap** methods are more efficient when dealing with large arrays where `k` is small relative to the number of elements.

Each method has its use cases, depending on the constraints and requirements of the problem. Choose the method that best fits the situation, especially considering time and space complexity.

[Find the Kth Largest Integer in the Array Leetcode](https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/submissions/1364770713/)
