# Combination Sum
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> Given an array of distinct integers **candidates** and a target integer **target**, return a list of all unique combinations of **candidates** where the chosen numbers sum to **target**. You may return the combinations in any order. <br><br>
The same number may be chosen from **candidates** an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different. <br><br>
The test cases are generated such that the number of unique combinations that sum up to **target** is less than **150** combinations for the given input.

Example 1:
> Input: candidates = [2,3,6,7], target = 7\
Output: [[2,2,3],[7]]\
Explanation:\
2 and 3 are candidates, and 2 + 2 + 3 = 7. \
Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

Example 2:
> Input: candidates = [2,3,5], target = 8\
Output: [[2,2,2,2],[2,3,3],[3,5]]

Example 3:
> Input: candidates = [2], target = 1\
Output: []
 

Constraints:
- $1$ <= candidates.length <= $30$
- $2$ <= candidates[i] <= $40$
- All elements of candidates are distinct.
- $1$ <= target <= $40$

Problem can be found in [here](https://leetcode.com/problems/combination-sum)!

## Solution
### [Solution](/Array/39-CombinationSum/solution.py): Backtracking

```python
def combinationSum(candidates: List[int], target: int) -> List[List[int]]:
    def find_all_combination(index: int, target: int, path: List[int]):
        if target < 0:
            return
        elif target == 0:
            output_list.append(path)
        else:
            for i in range(index, cand_length):
                find_all_combination(i, target-cand[i], path+[cand[i]])
        return

    output_list = []
    cand = candidates
    cand_length = len(candidates)
    find_all_combination(0, target, [])

    return output_list
```

Explanation: The algorithm is simple; just use backtracking techniques. Noted that we use variable index to avoid duplicated combination. So, whenever index becomes larger, we cannot choose number before the index element in candidates array.

Time Complexity: $O(2^k)$, where k is the number of tree nodes of the recursion tree. In this given problem, k is the sum of target/candidates[i] from i=0 to len(candidates)-1.

Space Complexity: $O(n)$, where n is the length of longest combination. In worst case scenario, N = target when 1 is in the candidates array.
