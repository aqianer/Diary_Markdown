Todo:
新建工作记录
登山
吾辈才情之所向 虽风云并趋耳
> 错误码多语言适配 ---数据字典


> 同步业务超时响应和网络超时响应问题


> 北向接口要和前端沟通好传参请求报文和响应报文（最好生成json在编排的时候直接导入，避免使用结构体容易出错）


> 内部接口请求头那个部分每个接口就Commandid不一样，设置好公共变量以后都统一起来，公共变量命名要和别的局点区分开来（Keyowner -->DjiboutiKeyowner）
> 内部接口的端点都是用统一的，不要去自己生成xsd导入进来，外发接口端点最好集中起来写在yaml文件里。

Api


开发流程：
1、参与se评审规格，提出疑问，同步准备环境，fork代码仓库，se分解需求
2、书写story，story写出开发实现方案，书写ST用例，评审story和用例，发评审结论邮件，并上传到d-box，上ewindcloud领取story，并启动，同时将st用例上传到ewindcloud
3、编码，自验证，自己参照checklist检查一遍编码规范，然后使用需求/问题单提交代码到自己的代码仓库，再使用使用需求/问题单发起合并，找对应局点/模块MDE评审代码，再找commit评审合入代码
4、通知pm、ci出包，升级ci环境，并上ci环境验证、showcase，showcase用例可以使用st用例或者是测试提供的showcase用例，发showcase结论邮件，如有问题先修改问题后通知pm\ci出包升级，并验证通过，然后上传邮件到d-box，同时上ewindcloud将story走到开发结束状态，st用例pass掉
5、pm发邮件转测试，之后就是有问题改问题单就行

python碰到的问题





# 列表匹配:
# 涉及到的函数参数问题，以及数据结构

print('-- match list --')

args = ['gcc', 'hello.c', 'world.c','ccl.java','xx.md']
# args = ['clean']
# args = ['gcc']

match args:
    # 如果仅出现gcc，报错:
    case ['gcc']:
        print('gcc: missing source file(s).')
    # 出现gcc，且至少指定了一个文件:
    case ['gcc', file1, *files]:
        print('gcc compile: ' + file1 + ', ' + ', '.join(files))
    # 仅出现clean:
    case ['clean']:
        print('clean')
    case _:
        print('invalid command.')

case ['gcc', file1, *files]表示列表第一个字符串是'gcc'，第二个字符串绑定到变量file1，后面的任意个字符串绑定到*files

#函数的参数

#位置参数

def power(x):
    return x * x

def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s

#默认参数

def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s

def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)

def add_end(L=[]):
    L.append('END')
    return L

def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L


#可变参数

def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

>>> calc(1, 2)
5
>>> calc()
0

>>> nums = [1, 2, 3]
>>> calc(*nums)
14

*nums表示把nums这个list的所有元素作为可变参数传进去。这种写法相当有用，而且很常见。

#关键字参数

关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。

def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)

调用实例：
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}


>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}


#命名关键字参数

对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。至于到底传入了哪些，就需要在函数内部通过kw检查。这就是引入命名关键字的原因

def person(name, age, *, city, job):
    print(name, age, city, job)
和关键字参数**kw不同，命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数。

def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)

>>> person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer


#参数组合


def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)

>>> f1(1, 2)
a = 1 b = 2 c = 0 args = () kw = {}
>>> f1(1, 2, c=3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> f1(1, 2, 3, 'a', 'b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
>>> f2(1, 2, d=99, ext=None)
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None}


>>> args = (1, 2, 3, 4)
>>> kw = {'d': 99, 'x': '#'}
>>> f1(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': '#'}
>>> args = (1, 2, 3)
>>> kw = {'d': 88, 'x': '#'}
>>> f2(*args, **kw)
a = 1 b = 2 c = 3 d = 88 kw = {'x': '#'}

