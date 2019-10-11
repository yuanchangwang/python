# day12 python中的内置函数

## 今天内容概要

1. 推导式
2. 内置函数

## 上周内容回顾

1. 迭代器
   - 可迭代对象：具有`__iter__()`方法的就是一个可迭代对象
   - 迭代器:具有`__iter__()`和`__next__()`方法
   - 迭代器就是用时间换空间
   - 可迭代对象是用空间换时间
2. 生成器
   - 生成器也是一个迭代器，迭代器不一定是一个生成器
   - 迭代器和生成器最大的区别:
     - 迭代器是python提供的
     - 生成器是程序员自己写的
   - 迭代器和生成器进行区别：
     - 看内存地址
     - 生成器有`send()`方法，迭代器没有
   - next要与yield一一对应
   - yield与return比较
     - yield可以有多个，并且都可以被执行
     - yield也能返回任意数据类型
     - yield也能够返回多个数据，以元组形式接收
     - yield不写值也是默认返回None
     - yield能够记录执行位置
     - yield能够暂停生成器的运行但是不会终止其运行
   - yield from 将数据元素逐个返回
   - 生成器和迭代器优点
     - 节省空间
   - 生成器和迭代器的缺点：
     - 不能直接使用元素
     - 不能直接查看元素个数
     - 时间消耗大
     - 一次性，单向不可逆
     - 使用不灵活

## 今天内容详细

### 推导式

#### 列表推导式

推导式用来创建一些有规律的可变数据结构，能够让代码变得更加简洁。

比如，我们想要通过循环的方法创建一个数字从1到50的列表，可以这样做：

```python
lst = []
for i in range(1,51):
    lst.append(i)
print(lst)
```

如果使用列表推导式，我们只需要一行代码：

```python
print([i for i in range(1, 51)])
```

我们就成功创建了一个列表推导式。我们还可以运用字符串的格式化实现更多样化的输出：

```python
print([f'python学习第{i}天' for i in range(1,51)])
```

前面两种是列表推导式的普通循环模式，它的基本结构为：

```python
[加工后的变量 for循环]
```

除了普通循环模式，我们还可以通过给循增加筛选模式的列表推导式：

```python
print([i for i in range(1,51) if i > 25])
```

筛选模式的列表推导式的基本结构为：

```python
[加工后的变量 for循环 加工条件]
```

列表推导式还支持嵌套。

对于这样一个嵌套的循环：

```python
lst = []
for i in range(2):
    for j in range(2):
        lst,append(i+j)
print(lst)
```

改成列表推导式结构就成了这样

```python
print([i+j for i in range(2) for j in range(2)])
```

虽然列表推导式能节省很多代码，但是最多建议嵌套三层。

生成器可以让代码更加简化。比如，我们想求字符串`yuan,meet`中每个字母`e`的索引。如果用for循环来写是可以实现的，但是需要多行代码：

```python
s = "yuan,meet"
count = 0
lst =[]
for i in s:
    if i == "e":
        lst.append(count)
     count += 1
print(lst)
```

而如果使用列表生成器话，只需要一行代码实现：

```python
print([i for i in range(len(s))] if s[i] == 'e')
```

字典推导式和集合推导式

除了列表之外，其他可变数据类型，比如字典和集合也可以通过推导式的方式来创建：

```python
# 字典推导式
print({i:i+1 for i in range(3)})
print({f'python{i}': i+1 for i in range(3)})
print({i: i+1 for i in range(3) if i > 1})

# 集合推导式
print({i for i in range(3)})
print({i for i in range(3) if i < 2})
```

#### 生成器表达式（推导式）

我们前几天学到生成器，除了可以通过函数的方式实现，还可以使用表达式来实现，与列表表达式相似，生成器表达式也有普通模式和筛选模式：

```python
#普通模式
g = (i for i in range(4))

#筛选模式
g = (i for i in range(3) if i + 1 == 2)
```

生成器推导式的三个：简化代码，提高逼格和提高可读性。

同列表表达式一样，生成器推导式用于生成一些有规律的数据，当我们生成数据较大时，建议使用生成器推导式。

### 内置函数一

#### `all`函数

`all`函数用来判断可迭代对象中是否所有的元素都为True：

```python
print(all([1,2,3,44,5,55]))

结果：True
```

#### `any`函数

`any`函数与用来判断可迭代对象中的元素是否有一个True：

```python
def func():
    pass
print(callable(func))
```

#### `bytes`函数

`bytes`函数可以将字符串编码为二进制形式，它的功能和字符串的`.encode()`方法十分相似，更加推荐使用`.encode()`方法：

```python
print('你好'.encode('utf-8'))
print(bytes('你好',encoding='utf-8'))

结果：
b'\xe4\xbd\xa0\xe5\xa5\xbd'
b'\xe4\xbd\xa0\xe5\xa5\xbd'

```

#### `chr`和`ord`函数

`chr`函数根据当前编码（python3中为Unicode）解码为字符，ord为chr方法的逆运算，用来将字符编码为数字：

```python
print(chr(20320))
print(ord("你"))

结果：
你
20320

```

#### `comlpex`和`divmod`函数

这两个函数用来计算。complrx函数用来将一堆数字转换为复数形式，第一个数作为复数的实部，第二个数为复数的虚部：

```python
print(complex(20, 3))
```

divmode函数会将一对数字做商，第一数字做被除数，第二个数字除数，返回值为一个元组，元组的第一个元素是商，第二元素是余数：

```python
print(divmod(20,3))
```

#### `eval`和`exec`函数

这两个函数用来将字符串中的代码转换成可执行的状态。其中，eval函数可以转换一行代码，exec函数可以转换多行代码：

```python
msg = 'print(1)'
eval(msg)

msg2 = """
def func():
	print('你太厉害了'）
func()
"""
exec(msg2)
```

但是这两个函数在日后的编程中是被禁止使用的，因为有可能会出现被恶意注入的bug。

#### frozenset函数

frozenset可以生成一个冻结的不可变的集合：

```python
dic = {frozenset({1,2,3,4,5}): 1}
print(dic)
```

既然能做字典的键，就说明冻结集合是一个不可变数据。

#### hash函数

hash函数用来判断一个数据是否可哈希。如果可哈希，会返回该数据的哈希值；如果不可哈希，会报错：

```python
print(hash('12'))
print(hash(12))
print(hash(True))
print(hash(False))
print(hash([1,2]))
print(hash(1,2))
print(hash({1:2}))
print(hash{1,2})
```

#### help函数

help函数可以查看帮助信息：

```python
help(list) # 使用help函数不需要打印
```

#### 进制转换函数

bin、oct和hex三个函数分别能够将十进制数转换为二进制。八进制，十六进制；int方法则能将各种进制数转换为十进制数：

```python
print(bin(10))
print(oct(10))
print(hex(30))
print(int('0xle',16))
print(int('le',16))
print(int('0o11', 8))
print(int('ob11', 2))
```

#### pow函数

pow函数用来进行幂运算，返回的结果是前一个数的最后一个数次幂：

```python
print(pow(3,4))
```

#### repr函数

repr函数用来显示打印出来的字符串两端的双引号，即令字符串原形毕露：

```python
print('123')
print(repr("123"))
```

#### round函数

round函数用来将小数取整，取整规则是四舍五入成双，也可以指定保留的小数位数：

```python
print(round(3.4))
print(round(3.5))
print(round(3.6))
print(round(4.3))
print(round(3.1414926, 3))
```

#### abs函数

abs函数用来求数字的绝对值：

```python
print(abs(-9))
```

format函数

format函数用来格式化字符串，与字符串的.center()方法类似：

```python
s = '你好'
s1 = format(s,'>20')
s2 = format(s, '<20')
s3 = format(s,'^20')
print(s1,s2,s3,sep ="\n")
```

format也可以用来进行数字的进制转换：

```python
s = 18
print(format(s, '08b'))
print(format(s,'08o'))
print(format(s,'08x'))
print(format(s,'08d'))
```

format方法对于转换ip地址会很好用。

#### sum方法

sum方法用来求一个可迭代对象中元素的总和：

```python
print(sum[1,2,3,4])
```

#### dir方法

dir方法用来查看当前对象有哪些方法

```python
print(dir(list))
```

### 内置函数二

这一部分主要是一些python中内置函数的高阶函数，所谓的高阶函数，就是函数为参数的函数。

#### 匿名函数

匿名函数的关键字是lambda。匿名函数在高阶函数中应用十分广泛，它能极大地简化代码。

比如这个经典的函数定义和调用的代码：

```python
def func(a,b):
    c = a +b
    return c
print(func(1,2))
```

如果使用匿名函数，只需要两行代码即可：

```python
f = lambda a, b: a + b
print(f(1,2))
```

甚至一行代码就能实现：

```python
print((lambda a, b: a + b)(1, 2))
```

在上面代码中：

- lambda和def的作用类似，用来声明要定义一个函数
- a， b和（a，b）的表达含义类似，用来声明形参
- ：a+ b和return a+b的含义类似，用来声明返回值

在匿名函数中的形参可以接受位置参数，动态位置参数，默认参数，动态关键字参数，也可以什么都不写。

匿名函数的冒号`:`后面接的是函数的返回值，只能返回一个数据，而且是必须写的。

当for循环和匿名函数一起使用时，会有一个坑；如果是循环后调用，for循环的变量会使用最后一个，而不是期间每一个元素值：

```python
lst = []
for i in range(3):
    lst.append(lambda: i)
    
for j in lst:
    print(j())
```

当第一个循环结束时，列表中存储的值为三个匿名函数的内存地址。每个匿名函数实际上只有一个内容：返回i。但是在调用之前，这一行代码并不会执行，函数中记录的还是一个i。当循环结束，我们调用这些函数时，i已经变成2。虽然前面两个函数被加入到列表中时i的值还是1和2，但它们没有被记录在函数中。

我们可以把上面的代码拆分开，这样看起来会直观些：

```python
lst = []
for i in range(3):
    def func():
        return i
    lst.append(func)
 for j in lst:
    print(j())
```

如果将匿名函数和for循环封装在列表推导式中，会更有迷惑性：

```python
g = [lambda : i + 1 for i in range(3)]
print([em() for en in g:])
```

对于生成器表达式，情况又发生了变化--因为当函数被拿出来之后，循环才会向下走：

```python
g = (lambda :i + 1 for i in range(3))
print([em() for em in g])
```

#### filter函数

lilter函数用来过滤不符合条件的元素。filter函数有两个参数，第一个参数为规则函数，第二参数为可迭代对象：

```python
lst = [1,2,3,4,5,6,7]
def foo(x):
    return x > 4
print(filter(foo,lst))
print(list(filter(foo,lst)))
```

filter的返回值为filter对象，可迭代，可以通过list函数转化为列表。

我们可以通过for 循环模拟内置函数filter：

```python
def filter(func, iter):
    lst = []
    for i in iter:
        if func(i):
            lst.append(i)
    return lst
```

也可以使用匿名函数作为规则函数，这样可以让代码看起来非常简洁：

```python
lst = [{"id": 1,'name': "yuan",'age: 18},
      {'id': 2,'name':'chang','age';19},]

print(list(filter(lambda x:x['age'] > 18,lst)))
        
```

#### map函数

map函数也称作为映射函数，用来将可迭代对象中每一个元素执行函数功能：

```python
lst = [1,2,3,4,5,56,5]
print(map(str,lst))
print(list(map(str,lst)))
```

map函数返回的是map对象，也可以使用list函数转换为列表。

map函数可以使用更多参数的规则函数来整合多个迭代对象：

```python
lst1 = [1,2,3]
lst2 = [3,2,1]
lst3 = [3,2,1,5]
print(list(map(lambda x,y,z: x+y+z,lst1,lst2,lst3)))
```

如果可迭代对象长度不同，map函数的迭代次数以最短的可迭代对象为准。

#### sorted函数

sorted函数用来将可迭代对象排序：

```python
print(sorted('yuan,chang'))
print(sorted(('yaun,chang'),reverse = True))

dic = {1:'a',3:'c',2:'d'}
print(sorted(dic))
```

不管输入的可迭代对象是什么样的数据类型，sorted函数的返回值都是一个列表。

sort函数也可以使用规则函数，只是这些规则函数要通过使用关键字参数的方式引入：

```python
lst = ['天龙八部','西游记','红楼梦','三国演义']
print(sorted(lst,key=len))
print(sorted(lst,key=lambda x:len(x)))

lst = [{'id':1,'name':'yuan','age':18},
      {'id':2,'name':'chang','age':35}]

print(sorted(lst,key=lambda x:x['age'],reverse=True))
```

列表的.sort()方法是在列表所在的原地进行修改，而sorted函数则是新建一个列表：

```python
lst = [1,2,3,4,5,6,7,-9]
print(sorted(lst))
print(lst)

lst1 = [1,3,4,5,6,7,-5]
print(lst1.sort())
print(lst1)
```

#### nax和min函数

max和min函数用来选取可迭代对象中的最大或最小值，可以指定规则函数进行更复杂的选择：

```python
lst = [1,2,3,4,5,6,7,-3,5,-33]
print(max(lst))
print(min(lst,key=abs))
print(max(lst,key=lambda x:pow(x,4)-pow(x,2)+x))
```

也可以通过这两个函数找到最大的值或者最小的值对应的键：

```python
dic = {'a':3,'b':2,'c':1}
print(max(dic.values()))
print(min(dic,key=lambda x: dic[x]))
```

reduce函数

reduce函数用来进行累运算。规则函数中会有两个参数，第一参数用来存储上一次运算的结果，第二个参数传入下一个值，返回值为 运算操作。

需要注意的是，在python2中，reduce可以直接使用，而在python3中，需要在functools里面导入reduce函数：

```python
from functools import reduce
```

我们可以通过reduce函数实现累乘运算：

```python
from functools import reduce
def func(x,y):
    return x * y
print(reduce(func,range(1,6)))
```

将函数用匿名函数整合会让代码更加简洁：

```python
from functools import reduce
print(redue(lambda x,y: x*y, range(1,6)))
```

#### print()函数

print函数我们已经非常熟悉了，用来将内容打印出来。我们还需要了解的是print有两个关键字参数：sep和end。

sep用来规定print中多个元素以什么间隔开，默认值为一个空格` ' '`;end用来规定函数打印完全后以什么为结尾，默认为换行符`\n`

我们可以通过修改sep和end的值来实现不同的打印输出的效果：

```python
print('yuan','chang','dsb',sep='-',end=' ')
print('meet')
```

我们可以利用print的这两个参数实现打印九九乘法表：

```python
for i in range(1,10):
    for j in range(1,i+1):
        print(f'{i} * {j} = {i * j}',end=" ")
    print()
```

除了能够将信息打印到屏幕上，print也能将信息写入到文件中：

```python
f = open('test', 'a', encoding='utf-8')
print('meet',file=f)
```

#### zip函数

zip是拉链的意思，用来将两个可迭代对象以关联起来，以返回值zip对象，可以转换为列表，列表中的每一个元素为原来的可迭代对象中元素的元组：

```python
lst1 = [1,2,3,4,5]
lst2 = [5,4,3,2,1]
print(zip(lst1,lst2))
print(list(zip(lst1,lst2)))
```

使用map函数也是可以实现类似的功能：

```python
lst1 = [1,2,3,4,5]
lst2 = [5,4,3,2,1]
print(list(map(lambda x, y: (x, y),lst1,lst2)))
```

这种数据类型可以直接使用字典的工厂函数dict转换为字典：

```python
lst1 = [1,2,3,4,5]
lst2 = [5,4,3,2,1]
print(dict(zip(lst1,lst2)))
```

#### 高阶内置函数比较

|          函数名           |  规则函数位置   | 规则函数形参数目 |       返回值数据类型        |
| :-----------------------: | :-------------: | :--------------: | :-------------------------: |
|   [filter](#filter函数)   |      首位       |       1个        |  filter对象，可转换为列表   |
|      [map](#map函数)      |      首位       |    1个或多个     |    map对象，可转换为列表    |
|   [reduce](#reduce函数)   |      首位       |       2个        |     可迭代对象中的元素      |
| [max和min](#max和min函数) | 末尾，用key指明 |       1个        |     可迭代对象中的元素      |
|   [sorted](#sorted函数)   | 末尾，用key指明 |       1个        |            列表             |
|      [zip](#zip函数)      |       无        |        无        | zip对象，可转换为列表或字典 |






