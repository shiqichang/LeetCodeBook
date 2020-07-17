# 存在重复元素

## [题干](https://leetcode-cn.com/problems/contains-duplicate/)

给定一个整数数组，判断是否存在重复元素。

如果任意一值在数组中出现至少两次，函数返回 `true`, 如果数组中每个元素都不相同，则返回 `false`.

难度：简单

## 我的解法

python

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        for num in nums:
        if nums.count(num) >= 2:
            return True
        return False
```

```python
import collections


class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        counts = collections.Counter(nums)
        if max(counts.values()) >= 2:
            return True
        return False
```

以上两种方法均超出时间限制。

## 优秀解法

python

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(nums) != len(set(nums))
```

## 排序

时间复杂度：O(nlogn), 空间复杂度：O(1).

java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; ++i) {
            if (nums[i] == nums[i + 1]) return true;
        }
        return false;
    }
}
```

## 哈希表

利用支持快速搜索和插入操作的动态数据结构。

时间复杂度：O(n), 空间复杂度：O(n).

java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>(nums.length);
        for (int x: nums) {
            if (set.contains(x)) return true;
            set.add(x);
        }
        return false;
    }
}
```
