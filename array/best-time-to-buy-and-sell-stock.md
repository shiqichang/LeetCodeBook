# 买卖股票的最佳时机

## [题干](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

给定一个数组，它的第 `i` 个元素是一支给定股票第 `i` 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

难度：简单

## 我的解法：暴力法

- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

Java

```java
public class Solution {
    public int maxProfit(int prices[]) {
        int maxProfit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            for (int j = i + 1; j < prices.length; j++) {
                int profit = prices[j] - prices[i];
                if (profit > maxProfit) {
                    maxprofit = profit;
                }
            }
        }
        return maxprofit;
    }
}
```

## 官方解法：一次遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

python

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        inf = int(1e9)
        min_price = inf
        res = 0
        for price in prices:
            res = max(price - min_price, res)
            min_price = min(price, min_price)

        return res
```
