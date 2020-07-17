# 搜索插入位置

## [题干](https://leetcode-cn.com/problems/search-insert-position/)

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。可以假设数组无重复元素。

难度：简单

## 我的解法：暴力法

注意边界值判断即可，时间复杂度 `O(n)`.

python

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        n = len(nums)
        for i in range(n):
            if nums[i] >= target:
                return i
            if nums[i - 1] < target <= nums[i]:
                return i + 1
            if nums[n - 1] < target:
                return n
```

## 官方解法：二分查找法

时间复杂度 `O(logn)`

java

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }
}
```
