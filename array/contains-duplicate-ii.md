# 存在重复元素 II

## [题干](https://leetcode-cn.com/problems/contains-duplicate-ii/)

给定一个整数数组和一个整数 `k`, 判断数组中是否存在两个不同的索引 `i` 和 `j`, 使得 `nums[i] = nums[j]`, 并且 `i` 和 `j` 的差的**绝对值**至多为 `k`.

难度：简单

## 我的解法

思路：用一个临时的字典，键为数组元素，值为元素所对应的下标。如果碰到相同的值，但下标差超过 `k`, 则从字典中删除该元素，继续循环。

python

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        tmp_map = dict()
        for i in range(len(nums)):
            if nums[i] in tmp_map.keys():
                if i - tmp_map[nums[i]] <= k:
                    return True
                else:
                    tmp_map.pop(nums[i])
            tmp_map.update({nums[i]: i})
        return False
```

## 哈希

维护一个哈希表，里面始终最多包含 `k` 个元素，当出现重复值时则说明在 `k` 距离内存在重复元素。

时间复杂度：O(n).

java

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (set.contains(nums[i])) {
                return true;
            }
            set.add(nums[i]);
            if (set.size() > k) {
                set.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```
