# 找到所有数组中消失的数字

## [题干](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

给定一个范围在 `1 <= a[i] <= n` （n = 数组大小）的整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 `[1, n]` 范围之间没有出现在数组中的数字。

是否能不在使用额外空间且时间复杂度为 `O(n)` 的情况下完成？可以假设返回的数组不算在额外空间中。

难度：简单

## 我的解法

python

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        if not nums:
            return []
        return list(set(range(1, len(nums) + 1)) - set(nums))
```

## 使用哈希表

时间复杂度：O(n), 空间复杂度：O(n).

python

```python
class Solution(object):
    def findDisappearedNumbers(self, nums):
        hash_table = {}
        for num in nums:
            hash_table[num] = 1

        result = []
        for num in range(1, len(nums) + 1):
            if num not in hash_table:
                result.append(num)

        return result
```

## 原地修改

算法：

- 遍历输入数组的每个元素一次
- 把 `|nums[i]| - 1` 索引位置的元素标记为负数，即 `nums[|nums[i]| - 1] x -1`
- 再遍历数组，若当前数组元素 `nums[i]` 为负数，说明在数组中存在数字 `i+1`

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution(object):
    def findDisappearedNumbers(self, nums):
        for i in range(len(nums)):
            new_index = abs(nums[i]) - 1
            if nums[new_index] > 0:
                nums[new_index] *= -1

        result = []
        for i in range(1, len(nums) + 1):
            if nums[i - 1] > 0:
                result.append(i)

        return result
```
