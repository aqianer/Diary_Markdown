## 循环
### for循环

> Python的循环有两种，一种是for...in循环，依次把list或tuple中的每个元素迭代出来

```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```

> 比如计算1~10的和

```python
sum = 0
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    sum = sum + x
print(sum)
```

> 如果要计算1-100的整数之和，从1写到100有点困难，幸好Python提供一个`range()`函数，可以生成一个整数序列，再通过`list()`函数可以转换为list。比如`range(5)`生成的序列是从0开始小于5的整数

```python
>>> list(range(5))
[0, 1, 2, 3, 4]
```

```python
sum = 0
for x in range(101):
    sum = sum + x
print(sum)
```


### while循环

```python
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```

## Break

```python
n=1
while n <= 100:
    if n>10:
        break
    print(n)
    n=n+1
print('END')
```

## continue

> 只打印奇数，碰到偶数就跳过

```python
n=0
while n<=100:
    if n%2==0:
        n=n+1
        continue
	print(n)
    n=n+1
print('END')
```



