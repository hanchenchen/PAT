# [1069 The Black Hole of Numbers][https://pintia.cn/problem-sets/994805342720868352/problems/994805400954585088]

| Submit Time           | Status   | Score | Problem                                                      | Compiler          | Run Time | User |
| --------------------- | -------- | ----- | ------------------------------------------------------------ | ----------------- | -------- | ---- |
| 08/15/2020 5:38:06 PM | Accepted | 20    | [1069](https://pintia.cn/problem-sets/994805342720868352/problems/994805400954585088) | Python (python 3) | 20 ms    | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 20 ms    | 2944 KB |
| 1    | Accepted | 20 ms    | 3180 KB |
| 2    | Accepted | 20 ms    | 2984 KB |
| 3    | Accepted | 19 ms    | 3044 KB |
| 4    | Accepted | 19 ms    | 3072 KB |
| 5    | Accepted | 20 ms    | 2944 KB |
| 6    | Accepted | 19 ms    | 3044 KB |

```python



def greater(x: int):
    arr = []
    for i in range(4):
        arr.append(x % 10)
        x //= 10
    x = 0
    arr.sort()
    # print("arr",arr)
    for i in arr:
        x *= 10
        x += i
    return x


def less(x: int):
    arr = []
    for i in range(4):
        arr.append(x % 10)
        x //= 10
    x = 0
    arr.sort(reverse=True)
    for i in arr:
        x *= 10
        x += i
    return x


n = int(input())
l = less(n)
g = greater(n)
n = l - g
print('{0:0>4d} - {1:0>4d} = {2:0>4d}'.format(l, g, n))
while n != 6174 and n:
    l = less(n)
    g = greater(n)
    n = l - g
    print('{0:0>4d} - {1:0>4d} = {2:0>4d}'.format(l, g, n))
```

