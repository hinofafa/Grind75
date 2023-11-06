# Letter Combinations of a Phone Number
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.<br><br>
A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![alt image](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

Example 1:
> Input: digits = "23"\
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

Example 2:
> Input: digits = ""\
Output: []

Example 3:
> Input: digits = "2"\
Output: ["a","b","c"]

Constraints:
- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

Problem can be found in [here](https://leetcode.com/problems/letter-combinations-of-a-phone-number)!

### [Solution](/Recursion/17-LetterCombinationsofaPhoneNumber/solution.py): Recursion

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        self.digit2letter = {"2": "abc", "3": "def", "4": "ghi", "5": "jkl",
                             "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"}
        output_list = []
        if digits:
            self.dfs(output_list, digits, 0, [])
        return output_list

    def dfs(self, output_list: List[str], digits: str, index: int, tempt: List[int]):
        if len(digits) == index:
            output_list.append("".join(tempt))
            return

        for letter in self.digit2letter[digits[index]]:
            tempt.append(letter)
            self.dfs(output_list, digits, index+1, tempt)
            tempt.pop()
```

Time Complexity: $O(4^n)$, Space Complexity: $O(n)$, where n is the length of array $digits$.
