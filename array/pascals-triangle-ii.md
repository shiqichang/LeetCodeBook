# 杨辉三角 II

## [题干](https://leetcode-cn.com/problems/pascals-triangle-ii/)

给定一个非负索引 k, 其中 k <= 33, 返回杨辉三角的第 k 行。

难度：简单

进阶：你可以优化你的算法到 `O(k)` 空间复杂度。

## 我的解法

python

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        triangle = []
        for i in range(rowIndex + 1):
            row = [None for _ in range(i + 1)]
            row[0], row[-1] = 1, 1

            for j in range(1, len(row) - 1):
                row[j] = triangle[i - 1][j - 1] + triangle[i - 1][j]

            triangle.append(row)

            if i == rowIndex:
                return row
```

这里需要注意一点，第 k 行，指的是索引 k.

## 优秀解法

思路：从倒数第二个元素开始往前更新，`row[i] = row[i] + row[i -1]`.

python

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        row = [1 for _ in range(rowIndex + 1)]

        for i in range(rowIndex + 1):
            for j in range(i - 1, 0 , -1):
                row[j] = row[j] + row[j - 1]

        return row
```

处理方法：先处理行尾，循环中从后往前修改。
