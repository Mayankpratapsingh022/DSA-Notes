# Course Schedule 207
### Problem Statement
We need to determine if you can finish all courses given a number of courses (`numCourses`) and a list of prerequisite pairs. Each pair `[a, b]` means you need to take course `b` before course `a`. The task is to check if it's possible to finish all courses without running into a cycle (which would make it impossible to complete the courses).

### Step-by-Step Explanation of the Code

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # Create an adjacency list where each course points to the list of courses that depend on it.
        preMap = { i:[] for i in range(numCourses)}

        # Fill the adjacency list with the given prerequisites.
        for crs, pre in prerequisites:
            preMap[crs].append(pre)

        # visited set is used to track courses in the current DFS path.
        visitSet = set()

        # Define the DFS function to explore each course.
        def dfs(crs):
            # If the course is already in visitSet, we've encountered a cycle.
            if crs in visitSet:
                return False

            # If the course has no prerequisites, it can be finished.
            if preMap[crs] == []:
                return True

            # Mark the course as visited in the current path.
            visitSet.add(crs)

            # Recursively visit all the prerequisites for the current course.
            for pre in preMap[crs]:
                if not dfs(pre):
                    return False

            # After visiting all prerequisites, remove the course from visitSet.
            visitSet.remove(crs)

            # Mark the course as having no prerequisites, meaning it's been processed.
            preMap[crs] = []

            # If all prerequisites are successfully visited, return True.
            return True

        # Start DFS for each course. If any course can't be completed, return False.
        for crs in range(numCourses):
            if not dfs(crs):
                return False

        # If all courses can be completed, return True.
        return True
```

### Detailed Steps

1. **Initialization**:
   - `preMap` is an adjacency list that stores which courses depend on which. For example, if `prerequisites = [[1,0],[2,1]]`, then `preMap` will look like `{0: [], 1: [0], 2: [1]}`.

2. **Building the Prerequisite Map**:
   - The for-loop populates `preMap` with prerequisites for each course.

3. **DFS Function**:
   - The DFS function is designed to detect cycles:
     - If `crs` (the current course) is already in `visitSet`, a cycle is detected, and the function returns `False`.
     - If `crs` has no prerequisites (`preMap[crs] == []`), then it can be completed, so the function returns `True`.
     - The course is added to `visitSet`, and we recursively call DFS on all its prerequisites.
     - If DFS returns `False` for any prerequisite, the current course also returns `False`, indicating it's not possible to complete the courses.
     - If the course and its prerequisites are processed without detecting a cycle, it's removed from `visitSet` and marked as processed in `preMap` by setting `preMap[crs] = []`.

4. **Main Loop**:
   - The main loop runs DFS for each course. If DFS returns `False` for any course, the function immediately returns `False` (not all courses can be completed).
   - If all courses pass the DFS check, the function returns `True` (indicating all courses can be completed).

This approach uses Depth-First Search (DFS) to detect cycles in a directed graph, where courses are nodes and prerequisites are edges. If there's a cycle, it means you can't complete all courses due to a deadlock, and the function returns `False`. If no cycle is detected, it returns `True`.

[Course Schedule Leetcode](https://leetcode.com/problems/course-schedule/submissions/1372415998/)
