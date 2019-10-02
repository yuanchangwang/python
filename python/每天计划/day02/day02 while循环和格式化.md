# day02 while循环和格式化

## 今日内容摘要

1. while循环
2. 格式化
3. 运算符
4. 编码初识

## 昨日内容回顾

1. 变量

   变量命名规范

   1. 由数字，字母和下划线组成
   2. 不能以数字开头
   3. 不能使用python的关键字
   4. python中的变量名区分大小写
   5. 变量的命名要具有可描述性
   6. 变量名不应该有汉字和拼音
   7. 变量名推荐写法：
      1. 驼峰体
      2. 下划线

2. 常量

3. 基本数据类型

   1. 字符串
   2. 整型
   3. 布尔值

4. 注释

5. 用户交互

6. 流程控制

## 今日内容详细

### 1、while 循环

while循环基本结构

循环就是不断地重复某件事情。```while```就是while循环的关键字。

while循环的基本结构：

```python
while 条件：
缩进 循环体
```

典型while循环示例

```python
print(1111)
while True:  #死循环
    print("坚强")
    print("过火")
    print("单身情歌")
    print("哼小曲")
    print("鸡你太美")
print("痒") #这里永远都不能执行到
```

上面的例子中，第一步，先打印```1111```.第二部，进入while循环语句，判断```while```后的条件是否为真。为真，进入循环体。第三步，打印```坚强```。第四五六七步分别打印```过火```,```单身情歌```, ```哼小曲```和```鸡你太美``` 。循环体中的内容运行完毕，程序又返回到while语句。第八步，继续判断```while```后的条件是否为真，然后继续进入循环体，重新打印内容，随后又返回到while语句中。因为while语句后面的条件一直都是```Ture```,故而循环往复，永不停息，成为了死循环。最后一条的```痒```永远也打印不出来。 

![1569766696218](C:\Users\99155\Desktop\新建文件夹\python\每天计划\day02\1569766696218.png)

#### break语句

很显然，这样的死循环并不能满足我们日常编程的需要。如果能有办法限制循环次数，将会十分实用。在这里，我们可以引入break语句。break可以终止当前循环。结合if条件语句，可以把死循环转换成有限的循环。例如：

```python
#循环5次
count = 0
while Ture:
    count += 1
    print(count)
    if count == 5:
        print(count)
        break  #终止当前循环
        
  
运行的结果：
1
2
3
4
5
5
```

在这个例子中，我们先定义了一个变量`count`用来计数，也成为`计数器`。每一次循环，`count`就会增加`1`。当`count`等于`5`时，if语句的条件成立，打印出当前`count`的数值，运行`break`，退出循环。我们就成功把死循环转换成了有限循环。

![1569767802408](C:\Users\99155\Desktop\新建文件夹\python\每天计划\day02\1569767802408.png)

#### continue语句

除了`break`，while循环中还有一个很重要的语句`continue`。`continue`语句的意思是跳出本次循环，继续下次循环。用通俗的话来讲，`continue`就是伪装成循环体中最后一行代码。例如：

```python
count = 0
while True:  # 死循环
    count = count + 1  # 先执行 = 右边的内容
    if count == 5:
        print(111)
        continue  # continue 就是伪装成循环体中最后一行代码
    print(count)
```

很显然，这还是一个死循环。只不过当计数器`count`等于`5`的时候，会打印一次`111`，并且这次的`count`，也就是`5`，不会被打印出来。

![1569768891862](C:\Users\99155\Desktop\新建文件夹\python\每天计划\day02\1569768891862.png)

#### 条件控制循环

除了通过使用break关键字来终止循环，我们还可以通过while后面的条件来控制循环次数：

```python
count = 0
while count < 2:
    print(count)
    count = count + 1
    
   
打印结果：
0
1
```

在上面的例子中，最开始计数器`count`的值为`0`。然后运行到while条件，`count < 2`是成立的，于是进入循环体。首先把`count`的内容`0`打印出来，然后`count`增加`1`，进入下一次循环。第二次循环也一样，打印`1`之后，`count`变成了`2`，再回到while判断语句。此时，`count < 2`不成立，循环终止。



#### while else语句![QQ鍥剧墖20190906145142](C:\Users\99155\Desktop\新建文件夹\python\每天计划\day02\QQ鍥剧墖20190906145142.png)

while语句也有判断的行为，所以也可以配合else语句使用。while else结构和if else结构很相似。只有当while后判断的条件不成立时，才会执行else中的语句。如果循环中没有break，else语句中的内容将在循环结束后执行；如果循环中有break，else语句中的内容有可能不被执行。观察下面两个例子：

```python
print(222)
count = 0
while count < 3:
    print(count)
    count = count + 1
else:
    print(111)
 运行结果：222 0 1 2 111

print(222)
count = 0
while count < 3:
    print(count)
    count = count + 1
    break
else:
    print(111)
    
运行结果： 222 0
```

在第一个例子中，经过三次循环后，计数器`count`的值将增加到`3`。此时，条件`count < 3`不再满足，跳出循环，执行`else`语句，打印出`111`来。而第二个例子中，在第一次循环中就遇到了`break`，循环被强行终止，并没有再次判断`count < 3`，于是就不会进入到`else`中，`111`便打印不出来。

#### while循环小结

- `break`：终止当前循环
- `continue`：跳出本次循环，继续下次循环（就是伪装成循环体中最后一行代码）
- `continue`和`break`下方的代码都不会执行
- `while` 循环可以通过条件控制循环的次数
- `while` 语句可以和 `else` 语句配合使用，当 `while`后的条件不满足时，将会运行`else`中的语句。

## 2、格式化

有这样一个字符串：

```
msg = """
------info------
name:meet
age:18
sex:男
hobby:女
-------end------
"""
```

如果我们想让用户输入名字，年龄，性别和爱好，然后程序按照上面的格式给打印出来。从目前我们所学的知识，我们可以用这样的代码来实现：

```
a = "------info------"
b = "name:"
c = "age:"
d = "sex:"
e = "hobby:"
f = "-------end------"
name = input("name")
age = input("age")
sex = input("sex")
hobby = input("hobby")
print(a)
print(b + name)
print(c + age)
print(d + sex)
print(e + hobby)
print(f)

代码运行后就是这样的：
namealex
age18
sex男
hobby女
------info------
name:alex
age:18
sex:男
hobby:女
-------end------
```

#### %格式化

不过虽然我们实现了需求，但是太过繁琐。这里就可以用到格式化的方法。格式化，就是在字符串中需要自定义的位置放入占位符，然后通过给占位符提供数据，从而构建新的字符串。提供的数据需要和占位符一一对应，否则将会报错。

Python中常用的占位符有：

- `%s` 字符串 :`%s`可以填充字符串也可以填充数字
- `%d`|`%i`整型 : 必须填充数字
- `%%` 转义：变成普通的`%`

有了格式化的方法，上面的例子我们就可以简化成这个样子：

```
name = input("name")
age = input("age")
sex = input("sex")
hobby = input("hobby")
a = "哈哈啊"
msg = """
------info------
name:%s
age:%s
sex:%s
hobby:%s
-------end------
"""
print(msg%(name,int(age),sex,hobby))
```

#### f-strings格式化

在Python 3.6及以后的版本中引入了一个新的`f-strings`方法格式字符串，把上面的格式化方法进一步简化，具体做法为：

```
msg = f"""
------info------
name:{input("name")}
age:{input("age")}
sex:{input("sex")}
hobby:{input("hobby")}
-------end------
"""
print(msg)
```

用大括号将需要格式化的位置标记出来，在大括号里面填入变量或者数据，构建成新的字符串。

其中，可以通过两个大括号`{{}}`来转义，表示普通的大括号。

## 3、运算符

#### 比较运算符

比较运算符主要有六个：

1. `>`：大于
2. `<`：小于
3. `>=`：大于等于
4. `<=`：小于等于
5. `==`：等于
6. `!=`：不等于

比较运算返回的值为`True`或`False`。

#### 算术运算符

Python中的算术运算符有七个：

1. `+`：加和
2. `-`：相减
3. `*`：相乘
4. `/`：相除
5. `//`：整除|地板除（向下取整）
6. `**`：幂运算
7. `%`：取余（模）

算术运算主要用于数字的计算。字符串也可以用`+`和`*`进行拼接。

#### 赋值运算符

赋值运算符为`=`。在Python中，为了输入简便，还从其中算术运算符中衍生出了七种赋值运算符：`+=`，`-=`， `*=`， `/=`， `//=`， `**=`， `%=`。它们的用法和含义如下：

```
a = 10
b = 2
b += 1	# b = b + 1
a -= 1  # a = a - 1
a *= 2  # a = a * 2
a /= 2  # a = a / 2
a //= 2 # a = a // 2
a **= 2 # a = a ** 2
a %= 2  # a = a % 2
```

#### 逻辑运算符

逻辑运算符有三个：与（`and`，并且）、或（`or`）、非（`not`，不是）。

逻辑运算的优先级是`() > not > and > or`，查找顺序为从左向右。例如：

```
3>2 and 4>2 or True and not False and True
# 先运算比较
True and True or True and not False and True
# 再运算not
True and True or True and True and True
# 运算and
True or True
# 最后运算or
True
```

当数字之间进行逻辑运算时，有这样一套规则：

```
and数字进行逻辑运算时:
    两边都不为0和False时，选择and后边的内容
    两边都为假时，选择and前的内容
    一真一假选择假

or 数字进行逻辑运算时:
    两边都不为0和False时，选择or前边的内容
    两边都为假时，选择or后边的内容
    一真一假选择真
```

官方给出的运算规则是这个样子的：

| 操作    | 结果                               |
| ------- | ---------------------------------- |
| x or y  | 如果x为假，选择y，否则选择x        |
| x and y | 如果x为假，选择x，否则选择y        |
| not x   | 如果x为假，返回True，否则返回False |

可以通过下面的示例来找到这些规律：

```
print(1 and 3)
print(0 and 8)
print(9 and 4)
print(False and 5)
```

#### 成员运算符

在Python中，成员运算符有两个：

- a in b：用于判断a是否在b中
- a not in b：用于判断a是否不在b中

具体使用示例：

```
name = "alex"
msg = input(">>>")
if name in msg:
    print(111)
else:
    print(222)
    
输出结果为：
>>>alexad
111
>>>alecxaa
222
```

## 4、编码初识

常见编码集：

1. ascii：
   - 不支持中文
   - 一个字符占用8位
2. gbk（包含ascii）国标码：
   - 一个英文字符占用8位（1字节）
   - 一个中文字符占用16位（2字节）
3. Unicode：
   - 英文：4个字节，32位
   - 中文：4个字节，32位
4. utf-8（最流行的编码集）：
   - 英文：1个字节，8位
   - 欧洲：2个字节，16位
   - 亚洲：3个字节，24位

单位转换：

- 1字节 = 8位
- 1Byte = 8 bits
- 1024bytes = 1KB
- 1024KB = 1MB
- 1024MB = 1GB
- 1024GB= 1TB #够用了
- 1024TB = 1PB