# Valid Parentheses
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. 

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.
 
Example 1:
> Input: s = "()"\
Output: true

Example 2:
> Input: s = "()[]{}"\
Output: true

Example 3:
> Input: s = "(]"\
Output: false
 

Constraints:
- $1$ <= s.length <= $10^4$
- s consists of parentheses only '()[]{}'.

Problem can be found in [here](https://leetcode.com/problems/valid-parentheses)!

## Solution
### [Solution](/Stack/20-ValidParentheses/solution.py)

```python
def isValid(s: str) -> bool:
    stack = []
    bracket = {"(": ")", "[": "]", "{": "}"}
    for char in s:
        # Case 1: Left Bracket, just simply push into stack
        if char in set("([{"):
            stack.append(char)
        # Case 2: Right Bracket, may cause invalid parentheses
        else:
            if not stack or bracket[stack[-1]] != char:
                return False
            else:
                stack.pop()

    return not stack
```

Time Complexity: $O(n)$, Space Complexity: $O(n)$
 