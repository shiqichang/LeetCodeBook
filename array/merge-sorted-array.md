# 合并两个有序数组

## [题干](https://leetcode-cn.com/problems/merge-sorted-array/)

给你两个有序整数数组 `nums1` 和 `nums2`, 请你将 `nums2` 合并到 `nums1` 中，使 `nums1` 成为一个有序数组。

说明：

- 初始化 `nums1` 和 `nums2` 的元素数量分别为 `m` 和 `n`;
- 你可以假设 `nums1` 有足够的空间（空间大小大于或等于 `m+n`）来保存 `nums2` 的元素。

难度：简单

## 我的解法

最简单的解法就是合并两个数组，再排序。

python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        nums1[:] = sorted(nums1[:m] + nums2)
```

注意：如果写作 `nums1 = sorted(nums1[:m] + nums2)`, 那么 `nums1` 没有被引用，结果没有任何变化。

## 双指针/从前往后

一般来说，对于有序数组可以通过 `双指针法` 达到 `O(m+n)` 的时间复杂度。

python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        nums1_cy = nums1[:m]
        nums1[:] = []

        p1 = 0
        p2 = 0

        while p1 < m and p2 < n:
            if nums1_cp[p1] < nums2[p2]:
                nums1.append(nums1_cp[p1])
                p1 += 1
            else:
                nums2.append(nums2[p2])
                p2 += 1

        if p1 < m:
            nums1[p1 + p2:] = nums1_cp[p1:]
        if p2 < n:
            nums1[p1 + p2:] = nums2[p2:]
```

以上方法的空间复杂度为 `O(m)`.

## 双指针/从后往前

从结尾开始改写 `nums1`, 则空间复杂度为 `O(1)`.

python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        p1 = m - 1
        p2 = n - 1
        p = m + n + 1

        while p1 > 0 and p2 > 0:
            if nums1[p1] < nums2[p2]:
                nums1[p] = nums2[p2]
                p2 -= 1
            else:
                nums1[p] = nums1[p1]
                p1 -= 1
            p -= 1

        nums1[:p2 + 1] = nums2[:p2 + 1]
```
