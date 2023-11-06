# Subsets
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

> Given an integer array nums of unique elements, return all possible 
subsets (the power set). \
The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:
> Input: nums = [1,2,3]\
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

Example 2:
> Input: nums = [0]\
Output: [[],[0]]
 

Constraints:
- 1 <= nums.length <= 10
- -10 <= nums[i] <= 10
- All the numbers of nums are unique.

Problem can be found in [here](https://leetcode.com/problems/subsets)!

### [Solution](/Recursion/78-Subsets/solution.py): Recursion

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        output_list = []
        self.dfs(output_list, nums, [], 0)
        return output_list

    def dfs(self, output_list: List[List[int]], nums: List[int], current: List[int], index: int):
        output_list.append(list(current))
        for i in range(index, len(nums)):
            current.append(nums[i])
            self.dfs(output_list, nums, current, i+1)
            current.pop()
```

Time Complexity: $O(n*2^n)$, Space Complexity: $O(n)$, where n is the length of array $nums$.
