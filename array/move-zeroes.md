# 移动零

## [题干](https://leetcode-cn.com/problems/move-zeroes/)

给定一个数组 `nums`, 编写一个函数将所有的 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

说明：

1. 必须在原数组上操作，不要拷贝额外的数组。
2. 尽量减少操作次数。

难度：简单

## 我的解法

python

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        counts = nums.count(0)
        [nums.remove(0) for _ in range(counts)]
        nums[:] = nums + [0] * counts
```

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        counts = nums.count(0)
        for _ in range(counts):
            nums.remove(0)
            nums.append(0)
```

## 两次遍历

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution:
    def moveZeroes(self, nums):
        if not nums:
            return 0
        j = 0
        for i in xrange(len(nums)):
            if nums[i]:
                nums[j] = nums[i]
                j += 1

        for i in xrange(j, len(nums)):
            nums[i] = 0
```

## 一次遍历

思路：参考快速排序的思想，首先确定一个待分割的元素做中间点 `x`, 然后把所有小于等于 `x` 的元素放到 `x` 的左边，大于 `x` 的元素放到其右边。

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution:
    def moveZeroes(self, nums):
        if not nums:
            return 0
        j = 0
        for i in xrange(len(nums)):
            if nums[i]:
                nums[j], nums[i] = nums[i], nums[j]
                j += 1
```
