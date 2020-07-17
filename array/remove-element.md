# 移除元素

## [题干](https://leetcode-cn.com/problems/remove-element/)

给定一个数组 nums 和一个值 val, 你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不用使用额外的数组空间，必须在原地修改输入数组，使用 `O(1)` 额外空间完成。元素的顺序可以改变。

难度：简单

## 方法一：逆序循环法

这种解法是我在评论里看到的，觉得很棒！相比较正序解法会导致`索引越界`的问题，逆序的过程中，无论相不相等，最终都会向前移一位，保证每个元素都能被比较到。

python

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        for i in range(len(nums)-1, -1, -1):
            if nums[i] == val:
                nums.pop(i)
        return len(nums)
```

下面进入官方解法👇

## 方法二：双指针法

思路是用两个指针，一个慢指针 i, 一个快指针 j. 当 nums[j] 与给定值相等时，递增 j, 反之，复制 nums[j] 到 nums[i], 并同时递增两个索引。

解法与 [删除排序数组中的重复项](./remove-duplicates-from-sorted-array.md) 相似。

python

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for j in range(len(nums)):
            if nums[j] != val:
                nums[i] = nums[j]
                i += 1
        return i
```

java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for (int j = 0; j < nums.length; j++) {
            if (nums[j] != val) {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
}
```

注意⚠️：算法题的每一步都是很严谨的，随意调换顺序，结果完全不一样。

## 方法三：双指针法 -- 当要删除的元素很少时

算法：当 nums[i] = val 时，将当前元素与最后一个元素交换，并释放最后一个元素，使数组大小减 1.

java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        int n = nums.length;
        while (i < n) {
            if (nums[i] == val) {
                nums[i] = nums[n - 1];
                n--;
            } else {
                i++;
            }
        }
        return n;
    }
}
```
