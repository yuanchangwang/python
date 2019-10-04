# day 04 列表和元组

## 今日内容概要

1. 列表
2. 元组
3. range

## 昨日内容回顾

1. 整型

   - python 2 中由int和long；python 3中只有int
   - 进制转换

2. 字符串的索引

3. 切片和步长

   - 变量名[起始位置：终止位置：步长默认为1] 顾头不顾尾
   - 通过修改步长可以控制查找的步数和查找的方向
   - 索引超出最大值时会报错
   - 切片超出最大值不会报错

4. 字符串方法

5. for 循环

   - `for`: 关键字

   - `i`: 变量名

   - `in`: 关键字

   - 可迭代对象

   - for循环打印九九乘法biao

     ```python
     for i in range(1, 10):
         for j in range(1, i+1):
             print(f"{j} * {i} = {i*j}", end = "")
         print()
     ```

     



## 今日内容详细

#### 列表

##### 列表的定义

同`整型`，`字符串`和`布尔值`一样，`列表`也是python中数据结构之一。`列表`的关键字是`list`。在python中，最常用的三种用来存储数据的数据分别是`字典`，`列表`和`字符串`，可见它是十分重要的。

列表的作用更像是一种容器，形象一点点就是我们用的书包：

1. 列表能存储大量的数据
2. 列表能存储不同数据类型的数据

与列表相对照，我们先来观察一下这样一个字符串：`a = 1234yuanTrue`这个字符串中包含数字、字母和布尔值，但是表现出来的全是字符串。我们虽然能够通过索引取到内容，但取到的值仍然是字符串。这就需要我们进行额外的判断转换操作。列表则不同，列表可以存储不同数据类型，并且可以随时把它们直接取出来用。就像把东西装书包里，用的时候取出来即可。

我们可以通过如下方法定义一个列表：

```python
lst = [1, "yuan", True]
```

列表中的每一个元素以逗号分割。各个元素以原来的数据类型存储在列表中。

##### 列表元素的增加

列表元素的增加主要有三种方法：`.append()` `.insert(`) 和`.extend()`。

`.append()` 方法实在列表的末尾添加内容。`.append()`的参数就是需要增加的列表元素：

```python
lst = ["python学习手册"， "核心编程"]
print(lst.append("流畅的python"))
print(lst)

结果：
None
['Python学习手册', '核心编程', '流畅的Python']
```

`None`在python中是空的意思。`,append()`返回值为`None`。而当我们打印列表`lst`时发现，列表已经被改变。这里我们可以得出结论：

- 列表是可变数据类型
- `.append()`操作会直接对列表进行修改而不需要重新赋值

`insert()`方法用来向列表插入数据。`.insert()`方法有两个参数，`参数1`是要插入位置的`索引值`，`参数2`是要插入的`内容`：

```python
lst = ["python学习手册"， "核心编程"]
lst.insert(1, "流畅的python")
print(lst)

结果：
['Python学习手册', '流畅的Python', '核心编程']
```

实际操作中，不推荐使用`insert()`方法。因为一旦使用这个方法，需要把插入后的每一个元素都后移一位，且发生索引值的变化，有可能给现目带来不可预测的影响。

`.extend()`方法也是在列表的最后插入内容。`.extend()`方法的参数必须是可迭代带对象。执行`.extend()`方法时，会将参数内容`迭代追加`到列表结尾

```python
lst = ["python学习手册"， "核心编程"]
lst.extend("流畅的python")
结果：
['Python学习手册', '核心编程', '流', '畅', '的', 'P', 'y', 't', 'h', 'o', 'n']
```

##### 列表元素的删除

列表元素的删除主要有四种方法：`.remove()` , `.pop()` `.clear()`和 `del`

`.remove()`方法可以删除指定元素名的列表元素，它的参数是要删除的元素名：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
lst.remvoe("新力")
print(lst)

结果：
['大圣', '海芋', '一帆', '靓仔', '石淦']
```

`.pop()`方法如果不加参数的话，默认删除列表中最后一个元素，并且有返回值，返回的内容是被删除的元素。`.pop()`是唯一一个有返回值的列表元素删除方法：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
print(lst.pop())
print(lst)

结果：
石淦
['大圣', '海芋', '新力', '一帆', '靓仔']
```

`.pop()`方法也可以通过输入索引参数的方法，删除指定位置的列表元素：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
print(lst.pop(1))
print(lst)

结果：
海芋
['大圣', '新力', '一帆', '靓仔', '石淦']

```

`.clear()`方法用来将列表清空，最终会得到一个空列表：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
lst.clear()
print(lst)

结果：
[]
```

`del`是用来删除的关键字。`del`后面直接跟着列表名，会将列表整个删除掉：

```python
>>> lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
>>> del lst
>>> print(lst)

报错：
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'lst' is not defined

```

程序报错，因为`lst`已经被从内存中整个移除。后来`print`调用`lst`时。找不到相应内容，所以报错。

也可以用del删除指定索引的列表元素：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
del lst[2]
print(lst)

结果：
 ['大圣', '海芋', '一帆', '靓仔', '石淦']
```

##### 列表元素的修改

列表元素可以通过索引赋值直接修改：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
lst[2] = "秀色可餐"
print(lst)

结果：
['大圣', '海芋', '秀色可餐', '一帆', '靓仔', '石淦']
```

也可以通过列表的切片方法对列表元素进行批量修改：

```python
lst = ['大圣', '海芋', '新力', '一帆', '靓仔', '石淦']
lst[1:4] = 10, 20, 30
print(lst)

结果：
['大圣', 10， 20，30， '靓仔', '石淦']
```

切片获取的内容空间是连续的时候，修改时内容可以多可以少；切片获取的内容空间是不连续的时候，修改时内容必须一一对应：

```
lst = ["大圣","海煜","新力","一帆","靓仔","石淦"]
lst[1:4] = 10, 20, 30, 40 #切片空间连续，可多
print(lst)
lst = ["大圣","海煜","新力","一帆","靓仔","石淦"]
lst[1:4] = 10, 20 #切片空间连续，可少
print(lst)
lst = ["大圣","海煜","新力","一帆","靓仔","石淦"]
lst[1:5:2] = ['alex', 'wusir'] # 切片空间不连续，必须一一对应
print(lst)

输出的结果为：
['大圣', 10, 20, 30, 40, '靓仔', '石淦']
['大圣', 10, 20, '靓仔', '石淦']
['大圣', 'alex', '新力', 'wusir', '靓仔', '石淦']
```

##### 列表元素的查看

裂变元素可以通过索引查询和for循环遍历两种方法查看：

```python
lst = ["大圣","海煜","新力","一帆","靓仔","石淦"]
print(lst[3])
for i in lst:
    print(i)
```

需要注意的是，进行切片操作时，获取的内容时切片的原数据本身。也就是说，切片不会改变数据类型。字符串切片后得到的还是字符串，列表切片后得到还是列表：

```python
lst = ["大圣","海煜","新力","一帆","靓仔","石淦"]
print(lst[1: 4])

a = "yuan"
print(a[1:3])

结果：
["海煜","新力","一帆"]
ua
```

##### 列表总结

- 列表是可变数据类型，可迭代数据类型，有序的数据结构
- 列表用来存储大量数据，并且可以存储不同数据类型
- 列表就是一个容器
- 列表存储的是元素的内容地址



##### 列表的嵌套

因为列表可以存储各种数据类型的数据，那么列表当然也可以存储列表，这就造成了列表的嵌套。

现在有这样一个相互嵌套的列表：

```python
lst = [1,"yuan",True,["chang","污",["嫂子","衣服多"]], ["yuan","吹nb","熬鸡汤",["嫂子","教育","从基层做起"]]]
```

这样，`lst3`就是我们想要的`"衣服多"`字符串。

但是这样的操作实在太过繁琐。我们发现，`lst1 = lst[3]`，既然如此，第二个式子我们可不可以把`lst1[2]`替换成`lst[3][2]`呢？那进一步说，我们可不可以直接通过`lst[3][2][1]`来调出`"衣服多"`字符串呢？

答案是完全可以的：

```python
lst = [1,"yuan",True,["chang","污",["嫂子","衣服多"]], ["yuan","吹nb","熬鸡汤",["嫂子","教育","从基层做起"]]]

print(lst[3][2][1])
print(lst[4][3][1])

结果：
衣服多
教育
```

像这样调用嵌套在内层列表元素的方法也被称作`降维`，就是将类似于`["chang","污",["嫂子","衣服多"]`的结构当作一个元素查看。



#### 元组

元组也是python中的数据类型之一。元组的关键字是`tuple`.

元组的定义方法和列表极其相似，只是将`中括号`变成了`小括号`。很多时候，小括号可以省略：

```python
tu = (1, 2, 3, "yuan")
tu1 = 1, 2, 3, "yuan"
```

元组就是一个不可变的列表，因为不可变，元组没有增删改的方法，只能进行查看。

元组也可以通过索引方式进行查找，也同样支持切片操作：

```python
tu1 = 1, 2, 3, "yuan"
print(tu1[0])
print(tu1[1:3])

结果：
1
(2, 3)
```

注意元组切片后得到还是元组数据。

元组同样可以通过for循环的方法来查看：

```python
tu1 = 1, 2, 3, "yuan"
for i in tu1:
    print(i)
```

元组的`.count()`方法可以用来统计指定元素在元组中出现的次数；`.index()`方法可以通过元素的名称获取元素的索引：

```python
tu1 = 1, 2, 3, "yuan"
print(tu1.count(3))
print(tu1.index(3))

结果：
1
2

```

需要注意是，并不是出现小括号表示该数据类型是元组。当小括号中没有出现逗号时，数据类型就是括号中数据类型本身：

```python
a = (10)
print(type(a))
b = ("yuan",)
print(type(b))

输出的结果为：
<class 'int'>
<class 'str'>
```

当小括号中没有数据时，代表的是空元组：

```python
c = ()
print(c)
print(type(c))

结果：
()
<class 'tuple'>
```

元组的应用场景有：

1. 为了防止误操作时修改数据，元组用来存储一些重要数据
2. 配置文件中用来存储数据



#### range

在python中，通过range可以达到循环数字的效果：

```python
for i in range(1, 5):
    print(i)
    
结果：
1
2
3
4
```

对于下面一行代码：

```python
a = range(5)
print(a)
```

在python2中，会打印列表[0,1,2,3,4];在python3中则会被打印为range(5).可以通过list()函数将range对象转换为列表：

```python
a = range(5)
print(list(a))

结果：
[0,1,2,3,4]
```

`range`中的参数和`切片`极其相似，range的索引是几，其对应的值就是几：

```
for i in range(0, 51, 2):
    print(i)	# 打印0-50间的所有偶数
for i in range(1, 51, 2):
    print(i)	# 打印0-50间的所有奇数
```

`range`与`切片`所不同的是，`range`的终止位置为负数时，表示的是负数位置，而不是从右向左数的位置：

```
for i in range(10, -11, -1):
    print(i)	# 打印10到-10的数字
```

一般情况下，我们可以直接写入一个终止位置。这时，起始位置默认为`0`，步长默认为`1`：

```
print(list(range(5)))

输出结果为：[0, 1, 2, 3, 4]
```

需要注意，如果要设置步长，一定要把变量写全，要包含起始位置。

很显然，`range`是一个可迭代对象。

## Python列表函数&方法

Python包含以下函数:

| 序号 | 函数                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [len(list)](https://www.runoob.com/python3/python3-att-list-len.html) 列表元素个数 |
| 2    | [max(list)](https://www.runoob.com/python3/python3-att-list-max.html) 返回列表元素最大值 |
| 3    | [min(list)](https://www.runoob.com/python3/python3-att-list-min.html) 返回列表元素最小值 |
| 4    | [list(seq)](https://www.runoob.com/python3/python3-att-list-list.html) 将元组转换为列表 |

Python包含以下方法:

| 序号 | 方法                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| 2    | [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| 3    | [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| 4    | [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| 5    | [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| 6    | [list.pop([index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| 7    | [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| 8    | [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| 9    | [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| 10   | [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| 11   | [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) 复制列表 |

## 元组内置函数

Python元组包含了以下内置函数

| 序号 | 方法及描述                        | 实例                                                         |
| :--- | :-------------------------------- | :----------------------------------------------------------- |
| 1    | len(tuple) 计算元组元素个数。     | `>>> tuple1 = ('Google', 'Runoob', 'Taobao') >>> len(tuple1) 3 >>>  ` |
| 2    | max(tuple) 返回元组中元素最大值。 | `>>> tuple2 = ('5', '4', '8') >>> max(tuple2) '8' >>>  `     |
| 3    | min(tuple) 返回元组中元素最小值。 | `>>> tuple2 = ('5', '4', '8') >>> min(tuple2) '4' >>>  `     |
| 4    | tuple(seq) 将列表转换为元组。     | `>>> list1= ['Google', 'Taobao', 'Runoob', 'Baidu'] >>> tuple1=tuple(list1) >>> tuple1 ('Google', 'Taobao', 'Runoob', 'Baidu')` |