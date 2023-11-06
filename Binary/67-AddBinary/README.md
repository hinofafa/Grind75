# Add Binary
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

Given two binary strings a and b, return their sum as a binary string.

Example 1:
> Input: a = "11", b = "1"\
Output: "100"

Example 2:
> Input: a = "1010", b = "1011"\
Output: "10101"
 

Constraints:
- $1$ <= a.length, b.length <= $10^4$
- a and b consist only of '0' or '1' characters.
- Each string does not contain leading zeros except for the zero itself.

Problem can be found in [here](https://leetcode.com/problems/add-binary)!

### [Solution](/Binary/67-AddBinary/solution.py): Binary

```python
def addBinary(a: str, b: str) -> str:
    result, carry = "", 0
    index_a, index_b = len(a)-1, len(b)-1
    while index_a >= 0 or index_b >= 0:
        tempt = carry
        if index_a >= 0:
            tempt += int(a[index_a])
        if index_b >= 0:
            tempt += int(b[index_b])

        index_a, index_b = index_a-1, index_b-1
        carry = 1 if tempt > 1 else 0
        result += str(tempt % 2)

    if carry != 0:
        result += str(carry)
    return result[::-1]
```

Time Complexity: $O(max(n,m))$, Space Complexity: $O(max(n,m))$, where n and m is the length of a and b, respectively.
