# 169 Majority Element 

### Boyer-Moore Voting Algorithm

### Explanation

The Boyer-Moore Voting Algorithm is used to find the majority element in a list of numbers. The majority element is the element that appears more than half the time in the list. The algorithm works in two phases:

1. **Finding a Candidate:**
    - Maintain a candidate and a count.
    - Iterate through the list of numbers.
    - If the count is zero, set the current number as the candidate.
    - If the current number is the same as the candidate, increase the count.
    - If the current number is different from the candidate, decrease the count.
2. **Verifying the Candidate:**
    - After finding the candidate, verify that it actually is the majority element by counting its occurrences.

### Problem Statement

Given an array `nums` of size `n`, return the majority element. The majority element is the element that appears more than `⌊n / 2⌋` times. We assume that the majority element always exists in the array.

### Examples

1. **Input:** `nums = [3,2,3]`**Output:** `3`
2. **Input:** `nums = [2,2,1,1,1,2,2]`**Output:** `2`

### Approach

To solve this problem using the Boyer-Moore Voting Algorithm, we will:

1. Initialize `count` to 0 and `candidate` to `None`.
2. Iterate through the array and use the Boyer-Moore Voting Algorithm to find the candidate.
3. Return the candidate.

### Pseudocode

```
function majorityElement(nums):
    count = 0
    candidate = None

    for each num in nums:
        if count == 0:
            candidate = num
        if num == candidate:
            count += 1
        else:
            count -= 1

    return candidate

```

### Python Code

Let's go through the provided Python code and explain it line by line.

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = 0
        candidate = None

        for num in nums:
            if count == 0:
                candidate = num
            if num == candidate:
                count += 1
            else:
                count -= 1

        return candidate

```

### Explanation of the Python Code

1. **Class Definition:**
    
    ```python
    class Solution:
    
    ```
    
    - We define a class `Solution` which will contain our method to find the majority element.
2. **Method Definition:**
    
    ```python
    def majorityElement(self, nums: List[int]) -> int:
    
    ```
    
    - Define a method `majorityElement` that takes a list of integers `nums` and returns an integer.
3. **Initialize Variables:**
    
    ```python
    count = 0
    candidate = None
    
    ```
    
    - Initialize `count` to 0. This will keep track of the current count of the candidate.
    - Initialize `candidate` to `None`. This will store the current candidate for the majority element.
4. **Iterate Through the List:**
    
    ```python
    for num in nums:
    
    ```
    
    - Loop through each number `num` in the list `nums`.
5. **Check Count:**
    
    ```python
    if count == 0:
        candidate = num
    
    ```
    
    - If `count` is 0, set `candidate` to the current number `num`.
6. **Update Count:**
    
    ```python
    if num == candidate:
        count += 1
    else:
        count -= 1
    
    ```
    
    - If the current number `num` is the same as the `candidate`, increment `count` by 1.
    - If the current number `num` is different from the `candidate`, decrement `count` by 1.
7. **Return Candidate:**
    
    ```python
    return candidate
    
    ```
    
    - After the loop, return the `candidate` which is the majority element.

### Summary

The Boyer-Moore Voting Algorithm efficiently finds the majority element by maintaining a candidate and a count. It scans through the array once, making it an O(n) time complexity solution with O(1) space complexity. This is ideal for large arrays and ensures that we meet the problem's constraints and requirements.
[Majority Element LeetCode My-Sol](https://leetcode.com/problems/majority-element/submissions/1348796038/)
