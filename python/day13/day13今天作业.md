# day13今天作业

2.都完成的做一下作业（下面题都是用内置函数或者和匿名函数结合做出）：

1. 用map来处理下述l，然后用list得到一个新的列表，列表中每个人的名字都是sb结尾

```
l=[{'name':'yuan'},{'name':'chang'}]
```

```python
l=[{'name':'yuan'},{'name':'chang'}]
lst = list(map(lambda x:{'name':x['name']+'sb'}, l))
print(lst)
```



2)用filter来处理,得到股票价格大于20的股票名字

```
shares={
 'IBM':36.6,
 'Lenovo':23.2,
 'oldboy':21.2,
 'ocean':10.2,
         }
```

```python
shares={
 'IBM':36.6,
 'Lenovo':23.2,
 'oldboy':21.2,
 'ocean':10.2,
         }
lst = list(filter(lambda x: shares[x] > 20, shares))
print(lst)
```



3)有下面字典，得到购买每只股票的总价格，并放在一个迭代器中。
结果：list一下[9110.0, 27161.0,......]

```
portfolio = [
  {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
{'name': 'ACME', 'shares': 75, 'price': 115.65}]
```

```python
portfolio = [
  {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
{'name': 'ACME', 'shares': 75, 'price': 115.65}]
gen = (x['shares'] * x['price'] for x in portfolio)
print(list(gen))
```



4)还是上面的字典，用filter过滤出单价大于100的股票。

```python
portfolio = [
  {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
{'name': 'ACME', 'shares': 75, 'price': 115.65}]
lst = list(filter(lambda x: x['price'] > 100, portfolio))
print(lst)
```



5)有下列三种数据类型，

```
 l1 = [1,2,3,4,5,6]
 l2 = ['oldboy','yuan','chang','太白','日天']
 tu = ('**','***','****','*******')
```

写代码，最终得到的是（每个元祖第一个元素>2,第三个*至少是4个。）

```
 [(3, 'wusir', '****'), (4, '太白', '*******')]
```

这样的数据。

```python
l1 = [1,2,3,4,5,6]
l2 = ['oldboy','yuan','chang','太白','日天']
tu = ('**','***','****','*******')
lst = zip([i[1] for i in enumerate(l1) if i[0] > 1],[j[1]for j in enumerate(l2) if j[0] > 1],[q for q in tu if len(q) >= 4 ])
print(list(lst))
```



6)有如下数据类型(实战题)：

```
 l1 = [{'sales_volumn': 0},
       {'sales_volumn': 108},
       {'sales_volumn': 337},
       {'sales_volumn': 475},
       {'sales_volumn': 396},
       {'sales_volumn': 172},
       {'sales_volumn': 9},
       {'sales_volumn': 58},
       {'sales_volumn': 272},
       {'sales_volumn': 456},
       {'sales_volumn': 440},
       {'sales_volumn': 239}]
```

将l1按照列表中的每个字典的values大小进行排序，形成一个新的列表。

```python
l1 = [{'sales_volumn': 0},
      {'sales_volumn': 108},
      {'sales_volumn': 337},
      {'sales_volumn': 475},
      {'sales_volumn': 396},
      {'sales_volumn': 172},
      {'sales_volumn': 9},
      {'sales_volumn': 58},
      {'sales_volumn': 272},
      {'sales_volumn': 456},
      {'sales_volumn': 440},
      {'sales_volumn': 239}]
lst = sorted(l1, key=lambda x: x['sales_volumn'])
print(lst)
```



3.有如下数据结构,通过过滤掉年龄大于16岁的字典

```
lst = [{'id':1,'name':'yuan','age':18},
        {'id':1,'name':'chang','age':17},
        {'id':1,'name':'taibai','age':16},]
```

```python
lst = [{'id':1,'name':'yuan','age':18},
        {'id':1,'name':'chang','age':17},
        {'id':1,'name':'taibai','age':16},]
l = filter(lambda x: x['age'] <= 16,lst)
print(list(l))
```



4.有如下列表,按照元素的长度进行升序

```
lst = ['天龙八部','西游记','红楼梦','三国演义']
```

```python
lst = ['天龙八部','西游记','红楼梦','三国演义']
l = sorted(lst,key=lambda x: len(x))
print(l)
```



5.有如下数据,按照元素的年龄进行升序

```
lst = [{'id':1,'name':'yuan','age':18},
    {'id':2,'name':'chang','age':17},
    {'id':3,'name':'taibai','age':16},]
```

```python
lst = [{'id':1,'name':'yuan','age':18},
    {'id':2,'name':'chang','age':17},
    {'id':3,'name':'taibai','age':16},]
l = sorted(lst,key=lambda x: x['age'])
print(l)
```



6.看代码叙说,两种方式的区别

```
lst = [1,2,3,5,9,12,4]
lst.reverse()
print(lst) # 在原列表进行修改

print(list(reversed(lst))) # 新建新的列表
```

7.求结果(面试题)

```
v = [lambda :x for x in range(10)]
print(v) # [内存地址1，内存地址2，……，内存地址10]
print(v[0]) # 内存地址1
print(v[0]()) # 9
```

```python
v = []
for x in range(10):
    def func():
        return x
    v.append(func)
print(v)
print(v[0])
print(v[0]())
```



8.求结果(面试题)

```
v = (lambda :x for x in range(10))
print(v) # 生成器内存地址
print(v[0]) # 报错了，生成器不能使用索引
print(v[0]()) # 报错， 同上
print(next(v)) # 匿名函数内存地址
print(next(v)()) # 0
```

```python
def func():
    for x in range(10):
        def foo():
            return x
        yield foo
v = func()
print(next(v))
print(next(v)())

print([i for i in v])
```



9.map(str,[1,2,3,4,5,6,7,8,9])输出是什么? (面试题)

```python
map(str,[1,2,3,4,5,6,7,8,9]) # map对象 内存地址
print(map(str,[1,2,3,4,5,6,7,8,9])) #  内存地址
print(list(map(str,[1,2,3,4,5,6,7,8,9])))
```



10.有一个数组[34,1,2,5,6,6,5,4,3,3]请写一个函数，找出该数组中没有重复的数
的总和（上面数据的没有重复的总和为1+2+34=40)(面试题)



```python
lst = [34,1,2,5,6,6,5,4,3,3]
def sun_unique(lst):
    return sum([i for i in lst if lst.count(i) == 1])
print(sum_unique(lst))
```



11.求结果：（面试题）

```
def num():
    return [lambda x:x**i for i in range(4)]
print([m(2)for m in num()]) #[8, 8, 8, 8]
```

1. 

看代码写结果：

```
def wrapper(f):
    def inner(*args, **kwargs):
        print(111)
        ret = f(*args, **kwargs)
        print(222)
        return ret

    return inner


def func():
    print(333)


print(444) # 444
func() # 333
print(555) # 555
```

1. 

编写装饰器, 在每次执行被装饰函数之前打印一句’每次执行被装饰函数之前都得先经过这里’。

```python
def wrapper(func):
    def inner(*args, **kwargs):
        print('每次执行被装饰函数之前都先经过这里')
        ret = func(*args, **kwargs)
        return ret
    return inner
@wrapper
def test(a):
    print('hello world')
    return a
print(test('suprise'))
```



为函数写一个装饰器，把函数的返回值 + 100然后再返回。

```
@wrapper
def func():
    return 7


result = func()
print(result)
```

```python
def wrapper(foo):
    def inner(*args, **kwargs):
        ret = foo(*args, **kwargs)
        return ret + 100
    return inner

@wrapper
def func():
    return 7

result = func()
print(result)
         
```



请实现一个装饰器，通过一次调用使被装饰的函数重复执行5次。

```python
def wrapper(func):
    def inner(*args, **kwargs):
        for i in range(5):
            func(*args, **kwargs)
    return inner

@wrapper
def foo():
    print('我在运行拉')
foo()
```



请实现一个装饰器，每次调用函数时，将被装饰的函数名以及调用被装饰函数的时间节点写入文件中。

```
可用代码：
import time
struct_time = time.localtime()
print(time.strftime("%Y-%m-%d %H:%M:%S", struct_time))  # 获取当前时间节点


def func():
    print(func.__name__)


函数名通过： 函数名.__name__获取。
```

```python
import time
struct_time = time.localtime()
print(time.strftime("%F-%m-%d %H:%M:%S",struct_time))
def wrapper(foo):
    def inner(*args, **kwargs):
        foo()
        s = f'\n{func.__name__}|{time.strftime("%F-%m-%d %H:%M:%S,struct_time")}'
        with open('log','a',encoding='utf-8') as f:
            f.write(s)
    return inner

@wrapper
def func():
    print(func.__name__)

func()
```

