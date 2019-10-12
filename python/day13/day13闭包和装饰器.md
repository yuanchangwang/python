# day13闭包和装饰器

## 今日内容概要

1. 闭包
2. 装饰器初识
3. 标准装饰器

## 昨日内容回顾

1. 推导式

   - 列表推导式

     ```python
     [i for i in range(4)]
     [i for i in range(9) if i % 3 == 0]
     ```

   - 字典推导式：

     ```python
     {i: i + 1 for i in range(5)}
     {i: i + 1 for i in range(9) if % 3 == 0}
     ```

   - 集合推导式：

     ```python
     {i for i in range(3)}
     {i for i in range(49) if i % 4 == 0}
     
     ```

2. 内置函数一

     ```python
     all()
     any()
     callable()
     hash()
     oct()
     hex()
     divmod()
     dir()
     help()
     complex()
     id()
     print()
     repr()
     frozenset()
     eval() # 禁用
     exec() # 禁用
     chr()
     ord()
     round()
     bytes()
     ```

3. 内置函数二

     ```python
     # 高阶函数
     abs()
     sum()
     max()
     min()
     map(规则函数，可迭代对象，可迭代对象)
     filter(规则函数，可迭代对象)
     zip()
     reversed(可迭代对象)
     sorted(可迭代对象，key=规则函数)
     reduce(累加函数，可迭代对象)  # from functools import reduce
     format()
     enumerate
     pow()
     
     lambda 匿名函数
     lambda 形参：返回值
     
     lst = [1,2,3,4,5,6,7]
     print(list(reversed(lst)))
     print(lst)
     ```

## 今天内容详细

### 闭包

在编程时，我们会处理到很多数据。但是对于一些数据，我们只想使用，不想修改，我们可以使用`闭包`来防止不经意间的数据修改

闭包的作用主要有两个：

1. 保护数据安全
2. 保护数据干净

满足下面两个条件的函数就是一个使用的闭包：

1. 在嵌套函数内，使用非全局变量（且不使用本层变量）
2. 将嵌套函数本身返回

我们可以用`.__closure__`方法来查看一个函数是否是一个闭包。当返回值为None时，说明该函数不是闭包，当返回值中有变量的内存地址时，说明该函数是个闭包。

例如，下面的函数就是一个闭包：

```python
def func():
    a = 10
    def foo():
    	print(a)
    return foo
f = func()
print(f.__closure__)
 
结果：
(<cell at 0x0000012A5C51CDF8: int object at 0x00007FFAD897E470>,)

```

方法中的`closure`就是`闭包`的意思。返回的`cell`是一个`单元格`对象，用来存储闭包中需要使用到的变量。

当函数执行完成后（也就是`func()`这一步骤），函数体会被销毁，但是闭包`foo`被返回给了`f`，还是被用到，所有照常存在，而闭包中需要使用的变量`a`，此时已经不存在函数`func`中，以为`func`本身已经不复存在，变量`a`在函数销毁后，升级为自由变量。

闭包是怎么做到保护数据的作用的呢？

比如我们现在有一个需求，使用一个函数，每天输入当天营业额，打印出来这几天的平均营业额。

如果我们把营业额的数据存储在列表中，放到全局，可以这样实现功能：

```python
lst = []
def ave_turnover(turnover_today):
    lst.append(turnover_today)
    ave = sum(lst) / len(lst)
    print(ave)
ave_turnover(122333)
ave_turnover(45454)
ave_turnover(1454564)
ave_turnover(124545)
结果：
122333.0
83893.5
540783.6666666666
436724.0


```

如果有一天，我们不小心在全局对lst列表做了修改：

```python
lst = []
def ave_turnover(turnover_today):
    lst.append(turnover_today)
    ave = sum(lst) / len(lst)
    print(ave)
ave_turnover(122333)
ave_turnover(45454)
lst[1] = 10
ave_turnover(1454564)
ave_turnover(124545)

结果：
122333.0
83893.5
525635.6666666666
425363.0

```

这就导致了数据的改变，使得第三天之后的数据全部都不准确。

如果我们把重要的数据`lst`封装到闭包中保护起来，就不会有这种烦恼了：

```python
def ave_turnover():
    lst = []
    def inner(turnover_today):
        lst.append(turnover_today)
        ave = sum(lst) / len(lst)
        print(ave)
    return inner

f = ave_turnover()
f(20000)
f(15000)
lst = [20]
f(140000)
f(120000)

结果：
20000.0
17500.0
58333.333333333336
73750.0

```

对于闭包，除了`.__closure__`方法之外，还有可以用来查看自由变量的`__code__.co_freevars`方法，和可以用来查看局部变量的`__code__.co_varnames`方法：

```python
def ave_turnover():
    lst = []
    def inner(turnover_today):
        lst.append(turnover_today)
        ave = sum(lst) / len(lst)
        print(ave)
    return inner
f = ave_turnover()
print(f.__closure__) # 判断是否是一个闭包
print(f.__code__.co_freevars) # 查看自由变量
print(f.__code__.co_varnames) # 查看局部变量

结果：
(<cell at 0x000001F7BBA7CDF8: list object at 0x000001F7B9E06288>,)
('lst',)
('turnover_today', 'ave')


```

没有将嵌套的函数返回也可以是一个闭包，但是这个闭包没有办法被使用：

```python
def func():
    a = 10
    def foo():
        print(a)
    print(foo.__closure__)
func()

结果：(<cell at 0x00000166EA9DCDF8: int object at 0x00007FFADB14E470>,)


```

闭包也可以通过外层函数加两个括号的方法来调用：

```python
def func():
    a = 10
    def foo():
        print(a)
    return foo
func()()

```

外层函数的参数也是局部变量，所以内层函数使用外层参数的形式也可以构成闭包：

```python
def wrapper(a, b):
    a = 11
    b = 12
    def inner():
        print(a)
        print(b)
    return inner

a = 11
b = 12
ret = wrapper(a,b)
print(ret.__closure__)
print(ret.__code__.co_freevars)
print(ret.__code__.co_varnames)
ret()

结果：
(<cell at 0x000001E5F3E6CDF8: int object at 0x00007FFADE56E490>, <cell at 0x000001E5F3F0E468: int object at 0x00007FFADE56E4B0>)
('a', 'b')
()
11
12

```

闭包的应用场景主要有两个：

1. 装饰器
2. 防止数据被误改动



### 装饰器

在编程中，有很多约定成俗的规则。开放封闭原则就是其中很重要的一个。

开放封闭原则体现在两方面：

1. 对扩展开放，支持增加新功能
2. 对修改源代码封闭，对调用方式的改变封闭

装饰器就是为了体现编程的开放封闭原则而存在的。

装饰器，顾名思义，就是在原有的基础上额外添加新功能的工具。

我们有下面一组函数：

```python
import time
def index():
    time.sleep(0.5)
    print('i am in index')
def func():
    time.sleep(0.8)
    print('i am in func')
def foo():
    time.sleep(0.4)
    print('i am in foo')
    
index()
func()
foo()
```

现在有这样一个需求：想要知道每一个函数运行的时间。

为了不改变函数源代码，我们可以尝试着在调用函数前后加入查看时间戳的代码，尝试着计算函数的运行时间：

```python
import time


def index():
    time.sleep(0.5)
    print('i am ini index')


def func():
    time.sleep(0.8)
    print('i am in func')


def foo():
    time.sleep(0.4)
    print('i am in foo')


start_time = time.time()
index()
print(time.time() - start_time)

start_time = time.time()
func()
print(time.time() - start_time)

start_time = time.time()
foo()
print(time.time() - start_time)

结果：
i am ini index
0.5000491142272949
i am in func
0.800959587097168
i am in foo
0.4001436233520508
```

我们好像得到我们想要的结果了，但不要忘了，我们一开始提到的，我们编程时需要遵循开放封闭原则，我们的确没有改变函数的源码，但是调用时，需要增加代码。我们改变了函数的调用方式。

另一方面，我们在调用的过程中，使用了大量重复代码：`start_time = time.time()`和`print(time.time() - start_time)`为了较少重复代码，我们或许尝试者使用函数，比如这样：

```python
import time
def index():
    time.sleep(0.5)
    print('i am in index')
    
def func():
    time.sleep(0.8)
    print('i am in func')

def foo():
    time.sleep(0.4)
    print('i am in foo')
    
def run_time(f):
    start_time = time.time()
    f()
    print(time.time() - start_time)
    
    
ff = index
index = run_time
index(ff)

ff = func
func = tun_time
func(ff)

ff = foo
foo = run_time
foo(ff)
```

在调用函数时，我之所以把函数写的得这么复杂，而不是简单地写成这样：

```python
run_time(index)
run_time(func)
run_time(foo)

```

是为了避免改变函数的调用方式。

可即便绞尽脑汁，函数最终的调用方式还是发生了变化-- 原本函数的调用是不需要参数的，增加参数`ff`。

不过我们已经离开正确的解决办法非常近了，只差一步，就可以解决我们的困难。

这就需要结合我们今天刚刚学到的内容：闭包。

如果我们把功能函数整合为闭包，就可以满足编程的开放封闭原则，并且不会增加太多重复代码：

```python
import time
def index():
    time.sleep(0.8)
    print('i am in index')
    
def func():
    time.sleep(0.5)
    print('i am in func')
    
def foo():
    time.sleep(0.3)
    print('i am in foo')
    
def run_time(f):
    def inner():
        start_time = time.time()
        f()
        print(time.time() - start_time)
    return inner

index = run_time(index)
index()
func = run_time(func)
func()
foo = run_time(foo)
foo()
```

上面这种给函数增加功能的方法就构成了python中的装饰器。

因为装饰器在python编程中十分好用，python还专门为类似`index = run_time(index)`的赋值运算设定了一个语法糖：

```python
import time
def run_time(f):
    def inner():
        start_time = time.time()
        f()
        print(time.time() - start_time)
        
    return inner
 
@run_time  # 等价于  index = run_time(index)
def index():
    time.sleep(0.5)
    print('i am in index')
    
index()
```

语法糖必须要放在被装饰函数的正上方，虽然有些空行，python解释器也能识别，但是阅读起来很变扭：

```python
@run_time



def index():
    time.sleep(0.6)
    print('i am in index')
```

## 标准装饰器

如果原函数中有参数，我们可以在装饰器的内部函数中设置加入参数：

```python
def plugin(f):
    def inner(user,pwd, hero):
        print('外挂开启')
        f(user,pwd,hero)
        print('外挂结束')
        
     return inner

@plugin
def gamming(user,pwd,hero):
    print('打开游戏')
    print(f'用户名：{user}, 密码: {pwd}')
    print(f'选择英雄：{hero}')
    print('游戏中')
    print('游戏结束了')
    
gamming('meet','12445','草丛论')
```

至此，我们已经把装饰器的内容都讨论过了，其实，装饰器本身并复杂，我们可以使用一个很规整简洁的代码写出一个装饰器：

```python
def wrapper(func):
    def inner(*args, **kwargs):
        """执行被装饰函数前，进行的操作"""
        ret = func(*args, **kwargs)
        """执行被装饰函数后，进行的操作"""
        return ret
    return inner

@wrapper
def foo():
    print('in foo')
foo()
```

这就是`标准版的装饰器`。

其实，对于没有参数的函数，可以只写一层函数实现装饰器的功能：

```python
def foo(func):
    print('新加了一个功能')
    return func


@foo
def index():
    print(2)


index()
```

虽然也能实现新功能，但是不建议这样写，因为不是很规范。而且下面继续调用index，并不会有新的功能加入：

```python
def foo(func):
    print('新功能')
    return func


@foo
def index():
    print(2)


index()
index()
```

函数调用两次，但是新功能仅执行了一次。这是因为在执行语法糖时，新的`index`最终的结果还是原来的`index()`函数，而不是像标准装饰中的`闭包`。

