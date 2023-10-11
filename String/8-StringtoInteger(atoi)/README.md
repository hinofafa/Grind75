# String to Integer (atoi)
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer (similar to C/C++'s atoi function).

The algorithm for myAtoi(string s) is as follows:
1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is '-' or '+'. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
3. Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. "123" -> 123, "0032" -> 32). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range [-231, 231 - 1], then clamp the integer so that it remains in the range. Specifically, integers less than -231 should be clamped to -231, and integers greater than 231 - 1 should be clamped to 231 - 1.
6. Return the integer as the final result.

Note:
- Only the space character ' ' is considered a whitespace character.
- Do not ignore any characters other than the leading whitespace or the rest of the string after the digits.
 
Example 1:
> Input: s = "42"\
Output: 42\
Explanation: The underlined characters are what is read in, the caret is the current reader position.\
Step 1: "42" (no characters read because there is no leading whitespace)\
&emsp;&emsp;&emsp;&emsp;^         
Step 2: "42" (no characters read because there is neither a '-' nor '+')\
&emsp;&emsp;&emsp;&emsp;^\
Step 3: "<ins>42</ins>" ("42" is read in)\
&emsp;&emsp;&emsp;&emsp;&emsp;^\
The parsed integer is 42.\
Since 42 is in the range [$-2^{31}$, $2^{31} - 1$], the final result is 42.

Example 2:
> Input: s = "&emsp;-42"\
Output: -42\
Explanation:\
Step 1: "<ins>&emsp;</ins>-42" (leading whitespace is read and ignored)\
&emsp;&emsp;&emsp;&emsp;&ensp; ^\
Step 2: "&emsp;<ins>-</ins>42" ('-' is read, so the result should be negative)\
&emsp;&emsp;&emsp;&emsp;&emsp;&ensp;^\
Step 3: "&emsp;-<ins>42</ins>" ("42" is read in)\
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&ensp; ^\
The parsed integer is -42.\
Since -42 is in the range [$-2^{31}$, $2^{31} - 1$], the final result is -42.

Example 3:
> Input: s = "4193 with words"\
Output: 4193\
Explanation:\
Step 1: "4193 with words" (no characters read because there is no leading whitespace)\
&emsp;&emsp;&emsp;&emsp;^\
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')\
&emsp;&emsp;&emsp;&emsp;^\
Step 3: "<ins>4193</ins> with words" ("4193" is read in; reading stops because the next character is a non-digit)\
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; ^\
The parsed integer is 4193.\
Since 4193 is in the range [$-2^{31}$, $2^{31} - 1$], the final result is 4193.
 

Constraints:
- $0$ <= s.length <= $200$
- s consists of English letters (lower-case and upper-case), digits (0-9), ' ', '+', '-', and '.'.

Problem can be found in [here](https://leetcode.com/problems/string-to-integer-atoi)!

## Solution
### [Solution](</String/8-StringtoInteger(atoi)/solution.py>)

```python
def myAtoi(s: str) -> int:
    answer = index = sign = 0
    MAX_INT, MIN_INT = 2147483647, -2147483648

    s = s.strip()
    if len(s) == 0:
        return 0

    sign = -1 if s[0] == "-" else 1
    if s[0] in set("+-"):
        index += 1

    while index < len(s) and s[index].isdigit():
        # In ASCII, int(s[index]) = ord(s[index]) - ord("0")
        answer = answer * 10 + int(s[index])
        index += 1

    answer *= sign
    # Make sure the returned value is in [-2^31, 2^31)
    answer = min(MAX_INT, max(answer, MIN_INT))
    return answer
```

Time Complexity: $O(n)$, Space Complexity: $O(1)$
