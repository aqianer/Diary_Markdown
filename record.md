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



## 数据类型和变量

> 主要说下与其他语言（比如Java）的区别

#### 字符串

转义字符

```python
>>> print('I\'m ok.')
I'm ok.
>>> print('I\'m learning\nPython.')
I'm learning
Python.
>>> print('\\\n\\')
\
\
```

> 如果字符串里面有很多字符都需要转义，就需要加很多`\`，为了简化，Python还允许用`r''`表示`''`内部的字符串默认不转义，可以自己试试：

```python
>>> print('\\\t\\')
\       \
>>> print(r'\\\t\\')
\\\t\\
```

```python
a = 123 # a是整数
print(a)
a = 'ABC' # a变为字符串
print(a)
```

> 这种变量本身类型不固定的语言称之为*动态语言*，与之对应的是*静态语言*。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。例如Java是静态语言，赋值语句如下

```python
int a = 123; // a是整数类型变量
a = "ABC"; // 错误：不能把字符串赋给整型变量
```

> 当我们写：
>
> ```python
> a = 'ABC'
> ```
>
> 时，Python解释器干了两件事情：
>
> 1. 在内存中创建了一个`'ABC'`的字符串；
> 2. 在内存中创建了一个名为`a`的变量，并把它指向`'ABC'`。
>
> 也可以把一个变量`a`赋值给另一个变量`b`，这个操作实际上是把变量`b`指向变量`a`所指向的数据，例如下面的代码：
>
> ```python
> # -*- coding: utf-8 -*-
> ----
> a = 'ABC'
> b = a
> a = 'XYZ'
> print(b)
> ```


