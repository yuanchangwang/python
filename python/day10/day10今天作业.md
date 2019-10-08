# day10今天作业

1.请写出下列代码的执行结果：
例一：

```
def func1():
	print('in func1')

def func2():
	print('in func2')

ret = func1

ret()  # in func1

ret1 = func2

ret1()  # in func2

ret2 = ret

ret3 = ret2
 
ret2()  # in func1

ret3()  # in func1
```

执行结果：

```python
in func1
in func2
in func1
in func1

```



例二：

```
def func1():
    print('in func1')

def func2():
    print('in func2')

def func3(x,y):

    x()

    print('in func3')

    y()
	
print(111)  # 111
func3(func2,func1) #  in func2  in func3 in func1 
print(222)  # 222
```

执行结果：

```python
111
in func2
in func3
in func1
222
```



例三（选做题）：

```
def func1():
    print('in func1')

def func2(x):
    print('in func2')
    return x

def func3(y):
    print('in func3')
    return y

ret = func2(func1) # in func2
ret()  # in func1
ret2 = func3(func2) # in func3
ret3 = ret2(func1) # in func2
ret3()  # in func1
```

执行结果：

```python
in func2
in func1
in func3
in func2
in func1
```



看代码写结果：
例四:

```
def func(arg):
    return arg.replace('yuan', '****')

def run():
    msg = "yuan和大家都是好朋友"
    result = func(msg)
    print(result)

run() # ****和大家都是好朋友
data = run() # ****和大家都是好朋友
print(data) # None
```

看代码写结果：

```python
****和大家都是好朋友
****和大家都是好朋友
None

```



例五:

```
data_list = []

def func(arg):
    return data_list.insert(0, arg)

data = func('绕不死你')
print(data) #None
print(data_list) # ["绕不死你"]
```

看代码写结果：

```python
None
['绕不死你']

```



例六:

```
def func():
    print('你好呀')
    return '好你妹呀'


func_list = [func, func, func]

for item in func_list:
    val = item() # 你好呀 * 3次 
    print(val) # 好你妹呀 * 3次
```

看代码写结果：

```python
你好呀
好你妹呀
你好呀
好你妹呀
你好呀
好你妹呀
```



例七:

```
def func():
    print('你好呀')
    return '好你妹呀'


func_list = [func, func, func]

for i in range(len(func_list)):
    val = func_list[i]() # 你好呀 * 3
    print(val) # 好你妹呀 * 3
```

看代码写结果：

```python
你好呀
好你妹呀
你好呀
好你妹呀
你好呀
好你妹呀
```



例八:

```
def func():
    return '大烧饼'


def bar():
    return '吃煎饼'


def base(a1, a2):
    return a1() + a2()


result = base(func, bar)
print(result) # 大烧饼吃煎饼

```

看代码写结果：

```python
大烧饼吃煎饼
```



例九:

```
def func():
    for item in range(10):
        pass
    	return item
func() # 不打印
```

看代码写结果：

```python
什么也没有，没有打印
```



例十:

```
def func():
    for item in range(10):
        pass
    	yield item
func() # 什么也没有，没有打印
```

看代码写结果：

例十一:

```
item = 'yuan'
def func():
    item = 'chang'
    def inner():
        print(item)
    for inner in range(10): # inner 是整型
        pass
    inner()
func() #TypeError: 'int' object is not callable
```

看代码写结果：

```python
TypeError: 'int' object is not callable
    报错，整型数据不能被调用
```



例十二:

```
l1 = []
def func(args):
    l1.append(args)
    return l1
print(func(1)) # [1]
print(func(2)) # [1,2]
print(func(3)) # [1,2,3]
```

看代码写结果：

```python
[1]
[1, 2]
[1, 2, 3]
```



例十三:

```
name = '宝元'
def func():
    global name
    name = '男神'
print(name) # 宝元
func() 
print(name) # 男神
```

看代码写结果：

```python
宝元
男神

```



例十四:

```
name = '宝元'
def func():
    print(name)
func() # 宝元
```

看代码写结果：

```python
宝元
```



例十五:(选做题)

```
name = '宝元'
def func():
    print(name)
    name = 'yuan'
func() # 报错
```

看代码写结果：

```python
UnboundLocalError: local variable 'name' referenced before assignment
    报错了，因为先打印name，就是要使用全局变量，name已经成了全局变量，后面再赋值就是要在局部空间修改全局变量，所以报错


```



例十六:

```
def func():
    count = 1
    def inner():
        nonlocal count
        count += 1
        print(count)
    print(count)
    inner()
    print(count)
func() # 1 2 2 
```

看代码写结果：

```python
1
2
2

```



例十七: (选做题)

```
def extendList(val,list=[]):
    list.append(val)
    return list

list1 = extendList(10)
list2 = extendList(123,[])
list3 = extendList('a')

print('list1=%s'%list1)  # list1 = [10, 'a']
print('list2=%s'%list2) # list2 = [123]
print('list3=%s'%list3) # list3 = [10,'a']
```

看代码写结果：

```python
list1=[10, 'a']
list2=[123]
list3=[10, 'a']

```



例十八:

```
def extendList(val,list=[]):
    list.append(val)
    return list
print('list1=%s'% extendList(10)) # list = [10]
print('list2=%s'% extendList(123,[])) # list = [123]
print('list3=%s'% extendList('a')) # list = [10, 'a']
```

2.用你的理解解释一下什么是可迭代对象，什么是迭代器。

```python
可迭代对象：具有.__iter__()方法的就是可迭代对象
迭代器：具有.__iter__()和 .__next__()方法的就是迭代器
```



3.使用while循环实现for循环的本质(面试题)

```python
lst = [1,2,3,4,5]
lst1 = lst.__iter__()
while True:
    try:
        i = lst1.__next__()
        print(i)
    except StopIteration:
        break
```

