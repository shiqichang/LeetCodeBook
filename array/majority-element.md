# 多数元素

## [题干](https://leetcode-cn.com/problems/majority-element/)

给定一个大小为 `n` 的数组，找到其中的多数元素，多数元素是指在数组中出现次数大于 `n/2` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

难度：简单

## 我的解法

思路：将该数组转换成一个临时集合，判断集合中每个元素在愿数组中出现的次数是否大于 `n/2`.

时间复杂度：O(n)

python

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        tmp = set(nums)
        for num in tmp:
            if nums.count(num) > len(nums) / 2:
                return num
```

## 哈希表

算法：使用哈希映射(HashMap)来存储每个元素以及出现的次数。

用一个循环遍历数组 `nums` 并将数组中的每个元素加入哈希映射表，再遍历哈希映射表中所有键值对，返回值最大的键。

同样也可以在遍历数组时使用打擂台的方法，维护最大的值。

java

```java
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            }
            else {
                counts.put(num, counts.get(num)+1);
            }
        }
        return counts;
    }

    public int majorityElements(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);

        Map.Entry<Integer, Integer> majorityEntry = null;
        for (Map.Entry<Integer, Integer> entry : counts.entrySet()) {
            if (majorityEntry == null || entry.getValue() > majorityEntry.getValue()) {
                majorityEntry = entry;
            }
        }

        return majorityEntry.getKey();
    }
}
```

python

```python
import collections


class Solution:
    def majorityElements(self, nums):
        counts = collections.Counter(nums)
        return max(counts.keys(), key=counts.get)
```

复杂度分析：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

## 排序

思路：如果将数组的所有元素按照单调递增或单调递减的顺序排序，那么下标为 `n/2` 的元素一定是众数。

java

```java
class Solution {
    public int majorityElements(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```

python

```python
class Solution:
    def majorityElements(self, nums):
        nums.sort()
        return nums[len(nums) // 2]
```

时间复杂度：O(nlogn), 空间复杂度：O(logn).

## 随机化

思路：随机挑选一个下标，检查是否是众数，是就返回，不是继续随机挑选。

java

```java
class Solution {
    private int randRange(Random rand, int min, int max) {
        return rand.nextInt(max - min) + min;
    }

    private int countOccurences(int[] nums, int num) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    public int majorityElements(int[] nums) {
        Random rand = new Random();

        int majorityCount = nums.length/2;

        while (True) {
            int candidate = nums[randRange(rand, 0, nums.length)];
            if (countOccurences(nums, candidate) > majorityCount) {
                return candidate;
            }
        }
    }
}
```

python

```python
import random


class Solution:
    def majorityElements(self, nums):
        majority_count = len(nums) // 2
        while True:
            candidate = random.choice(nums)
            if sum(1 for elem in nums if elem == candidate) > majority_count:
                return candidate
```

时间复杂度：O(n), 空间复杂度：O(1).

## 分治

时间复杂度：O(nlogn), 空间复杂度：O(logn).

python

```python
class Solution:
    def majorityElements(self, nums, lo=0, hi=None):
        def majority_element_rec(lo, hi):
            if lo == hi:
                return nums[lo]

            mid = (hi - lo) // 2 + lo
            left = majority_element_rec(lo, mid)
            right = majority_element_rec(mid, hi)

            if left == right:
                return left

            left_count = sum(1 for i in range(lo, hi + 1) if nums[i] == left)
            right_count = sum(1 for i in range(lo, hi + 1) if nums[i] == right)

            return left if left_count > right_count else right

        return majority_element_rec(0, len(nums) - 1)
```

## Boyer-Moore 投票算法

思路：如果把众数记为 `+1`, 其他数记为 `-1`， 显然和大于0.

时间复杂度：O(n), 空间复杂度：O(1).

python

```python
class Solution:
    def majorityElements(self, nums):
        count = 0
        candidate = None

        for num in nums:
            if count == 0:
                candidate = num
            count += (1 if num == candidate else -1)

        return candidate
```
