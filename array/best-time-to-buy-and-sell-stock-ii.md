# 买卖股票的最佳时机 II

## [题干](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

给定一个数组，它的第 `i` 个元素是一支给定股票第 `i` 天的价格。

设计一个算法来计算你能获取的最大利润，你可以尽可能的完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

难度：简单

提示：

- `1 <= prices.length <= 3 * 10 ^ 4`
- `0 <= prices[i] <= 10 ^ 4`

## 贪心算法

解题思路：

- 股票买卖策略：

  - 单独交易日：设今天价格 p1, 明天价格 p2, 则今天买入、明天卖出可赚取金额 `p2 - p1` (负值代表亏损)
  - 连续上涨交易日：设此上涨交易日股票价格分别为 p1,p2,...,pn, 则第一天买最后一天卖收益最大，即 `pn - p1 = (p2 - p1) + (p3 - p2) + ... + (pn - pn-1)`
  - 连续下降交易日：不买卖收益最大，即不会亏钱。

- 算法流程：遍历 `prices`, 所有上涨交易日都买卖，所有下降交易日都不买卖。

- 复杂度分析：

  - 时间复杂度：`O(n)`
  - 空间复杂度：`O(1)`

python

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        for i in range(1, len(prices)):
            profit = prices[i] - prices[i - 1]
            if profit > 0:
                res += profit

        return res
```

## 峰谷法

兴趣点是连续的峰和谷。需要考虑到紧跟谷的每一个峰值以最大化利润。

如果试图跳过其中一个峰值来获取更多利润，最终将失去其中一笔交易中获得的利润，从而导致总利润的降低。

- 复杂度分析：

  - 时间复杂度：O(n)
  - 空间复杂度：O(1)
  
java

```java
class Solution {
    public int maxProfit(int[] prices) {
        int i = 0;
        int valley = prices[0];
        int peak = prices[0];
        int maxprofit = 0;
        while (i < prices.length - 1) {
            while (i < prices.length - 1 && prices[i] >= prices[i + 1])
                i++;
            vallery = prices[i];
            while (i < prices.length - 1 && prices[i] <= prices[i + 1])
                i++;
            peak = prices[i];
            maxprofit += peak - vallery;
        }
        return maxprofit;
    }
}
```
