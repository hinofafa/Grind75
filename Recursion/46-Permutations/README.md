# Permutations
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium`

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:
> Input: nums = [1,2,3]\
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
> Input: nums = [0,1]\
Output: [[0,1],[1,0]]

Example 3:
> Input: nums = [1]\
Output: [[1]]
 
Constraints:
- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are unique.

Problem can be found in [here](https://leetcode.com/problems/permutations)!

### [Solution](/Recursion/46-Permutations/solution.py): Recursion

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        output_list = []
        visited_numbers = set()
        self.dfs(nums, output_list, visited_numbers, [])
        return output_list

    def dfs(self, nums: List[int], output_list: List[List[int]], visited_numbers: Set[int], tempt: List[int]) -> None:
        if len(tempt) == len(nums):
            output_list.append(tempt[:])
            return

        for number in nums:
            if number not in visited_numbers:
                visited_numbers.add(number)
                tempt.append(number)
                self.dfs(nums, output_list, visited_numbers, tempt)
                tempt.pop()
                visited_numbers.remove(number)
```

Time Complexity: $O(n*n!)$, Space Complexity: $O(n)$, where n is the length of array $nums$.
