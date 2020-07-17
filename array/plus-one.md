# 加一

## [题干](https://leetcode-cn.com/problems/plus-one/)

给定一个由**整数**组成的**非空**数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位，数组中的每个元素只存储**单个**数字。

难度：简单

## 我的解法

思路：倒序循环数组，用一个临时的字段，按 `digits[len(digits)-1-i] * (10**i)` 记数组元素组合加1的结果；然后，将临时字段类型由 int -> str, 再一次循环，从高到低添加字符串元素。

python

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        tmp = 0
        for i in range(len(digits)-1, -1, -1):
            tmp += (digits[len(digits)-1-i] * (10**i))
        tmp += 1
        res = []
        for i in str(tmp):
            res.append(int(i))
        return res
```

## 其他解法

### 解法一

思路：遍历是否为9，是9变0，不是返回即可

python

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        for i in range(1, len(digits) + 1):
            if digits[-i] != 9:
                digits[-i] += 1
                return digits
            digits[-i] = 0
        digits.insert(0, 1)
        return digits
```

### 解法二

java

```java
class Solution:
    public int[] plusOne(int[] digits) {
        for (int i = digits.length - 1; i >= 0; i--) {
            digits[i]++;
            digits[i] = digits[i] % 10;
            if (digits[i] != 0) return digits;
        }
        // 针对特殊情况：99, 999, ...
        digits = new int[digits.length + 1];
        digits[0] = 1;
        return digits;
    }
```
