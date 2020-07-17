# 缺失数字

## [题干](https://leetcode-cn.com/problems/missing-number/)

给定一个包含 `0, 1, 2, ..., n` 中 `n` 个数的序列，找到 `0..n` 中没有出现在序列中的那个数。

说明：算法应具有线性时间复杂度，能否仅使用额外常量空间来实现？

难度：简单

## 我的解法

时间复杂度：O(nlogn).

python

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        return sorted(list(set(range(len(nums) + 1)) - set(nums)))[0]
```

## 排序

复杂度分析：

- 时间复杂度：O(nlogn)，排序的时间复杂度为 O(nlogn)
- 空间复杂度：O(1) 或 O(n)，取决于排序算法是否进行原地排序

python

```python
class Solution:
    def missingNumber(self, nums):
        nums.sort()

        if nums[-1] != len(nums):
            return len(nums)
        elif nums[0] != 0:
            return 0

        for i in range(1, len(nums)):
            expected_num = nums[i - 1] + 1
            if nums[i] != expected_num:
                return expected_num
```

## 哈希表

分析：直接查询每个数是否在数组中出现过来找出缺失的数字，每次查询操作都是常数时间。

时间复杂度：O(n), 空间复杂度：O(n).

python

```python
class Solution:
    def missingNumber(self, nums):
        num_set = set(nums)
        n = len(nums) + 1
        for number in range(n):
            if number not in num_set:
                return number
```

### 位运算

分析：异或运算满足结合律，并且对一个数进行两次完全相同的异或运算会得到原来的数，则可以通过异或运算找到缺失的数字。

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution:
    def missingNumber(self, nums):
        missing = len(nuns)
        for i, num in enumerate(nums):
            missing ^== i ^ num
        return missing
```

## 数学

分析：利用**高斯求和公式**的和，减去数组中所有数的和，得到的就是缺失的数字。

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution:
    def missingNumber(self, nums):
        expected_sum = len(nums) * (len(nums) + 1) // 2
        actual_sum = sum(nums)
        return expected_sum - actual_sum
```
