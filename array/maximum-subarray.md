# 最大子序和

## [题干](https://leetcode-cn.com/problems/maximum-subarray/)

给定一个整数数组 `nums`, 找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

难度：简单

基本没有思路😓，只能想到定个初值 `nums[0]`, 再从索引 1 开始遍历数组。

## 方法一：暴力法

思路：用两个变量，一个记录最大和，一个记录当前和。时间复杂度 `O(n)`.

python

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        tmp = nums[0]
        max_sum = tmp
        for i in range(1, len(nums)):
            if tmp + nums[i] > nums[i]:
                max_sum = max(max_sum, tmp + nums[i])
                tmp += nums[i]
            else:
                # 当 nums[i] >= tmp + nums[i], 则从该元素开始，重新寻找最大子序列
                max_sum = max(max_sum, nums[i])
                tmp = nums[i]
        return max_sum
```

下面是官方解法：

## 方法二：动态规划

时间复杂度 `O(n)`, 空间复杂度 `O(1)`.

思路：用 f(i) 代表以第 i 个数结尾的**连续子数组的的最大和**, 则动态规划转移方程：f(i) = max{f(i-1) + a[i], a[i]}.

实现：用一个 f 数组来保存 f(i) 的值，用一个循环求出所有的 f(i). 我们可以只用一个变量 `pre` 来维护对于当前 f(i) 的 f(i-1)的值。类似 `滚动数组` 的思想。

c++

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int pre = 0, maxAns = nums[0];
        for (const auto &x: nums) {
            pre = max(pre + x, x);
            maxAns = max(maxAns, pre);
        }
        return maxAns;
    }
};
```

## 方法三：分治法

分治方法类似于 `线段树求解 LCIS 问题` 的 `pushUp` 操作。

时间复杂度 `O(nlogn)`, 空间复杂度 `O(logn)`.

对于一个区间 [l,r], 维护四个量：

- `lSum` 表示 [l,r] 内以 l 为左端点的最大子段和
- `rSum` 表示 [l,r] 内以 r 为右端点的最大子段和
- `mSum` 表示 [l,r] 内的最大子段和
- `iSum` 表示 [l,r] 的区间和

以下简称 [l,m] 为 [l,r] 的左子区间, [m+1,r] 为 [l,r] 的右子区间。对于长度为 1 的区间 [i,i], 四个量的值都和 a[i] 相等。对于长度大于 1 的区间：

- `iSum`: 左子区间的 `iSum` + 右子区间的 `iSum`;
- `lSum`: 要么等于左子区间的 `lSum`, 要么等于左子区间的 `iSum` + 右子区间的 `lSum`;
- `rSum`: 要么等于右子区间的 `rSum`, 要么等于右子区间的 `iSum` + 左子区间的 `rSum`;
- `mSum`: 如果 `mSum` 对应的区间不跨越 m, `mSum` 为左右子区间的 `mSum` 的一个；反之，则是左子区间的 `rSum` + 右子区间的 `lSum`.

c++

```c++
class Solution {
public:
    struct Status {
        int lSum, rSum, mSum, iSum;
    };

    Status pushUp(Status l, Status r) {
        int iSum = l.iSum + r.iSum;
        int lSum = max(l.lSum, l.iSum + r.lSum);
        int rSum = max(r.rSum, r.iSum + l.rSum);
        int mSum = max(max(l.mSum, r.mSum), l.rSum + r.lSum);
    };

    Status get(vector<int> &a, int l, int r) {
        if (i == r) return (Status) {a[l], a[l], a[l], a[l]};
        int m = (l + r) >> 1;
        Status lSub = get(a, l, m);
        Status rSub = get(a, m + 1, r);
        return pushUp(lSub, rSub);
    }

    int maxSubArray(vector<int>& nums) {
        return get(nums, 0, nums.size() - 1).mSum;
    }
};
```
