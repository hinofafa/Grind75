# Valid Palindrome
![#00ff00](https://placehold.co/1x1/00ff00/00ff00.png) `Easy`

> A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.<br><br>
Given a string s, return true if it is a palindrome, or false otherwise.


Example 1:
> Input: s = "A man, a plan, a canal: Panama"\
Output: true\
Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:
> Input: s = "race a car"\
Output: false\
Explanation: "raceacar" is not a palindrome.

Example 3:
> Input: s = " "\
Output: true\
Explanation: s is an empty string "" after removing non-alphanumeric characters.\
Since an empty string reads the same forward and backward, it is a palindrome.

Constraints:
- $1$ <= s.length <= $2 * 10^5$
- s consists only of printable ASCII characters.

Problem can be found in [here](https://leetcode.com/problems/valid-palindrome)!

## Solution
### [Solution1](/String/125-ValidPalindrome/solution1.py): Python String Functions

```python
def isPalindrome(s: str) -> bool:
    s = "".join(char for char in s if char.isalnum()).lower()
    return s == s[::-1]
```

Time Complexity: ![O(n)](<https://latex.codecogs.com/svg.image?\inline&space;O(n)>), Space Complexity: ![O(1)](<https://latex.codecogs.com/svg.image?\inline&space;O(1)>)

### [Solution2](/String/125-ValidPalindrome/solution2.py): Two Pointers

```python
def isPalindrome(s: str) -> bool:
    left, right = 0, len(s)-1

    while left < right:
        if not s[left].isalnum():
            left += 1
        elif not s[right].isalnum():
            right += 1
        else:
            if s[left].lower() != s[right].lower():
                return False
            else:
                left += 1
                right += 1

    return True
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$