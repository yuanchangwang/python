# day03 笔记 字符串详解

## 今日内容概要

1. 字符串详解
   1. 整型
   2. 进制转换
   3. 索引
   4. 切片
   5. 步长
   6. 字符串的方法

## 昨日内容回顾

1. while 循环

   - while循环基本结构：

     ```python
     while 条件：
     缩进 循环体
     ```

   - break ：终止循环

   - continue：跳出当前循环，开始下次循环

   - 可以通过条件控制循环次数

   - while else，当while后的条件不成立时，执行else中的代码

2. 格式化

   - %格式化基本结构：

     ```python
     a = "内容"
     b = "代码%s这样格式化" % (a,)
     ```

   - %格式化占位符：

     - ``%s``:字符串
     - ``%d``|``%i``:整型
     - ``%%``: 转义，表示一个可以打印的``%``

   - f-string字符串基本结构：

     ```python
     c = "这样就能{input("请输入内容")}格式化了"
     ```

3. 运算符

   - 比较运算符：`<` `>` `<=` `>=` `==` `!=`
   - 算术运算符：`+` `-` `*` `/` `//` `%` `**`
   - 赋值运算符：`=` `+=` `-=` `*=` `/=` `//=` `**=` `%=`
   - 逻辑运算符：`and` `or` `not`
   - 成员运算符：`in` `not in`

4. 编码初识

   - ascii：支持字母、数字和符号，不支持中文
   - gbk：
     - 包含ascii码
     - 一个英文1个字节
     - 一个中文2个字节
   - unicode：
     - 一个英文4个字节
     - 一个中文4个字节
   - utf-8：
     - 英文：1个字节
     - 欧洲：2个字节
     - 亚洲：3个字节



# 今日内容详细

### 整型

#### 整型数据概述

整型数字在Python中的关键字是`int`，整形在计算机中用于计算和比较。

在32位机器上int的范围是：`-2**31 ~ 2**31-1`，也就是`-2147483648～2147483647`；

在64位机器上int的范围是：`-2**63 ~ 2**63-1`，也就是`-9223372036854775808～9223372036854775807`；

在Python 3中，整型统统使用`int`。在Python 2中，较小的整形函数也用`int`，但是对于数值很大的整型，需要使用`long`。

在Python 2中，数值较大的整形函数结尾会出现一个`L`标识，例如`321312321L`。在Python 3中，无论数值有多大，都不会出现标识。

#### 进制转换初识

##### 10进制转换为2进制

整除2，获取余数，将余数从下向上整合。例如求11的二进制数：

```00.
除数	余数
11	 1
5	 1
2	 0
1 	 1
0
```

于是，`11`的二进制数就是`1011`。

##### 2进制转换为10进制

从右向左，每一位的权重是`2**（位数 - 1）`。位数是从右向左数到的次序。例如，倒数第一位的权重是`2**0`，即`1`，倒数第二位的权重为`2**1`，即`2`。将二进制转换为十进制，只需要将二进制每一位的数值乘以改为的权重然后将它们想加到一起即可。例如，我们可以这样计算二进制数`1011`的十进制数值：

```
1 * 2 ** 0 + 1 * 2 ** 1 + 0 * 2 ** 2 + 1 * 2 ** 3
= 1 + 2 + 0 + 8
= 11
```

##### 使用Python进行进制转换

- `bin(<十进制数>)`：将十进制数转换成二进制（常用）
- `int("字符串", 2)`：将某个进制（示例中为二进制）转换为十进制

示例如下：

```python
>>> bin(11)
'0b1011'
>>> int('01010',2)
10
```

整型（数字）总结

- 整型时不可变数据类型

- 可以在原地修改的叫做可变数据，不能在原地修改的叫做不可变数据类型

  我们可以用`id()`来查看数据的内存地址，例如：

  ```python
  a = 10    # 1428849040
  # id  -- 查看空间内存地址
  print(id(a))
  a = a + 1  # 1428849072
  print(id(a))
  ```

  将数据修改后，内容地址发生改变。

### 索引（下标）

索引又称下标，用来表示迭代对象中的某个元素的位置。

- 用正整数表示的索引值，从左向右定位，从0开始计数，如0，1，2

- 用负整数表示的索引值，从右向左定位，从-1开始计数，如-1，-2，-2

  例如

  ```python
  name = "meet" # 计算机从0开始数
  	  # 0123 (索引值|下标值) 从左向右
        #-4 -3 -2 -1          从右到左
  
  print(name[2]) #通过索引准确定位内容
  print(name[-4])
  
  结果：
  e
  m
  ```

  ### 切片

  有这样一个字符串：`meet_yuan_chang`，我们想要把其中的`yuan`取出来，该怎么做呢？一个可行的方法是，分别用`y、`u`、`a`和`n`的索引值，把它们分别取出来，再利用字符串的`加和`操作把它们拼接好，就像这样：

  ```python
  name = "meet_yuan_chang"
  a = name[5] #取出y
  b = name[6]
  c = name[7]
  d = name[8]
  print(a+b+c+d) #拼接并打印字符串
  ```

  当然也可以通过循环的方法来取出相应的字符，然后拼接成新的字符串：

  ```python
  name ="meet_yuan_chang"
  i = 5
  s = ""
  while i <= 8:
      s = name[i]
      i += 1
  print(s)
  ```

  因为这样的循环在Python中非常常用，所以被封装成为了一种简便的方法，就是字符串的`切片`。切片的基本格式和使用方法如下：

  ```python
  name = 'meet_yuan_chang'
  
  print(name[5:9])  # [起始位置:终止位置]  顾头不顾腚（起始位置保留，终止位置不保留）
  print(name[-5:])  # [起始位置:终止位置(默认到结尾)]  顾头不顾腚
  print(name[:])  # [起始位置(默认从开头):终止位置(默认到结尾)]  顾头不顾腚
  ```

  关于切片的终止位置的选择，还有一个技巧是：`终止位置 = 起始位置 + 切片长度`。例如上面的例子中，起始位置为`5`，切片长度为`4`，终止位置 =` 5 + 4 = 9`。

  有的时候我们并不想要一个一个取字符，而是要隔一个字符取一个。比如对于上面`"meet_yuan_chang`的例子，我们想要取第`3`、`5`、`7`位的`e`、`_`、`u`，该如何操作呢？

  我们依旧可以使用最原始的，分别取值，然后拼接字符串的方法：

  ```python
  name = "meet_yuan_chang"
  a = name[3]
  b = name[5]
  c = name[7]
  ```

  这种方法确实能得到我们想要的结果，但是太过繁琐。如果我们想要处理很长的字符串，就会非常麻烦了。这就需要我们在切片时引入`步长`变量。`步长`是使用切片方法的第三个参数，默认值为`1`。对于上面的例子，我们可以设置`步长`为`2`：

  ```python
  name = "meet_yuan_chang"
  	#  0123456789
      #   -6 -5 -4 -3 -2 -1
  print(name[2:7:2]) # [起始位置：终止位置：步长（默认为1）]
  ```

  如果我们步长设置成-1，可以实现从右向左查找：

  ```python
  name = "meet_alex_wusir"
  print(name[-1:3:-1]) #步长可以控制查找的方向
  ```

  在进行索引操作时，如果输入的参数超过最大索引值时，程序会报错。二在进行切片操作时，如果终止位置超出最大索引值时，程序不会报错，而是会走到字符串的结尾：

  ```python
  name = "meet_yuan_chang"
  print(name[2:20:2])
  ```

  需要注意的是，索引和切片只能给有序数据使用。整型和布尔值均不可以用来进行索引和切片操作。

  同整型一样，字符串也是一个不可变的数据类型：

  ```
  name = "meet"
  print(id(name)) # 2388909933712
  name = name + "最帅了"
  print(id(name)) # 2388910157296
  ```

  在python中，对于字符串的赋值，还会有这样一个有趣的情况：

  ```python
  name = "meet"
  name1 = "meet"
  
  print(id(name)) # 2313349022864
  print(id(name1)) # 2313349022864
  ```

  明明是两次赋值，两个字符串的内存地址居然是相同的。这是因为Python中有一个小数据池，小数据会驻留一段时间。如果在这段时间内，对相同的数据有新的赋值操作，不会新开辟一个内存空间，二是将变量指向已有数据的内存地址。



### 字符串方法详解

字符串方法有很多，本节课只讨论一些常用的，比较万能的点。\

`.upper()`方法

`.upper()`方法可以将字符串中的所有小写转换大写字母：

```python
name = "yuan"
name1 = name.upper() # 全部大写
print(name)
print(name1)

结果：
yuan
YUAN
```

`.lower()`方法

`lower()`方法与`.upper()`方法刚好相反，是将字符串中所有的大写转换为小写字母：

```python
name = "YUAN"
name1 = name.lower() # 全部小写
print(name)
print(name1)
结果：
YUAN
yuan
```

`.upper()` 和 `.lower()` 方法的一个很常见的应用场景是一些不需要区分大小写的情况，比如输入验证码或用户名时：

```python
yzm = "YuAn"
my_yzm = input("请输入验证码：[YuAn]")
if yzm.lower() == my_yzm.lower():
    print("ok")
else:
    print("滚")
```

`.starswith()`方法

`.startswith()`方法还支持字符串的`切片`，判断切片后的字符串是否是以相应的参数开头：

```python 
name = "yuan"
print(name.startswith("y", 1, 3))
结果 ： True
```

`.endswith()`方法

`.endswith()`的用法跟`startswith()`十分相似。不同的是，它是用来判断字符串是否以指定的字符串结尾，返回的同样是布尔值。`.endswith()`方法同样支持切片操作。

```python
name = 'yuan'
print(name.endswith("y"))

结果：
True
```

`.count()` 方法

`count()`方法用来统计输入的参数在字符串中出现的次数，例如：

```python
name = "yuan_chang"
print(name.count("a"))
结果:
    2
```

`.strip()`方法

补充知识：`\n`为 `换行符`，也就是键盘的`回车`键：`\t`为`制表符`,也就是键盘上的`Tab`键：

```python
print("你\n好")  #换行就是键盘上的回车键
print("你\t好")  #制表符就是键盘上的Tab

输出的结果为：
你
好
你	好
```

`.strip()`方法用来去除字符串两端的空格，换行符和制表符：

```python
name = '  \nyuan  \t'
print(name.strip())

结果：
yuan
```

`.strip()`方法也可以通过设定参数来指定去除头尾两端的内容：

```python
>>> name = "aaaaa yuan \naaaa\taaa\naaa"
>>> print(name.strip("a"))
结果
 yuan
aaaa    aaa
```

需要注意的是，当指定参数后，将不会清楚空格，换行符和制表符。

`.strip()`方法的应用场景是当输入账户密码时，忽视首位无意间输入的或者复制粘贴过来的空格：

```python
user = input("账户：").strip()
pwd = input("密码：").strip()
if user == "yuan" and pwd == "yuan122":
    print("ok")
else:
    print("滚")

```

另外，`int()`内部也封装了`.strip()`方法。故而当使用`int()`函数将字符串转换为整型时，不需要额外的`.strip()`操作：

```python
num = " \t 34 \n"
print(int(num))
```

`.split()`方法

`.split()`方法用来分割字符串。默认按照空格，换行符和制表符来进行分割，分割后，空格，制表符和换行符将不存在。`.split()`方法输出的时列表：

```python
a = "yuan chang"
lst = a.split()
print(lst)

结果：
["yuan", "chang"]
```

空格，换行符和制表符都有同样的结果：

```python
name = "yuan\nchang"
print(name.split())
name = "yuan\tchang"
pritn(name.split())
name = "yuan chang"
print(name.split())
```

`split`方法可以指定参数，通过特定的内容进行分割：

```python
a = "yuan:chang"
lst = a.split(":")
print(lst)
结果：["yuan", "chang"]
```

`replace()`方法

`replace()`方法可以替换字符串中的旧内容为新内容。`.replace()`有三个参数：参数1为旧值，参数2为新值，参数3为替换次数（默认全部替换）。例如：

```python
name = "yuanmeet"
name = name.replace('e', 's', 2)
print(name)
结果：
yuanmest
```

`is`系统方法（判断系统）

`is`系列方法有很多，主要用到的是四个：

- `name.isalnum()`:用来判断是不是由字母，中文或数字组成，返回的是布尔值
- `name.isalpha(): `用来判断是否由字母或中文组成，返回布尔值
- `name.isdigit()`用来判断是否由阿拉伯数字组成，返回布尔值。有一个bug是，⑤也会被认作阿拉伯数字
- `name.isdecimal()`用来判断是不是十进制组成，返回的是布尔值

for循环

与以死循环存在的`while循环`不同的是，`for循环`往往以有限循环的形式存在。

`for循环`的基本结构为：

```python
for i in xxx:
    循环体
```

其中，

- `for`：关键字
- `i`：变量名
- `in`：关键字
- `xxx`：可迭代对象

用已有的知识，如果我们想分别打印字符串`"yuan"`中的每一个字符，可以使用`while循环`来实现：

```python
name = "alex"
count = 0
while count < len(name):
    print(name[count])
    count += 1
```

这里补充一个知识点，函数`len()`是一个公共方法，它可以获得传入参数的长度：

```python
>>> name = "yuan"
>>> len(name)
4
```

如果使用`for循环`,我们可以更简便实现目的：

```python
name = "yuan"
for i in name: #每次循环，for都会把取到的元素赋值给i
    print(i)#打印变量i
```

看下面这样一个例子：

```
for i in "abcde":
    pass
print(i)
```

最终打印出来的结果只有一个`e`。那是因为`for循环`本质是一个`赋值`操作，每次循环都是将可迭代对象中的一个元素`赋值`给变量。当进行最后一次循环时，字符串`"abcde"`的最后一个元素`"e"`被赋值给了变量`i`。循环结束，`i`没有被重新`赋值`。虽然打印的动作不在循环体中，但不影响打印出`e`的结果。

思考题：

下面的代码会打印出什么样的结果呢？

```
num = 5
count = 1
while num:
    for i in "abc":
        print(i + str(count))
    count += 1
    num -= 1
```





## Python 的字符串内建函数

Python 的字符串常用内建函数如下：



| 序号 | 方法及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [capitalize()](https://www.runoob.com/python3/python3-string-capitalize.html) 将字符串的第一个字符转换为大写 |
| 2    | [center(width, fillchar)](https://www.runoob.com/python3/python3-string-center.html) 返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格。 |
| 3    | [count(str, beg= 0,end=len(string))](https://www.runoob.com/python3/python3-string-count.html) 返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数 |
| 4    | [bytes.decode(encoding="utf-8", errors="strict")](https://www.runoob.com/python3/python3-string-decode.html) Python3 中没有 decode 方法，但我们可以使用 bytes 对象的 decode() 方法来解码给定的 bytes 对象，这个 bytes 对象可以由 str.encode() 来编码返回。 |
| 5    | [encode(encoding='UTF-8',errors='strict')](https://www.runoob.com/python3/python3-string-encode.html) 以 encoding 指定的编码格式编码字符串，如果出错默认报一个ValueError 的异常，除非 errors 指定的是'ignore'或者'replace' |
| 6    | [endswith(suffix, beg=0, end=len(string))](https://www.runoob.com/python3/python3-string-endswith.html) 检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False. |
| 7    | [expandtabs(tabsize=8)](https://www.runoob.com/python3/python3-string-expandtabs.html) 把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8 。 |
| 8    | [find(str, beg=0, end=len(string))](https://www.runoob.com/python3/python3-string-find.html) 检测 str 是否包含在字符串中，如果指定范围 beg 和 end ，则检查是否包含在指定范围内，如果包含返回开始的索引值，否则返回-1 |
| 9    | [index(str, beg=0, end=len(string))](https://www.runoob.com/python3/python3-string-index.html) 跟find()方法一样，只不过如果str不在字符串中会报一个异常. |
| 10   | [isalnum()](https://www.runoob.com/python3/python3-string-isalnum.html) 如果字符串至少有一个字符并且所有字符都是字母或数字则返 回 True,否则返回 False |
| 11   | [isalpha()](https://www.runoob.com/python3/python3-string-isalpha.html) 如果字符串至少有一个字符并且所有字符都是字母则返回 True, 否则返回 False |
| 12   | [isdigit()](https://www.runoob.com/python3/python3-string-isdigit.html) 如果字符串只包含数字则返回 True 否则返回 False.. |
| 13   | [islower()](https://www.runoob.com/python3/python3-string-islower.html) 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False |
| 14   | [isnumeric()](https://www.runoob.com/python3/python3-string-isnumeric.html) 如果字符串中只包含数字字符，则返回 True，否则返回 False |
| 15   | [isspace()](https://www.runoob.com/python3/python3-string-isspace.html) 如果字符串中只包含空白，则返回 True，否则返回 False. |
| 16   | [istitle()](https://www.runoob.com/python3/python3-string-istitle.html) 如果字符串是标题化的(见 title())则返回 True，否则返回 False |
| 17   | [isupper()](https://www.runoob.com/python3/python3-string-isupper.html) 如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False |
| 18   | [join(seq)](https://www.runoob.com/python3/python3-string-join.html) 以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串 |
| 19   | [len(string)](https://www.runoob.com/python3/python3-string-len.html) 返回字符串长度 |
| 20   | [ljust(width[, fillchar\])](https://www.runoob.com/python3/python3-string-ljust.html) 返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。 |
| 21   | [lower()](https://www.runoob.com/python3/python3-string-lower.html) 转换字符串中所有大写字符为小写. |
| 22   | [lstrip()](https://www.runoob.com/python3/python3-string-lstrip.html) 截掉字符串左边的空格或指定字符。 |
| 23   | [maketrans()](https://www.runoob.com/python3/python3-string-maketrans.html) 创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。 |
| 24   | [max(str)](https://www.runoob.com/python3/python3-string-max.html) 返回字符串 str 中最大的字母。 |
| 25   | [min(str)](https://www.runoob.com/python3/python3-string-min.html) 返回字符串 str 中最小的字母。 |
| 26   | [replace(old, new [, max\])](https://www.runoob.com/python3/python3-string-replace.html) 把 将字符串中的 str1 替换成 str2,如果 max 指定，则替换不超过 max 次。 |
| 27   | [rfind(str, beg=0,end=len(string))](https://www.runoob.com/python3/python3-string-rfind.html) 类似于 find()函数，不过是从右边开始查找. |
| 28   | [rindex( str, beg=0, end=len(string))](https://www.runoob.com/python3/python3-string-rindex.html) 类似于 index()，不过是从右边开始. |
| 29   | [rjust(width,[, fillchar\])](https://www.runoob.com/python3/python3-string-rjust.html) 返回一个原字符串右对齐,并使用fillchar(默认空格）填充至长度 width 的新字符串 |
| 30   | [rstrip()](https://www.runoob.com/python3/python3-string-rstrip.html) 删除字符串字符串末尾的空格. |
| 31   | [split(str="", num=string.count(str))](https://www.runoob.com/python3/python3-string-split.html) num=string.count(str)) 以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num+1 个子字符串 |
| 32   | [splitlines([keepends\])](https://www.runoob.com/python3/python3-string-splitlines.html) 按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。 |
| 33   | [startswith(substr, beg=0,end=len(string))](https://www.runoob.com/python3/python3-string-startswith.html) 检查字符串是否是以指定子字符串 substr 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。 |
| 34   | [strip([chars\])](https://www.runoob.com/python3/python3-string-strip.html) 在字符串上执行 lstrip()和 rstrip() |
| 35   | [swapcase()](https://www.runoob.com/python3/python3-string-swapcase.html) 将字符串中大写转换为小写，小写转换为大写 |
| 36   | [title()](https://www.runoob.com/python3/python3-string-title.html) 返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle()) |
| 37   | [translate(table, deletechars="")](https://www.runoob.com/python3/python3-string-translate.html) 根据 str 给出的表(包含 256 个字符)转换 string 的字符, 要过滤掉的字符放到 deletechars 参数中 |
| 38   | [upper()](https://www.runoob.com/python3/python3-string-upper.html) 转换字符串中的小写字母为大写 |
| 39   | [zfill (width)](https://www.runoob.com/python3/python3-string-zfill.html) 返回长度为 width 的字符串，原字符串右对齐，前面填充0 |
| 40   | [isdecimal()](https://www.runoob.com/python3/python3-string-isdecimal.html) 检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false。 |

## Python转义字符

在需要在字符中使用特殊字符时，python用反斜杠(\)转义字符。如下表：

| 转义字符    | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| \(在行尾时) | 续行符                                                       |
| \\          | 反斜杠符号                                                   |
| \'          | 单引号                                                       |
| \"          | 双引号                                                       |
| \a          | 响铃                                                         |
| \b          | 退格(Backspace)                                              |
| \000        | 空                                                           |
| \n          | 换行                                                         |
| \v          | 纵向制表符                                                   |
| \t          | 横向制表符                                                   |
| \r          | 回车                                                         |
| \f          | 换页                                                         |
| \oyy        | 八进制数，**yy** 代表的字符，例如：**\o12** 代表换行，其中 o 是字母，不是数字 0。 |
| \xyy        | 十六进制数，yy代表的字符，例如：\x0a代表换行                 |
| \other      | 其它的字符以普通格式输出                                     |

------

## Python字符串运算符

下表实例变量a值为字符串 "Hello"，b变量值为 "Python"：

| 操作符 | 描述                                                         | 实例                             |
| :----- | :----------------------------------------------------------- | :------------------------------- |
| +      | 字符串连接                                                   | a + b 输出结果： HelloPython     |
| *      | 重复输出字符串                                               | a*2 输出结果：HelloHello         |
| []     | 通过索引获取字符串中字符                                     | a[1] 输出结果 **e**              |
| [ : ]  | 截取字符串中的一部分，遵循**左闭右开**原则，str[0,2] 是不包含第 3 个字符的。 | a[1:4] 输出结果 **ell**          |
| in     | 成员运算符 - 如果字符串中包含给定的字符返回 True             | **'H' in a** 输出结果 True       |
| not in | 成员运算符 - 如果字符串中不包含给定的字符返回 True           | **'M' not in a** 输出结果 True   |
| r/R    | 原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 **r**（可以大小写）以外，与普通字符串有着几乎完全相同的语法。 | `print( r'\n' ) print( R'\n' ) ` |
| %      | 格式字符串                                                   |                                  |

## python字符串格式化符号:



| 符   号 | 描述                                 |
| :------ | :----------------------------------- |
| %c      | 格式化字符及其ASCII码                |
| %s      | 格式化字符串                         |
| %d      | 格式化整数                           |
| %u      | 格式化无符号整型                     |
| %o      | 格式化无符号八进制数                 |
| %x      | 格式化无符号十六进制数               |
| %X      | 格式化无符号十六进制数（大写）       |
| %f      | 格式化浮点数字，可指定小数点后的精度 |
| %e      | 用科学计数法格式化浮点数             |
| %E      | 作用同%e，用科学计数法格式化浮点数   |
| %g      | %f和%e的简写                         |
| %G      | %f 和 %E 的简写                      |
| %p      | 用十六进制数格式化变量的地址         |

格式化操作符辅助指令:

| 符号  | 功能                                                         |
| :---- | :----------------------------------------------------------- |
| *     | 定义宽度或者小数点精度                                       |
| -     | 用做左对齐                                                   |
| +     | 在正数前面显示加号( + )                                      |
| <sp>  | 在正数前面显示空格                                           |
| #     | 在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X') |
| 0     | 显示的数字前面填充'0'而不是默认的空格                        |
| %     | '%%'输出一个单一的'%'                                        |
| (var) | 映射变量(字典参数)                                           |
| m.n.  | m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)        |

Python2.6 开始，新增了一种格式化字符串的函数 [str.format()](https://www.runoob.com/python/att-string-format.html)，它增强了字符串格式化的功能。