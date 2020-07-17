# 两数之和 II - 输入有序数组

## [题干](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

给定一个已按照**升序排列**的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2, 其中 index1 必须小于 index2.

说明：

- 返回的下标值不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且不可以重复使用相同的元素。

难度：简单

## 我的解法

思路：设置 `low = 0, high = len(numbers) - 1`, 对比两个下标对应的元素之和与目标值，小了 low 加一，大了 high 减一。

时间复杂度：O(n)
空间复杂度：O(1)

python

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        low, high = 0, len(numbers) - 1
        while low <= high:
            if numbers[low] + numbers[high] < target:
                low += 1
            elif numbers[low] + numbers[high] > target:
                high -= 1
            else:
                return low + 1, high + 1
```

哈哈，看了官方解法，发现我的解法就是官方解法——双指针法。
