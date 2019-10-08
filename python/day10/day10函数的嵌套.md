# day10函数的嵌套

## 今日内容概要

1. 函数的动态参数
2. 函数的注释
3. 函数的名称空间
4. 函数的嵌套 # 非常重要
5. global和nonlocal
6. 函数名的第一类对象及使用

## 昨日回顾

1. 函数初识

   - 封装代码
   - 减少重复

2. 函数的定义

   ```python
   def 函数名():
       函数体
   ```

3. 函数的调用

   ```python
   函数名()
   ```

   - 调用函数
   - 获取返回值

4. 函数的返回值

   - 函数执行完成后，函数体开辟的空间会被销毁
   - 函数体中存放的只是代码，只有当程序被调用时，函数体中代码才会被执行
   - return --返回
   - return会终止当前函数，return下方的代码不会被执行
   - 不写return默认返回None,写了return不写值也是返回Noen
   - return可以返回任意数据类型
   - return可以返回多个值，以元组的形式返回存储
   - return是将返回值返回给调用者
   - 可以写多个return，但是只执行要给return

5. 函数的参数

   - 形参：定义阶段的参数叫做形参
     - 位置参数：必须一一对应
     - 默认参数：可以不穿，可以传，传的时候会将默认值覆盖
     - 混合参数：位置参数 > 默认参数
   - 实参：调用阶段的参数叫做实参
     - 位置参数：必须一一对应
     - 关键字参数：指名道姓传参
     - 混合参数：位置参数 > 关键字参数
   - 传参：将实参传递给形参的过程就是传参

## 今日内容详细

### 函数的动态参数

我们已经学到了函数的两种参数：位置参数和默认参数。但是这两种参数而言，我们传入函数的数据不能多于参数的总个数。但是有些时候，参数的数量是不能很好控制的，这时候，我们就需要应用到动态参数

动态参数的作用主要有两个：

1. 能够接收不固定长度的参数
2. 位置参数过多时，可以应用动态参数

### 动态位置参数

我们可以通过下面的方法定义一个动态的位置参数：

```python
def func(*c):
    print(c)
    
func(1,2,3,4,5,6,7,8,9,0)

结果：
(1,2,3,4,5,6,7,8,9,0)
```

这个方法得到的数据类型是一个元组。

动态位置参数以`*形参`的形式表示。相信大家已经发现，这种方式跟切片十分类似。

事实上，同切片时将会多余数据打包的原理一样，子啊形参位置上的`*`就是聚合。同样，我们可以在函数体中使用`*`将聚合后得到的元组打散：

```python
def func(*c): # 形参位置上的*是聚合
    print(*c) # 函数体中的*就是打散
    
func(1,2,3,4,5,6,7,8,9,0)

结果：
1 2 3 4 5 6 7 8 9 0
```

因为动态位置参数会将多余的位置参数全部打包起来，所以一个函数中只需要一个动态位置参数就足够了。一帮情况下，动态位置参数会被命名为`*args`。当然也可以自定义参数名，但是不建议修改，因为这是程序员约定俗成的共识。

如果动态位置参数后面还有位置参数，那么后面的位置参数将会永远无法取到值，程序会直接报错：

```python
def eat(*args,a,b):
    print(a,b,args)
    
eat("面条","米饭","包子","馒头")

报错：TypeError: eat() missing 2 required keyword-only arguments: 'a' and 'b'
```

因为参数`a`和`b`永远也无法得到值，尽管我们输入很多内容，依旧无济于事。

一个比较标准的参数的参数设置方法是这样的：

```python
def eat(a, b, *args):
    print(a, b, args)
    
eat("面条","米饭","包子","馒头")

结果： 面条 米饭  ("包子","馒头")
```

位置参数一一对应获得参数，动态位置参数将剩余的参数打包起来成一个元组。

### 动态关键字参数（动态默认参数）

当我们在实际中传入的关键字在形参中存在时，会成功传递进入，可以如果形参中没有我们传入的实参，就会报错。

动态关键字参数就是用来接收这些没有被定义过的关键字参数。

我们可以在形参中使用`**参数名`的形式定义一个动态关键字参数。同样地，参数名可以随意选取，但是程序员约定成俗的动态关键字参数名为`**kwargs`：

```python
def func(a,b, *args, **keargs):
    print(a,b,args,kwargs)
    
func(1,2,3,4,5,6,7,8, c=100)

结果：1 2 (3, 4, 5, 6, 7, 8) {'c': 100}

```

前两个位置参数分别传入给了`a`和`b`，剩余的位置参数打包成元组传给了`args`，而关键字则以字典的形式传递给了`kwargs`。

当我们需要设置多种参数时，推荐使用：位置参数，动态位置参数，默认参数，动态关键字参数：

```python
def func(a, b, *args, m=8, **kwargs):
    # 位置参数， 动态位置参数 ， 默认参数， 动态关键字参数
    print(a, b, m, args, kwargs)


func(1, 2, 3, 4, 5, m=10, c=30, d=90)

结果：def func(a, b, *args, m=8, **kwargs):
    print(a, b, m, args, kwargs)


func(1, 2, 3, 4, 5, m=10, c=30, d=90)
```

### 函数参数总结

1. 优先级：位置参数 > 动态位置参数 (可变位置参数) > 默认参数 > 动态关键字参数（可变关键字参数）
2. `*args`和`**kwargs`是程序员之间约定成俗的命名法（可以更换但是不建议更换）
3.  `args`获取的是一个元组
4. `**kwargs`获取的是一个字典
5. `*args`只接收多余的位置参数
6. `**kwargs`只接受多余的关键字参数

## 函数参数补充#

### 万能传参

因为动态位置参数和动态关键字参数可以接收所有的位置参数和关键字参数，所以在设计形参时，我们甚至可以只设置`*args`和`**kwargs`两个形参，这种传参方式被称作万能传参：

```python
def func(*args, **kwargs):
    print(args, kwargs)


func(12, 3, 4, 5, 7, 8, a=3, b=55)

结果：(12, 3, 4, 5, 7, 8) {'a': 3, 'b': 55}
```

### 聚合和打散

在前面的动态位置参数部分已经讨论过，形参中的`*args`是将多于变量聚合为元组，函数体中的`*args`是将元组打散，其实对于`**kwargs`来说也很类似：形参中的`**kwargs`是将`key=3,key2=2`这样类型的语句转化为字典，而函数体中`*kwargs`是获取字典中所有的键，`**kwargs`是将字典打散为`key=3,key2=2`的语句。

除了函数中，我们可以在python的很多地方灵活运用打散和聚合的操作：

```python
lst = [1, 2, 3, 4, 5, 6, 7, 8]


def func(*args): # 聚合
    print(*args) # 打散


func(*lst) # 打散



dic = {"key": 1, "key2": 2}


def func(**kwargs): # 聚合
    print(kwargs) 


func(**dic) # 打散

结果：
1 2 3 4 5 6 7 8
{'key': 1, 'key2': 2}


```

### 函数的注释

在协同操作的过程中，大家或许会查看和使用彼此的代码。但是如果没有任何提示性内容的话，从头开始看起来会有很大的理解困难。如果我们将函数的一些功能，参数要求等信息在函数中写出来，别人阅读时就会节省很多时间，也容易理解调用和修改我们的函数。

标准的函数注释应该是这样的：

```python
def add(a,b):
    """
     数字的加法运算
    :param a: int
    :param b: int
    :return: int
    """
    return a + b

print(add(1,2))
```

函数中使用三对`"`，就是代表注释。也可以使用`'`表示，但是不推荐。

另外一种比较流行的注释方法是在形参后加入`:数据类型`,例如：

```python
def add(a: int, b: int):
    """
    加法
    :param a: 
    :param b: 
    :return: 
    """
    return a + b


add(1, 2)
add("1", "2")
```

需要注意的是，参数的作用只是起到提示的作用，并不会判断，约束我们传入变量的类型。

我们可以通过`函数名.__doc__`的方法查看函数的注释；通过`函数名.__name__`的方法查看函数的名字。

### 函数的名称空间

函数的名称空间一共有三种：

1. 内置空间，用来存放python自带的一些函数，python程序运行时会首先加载
2. 全局空间，当前py文件顶格编写的代码开辟的空间
3. 局部空间，函数开辟的空间

程序的加载顺序是：内置空间 > 全局空间 > 局部空间

程序的取值顺序是：局部空间 > 全局空间 > 内置空间

程序取值顺序提示：

```python
a = 10
def func():
    a = 5
    print(a)
func()

结果：5
```

变量取值时会优先查看局部空间，找到变量a，值为5，打印出来。

函数的作用域有两个：

1. 全局作用域：内置空间 + 全局空间，使用`globals()`方法查看全局作用域

2. 局部作用域：局部空间，使用`locals()`方法查看当前作用域（全局和局部作用域都可以查看。建议用此方法查看局部作用域）

   ```python
   a = 10
   def func():
       b = 5
       print(locals())
       
       
   print(globals())
   func()
   print(globals())
   print(locals())
   ```



## 函数名的第一类对象及使用

函数名的第一类对象只是一种称呼，是相对于第二类对象而言的。我们目前用到的函数基本都是第一类对象。

函数名的第一类对象主要有四个方面的应用：

1. 函数名可以当做值赋值给变量
2. 函数名可以当做另一个函数的参数的参数来使用
3. 函数名可以当做另一个函数的返回值
4. 函数名可以当做元素放在容器中

示例一：

```python
def func():
    print(1)
    
a = func
print(func)
print(a)
a()

结果：
<function func at 0x000002A57C85C268>
<function func at 0x000002A57C85C268>
1

```

`func`和`a`同样都是指向函数的内存地址，当我们调用`a`时，得到了同调用`func`相同的结果。

示例二：

```python
def func():
    print(1)
def foo(a):
    print(a)
foo(func)

结果：
<function func at 0x000001ED9EDFC268>
```

示例三：

```python
def func():
    return 1
def foo(a):
    return a
cc = foo(func)
print(cc)

结果：
<function func at 0x000002383C26C268>
```

示例四：

```python
def login():
    print("登录")
def register():
    print("注册")
def shopping():
    print("逛")
def add_shopping_car():
    print("加")
def buy_goods():
    print("买")
    
msg = """
1.注册
2.登录
3.逛
4.加
5.买
请输入你要选择的序号：
"""

while True:
    choose =input(msg)
    if choose.isdecimal():
        if choose == "1":
            register()
        elif choose == "2":
            login()
        elif choose == "3":
            shopping()
        elif choose == "4":
            add_shopping_car()
        elif choose == "5":
            buy_goods()
        else:
            print("拜拜")
```

通过将函数封装到字典里，我们可以大量减少重复的代码：

```python
def login():
    print("登录")


def register():
    print("注册")


def shopping():
    print("逛")


def add_shopping_car():
    print("加")


def buy_goods():
    print("买")


msg = """
1.注册
2.登录
3.逛
4.加
5.买
请输入你要选择的序号：
"""
func_dic = {"1": register,
            "2": login,
            "3": shopping,
            "4": add_shopping_car,
            "5": buy_goods
            }
while True:
    choose = input(msg)
    if choose in func_dic:
        func_dic[choose]()
    else:
        print("拜拜")

```

这种使用字典调用函数的方式是一种很重要的编程思想，以后经常用到。

## 函数的嵌套

函数的嵌套有两种方式：

1. 交叉嵌套
2. 回环嵌套

交叉嵌套的方式是在本函数中调用一级或上一级函数的嵌套方法：

```python
def func(foo):
    print(1)
    foo()
    print(3)
    
def a():
    print(1)
    
b = func(a)
print(b)

结果：
1
1
3
None

```

首先，程序会将python文件中顶格的代码运行。函数`func`和`a`都是先开辟内存空间存储起来，但不会被执行。当程序走到赋值操作时，会先执行等号右边的代码。函数`func`被调用，函数`a`作为参数被传到`func`中。`func`函数被执行，顺序也是从上往下，显示把`1`打印出来，然后调用参数`foo`。需要注意的是，`foo`是形参，实参是`a`调用`foo`在此时的意思是调用函数`a`。函数`a`被调用，又打印出一个`1`来函数`a`运行完毕，返回至函数`func`，继续执行下面的代码，打印出`3`来。最后，函数默认返回`None`,赋值给`b`。程序运行结束。

![1570521684060](C:\Users\99155\Desktop\新建文件夹\python\每天计划\图片\1570521684060.png)

再看下面的代码：

```python
def func():
    print(1)
    print("我太难了")
    print(2)


def foo(b):
    print(3)
    ss = b()
    print(ss)
    print(4)


def f(a, b):
    a(b)


f(foo, func)

结果：
3
1
我太难了
2
None
4


```

跟上面一样，先将函数全都加载到新开辟的内存空间中，但不执行。到最后f函数被调用，`foo`和`func`两个函数作为参数被传到函数`f`中。在函数`f`中，`foo`函数被调用，参数为`func`函数。进入到`foo`函数，先打印`3`。到赋值语句，先执行等号右边的代码，函数`func`被调用。在函数`func`中，打印三个内容`1`、`我太难了`和`2`。函数默认返回值为`None`，被赋值给`ss`。打印`ss`就是打印`None`。最后打印`4`，然后返回到函数`f`，再返回到全局空间。执行结束。

![1570523185384](C:\Users\99155\Desktop\新建文件夹\python\每天计划\图片\1570523185384.png)

回环函数就是在函数中调用下级函数的嵌套方法：

```python
def func(a,b):
    def foo(b,a):
        print(b,a)
    return foo(a,b) # 先执行函数调用
a = func(4,7)
print(a)

结果：
4 7 
None
```

函数依然先存储在新开辟的空间中不会被调用。运行到赋值语句时，还是先执行等号右边的代码，将两个数字传到函数`func`中。在函数内部，依然是先开辟空间把函数`foo`放进去。运行到`return`不会马上终止函数，而是先运行`return`后面的代码。`foo`函数被调用，传进去的值是`4`和`7`，然后打印出来。需要注意的是，函数`foo`的形参与函数`func`的形参是相同的，不要给搞混了。日常写代码时不建议这样使用。打印出`4`和`7`之后，运行到函数最后一行，函数默认返回`None`。然后再赋值给`a`，打印出来。

![1570523865826](C:\Users\99155\Desktop\新建文件夹\python\每天计划\图片\1570523865826.png)

## `global`和`nonlocal`

`global`方法

我们来看下这段代码：

```python
b = 100
def func():
    b = b + 1
    return b
print(func())
    
结果：
UnboundLocalError: local variable 'b' referenced before assignment
```

这段代码看上去中规中矩，似乎没有什么问题，但是程序运行后的确报错。

这是因为在python中，不允许直接在局部空间修改全局变量。`b = b + 1`是一个冲突的语句：等式右边的`b`是要调用一个全局变量，而等号左边变却是要定义一个局部变量。

![1570524456138](C:\Users\99155\Desktop\新建文件夹\python\每天计划\图片\1570524456138.png)

如果将`b`视作一个全局变量依然不合适，在函数中修改全局变量会对其他调用相同变量的函数造成影响，除非万不得已或者十分确定的情况下，不建议在函数中修改全局变量。

当我们确定需要在函数中修改全局变量时，可以通过`global`方法来实现：

```python
b = 100
def func():
    global b
    b = b + 1
    return b
print(func())
结果：
101
```

如果`global`声明的变量在全局空间中不存在，将会在全局空间中新建一个变量：

```python
def func():
global a
a = 10
a = a + 12
print(a)

func()
print(a)

结果：
22
22
```

`nonlocal`方法

对于回环嵌套的函数来说，也会有类似的问题，当尝试使用内层函数修改外层函数的变量时会报错：

```python
a = 15
def func():
    a = 10
    def foo():
        a = a + 1
    foo()
    print(a)
func()
print(a)

报错：UnboundLocalError: local variable 'a' referenced before assignment
```

类似地，也不建议在内层函数中修改外层函数的变量。如果一定要修改的话，可以使用`nonlacl`方法：

````python
a = 15
def func():
    a = 10
    def foo():
        nonlocal a
        a = a + 1
    foo()
    print(a)
    
func()
print(a)

结果：
11
15

````

`nonlocal`方法只修改离它最近的一层函数的变量，如果这一层没有就往上一层查找，只能在局部查找。另外，外层函数不能调用内层函数的变量，即便用`nonlocal`方法也不行。如果外层所有函数中都没有声明的变量，即便全局空间中有也不行，而且`nonlocal`不能创建变量。如果找不到，就会报错：

```python
a = 15
def func():
    def foo():
        nonlocal a
        a = a + 1
    foo()
func()
print(a)

报错：
SyntaxError: no binding for nonlocal 'a' found
```

其实想来这个设定也是合理的：如果外面套了很多层函数，这个变量该在哪一层创建呢？

## `global`和`nonlocal`方法总结

`global`只修改全局空间中的变量

- 在局部空间中可以使用全局中变量，但是不能修改，如果要强制修改，需要使用`global`声明
- 当变量在全局存在时，`global`就是声明我要修改全局的变量
- 当变量在全局中不存在时，`global`则是声明要在全局创建一个变量

`nonlocal`只修改局部空间中的变量，最多只能到达最外层函数

- 在内层函数中可以使用外层函数中的变量，但是不能修改，如果强制修改，需要使用`nonlocal`声明
- 只修改离`nonlocal`最近的一层，如果这层没有就往上层查找，不能找到全局中
- `nonlocal`不能创建变量，如果其声明的变量在外层函数中找不到，即便全局空间中有，也会报错

对函数的传参有一点补充，传参的时候相当于在当前函数体中进行了赋值操作：

```python
def func(a):
    # 相当于在func函数体中写了这么一个 a = 100操作
    print(locals())
func(100)
```

最后一道思考题，请确定下面函数输出的结果：

```python
a = 10
def func():
    a = 5
    def foo():
        a = 3
        def f():
            nonlocal a
            a = a + 1
            def aa():
                a = 1
                def b():
                    global a
                    a = a + 1
                    print(a)
                b()
                print(a)
            aa()
            print(a)
        f()
        print(a)
    foo()
    print(a)
func()
print(a)
```

