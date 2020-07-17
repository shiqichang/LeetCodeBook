# 最大连续1的个数

## [题干](https://leetcode-cn.com/problems/max-consecutive-ones/)

给定一个二进制数组，计算其中最大连续1的个数。

注意：

- 输入的数组只包含 `0` 和 `1`.
- 输入数组的长度是正整数，且不超过 10000.

难度：简单

## 我的解法

python

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        result, tmp = 0, 0
        for num in nums:
            if num == 1:
                tmp += 1
            else:
                result = max(result, tmp)
                tmp = 0
        result = max(result, tmp)
        return result
```

时间复杂度：O(n), 空间复杂度：O(1).

## 其他解法

在 `python` 中使用 `map`, `join`, `split` 函数解决。

python

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums):
        return max(map(len, ''.join(map(str, nums)).split('0')))
```
