# 旋转数组

## [题干](https://leetcode-cn.com/problems/rotate-array/)

给定一个数组，将数组中的元素向右移动 `k` 个位置，其中 `k` 是非负整数。

说明：

- 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
- 要求使用空间复杂度为 `O(1)` 的**原地**算法。

难度：简单

## 我的解法

思路：复制出一个临时数组，关系：`nums[(i+k)%len(nums)] = nums_cp[i]`.

时间复杂度：O(n), 空间复杂度：O(n)

python

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        length = len(nums)
        nums_cp = nums.copy()
        for i in range(length):
            nums[(i + k) % length] = nums_cp[i]
```

## 暴力法

时间复杂度：O(n * k), 空间复杂度：O(1).

java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int temp, previous;
        for (int i = 0; i < k; i++) {
            previous = nums[nums.length - 1]
            for (int j = 0; j < nums.length; j++) {
                temp = nums[j];
                nums[j] = previous;
                previous = temp;
            }
        }
    }
}
```

## 使用环状替换

时间复杂度：O(n), 空间复杂度：O(1).

java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        int count = 0;
        for (int start = 0; count < nums.length; start++) {
            int current = start;
            int prev = nums[start];
            db {
                int next = (current + k) % nums.length;
                int temp = nums[next];
                nums[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }
}
```

## 使用反转

算法：当旋转数组 `k` 次，`k%n` 个尾部元素会被移动到头部，剩下的元素会被往后移动。

这里首先将所有元素反转，然后反转前 `k` 个元素，再反转后面 `n-k` 个元素。

时间复杂度：O(n), 空间复杂度：O(1).

java

```java
class Solution {
    public void rotate(int[] nuns, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```
