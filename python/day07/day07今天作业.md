# day07今天作业



1.看代码写结果

```
v1 = [1,2,3,4,5]
v2 = [v1,v1,v1]
v1.append(6)
print(v1) #[1,2,3,4,5,6]
print(v2) #[[1,2,3,4,5,6,],[1,2,3,4,5,6],[1,2,3,4,5,6]]
```

2.看代码写结果

```
v1 = [1,2,3,4,5]
v2 = [v1,v1,v1]
v2[1][0] = 111
v2[2][0] = 222
print(v1) # [222,2,3,4,5]
print(v2) # [[222,2,3,4,5],[222,2,3,4,5],[222,2,3,4,5]]
```

3.看代码写结果，并解释每一步的流程。

```
v1 = [1,2,3,4,5,6,7,8,9]
v2 = {}
for item in v1:  # 迭代v1列表
    if item < 6: # 如果元素小于6
        continue  #跳出循环，不进行任何其它操作
    if 'k1' in v2:  #如果v2中有名字为“k1”的键
        v2['k1'].append(item) #就把元素放到字典v2的‘k1’的键对应的值所表示的列表中
    else: #如果字典中没有名字为‘k1’的键
        v2['k1'] = [item] #就创建一个‘k1’键，它对应的值是一个列表，列表中装着元素
print(v2)  #{'k1': [6,7,8,9]}
```

4.简述赋值和深浅拷贝？

```python
赋值：将多个变量指向同一个值对应的内存地址
浅拷贝：只拷贝最外层元素的内存地址
深拷贝：对于可变元素，会新开辟内存空间，对于不可变元素，共用内存地址
```



5.看代码写结果

```
import copy
v1 = "alex"
v2 = copy.copy(v1)
v3 = copy.deepcopy(v1)
print(v1 is v2) # 浅拷贝 True
print(v1 is v3) # 虽然是深拷贝，但字符串不可变，还是 True
```

6.看代码写结果

```
import copy
v1 = [1,2,3,4,5]
v2 = copy.copy(v1)
v3 = copy.deepcopy(v1)
print(v1 is v2) # False
print(v1 is v3) #False
```

7.看代码写结果

```
import copy
v1 = [1,2,3,4,5]
v2 = copy.copy(v1)
v3 = copy.deepcopy(v1)

print(v1[0] is v2[0]) #True
print(v1[0] is v3[0]) #True
print(v2[0] is v3[0])# True
```

8.看代码写结果

```
import copy

v1 = [1,2,3,4,[11,22]]
v2 = copy.copy(v1)
v3 = copy.deepcopy(v1)

print(v1[-1] is v2[-1]) # True
print(v1[-1] is v3[-1]) # False
print(v2[-1] is v3[-1]) # False
```

9.看代码写结果

```
import copy

v1 = [1,2,3,{"name":'太白',"numbers":[7,77,88]},4,5]
v2 = copy.copy(v1)

print(v1 is v2) #False
 
print(v1[0] is v2[0])  #Ture
print(v1[3] is v2[3]) #True


print(v1[3]['name'] is v2[3]['name']) # True
print(v1[3]['numbers'] is v2[3]['numbers']) # True
print(v1[3]['numbers'][1] is v2[3]['numbers'][1]) # True
```

10.看代码写结果

```
import copy
v1 = [1,2,3,{"name":'太白',"numbers":[7,77,88]},4,5]
v2 = copy.deepcopy(v1)
print(v1 is v2) #False
print(v1[0] is v2[0]) # True
print(v1[3] is v2[3]) # False

print(v1[3]['name'] is v2[3]['name']) # True
print(v1[3]['numbers'] is v2[3]['numbers']) #False
print(v1[3]['numbers'][1] is v2[3]['numbers'][1]) #True

```

11.请说出下面a,b,c三个变量的数据类型。
a = ('太白金星')
b = (1,)
c = ({'name': 'barry'})

```python
a = ('太白金星') # 字符串 str
b = (1,) #元组tuple
c = ({'name': 'barry'}) #字典 dict

```



12.按照需求为列表排序：

```
l1 = [1, 3, 6, 7, 9, 8, 5, 4, 2]
# 从大到小排序
l1.sort()
print(l1)
# 从小到大排序
l1.sort(reverse=True)
print(l1)

# 反转l1列表
print(l1[::-1])
l1.reverse()
print(l1)

```

13.利用python代码构建一个这样的列表(升级题)：

```
[['_','_','_'],['_','_','_'],['_','_','_']]
lst = []
ls =[lst,lst,lst]
for i in range(3):
	lst.append("_")
print(ls)
	
```

14.看代码写结果：

```
l1 = [1,2,]
l1 += [3,4]
print(l1) #[1,2,3,4]
```

15.看代码写结果：

```
dic = dict.fromkeys('abc',[])
dic['a'].append(666)
dic['b'].append(111)
print(dic)  #{'a':[666,111],"b":[666,111],"c":[666,111]}
```

16.l1 = [11, 22, 33, 44, 55]，请把索引为奇数对应的元素删除

```python
l1 = [11, 22, 33, 44, 55]
l2 = l1.copy()
for i in range(len(l2)):
    if i % 2 == 1:
        l1.remove(l2[i])
print(l1)

```



17.dic = {'k1':'太白','k2':'barry','k3': '白白', 'age': 18} 请将字典中所有键带k元素的键值对删除.

```python
dic = {'k1': '太白', 'k2': 'barry', 'k3': '白白', 'age': 18}
dic1 = dic.copy()
for i in dic1:
    if "k" in i:
        del dic[i]
print(dic)

```

```python
dic = {'k1': '太白', 'k2': 'barry', 'k3': '白白', 'age': 18}
dic1 = dic.copy()
for i in dic1:
    if "k" in i:
        dic.pop(i )
print(dic)

```



18.完成下列需求：
s1 = '宝元'
将s1转换成utf-8的bytes类型。
将s1转化成gbk的bytes类型。

```python
s1 = '宝元'
#将s1转换成utf-8的bytes类型。
print(s1.encode("utf-8"))
#将s1转化成gbk的bytes类型。
print(s1.encode("gbk"))
```

b = b'\xe5\xae\x9d\xe5\x85\x83\xe6\x9c\x80\xe5\xb8\x85'
b为utf-8的bytes类型，请转换成gbk的bytes类型。

```python
b = b'\xe5\xae\x9d\xe5\x85\x83\xe6\x9c\x80\xe5\xb8\x85'
# b为utf-8的bytes类型，请转换成gbk的bytes类型。
a = (b.decode("utf-8"))
print(a.encode("gbk"))
```



19.用户输入一个数字，判断一个数是否是水仙花数。
    水仙花数是一个三位数, 三位数的每一位的三次方的和还等于这个数. 那这个数就是一个水仙花数,
    例如: 153 = 1**3 + 5**3 + 3**3

```python
num = input("请输入数字")
if num.isdecimal() and int(num) > 0:
    num = int(num)
    first = num % 10
    second = num // 10 % 10
    third = num // 100
    if num == fi
    rst ** 3 + second **3 +third ** 3:
        print("这是水仙花数")
    else:
        print("这不是水仙花数")
else:
    print("输入有误，请重新输入")
```



20.把列表中所有姓周的⼈的信息删掉(此题有坑, 请慎重):
    lst = ['周⽼⼆', '周星星', '麻花藤', '周扒⽪']
    结果: lst = ['麻花藤']

```python
lst = ['周⽼⼆', '周星星', '麻花藤', '周扒⽪']
lis = lst.copy()
for i in lis:
    if "周" in i:
        lst.remove(i)
print(lst)

```



21.车牌区域划分, 现给出以下车牌. 根据车牌的信息, 分析出各省的车牌持有量. (选做题)
cars = ['鲁A32444','鲁B12333','京B8989M','⿊C49678','⿊C46555','沪 B25041']
locals = {'沪':'上海', '⿊':'⿊⻰江', '鲁':'⼭东', '鄂':'湖北', '湘':'湖南'}
结果: {'⿊⻰江':2, '⼭东': 2, '上海': 1}



```python
cars = ['鲁A32444', '鲁B12333', '京B8989M', '⿊C49678', '⿊C46555', '沪 B25041']
locals = {'沪': '上海', '⿊': '⿊⻰江', '鲁': '⼭东', '鄂': '湖北', '湘': '湖南'}
result = {}
for i in cars:
    if i[0] in locals:
        if locals[i[0]] in result:
            result[locals[i[0]]] += 1
        else:
            result[locals[i[0]]] = 1
print(result)


```

```python
result = {}
for i in cars:
    if i[0] in locals:
        result[locals[i[0]]] = result.get(locals[i[0]], 0) + 1    # 这一步很精妙，少了个判断
print(result)
```

