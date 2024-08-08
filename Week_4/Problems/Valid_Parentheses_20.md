# 20 Valide Parentheses
### Problem Explanation

You need to determine if a string of parentheses is valid. A string is considered valid if:

1. Every open bracket must have a corresponding close bracket of the same type.
2. Open brackets must be closed in the correct order.

### Examples

1. `s = "()"` should return `true` because the parentheses are correctly matched.
2. `s = "()[]{}"` should return `true` because all the different types of brackets are correctly matched.
3. `s = "(]"` should return `false` because the parentheses are not correctly matched.

### Approach

To solve this problem, you can use a stack to keep track of open brackets. The stack helps ensure that brackets are closed in the correct order.

### Detailed Steps

1. **Create a mapping** of open to close brackets using a dictionary.
2. **Initialize a stack** to keep track of open brackets.
3. **Iterate through each character** in the string:
    - If the character is an open bracket (`(`, `{`, or `[`), push it onto the stack.
    - If the character is a close bracket (`)`, `}`, or `]`):
        - Check if the stack is not empty and the top of the stack is the corresponding open bracket.
        - If true, pop the top of the stack.
        - If false, return `false` because the string is not valid.
4. **After the iteration**, if the stack is empty, return `true` because all open brackets were properly closed. Otherwise, return `false`.

### Pseudocode

```
function isValid(s):
    bracket_mapping = { "(": ")", "{": "}", "[": "]" }
    open_bracket = set(["(", "{", "["])
    stack = []

    for char in s:
        if char in open_bracket:
            stack.push(char)
        else if stack is not empty and char == bracket_mapping[stack.peek()]:
            stack.pop()
        else:
            return false

    return stack is empty

```

### Python Code Explanation

Let's go through the Python code provided:

```python
class Solution:
    def isValid(self, s: str) -> bool:
        # Dictionary to map open brackets to their corresponding close brackets
        bracket_mapping = {"(": ")", "{": "}", "[": "]"}
        # Set of open brackets
        open_bracket = set(["(", "[", "{"])
        # Stack to keep track of open brackets
        stack = []

        # Iterate through each character in the string
        for char in s:
            # If the character is an open bracket, push it onto the stack
            if char in open_bracket:
                stack.append(char)
            # If the character is a close bracket
            elif stack and char == bracket_mapping[stack[-1]]:
                # Pop the top element from the stack if it matches the corresponding open bracket
                stack.pop()
            else:
                # If it does not match or stack is empty, return False
                return False

        # If stack is empty, all brackets were matched correctly
        return stack == []

```

### Code Explanation Line by Line

1. **Dictionary Mapping:** `bracket_mapping = {"(": ")", "{": "}", "[": "]"}`
    - This dictionary maps each open bracket to its corresponding close bracket.
2. **Set of Open Brackets:** `open_bracket = set(["(", "[", "{"])`
    - This set contains all the open brackets for quick lookup.
3. **Initialize Stack:** `stack = []`
    - This stack will keep track of open brackets as we encounter them.
4. **Iterate through Characters:** `for char in s:`
    - Loop through each character in the input string.
5. **Check if Open Bracket:** `if char in open_bracket:`
    - If the character is an open bracket, push it onto the stack.
6. **Check if Close Bracket Matches:** `elif stack and char == bracket_mapping[stack[-1]]:`
    - If the character is a close bracket, check if it matches the top of the stack.
    - `stack[-1]` gives the top element of the stack.
    - `char == bracket_mapping[stack[-1]]` checks if the close bracket matches the open bracket.
7. **Pop from Stack:** `stack.pop()`
    - If it matches, pop the top element from the stack.
8. **Return False if No Match:** `else: return False`
    - If the close bracket does not match or the stack is empty, return `false`.
9. **Check if Stack is Empty:** `return stack == []`
    - After processing all characters, return `true` if the stack is empty, indicating all brackets were properly closed.

### Example Walkthrough

For `s = "[{()}]"`:

1. **Initial State:** `stack = []`
2. **First Character `[`:** Open bracket, `stack = ["["]`
3. **Second Character `{`:** Open bracket, `stack = ["[", "{"]`
4. **Third Character `(`:** Open bracket, `stack = ["[", "{", "("]`
5. **Fourth Character `)`:** Matches `(`, pop from stack, `stack = ["[", "{"]`
6. **Fifth Character `}`:** Matches `{`, pop from stack, `stack = ["["]`
7. **Sixth Character `]`:** Matches `[`, pop from stack, `stack = []`
8. **End:** Stack is empty, return `true`

This approach ensures that all brackets are properly matched and closed in the correct order.

[Valid Parenthese LeetCode My-Sol](https://leetcode.com/problems/valid-parentheses/submissions/1348794117/)
