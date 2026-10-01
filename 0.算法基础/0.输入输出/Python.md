---
title: Python
time: 2026-10-02 Fri 02:53
tags:
---

可以把 ACM 最常见的三个写法记成：

```python
# 一个整数
n = int(input())

# 一行多个整数
nums = list(map(int, input().split()))

# 一行多个字符串
words = input().split()
```

一个`input()`读一行，返回字符串。



# 1. 单个整数

## 输入

```
5
```

## 代码

```python
n = int(input())
```

------

# 2. 一行多个整数

最常见：

## 输入

```
1 2 3 4 5
```

## 代码

```python
nums = list(map(int, input().split()))
```

结果：

```python
[1, 2, 3, 4, 5]
```

------

# 3. 多行多个整数

例如：

```
3
1 2 3
4 5 6
7 8 9
```

第一行：

```python
n = int(input())
```

读取矩阵：

```python
matrix = []

for _ in range(n):
    matrix.append(list(map(int, input().split())))
```

------

# 4. 第一行给行列数

非常常见：

输入：

```
3 4
1 2 3 4
5 6 7 8
9 10 11 12
```

代码：

```python
m, n = map(int, input().split())

grid = []

for _ in range(m):
    grid.append(list(map(int, input().split())))
```

------

# 5. 字符串输入

## 一个字符串

输入：

```
abcde
```

代码：

```python
s = input()
```

------

## 多个字符串

输入：

```
hello world python
```

代码：

```python
words = input().split()
```

结果：

```python
["hello", "world", "python"]
```

------

# 6. 字符串数组

输入：

```
3
abc
def
ghi
```

代码：

```python
n = int(input())

words = []

for _ in range(n):
    words.append(input())
```

------

# 7. 字符矩阵

例如：

```
3 4
..#.
.#..
....
```

代码：

```python
m, n = map(int, input().split())

grid = []

for _ in range(m):
    grid.append(list(input()))
```

结果：

```python
[
 ['.','.','#','.'],
 ['.','#','.','.'],
 ['.','.','.','.']
]
```

DFS/BFS 岛屿问题经常这样输入。

------

# 8. 不定行输入（读到 EOF）

例如：

```
1 2
3 4
5 6
```

不知道多少行。

使用：

```python
import sys

for line in sys.stdin:
    nums = list(map(int, line.split()))
```

或者：

```python
data = sys.stdin.read().split()
```

------

# 9. 全部输入一次读取（竞赛推荐）

速度最快：

```python
import sys

data = sys.stdin.read().split()
```

例如输入：

```
3
1 2 3
```

得到：

```python
[
'3',
'1',
'2',
'3'
]
```

需要自己转换：

```python
it = iter(data)

n = int(next(it))

nums = []

for _ in range(n):
    nums.append(int(next(it)))
```

------

# 10. 第一行 T 组测试数据

非常常见：

输入：

```
3
2
1 2
3
4 5 6
4
7 8 9 10
```

含义：

```
3组测试
```

代码：

```python
T = int(input())

for _ in range(T):
    n = int(input())
    nums = list(map(int, input().split()))

    # solve
```

------

# 11. 输出一个数字

```python
print(ans)
```

------

# 12. 输出数组

输入：

```python
ans = [1,2,3]
```

输出：

```
1 2 3
```

代码：

```python
print(*ans)
```

等价：

```python
print(" ".join(map(str, ans)))
```

------

# 13. 输出二维数组

例如：

```python
matrix = [
 [1,2],
 [3,4]
]
```

输出：

```
1 2
3 4
```

代码：

```python
for row in matrix:
    print(*row)
```

------

# 14. 多组答案收集后统一输出

推荐：

```python
ans = []

for _ in range(T):
    res = solve()
    ans.append(str(res))

print("\n".join(ans))
```

避免频繁 `print()`。

------

# 15. ACM模板（推荐背）

## 普通输入

```python
import sys

def solve():
    nums = list(map(int, input().split()))

    # algorithm

    print(ans)


if __name__ == "__main__":
    solve()
```

------

## 快速输入模板

适合大数据：

```python
import sys

def solve():
    data = sys.stdin.buffer.read().split()

    idx = 0

    n = int(data[idx])
    idx += 1

    nums = []

    for _ in range(n):
        nums.append(int(data[idx]))
        idx += 1

    # algorithm


if __name__ == "__main__":
    solve()
```

------

# 16. 常见坑

## `input()` 返回字符串

错误：

```python
nums = input().split()

nums.sort()
```

排序的是字符串：

```python
["10","2","3"]
```

结果：

```
10 2 3
```

应该：

```python
nums = list(map(int,input().split()))
```

------

## 空输入

有些平台：

```python
input()
```

可能报错。

安全：

```python
import sys

data = sys.stdin.read().strip()

if not data:
    return
```

------

# 面试笔试最常见组合

| 类型     | 处理                                          |
| -------- | --------------------------------------------- |
| n + 数组 | `n=int(input())` + `map(int,input().split())` |
| m*n矩阵  | 循环读取                                      |
| 字符矩阵 | `list(input())`                               |
| T组测试  | 第一行 T                                      |
| EOF输入  | `sys.stdin.read()`                            |
| 输出数组 | `print(*ans)`                                 |
| 多行输出 | `"\n".join()`                                 |

掌握前 **1~8 类**基本覆盖 90% ACM 输入。
