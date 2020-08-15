# [1073 Scientific Notation][https://pintia.cn/problem-sets/994805342720868352/problems/994805395707510784]

| Submit Time           | Status   | Score | Problem                                                      | Compiler          | Run Time | User |
| --------------------- | -------- | ----- | ------------------------------------------------------------ | ----------------- | -------- | ---- |
| 08/15/2020 6:13:28 PM | Accepted | 20    | [1073](https://pintia.cn/problem-sets/994805342720868352/problems/994805395707510784) | Python (python 3) | 21 ms    | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 21 ms    | 2944 KB |
| 1    | Accepted | 20 ms    | 2944 KB |
| 2    | Accepted | 20 ms    | 2944 KB |
| 3    | Accepted | 20 ms    | 3100 KB |
| 4    | Accepted | 19 ms    | 3040 KB |
| 5    | Accepted | 19 ms    | 3080 KB |
| 6    | Accepted | 19 ms    | 3040 KB |

```python
s = input()
a = s.split('E')[0]
b = int(s.split('E')[1])
c = len(a)
for i in range(len(a)):
    c-=1
    if a[i]=='.':
        break
num = a[1:-c-1]+a[-c:]
p = a[0]
a = num
c -= b
# print(c,num)
if c>=len(a):
    num = '0'*(c-len(a)) + num
    a = '0.'+num
elif c>0:
    a = a[0:-c]+'.'+a[-c:]
else:
    a = a + '0'*(-c)
if p == '-':
    a=p+a# +9.1E-0
print(a)

```

