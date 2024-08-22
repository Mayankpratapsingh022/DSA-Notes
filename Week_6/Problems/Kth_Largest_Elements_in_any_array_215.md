# Kth Largest Element in an Array 215


### Problem Understanding

The task is to find the `kth` largest element in an unsorted array `nums`. The `kth` largest element is the element that would appear in the `kth` position if the array were sorted in descending order.

### Approach

The most straightforward way to solve this problem is by sorting the array in descending order and returning the element at index `k-1`. However, the problem asks if we can solve it without sorting the entire array. This requirement hints that we should use a more efficient approach, such as a **min-heap**.

### Min-Heap Approach

A min-heap is a binary tree structure where the smallest element is always at the root. By maintaining a min-heap of size `k`, we can efficiently keep track of the `k` largest elements seen so far. Once we've processed all elements, the root of the min-heap will be the `kth` largest element in the array.

### Steps to Implement

1. **Initialize a Min-Heap**: Create a min-heap of size `k` with the first `k` elements of the array.

2. **Process the Remaining Elements**:
   - For each element in the array from index `k` to the end:
     - Compare the element with the root of the heap (which is the smallest element in the heap).
     - If the element is larger than the root, replace the root with this element and re-heapify the heap.
     - This ensures that the heap always contains the `k` largest elements.

3. **Return the Root of the Heap**: After processing all elements, the root of the heap will be the `kth` largest element.

### Code Implementation

Here's how you can implement the solution:

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # Step 1: Create a min-heap with the first k elements from nums
        min_heap = nums[:k]
        heapq.heapify(min_heap)
        
        # Step 2: Process the remaining elements in the array
        for num in nums[k:]:
            if num > min_heap[0]:  # Compare with the smallest element in the heap
                heapq.heappop(min_heap)  # Remove the smallest element
                heapq.heappush(min_heap, num)  # Add the current element
        
        # Step 3: The root of the heap (min_heap[0]) is the kth largest element
        return min_heap[0]
```

### Explanation of the Code

1. **`import heapq`**:
   - We import the `heapq` module, which provides an efficient implementation of a min-heap in Python.

2. **`class Solution:`**:
   - We define a class `Solution` where the method `findKthLargest` will be implemented.

3. **`def findKthLargest(self, nums: List[int], k: int) -> int:`**:
   - This method takes an array `nums` and an integer `k` as input, and it returns the `kth` largest element in the array.

4. **`min_heap = nums[:k]`**:
   - We create a min-heap using the first `k` elements of `nums`.

5. **`heapq.heapify(min_heap)`**:
   - We use `heapq.heapify` to convert the list `min_heap` into a heap. This operation is `O(k)`.

6. **Processing Remaining Elements**:
   - We iterate over the elements in `nums` starting from the `kth` element.
   - For each element, we compare it to the root of the heap (`min_heap[0]`).
   - If the current element is larger than the root, it means it should be part of the `k` largest elements. We pop the smallest element from the heap and push the current element into the heap.

7. **Return the `kth` Largest Element**:
   - After processing all elements, the smallest element in the heap (`min_heap[0]`) is the `kth` largest element in the array.

### Time and Space Complexity

- **Time Complexity**: 
  - Building the heap with the first `k` elements takes `O(k)`.
  - Processing the remaining `n-k` elements involves `O((n-k) * log k)` operations, as each `push` and `pop` operation on the heap takes `O(log k)`.
  - The overall time complexity is `O(n log k)`.

- **Space Complexity**: 
  - The space complexity is `O(k)` since we're maintaining a heap of size `k`.

### Summary

This approach is more efficient than sorting the entire array, especially for large arrays with a small `k`, as it only requires keeping track of the `k` largest elements rather than fully sorting the array.

[Kth Largest Elements in an array 215](https://leetcode.com/problems/kth-largest-element-in-an-array/submissions/1364524125/)
