# day05 字典

## 今天内容概要

1. 字典--非常重要
2. 解构
3. 字典的嵌套

## 昨日内容回顾

1. 列表
   1. 列表用来存储大量数据，关键字是list
   2. 列表是可变的，有序的（可用索引查找点位），可迭代的
      - 列表的增加（append ， insert ， extend）
      - 列表的删除 （remove ， pop ， clear ，del）
      - 列表的修改 （lst[索引] =值，可切片）
      - 列表的查找 （索引，for循环）
2. 元组
   1. 元组是一种不可变的列表，关键字是tuple
   2. 元组有序，不可变，可迭代
3. range
   1. 用于循环数字，可迭代
   2. python2中返回列表，python2中返回range本身
   3. range（起始位置：终止位置：步长）顾头不顾腚
   4. range（终止位置）

## 今日内容详细

### 字典

我们来看下面的一个例子：

```python
name_lst = ["新力", "一帆", "海绵", "秀"]
id_lst = [18, 9, 25, 50]
```

其中，列表`name_lst`中存储的是同学的名字，`id_lst`中存储的是对应同学的学号。例如，`新力`的学号是`18`。

如果我们要查找新力的学号，就要去另一个列表中找到其索引对应的学号值，例如：

```
name_lst[0]
id_lst[0]
```

这样的操作虽然也能满足我们的需求，但是显然有些繁琐。而且一旦任何一个列表中的索引发生了变化（比如进行了插入或者删除数据的操作），就要对另一个列表进行同样的改动，否则会造成混乱。

如果我们使用字典来进行这一类操作，就可以避免这样的麻烦。

字典也是Python中的基本数据类型之一。字典是唯一一种使用{}，包含键值对的数据类型。字典是一种键值对数据。

字典在Python中的关键字是`dict`

字典用来存储大量数据，数据量比列表存储的还要大。

字典能够将数据和数据之间进行关联。

字典的定义方法是这个样子的：`dic = {'键': '值'}`，具体的例子就是：

```python
dic = {"新力": ["开车", "唱", "跳"], "一帆": 9, 25: "海绵", True: "秀", (1, 2, 3): "大圣"}
```

通过键可以准确地找到其对应的 值：

```python
print(dic["新力"])
```

在这里补充一个概念，`哈希`:

- 可变数据类型不可哈希
- 不可变数据类型可哈希

目前我们学到的数据类型有：列表和字典；不可变数据类型有：整型，字符串，布尔值，和元组。

字典的键必须是不可变数据类型（也就叫可哈希）且唯一（字典中的键只能存在一个）。如果字典中的键出现了重复，后面的键值对会覆盖前面的键值对。

字典的值可以是任意的数据类型。

字典本身也是一个可变数据类型：

```python
>>> dic = {{"a":1}:"yuan"}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'
>>>
```

运行上面的代码会报错，错误原因是字典是不可哈希的数据类型。也就是说，字典是可变的。

### 字典元素的增加

字典的增加操作可以通过`dic["键"] = 值`的方式实现：

```python
dic = {"key": 1}
dic["yuan"] = 19
print(dic)
结果：
	{'key': 1, 'yuan': 19}
```

这种通过赋值的方式增加变量的方法有些“暴力”，因为如果字典中原本存在相同的键，赋值操作将把原来的键对应的值替换为新值：

```python
dic = {"key": 1, "yuan": 19}
dic["yuan"] = 50
print(dic)

结果：
	{'key': 1, 'yuan': 50}
```

还有一种相对“温柔”的增加字典元素的方法，`.setdefault()`。通过这种方法，如果原字典中已经有了同样的键，返回值为改键对应的值，不会进行修改操作。如果原字典中不存在这样的值，将会增加新的键值对。值默认为`None`,也可以自定义要添加的值。范围值为增加之后的键对应的新值。例如：

```python
dic = {"key": 1}
print(dic.setdefault("key"))
print(dic.setdefault("meet"))
print(dic.setdefault("yaun", 18))
print(dic)

结果：
	1
    None
    18
    {'key': 1, 'meet': None, 'yaun': 18}
    
```

对于`.setdefault()`的返回值，可以这样记忆：最终字典的键对应的值是什么，就返回什么。

![1570075065948](C:\Users\99155\Desktop\新建文件夹\python\每天计划\day05\1570075065948.png)

`.setdefault()`方法是通过两个步骤进行的：

1. 先通过减去字典中查找，如果键存在，返回对应的值，不会继续执行第二步；如果键不存在，返回不存在，返回将要赋值给该键的值，默认为`Nune`，去执行第二步。
2. 将键和值添加到字典中

### 字典的删除

字典的删除主要有`.clear()` `.pop()` ,`popitem() ` 和`del`四种方法。

需要注意的是，字典没有`.remove()`方法。

`.clear()`方法用来清空字典，使用该方法后，会得到一个空字典：

```python
dic = {"key": 1, "dsb": "yuan"}
dic.clear()
print(dic)

结果：
	{}
```

`pop()`方法需要输入想要删除的键作为参数，返回的是被删除的键对应的值：

```python
dic = {"key": 1, "dsb": "yaun"}
print(dic.pop("key"))

结果：
	1
```

`.popitem()`是随机删除。但是在python3 和最新版本的python2中，默认删除字典最后一组键值对，返回值为删除掉键值对元组（注意，是元组 ，而不是像`.pop()`一样返回的值）：

```python
dic = {"key": 1, "dsb": "yaun"}
print(dic.popitem())

结果：
	("dsb", "yuan")
```

与列表不同的是，字典中没有`remove`方法。

字典中`del`方法的用法和列表十分相似，如果不指定要删除的键，将会删除整个字典：

```python
dic = {"key":1, "dsb": "yuan"}
del dic
print(dic)

结果：
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'dic' is not defined
```

代码运行后报错，因为dic已经被完全删除了。

我们也可以通过指定键的方法，删除特定的键值对：

```python
dic = {"key":1, "dsb": "yuan"}
del dic["dsb"]
print(dic)

结果：
	{"key": 1}
```

### 字典的修改

字典的修改有两种方式，第一种是暴力增加的方法`dic["键"]="值"`对已经存在的键进行修改；第二种是通过`.update()方法来合并两个字典。

使用`dic['键'] = '值'`进行修改，当字典中存在指定的键时，该键对应的值将会被替换为新值：

```python
dic = {"key": 1, "dsb": "yaun"}
dic["dsb"] = "Yuan" #修改
dic["ss"] = "yuan"	#增加
print(dic)

结果：
	{'key': 1, 'dsb': 'Yuan', 'ss': 'yuan'}

```

`.update()`方法可以将两个字典合并。`update`中输入的字典的级别要高于前面的字典。也就是说，如果新输入的键已经在字典中存在，该键对应的新值将对应替换旧值：

```python
dic = {"key": 1, "dsb": "yuan"}
dic.update({"key": 2, "meet": 23})
print(dic)

结果：
{'key': 2, 'dsb': 'yuan', 'meet': 23}
```

### 字典的查找

字典可以直接通过键来查找值，不过这种查找方式相对”暴力“：当键存在时，返回对应的值；当键不存在时，程序会报错：

```python
dic = {"key": 1, "dsb"："yuan"}
print(dic["dsb"]) #返回‘yuan’
print(dic["yuan"])#程序报错

结果：
	yuan
    Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'yuan'
```

因为这种直接查找的方式当键不存在时会报错，有时我们需要使用`.get()`方法：当键存在时，返回键对应的值；当键不存在时，返回None：

```python
dic = {"key": 1, "dsb": "yaun"}
print(dic.get("dsb"))
print(dic.get("yuan"))

结果：
	yuan
    None
```

我们甚至可以改变键不存在时的返回值：

```python
print(dic.get("yuan","没有找到啊"))
```

我们也可以通过`.keys()`,`.values()` `.items()`方法获取字典全部的键，值和键值对。这三种的方法返回值都是一种`高仿列表`，可以迭代但不支持索引。我们可以通过`list`函数将返回的高仿列表转化为普通列表：

```
dic = {"key":1, "dsb": "yuan"}
print(dic.keys())
print(dic.values())
print(dic.items())
for i in dic.keys():
	print(i)
print(list(dic.values))
```

也可以使用for循环迭代字典，将会遍历字典的键：

```python
dic = {"key": 1, "dsb": "yuan"}
for i in dic:
    print(i)
```

### 解构

我们刚刚提到了字典的`.items()`方法会返回键值对元组的键值对元组列表：

```python
dic = {"key": 1, "dsb": "yuan"}
print(dic.items())

结果：
	dict_items([('key', 1), ('dsb', 'yuan')])
```

我们得到的是一个键值对列表，每个键值对以元组的形式存在。

如果现在，我们需要提取其中的每一个元素。可以这样操作：

```python
dic = {"key": 1, "dsb": "yuan"}
lst = list(dic.items())
print(lst[0][0])
print(lst[0][1])
print(lst[1][0])
print(lst[1][1])
```

虽然能够实现，但是十分繁琐，这就需要用到解构的方法。

解构的基本样式是这样的；

```python
a, b = (10, 20)
print(a)
print(b)
```

可以看的出来，`10`和`20`的值分别被赋值给了`a`和`b`。这种将等号右边的数据分别赋值给等号前面的变量的方法，就是解构。

在看下面的例子：

```python
a, b = "你好"
print(a)
print(b)
```

a获取到你，b获取到好。也就是说，解构不仅使用于元组，也适用于字符串。事实上，只要是可迭代的对象，都可以用来解构：

```python
a, b, c = [10, 20, 30]
print(a)
print(b)
print(c)

a, b = {"key": 1, "dsb": "yaun"}
print(a)
print(b)
```

需要注意的是，字典在进行迭代操作时，只会返回键，而不会返回值。

解构时，等式左边的变量数要和右边的元素数目相等，否则就会报错。

如果想要使用少数的百年来接收更多的元素，就需要使用`*`来将最后面的多个元素进行`聚合`：

```python
a, b, *c = (1, 2, 3, 4, 5, 6)
print(a)
print(b)
print(c)

结果：
	1
    2
    [3, 4, 5, 6]
```

`3` `4` `5` 和`6` 被统一打包给了`c`，打包后的数据以`列表`的形式存储`

返回前面字典的`.items()`方法返回值的使用上，如果用解构的方法，我们可以很容易地打印出键值对的内容来：

```python
dic = {"key1": 1, "key2": 2, "key3": 3,"key4": 4}
for k, v in dic.items():
    print(k, v)
    
结果：
key1 1
key2 2
key3 3
key4 4
```



### 字典的嵌套

有下面这样一个字典：

```python
house = {
    101:{1:{"皮裤男":{"某女":["小钢炮"],"国际章":["熊大","熊二"]},
            2:{"林俊杰":["磨牙"]}}},
    102:{1:{"皮裤女":{"林宥嘉":["说谎","你是我的眼"]}},
         2:{"王菲":["天后","传奇","红豆","笑忘书"]}},
    103:{1:{"韦小宝":{"阿珂":"刺客","建宁":"公主","双儿":"丫鬟","教主老婆":"龙儿"}},
         2:{"张无忌":{"灭绝师太":"倚天剑","金毛狮王":"屠龙刀","张三丰":"太极拳"}}},
    104:{1:{"西游记":{"大圣":"金箍撸撸棒","唐僧":"叨逼叨","八戒":"高老庄主任"}}},
    105:{1:{"水浒传":{"武松":"打老虎","鲁智笙":"拔树","林冲":"教头","宋江":"老大"}},
         2:{"官场":{"高俅":"足球"}}},
    106:{1:{"老男孩":{"yuan":"dsb","chang":"污","宝元":"大卡车","江毅":"兽"}}},
}
```

要想找到里面的`"倚天剑"`的`剑`字和`"熊大"`的`熊`字，我们可以这样找到：

```python
print(house[103][2]['张无忌']['灭绝师太'][2])
print(house[101][1]['皮裤男']['国际章'][0][0])
```

从上面例子中，我们就可以发现，字典相较是很有优势的：

1. 字典查找内容更加方便
2. 字典查找速度更加块

字典还可以简化流程控制的过程。

举个例子，如果我们设计这样一个程序，用户输入编号，程序自动返回该编号对应的菜品。如果我们用if条件语句来实现，将会非常繁琐：

```python
while True:
    choose = int(input("请输入数字（1-12）："))
    if choose == 1:
        print('饺子')
    elif choose == 2:
        print('粥')
    elif choose == 3:
        print('面条')
    elif choose == 4:
        print('肉')
    elif choose == 5:
        print('土')
    elif choose == 6:
        print('东南风')
    elif choose == 7:
        print('切糕')
    elif choose == 8:
        print('烤全羊')
    elif choose == 9:
        print('烤骆驼')
    elif choose == 10:
        print('锅包肉')
    elif choose == 11:
        print('杀猪菜')
    elif choose == 12:
        print('乱炖')
    else:
        print('输入错误，请重新输入！')
```

如果我们使用字典的方法，只需要这样即可：

```python
dic = {"1":"饺子",
       "2":"粥",
       "3":"面条",
       "4":"肉",
       "5":"土",
       "6":"东南风",
       "7":"切糕",
       "8":"烤全羊",
       "9":"烤骆驼",
       "10":"锅包肉",
       "11":"杀猪菜",
       "12":"乱炖"
       }
while True:
    choose = input("请输入数字（1-12）：")
    if choose in dic:
        print(dic[choose])
    else:
        print('输入错误，请重新输入！')
```

我们看到，使用字典之后，代码节省了不少，而且少了很多重复代码。以后如果需要增加或者删改列表，只需要在字典中进行操作即可，不需要对程序进行改动，后期维护也更为便利。

## 字典内置函数&方法

Python字典包含了以下内置函数：

| 序号 | 函数及描述                                                   | 实例                                                         |
| :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1    | len(dict) 计算字典元素个数，即键的总数。                     | `>>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> len(dict) 3 ` |
| 2    | str(dict) 输出字典，以可打印的字符串表示。                   | `>>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> str(dict) "{'Name': 'Runoob', 'Class': 'First', 'Age': 7}" ` |
| 3    | type(variable) 返回输入的变量类型，如果变量是字典就返回字典类型。 | `>>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> type(dict) <class 'dict'> ` |

Python字典包含了以下内置方法：

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [radiansdict.clear()](https://www.runoob.com/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| 2    | [radiansdict.copy()](https://www.runoob.com/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| 3    | [radiansdict.fromkeys()](https://www.runoob.com/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| 4    | [radiansdict.get(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-get.html) 返回指定键的值，如果值不在字典中返回default值 |
| 5    | [key in dict](https://www.runoob.com/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| 6    | [radiansdict.items()](https://www.runoob.com/python3/python3-att-dictionary-items.html) 以列表返回可遍历的(键, 值) 元组数组 |
| 7    | [radiansdict.keys()](https://www.runoob.com/python3/python3-att-dictionary-keys.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| 8    | [radiansdict.setdefault(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-setdefault.html) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default |
| 9    | [radiansdict.update(dict2)](https://www.runoob.com/python3/python3-att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| 10   | [radiansdict.values()](https://www.runoob.com/python3/python3-att-dictionary-values.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| 11   | [pop(key[,default\])](https://www.runoob.com/python3/python3-att-dictionary-pop.html) 删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。 |
| 12   | [popitem()](https://www.runoob.com/python3/python3-att-dictionary-popitem.html) 随机返回并删除字典中的最后一对键和值。 |