# 第三大的数

## [题干](https://leetcode-cn.com/problems/third-maximum-number/)

给定一个非空数组，返回此数组中第三大的数，如果不存在，则返回数组中最大的数，要求算法时间复杂度必须是 `O(n)`.

解释：注意，要求返回第三大的数，是指第三大且唯一出现的数。存在两个值为 2 的数，它们都是排第二。

难度：简单

## 我的解法

时间复杂度：O(nlogn)，没有达到要求。

python

```python
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        tmp = sorted(list(set(nums)), reverse=True)
        if len(tmp) < 3:
            return tmp[0]
        return tmp[2]
```

## 优秀解法

巧用 set 和 remove 函数，时间复杂度：O(n).

python

```python
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        set_nums = set(nums)
        if len(set_nums) < 3:
            return max(set_nums)
        else:
            set_nums.remove(max(set_nums))
            set_nums.remove(max(set_nums))
            return max(set_nums)
```
