# day09 今天作业

1.整理函数相关知识点,将以前学习知识整理思维导图

2.写函数，检查获取传入列表或元组对象的所有奇数位索引对应的元素，并将其作为新列表返回给调用者。

```python
def odd(container):
    return list(container[::2])
```



3.写函数，判断用户传入的对象（字符串、列表、元组）长度是否大于5。

```python
def bigger_than_5(a):
    if len(a) > 5:
        return True
    else:
        return False
    
  l = ["a", "c", 3, 5]
print(bigger_than_5(l))
```



4.写函数，检查传入列表的长度，如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。

```python
def first_two(l):
    if len(l) > 2:
        l = l[:2]
    return l
lst = [1,2,3,4,5,6]
print(first_two(lst))
```



5.写函数，计算传入函数的字符串中,[数字]、[字母和中文]以及 [其他]的个数，并返回结果。

```python
def num(s):
    result = {"num": 0, "alpha": 0, "other": 0}
    for i in s:
        if i.isdecimal():
            result["num"] += 1
        elif i.isalpha():
            result["alpha"] += 1
        else:
            result["other"] += 1
    return result

s = "ffddjkfhj3489+++---"
print(num(s))
```



6.写函数，接收两个数字参数，返回比较大的那个数字。

```python
def bigger(a, b):
    if a < b:
        return b
    return a

print(bigger(20,1))
```



```python
def bigger(a,b):
    return a if a > b else b


print(bigger(1,2))
    
```



7.写函数，检查传入字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。
dic = {"k1": "v1v1", "k2": [11,22,33,44]}
PS:字典中的value只能是字符串或列表



```python
dic = {"k1": "v1v1", "k2": [11,22,33,44]}
def first_two(dic):
    for k in dic:
        dic[k] = dic[k][:2]
    return dic
        
```



8.写函数，此函数只接收一个参数且此参数必须是列表数据类型，此函数完成的功能是返回给调用者一个字典，此字典的键值对为此列表的索引及对应的元素。例如传入的列表为：[11,22,33] 返回的字典为 {0:11,1:22,2:33}。

```python
lst = [11,22,33] 
def list_dict(lst):
    dic = {}
    for i in range(len(lst)):
        dic[i] = lst[i]
    return dic
print(list_dict(lst))
       
```



9.写函数，函数接收四个参数分别是：姓名，性别，年龄，学历。用户通过输入这四个内容，然后将这四个内容传入到函数中，此函数接收到这四个内容，将内容追加到一个student_msg文件中。

```python
def a_file(name,sex,age,education):
    with open("student_msg","a",encoding="utf-8") as f:
        st = f"姓名：{name} 性别：{sex}, 年龄：{age} 学历：{education}\n"
        f.write(st)
        f.flush()
        
name = input('请输入姓名：')
sex = input('请输入性别：')
age = input('请输入年龄：')
education = input('请输入学历：')

a_file(name, sex, age, education)
```



10.对第9题升级：支持用户持续输入，Q或者q退出，性别默认为男，如果遇到女学生，则把性别输入女。

```python
def a_file(name, age, education, sex="男"):
    with open("student_msg", "a", encoding="utf-8") as f:
        st = f"姓名：{name} 性别：{sex}, 年龄：{age} 学历：{education}\n"
        f.write(st)
        f.flush()


while True:
    name = input("请输入姓名（Q退出)")
    if name.upper() == "Q":
        break
    sex = input("请输入性别（Q退出）")
    if sex.upper() == "Q":
        break
    age = input("请输入年龄 （Q退出）")
    if  age.upper() == "Q":
        break
    education = input("请输入学历 （Q退出）")
    if education.upper() == "Q":
        break
    if sex == "女":
        a_file(name, age, education, sex)
    else:
        a_file(name, age, education)

```



11.写函数，用户传入修改的文件名，与要修改的内容，执行函数，完成整个文件的批量修改操作（选做题）。

```python
import os 
def modification(filename,old,new):
    with open(filename, "r", encoding="utf-8") as f,\
    open("temp","w",encoding="utf-8") as f1:
        for line in f:
            line = line.replace(old,new)
            f1.write(line)
            f1.flush()
    os.rename(filename,filename+".bak")
    os.rename("temp",filename)
modification("a.txt",'3',"a little")
```

