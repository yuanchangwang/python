# day11 迭代器和生成器

## 今日内容概要

1. `f-strings`详解
2. 迭代器
3. 生成器

## 昨日内容回顾

1. 函数的默认参数

   1. 动态位置参数：`*args`，接收多余位置参数，以元组形式存储
   2. 动态关键字参数：`**kwargs`，接收多余默认参数，以字典形似存储
   3. 参数的优先级：位置参数 > 动态位置参数 > 默认参数 > 动态关键字参数
      - 函数的定义阶段，碰到`*`和`**`是聚合
      - 在函数体中碰到`*`是打散，`*args`打散元组，`**kwargs`打散字典，获取的是键
      - 在函数的调用也可以用到`*`打散，后期可能会用到

2. 函数的注释

   ```python
   def func(a: int, b: str):
       """
       计算字符串的乘法
       :param a: int
       :param b: str
       :return: str
       """
       return a * b
   
   c = func(3, 'a')
   print(c)
   ```

   - `print(func.__doc__())`查看函数的注释
   - `print(func.__name__())`查看函数的名字

3. 函数的名称空间

   1. 内置空间
   2. 全局空间
   3. 局部空间
      - 加载：内置 > 全局 > 局部
      - 取值：局部 > 全局 > 内置
      - 作用域：
        - 全局 = 内置 + 全局
        - 局部 = 局部
   4. 函数名的第一类对象及使用
      1. 函数名可以作为赋值给变量
      2. 函数名可以作为另一个函数的参数
      3. 函数名可以作为另个函数的返回值
      4. 函数名可以作为元素存储在容器中
   5. 函数的嵌套
      1. 交叉嵌套
      2. 回环嵌套
   6. `global`和`nonlocal`
      1. `global`只能声明要修改全局变量
         - 当全局中没有这个变量时，会给全局创建这个变量
         - 当全局中有这个变量时，会修改这变量的值
      2. `nonlocal`只能声明要修改局部变量
         - 当局部中没有这个变量时，不但不会创建，还会报错，即使全局中有也不成
         - 当局部中有这个变量时，只会修改离`nonlocal`最近的一层变量
         - 如果`nonlocal`的上一层没有就继续向上一层寻找，直到找到最外层局部空间

   


## 今日内容详细

### `f-strings`详解

`f-strings`在字符串格式化的那一部分已经有所讨论。其实当时当时已经讨论得差不多了，今天只是稍微地有一点补充。主要还是复习。

`f-strings`基本结构是这样的：

```python
nane = "神州"
age = 18
sex = "男"
msg = F'姓名：{name}, 性别：{age},年龄：{sex}' # 大写字母也可以
msg = f'姓名：{name}, 性别 ：{age}, 年龄：{sex}' #建议小写 
print(msg)
```

`f-strings`就是在字符串的引号前面加上一个字母`f`。字母大小写都可以，但是推荐使用小写。`{}`中除了可以使用变量外，还可以放入函数：

```python
def func(a,b):
    return a + b
msg = f'运行结果：{func(1,2)}'
print(msg)
```

甚至可以在`{}`中放入`input`函数，让用户输入：

```python
print(f'姓名：{input("请输入姓名：")}，年龄：{input("请输入年龄：")}，性别：{input("请输入性别：")}')
```

除了字符串，`{}`中也可以放入列表和字典：

```python
lst = [1,2,3,4,5,6,44,6]
msg = f'运行结果：{lst[0:3]}'
print(msg)

dic = {'key':1,'key1':22}
msg = f'运行结果：{dic["key1"]}'
print(msg)
```

`f-strings`可以写成多行的形式，但依然打印成一行：

```python
msg = f"窗前明月{'光'}，" \
	  f"玻璃好上{'霜'}，" \
      f"要不及时{'擦'}，" \
      f"一会就很{'脏'}。"
print(msg)
```

想要打印多行字符串，还是要使用三对引号：

```python
msg = f'''
窗前明月{'光'}，
玻璃好上{'霜'}，
要不及时{'擦'}，
一会就很{'脏'}。
'''
print(msg)
```

通过使用三元运算，配合`f-strings`我们可以进一步节省代码：

```python
a = 10
b = 20
msg = f'{a if a < b else b}'
print(msg)
```

同时使用两个括号表示一个可以打印的的大括号：

```python
msg = f'{{"yuan":"chang"}}'
print(msg)
```

### 迭代器

迭代器就是用来将可迭代对象的值一个以取出来的工具。

我们学过的可迭代的数据类型有：字符串，列表，字典，元组，集合

不可迭代的数据类型有：整型，布尔值

python中规定，只要是具有`__iter__()`方法就是可迭代对象：

```python
str.__iter__()
list.__iter__()
tuple.__iter__()
set.__iter__()
```

可迭代对象可以通过for循环获取每一个元素，且可以重复取值：

```python
s = "yuan"
for i in s:
    print(i)
for j in s:
    print(j)
    
结果：
y
u
a
n
y
u
a
n

```

我们可以使用可迭代对象的`.__iter__()`方法，将其转化为迭代器。可以通过`.__next__()`方法取下一位的值：

```python
lst = [1,2,3,4,5]
l = lst.__iter__()
print(l)
print(l.__next__())
print(l.__next__())
print(l.__next__())

结果：
<list_iterator object at 0x000001CB5EF9B4E0>
1
2
3
4
5


```

需要注意的是，迭代器中有多少个元素，就是只能使用多少次`.__next__()`方法，如果使用次数超过元素个数，就会报错：

```python
print(l.__next__())
StopIteration
```

在python中，有`.__iter__()`和`.__next__()`方法的就是一个迭代器。

不难看出，文件句柄也是一个迭代器：

```python
f = open('yuan', 'a', encoding='utf-8')
f.__iter__()
f.__next__()
```

这里说一句，当我们使用id函数获取到内存地址，并不是数据正真存放的位置，只是一串供我们参考的数字而已，不可当真。

需要注意的是，当对同一个可迭代对象多次使用`.__iter__()`方法创建迭代器的时候，我们是创建了多个生成器，这些生成器之间不会互相影响：

```python
lst = [1,2,3,4,5,6]
l1 = lst.__iter__() # 这是一个迭代器1
l2 = lst.__iter__() # 这是一个迭代器2
l3 = lst.__iter__() # 这是一个迭代器3
print(l1.__next__())
print(l2.__next__())
print(l3.__next__())
print(l2.__next__())
print(l3.__next__())

结果：
1
1
1
2
2

```

本质上来讲，for循环底层，就是将可迭代对象转换为生成器，通过循环迭代，获取每个元素的：

```python
s = "yuan"
s1 = s.__iter__()
while True:
    try:
        print(s1.__next__())
    except StopIteration:
        break
        
结果：
y
u
a
n
```

除了使用可迭代对象的`._——iter__()`和`.__next__()`方法创建和操作迭代器，我们还可以使用python的内置函数，`iter()`和`next()`来实现同样地功能：

```python
lst = [1,2,3,4,5]
l = iter(lst)
print(next(l))
print(next(l))
print(next(l))
```

需要注意的是，在python 2中，创建和使用迭代器只能使用内置函数`iter()`和`next()`，迭代器的`.__iter__()`和`.__next__()`方法不可用；在python 3中，既可以使用内置函数`iter()`和`next()`，也可以使用`.__iter__()`和`__next__()`方法创建和使用迭代器。但是推荐使用兼容性更高的内置函数`iter()`和`nxet()`。

可迭代对象与迭代器的比较：

```python
可迭代对象：str list tuple ...
	具有.__iter__()方法的就是一个可迭代对象
    优点：
    	1.使用灵活（每个可迭代对象都有自己的方法）
        2.能够直接且直观地查看元素个数
    缺点：
    	占内存
    应用：当内存空间大，数据量比较少的情况，建议使用可迭代对象
    
迭代器： 文件句柄就是一个迭代器
	具有.__iter__()和.__next__()方法的，就是一个迭代器
    优点：
    	节省内存
    缺点：
    	1.只能一个方向执行
        2.一次性
        3.不能灵活操作，不能直观查看元素个数
    应用：当内存小，数据量大的情况，建议使用迭代器
```

迭代器除了节省内存之外，似乎没有什么好处，但是广泛应用于python编程过程中，就是因为它能大量节省内存空间，在编程过程中，我们常常会进行空间和时间的抉择

- 时间换空间：迭代器，生成器，用大量的时间来节省空间的使用
- 空间换时间：可迭代对象，使用大量的空间来节省时间

迭代器同样具有`.__iter__()`方法，因此也是一个可迭代对象，可以直接被for循环：

```python
lst = [1, 3, 4, 4, 5, 6]
l = iter(lst)
for i in l: # for循环可以直接循环迭代器
    print(i)
```

### 生成器 

生成器的本质就是一个迭代器。

生成器和迭代器的最大区别为：

- 迭代器：比如文件句柄，是通过数据转换，由python自带提供的
- 生成器：程序员自己编写实现

生成器的定义方式有两种：

1. 基于函数实现生成器
2. 使用表达式实现生成器

我们可以通过这个方式来定义和使用一个函数：

```python
def func():
    print(1)
    return 5
print(func())
```

如果我们把函数中return替换成yield，就创建了一个生成器：

```python
def func():
    print(2)
    yield 5
    
print(func())

结果：
<generator object func at 0x0000016F5B5361B0>
```

`func`函数调用时，会生成一个生成器对象，`print`打印出来的就是这个生成器对象的内存地址。

补充一点知识，下面这段代码：

```python
def func():
    print(foo)
def func():
    print(foo)
```

运行过后程序并没有报错，虽然并没有变量或者函数名为`foo`。这是因为程序运行过程中，会分析过程：语法分许和词法分析。

词法分析就是分析代码中是否所有的词语都符合规范，如果不规范，则会报错。

语法分析则是判断每个语句是否符合语法规范

上面两个代码，词法分析是可以的，语法分析因为不会进入到函数体中，所以也不会报错，故而没有报错。

生成器的特点是：惰性机制，也就是只有使用next方法调用生成器时，才会开始执行生成器的代码。即便是在创建生成器对象时，也不会运行装饰器中的内容。

yield和return的部分功能很像

我们可以设定多个yield，每次使用next函数，就会运行到下一个yield，直至最后：

```python
def func():
    yield 1
    yield 2
    yield 3
    
g = func()
print(next(g))
print(next(g))
print(next(g))

结果：
1
2
3
```

同迭代器类似，也可以创建多个生成器对象，这些生成器对象彼此独立，互不干扰：

```python
def func():
    yield 1
    yield 2
    yield 3
    
g1 = func()
g2 = func()
g3 = func()
print(g1,g2,g3)
print(next(g1))
print(next(g2))
print(next(g3))
print(next(g1))
print(next(g3))

结果：
<generator object func at 0x000001E47C2061B0> <generator object func at 0x000001E47C206F48> <generator object func at 0x000001E47C363048>
1
1
1
2
2

```

三个生成器的内存地址各不相同，使用next方法也是互不影响。

如果yield后面什么也不写，默认返回的值为None:

```python
def func():
    yield 
    
print(func().__next__())

结果：
None
```

同return类似，yield后面也可以接任意数据类型：

```PYTHON
def func():
    yield [1, 2, 3, 4, 5]


print(func().__next__(), type(next(func())))


def foo():
    yield {'key': 1}


print(foo().__next__(), type(next(foo())))


def f():
    def f1():
        print(123)

    yield f1


print(next(f()), type(next(f())))


def f2():
    yield 1, 2, 4, 5, 6


print(next(f2()), type(f2()))


结果：
[1, 2, 3, 4, 5] <class 'list'>
{'key': 1} <class 'dict'>
<function f.<locals>.f1 at 0x0000017BEC5D3598> <class 'function'>
(1, 2, 4, 5, 6) <class 'generator'>


```

生成器的好处同迭代器一样，也可以节省大量的内存空间。

除了yield方法，我们还可以yield from 方法来逐个返回可迭代对象中的元素：

```python
def func():
    yield from [1, 2, 3, 5, 6] # 将列表中的元素逐个返回
    
g = func()
print(next(g))
print(next(g))
print(next(g))
```

如果两个yield from同时存在，会先将前面的可迭代对象逐个返回之后，再返回后面的可迭代对象：

```python
def func():
    yield from [22, 3, 45, 4, 66]
    yield from [1, 2, 3, 4]
g = func()
print(next(g))
print(next(g))
print(next(g))
```

### 总结

生成器一定是一个迭代器，但是迭代器不一定是一个生成器；

迭代器一定是一个可迭代对象，但是可迭代对象不一定是一个迭代器。

生成器的本质是一个迭代器，迭代器的本质是一个可迭代对象。

迭代器和生成器的优点：

- 节省空间

迭代器和生成器的缺点：

1. 不能直接使用元素
2. 不能直观查看元素个数
3. 使用不灵活
4. 稍微消耗时间
5. 操作是一次性的，不可逆的

当数据特别巨大时，要记得使用生成器

区分迭代器和生成器：

```python
lst = [1, 2, 3]
l = lst.__iter__()

def func():
    yield l
    
g = func()
print(l, g)
```

1. 将对象直接用`print`函数打印出来，查看内存地址。如果显示的是`iterator`,就是迭代器；如果是`generator`,就是生成器（主推荐）；
2. 查看是否可用`.send()`方法，如果可用，则是生成器，不可用则是迭代器。

yield的特点：

1. yield能返回多个数据类型，以元组的形式存储
2. yield能返回各种数据类型（python中的任意对象）
3. yield能够写入多个并且都可以执行
4. yield能够记录执行的位置
5. yield后面不写内容，默认返回None
6. yield都是将数据一次性返回

yield from的特点：

- 将可迭代对象逐个返回

可迭代对象，迭代器和生成器的比较：

- 可迭代对象：具有`.__iter__()`方法的就是可迭代对象

- 迭代器：具有`.__iter__()`和`.__next__()`方法的就是一个迭代器

- 生成器：基于函数创建的生成器，函数体中必须存在yield

  



   