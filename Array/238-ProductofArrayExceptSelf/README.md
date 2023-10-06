# Product of Array Except Self
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> Given an integer array **nums**, return an array **answer** such that **answer[i]** is equal to the product of all the elements of **nums** except **nums[i]**.<br><br>
The product of any prefix or suffix of **nums** is guaranteed to fit in a 32-bit integer. <br><br>
You must write an algorithm that runs in **$O(n)$** time and without using the division operation.

Example 1:
> Input: nums = [1,2,3,4]\
Output: [24,12,8,6]

Example 2:
> Input: nums = [-1,1,0,-3,3]\
Output: [0,0,9,0,0]
 
Constraints:
- $2$ <= nums.length <= $10^5$
- $-30$ <= nums[i] <= 30
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
 

Follow up: Can you solve the problem in $O(1)$ extra space complexity? (The output array does not count as extra space for space complexity analysis.)

Problem can be found in [here](https://leetcode.com/problems/product-of-array-except-self)!

## Solution
### [Basic Solution](/Array/238-ProductofArrayExceptSelf/solution1.py): Prefix Product & Suffix Product

```python
def productExceptSelf(nums: List[int]) -> List[int]:
    prefix_poduct, output_list = 1, []
    for number in nums:
        output_list.append(prefix_poduct)
        prefix_poduct *= number

    suffix_poduct = 1
    for i in range(len(nums) - 1, -1, -1):
        output_list[i] *= suffix_poduct
        suffix_poduct *= nums[i]

    return output_list
```

Explanation: Since we only iterate _nums_ twice and all of operations inside loops are performed in constant time, so the algorithm runs in $O(2n)$ = O(n) time. Suppose _nums_ = [a, b, c, d]. After first loop, we will get output_list = [1, a, ab, abc]. Noted that the value of the last element is exactly the product of array except self. With this in mind, we only need to iterate _nums_ backward to calculate the value of each element via suffix_poduct. In the second for-loop, when i = len(nums)-1 (the last element), output_list\[i] is exactly output_list and suffix_product = 1 \* d. When i=len(nums)-2, the value will be output_list\[i] \* suffix_product = ab \* d = abd. As as result, we get an array with its value is the product of array except self.

Time Complexity: $O(n)$, Space Complexity: $O(1)$

> Please noted that the output array does not count as an extra space for space complexity analysis!

### [Improved Solution](/Array/238-ProductofArrayExceptSelf/solution2.py)

```python
def productExceptSelf(nums: List[int]) -> List[int]:
    output_list = [1] * len(nums)
    prefix_poduct = suffix_poduct = 1
    for index, number in enumerate(nums):
        output_list[index] *= prefix_poduct
        prefix_poduct *= number
        output_list[-1 - index] *= suffix_poduct
        suffix_poduct *= nums[-1 - index]

    return output_list
```

Notes: Optimizing the algorithm for needing only for-loop.

Time Complexity: $O(n)$, Space Complexity: $O(1)$