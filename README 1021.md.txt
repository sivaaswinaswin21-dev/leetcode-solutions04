# Remove Outermost Parentheses

Solution to [LeetCode 1021: Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/).

## Problem

A valid parentheses string is *primitive* if it is nonempty and cannot be split into two nonempty valid parentheses strings. Given a valid parentheses string `s`, split it into primitive strings and return `s` with the outermost parentheses of every primitive string removed.

**Examples**

| Input | Output | Explanation |
|-------|--------|-------------|
| `"(()())(())"` | `"()()()"` | `"(()())" + "(())"` becomes `"()()" + "()"` |
| `"(()())(())(()(()))"` | `"()()()()(())"` | `"()()" + "()" + "()(())"` |
| `"()()"` | `""` | `"()" + "()"` becomes `"" + ""` |

**Constraints**

- `1 <= s.length <= 10^5`
- `s[i]` is `'('` or `')'`
- `s` is a valid parentheses string

## Approach

Scan the string once while tracking the nesting depth.

- On `(`: if the depth is already greater than 0, keep the character. Then increase the depth.
- On `)`: decrease the depth first. If the depth is still greater than 0, keep the character.

A primitive string begins when the depth goes from 0 to 1 and ends when it returns to 0. Those two characters are the outermost parentheses, and they are the only ones skipped.

## Solution

```python
class Solution:
    def removeOuterParentheses(self, s: str) -> str:
        res = []
        depth = 0
        for ch in s:
            if ch == '(':
                if depth > 0:
                    res.append(ch)
                depth += 1
            else:
                depth -= 1
                if depth > 0:
                    res.append(ch)
        return "".join(res)
```

## Usage

```python
from remove_outermost_parentheses import Solution

print(Solution().removeOuterParentheses("(()())(())"))  # ()()()
print(Solution().removeOuterParentheses("()()"))        # (empty string)
```

## Complexity

| | Complexity | Notes |
|---|-----------|-------|
| Time | O(n) | Single pass over the string |
| Space | O(n) | Output list; O(1) extra beyond that |