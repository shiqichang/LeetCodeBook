# 斐波那契数

## [题干](https://leetcode-cn.com/problems/fibonacci-number/)

**斐波那契数**, 通常用 `F(n)` 表示，形成的序列称为**斐波那契数列**, 该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。

也就是：

```log
F(0) = 0, F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

给定 `N`, 计算 `F(N)`.

提示：0 <= N <= 30

难度：简单

## 我的解法

### 递归

时间复杂度：O(2^N), 空间复杂度：O(N).

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N == 0:
            return 0
        if N == 1:
            return 1

        return self.fib(N - 1) + self.fib(N - 2)
```

### 循环

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N == 0:
            return 0
        if N == 1:
            return 1

        result = [0, 1]
        for i in range(2, N + 1):
            result.append(result[i - 1] + result[i - 2])
        return result[-1]
```

## 记忆化自底向上的方法

时间复杂度：O(N), 空间复杂度：O(N).

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N <= 1:
            return N
        return self.memoize(N)

    def memoize(self, N: int) -> {}:
        cache = {0: 0, 1: 1}

        for i in range(2, N+1):
            cache[i] = cache[i-1] + cache[i-2]

        return cache[N]
```

## 记忆化自顶向下的方法

时间复杂度：O(N), 空间复杂度：O(N).

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N <= 1:
            return N
        self.cache = {0: 0, 1: 1}
        return self.memoize(N)

    def memoize(self, N: int) -> {}:
        if N in self.cache.keys():
            return self.cache[N]
        self.cache[N] = self.memoize(N-1) + self.memoize(N-2)
        return self.memoize(N)
```

## 自底向上进行迭代

时间复杂度：O(N), 空间复杂度：O(1).

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N <= 1:
            return N
        if N == 2:
            return 1

        current = 0
        prev1 = 1
        prev2 = 1

        for i in range(3, N+1):
            current = prev1 + prev2
            prev2 = prev1
            prev1 = current
        return current
```

## 矩阵求幂

时间复杂度：O(logN), 空间复杂度：O(logN).

python

```python
class Solution:
    def fib(self, N: int) -> int:
        if N <= 1:
            return N

        A = [[1, 1], [1, 0]]
        self.matrix_power(A, N-1)

        return A[0][0]

    def matrix_power(self, A: list, N: int):
        if N <= 1:
            return A

        self.matrix_power(A, N//2)
        self.multiply(A, A)
        B = [[1, 1], [1, 0]]

        if N % 2 != 0:
            self.multiply(A, B)

    def multiply(self, A: list, B: list):
        x = A[0][0] * B[0][0] + A[0][1] * B[1][0]
        y = A[0][0] * B[0][1] + A[0][1] * B[1][1]
        z = A[1][0] * B[0][0] + A[1][1] * B[1][0]
        w = A[1][0] * B[0][1] + A[1][1] * B[1][1]

        A[0][0] = x
        A[0][1] = y
        A[1][0] = z
        A[1][1] = w
```

## 公式法

时间复杂度：O(1), 空间复杂度：O(1).

python

```python
class Solution:
    def fib(self, N):
        golden_ratio = (1 + 5 ** 0.5) / 2
        return int((golden_ratio ** N + 1) / 5 ** 0.5)
```
