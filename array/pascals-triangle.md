# 杨辉三角

## [题干](https://leetcode-cn.com/problems/pascals-triangle/)

给定一个非负整数 `numRows`, 生成杨辉三角的前 `numRows` 行。

在杨辉三角中，每个数都是它左上方和右上方的数的和。

难度：简单

## 我的解法

思路：公式 `lists[i][j] = lists[i-1][j-1] + lists[i-1][j]`, 同时考虑 0, 1, 2 三种特殊情况。

python

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        if numRows == 0:
            return []
        if numRows == 1:
            return [[1]]
        if numRows == 2:
            return [[1], [1, 1]]

        lists = [[0 for i in range(j)] for j in range(1, numRows + 1)]
        lists[0][0] = 1
        lists[1][0] = 1
        lists[1][1] = 1
        for i in range(2, numRows):
            for j in range(0, i + 1):
                if j == 0 or j == i:
                    lists[i][j] = 1
                else:
                    lists[i][j] = lists[i - 1][j - 1] + lists[i - 1][j]
        return lists
```

## 官方解法：动态规划

算法：先生成整个 `triangle` 列表，三角形的每一行都以子列表的形式存储。检查行数为0的情况。

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        triangle = []

        for row_num in range(numRows):
            row = [None for _ in range(row_num + 1)]
            row[0], row[-1] = 1, 1

            for j in range(1, len(row) - 1):
                row[j] = triangle[row_num - 1][j - 1] + triangle[row_num - 1][j]

            triangle.append(row)

        return triangle
```

复杂度分析：

- 时间复杂度：O(numRows^2)
- 空间复杂度：O(numRows^2)

看到这，我才知道，这个题本身就只有 `O(n^2)` 的解法，官方解法和我的大同小异呢。

## 优秀解法

思路：当前一行只比上一行多了一个元素，本行元素等于上一行元素往后错一位再逐个相加。

python

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        if numRows == 0:
            return []
        res = [[1]]
        while len(res) < numRows:
            newRow = [a + b for a, b in zip([0] + res[-1], res[-1] + [0])]
            res.append(newRow)
        return res
```
