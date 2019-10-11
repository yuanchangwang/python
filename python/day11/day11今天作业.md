



# day11今天作业

项目分析：
1．首先程序启动，显示下面内容供用户选择：

```
1.请登录
2.请注册
3.进入文章页面
4.进入评论页面
5.进入日记页面
6.进入收藏页面
7.注销账号
8.退出整个程序
```

```python
msg ="""
1.请登录
2.请注册
3.进入文章页面
4.进入评论页面
5.进入日记页面
6.进入收藏页面
7.注销账号
8.退出整个程序
"""
ddic = {
    '1': login,
    '2': register,
    '3': article,
    '4': comment,
    '5': diary,
    '6': collect,
    '7': logout,
    '8': quit_blog,
}
inp = f'{input(msg)}'
```



2．必须实现的功能：

```
1.注册功能要求：
a.用户名、密码要记录在文件中。
b.用户名要求：不能有特殊字符并且确保用户名唯一。
c.密码要求：长度要在6~14个字符之间。

2.登录功能要求：
a.用户输入用户名、密码进行登录验证。
b.登录成功之后，才可以访问3 - 7选项，如果没有登录或者登录不成功时访问3 - 7选项，不允许访问,提示用户进行登录!
c.超过三次登录还未成功，则退出整个程序。
```

1. 注册

```python
name_list = []
user_info = []
while True:
    usr_name = input("请输入用户名：[Q退出]").strip()
    if usr_name.upper() == "Q":
        break
    elif usr_name in name_list:
        print('用户名与存在，请重新输入！')
    elif not usr_name.isalnum():
        print("用户名中不能存在特殊字符")
     else:
        pwd = input("请输入密码：")
        pwd = pwd.replace(" ","")
        if 6 < len(pwd) < 14:
            name_list.append(usr_name) # 添加用户名
            user_info.append({"name": usr_name, 'pwd':pwd}) # 添加用户名和密码
            print("注册成功")
        else:
            print("密码长度要在6~14个字符之间")
            

with open("user_info",)            
print(name_list)
print(user_info)
            
            
    
```

1. 升级函数

```python
def register():

while True:
    usr_name = input("请输入用户名：[Q退出]").strip()
    if usr_name.upper() == "Q":
        break
    elif usr_name in name_list:
        print('用户名与存在，请重新输入！')
    elif not usr_name.isalnum():
        print("用户名中不能存在特殊字符")
     else:
        pwd = input("请输入密码：")
        pwd = pwd.replace(" ","")
        if 6 < len(qwd) < 14:
            name_list.uppend(uer_name) # 添加用户名
            user_info.append({"name": usr_name, 'pwd':pwd}) # 添加用户名和密码
            print("注册成功")
        else:
            print("密码长度要在6~14个字符之间")
            
name_list = []
user_info = []
register()

print(name_list)
print(user_info)
            
            
    
    
```

```python
user_info = []
```



3.进入文章页面要求：
提示欢迎xx进入文章页面。(xx是当前登录的用户名)

4.进入评论页面要求：

​	提示欢迎xx进入评论页面

5.进入日记页面要求：
提示欢迎xx进入日记页面。

6.进入收藏页面要求：
提示欢迎xx进入收藏页面。

7.注销账号要求：
不是退出整个程序，而是将已经登录的状态变成未登录状态（在次访问3~7选项时需要重新登录）

8.退出整个程序要求：
就是结束整个程序

四.用代码实现三次用户登录及锁定(选做题,这是一个单独的程序)
项目分析:
一.首先程序启动,显示下面内容供用户选择:
1.注册
2.登录

a.用户选择登录的时候,首先判断用户名在userinfo.txt表中存在不在,存在就不能进行注册
b.当注册的用户名不存在的时候将用户名和密码写入到userinfo.txt文件中
c.用户选择登录的时候,判断用户输入的账号和密码是否userinfo.txt存储的一致
d.用户名和密码一致就终止循环,并提示用户登录成功!
e.用户名和密码不一致,只有三次登录机会,三次过后提示用户名被锁定,请联系管理员!并终止循环
f.当用户名错误三次,再次运行程序.登录锁定的账号继续提示用户名被锁定,请联系管理员!

```python
import os

def login():
    global login_status, q
    while True:
        if login_status:
            print("你已经登录成功，不必再次登录！")
        else:
            user_name = input("请输入用户名[Q退出]")
            if user_name.upper() == "Q":
                pass
            else:
                pwd = input('请输入密码')
                if user_name in name_list:
                    i = name_list.index(user_name)
                    if user_info[i]['count'] == '0':
                        print('你的账号已经被冻结，请联系管理员!')
                    elif pwd == user_info[i]['pwd']:
                        login_status = True
                    else:
                        user_info[i]['count'] = str(int(user_info[i]['count'])-1)
                        file_write()
                        if user_info[i]['count'] == '0':
                            print('你的账号已经被冻结，请联系管理员！')
                            q = True
                        else:
                            print(f'你输入的密码有误，还有{user_info[i]["count"]}次机会')
                            continue
        break


def register():
    while True:
        usr_name = input("请输入用户名[q退出]：").strip()
        if usr_name.upper() == 'Q':
            break
        elif usr_name in name_list:
            print("用户名已经存在，请重新输入")
        elif not usr_name.isalnum():
            print("用户名中不能存在特殊字符")
        else:
            pwd = input("请输入密码：").strip()
            pwd = pwd.replace(" ", '')
            if 6 < len(pwd) < 14:
                user_info.append({"name": usr_name, "pwd": pwd, "count": "3"})
                file_write()
                print('注册成功')
                break
            else:
                print("密码长度要在6-14个字符之间！")



def article():
    if login_status:
        print("欢迎进入文章")
    else:
        print("你还没有登录")
        login()

def comment():
    if login_status:
        print('欢迎进入评论区')
    else:
        print('你还没有登录，请登录')
        login()

def diary():
    if login_status:
        print('欢迎进入评论区')
    else:
        print('你还没有登录，请登录')
        login()

def collect():
    if login_status:
        print('欢迎进入收藏区')
    else:
        print('你还没有登录，请登录')
        login()

def logout():
    global login_status
    login_status = False
    print('你已成功注销账户')

def quit_blog():
    global q
    q = True
    print('退出成功，欢迎下次再来')

def file_write():
    with open('temp', 'w', encoding="utf-8") as f1:
        for j in user_info:
            f1.write(f'{j["name"]} {j["pwd"]} {j["count"]}\n')
            f1.flush()
    if 'userinfo.bak' in os.listdir("."):
        os.remove('userinfo.bak')
    os.rename('user_info', 'userinfo.bak')
    os.rename('temp', 'user_info')



msg = """1.请登录
2.请注册
3.进入文章页面
4.进入评论页面
5.进入日记页面
6.进入收藏页面
7.注销账号
8.退出整个程序
请输入您要选择项目的序号："""

dic = {
    '1': login,
    '2': register,
    '3': article,
    '4': comment,
    '5': diary,
    '6': collect,
    '7': logout,
    '8': quit_blog,
}

q = False

login_status = False
user_info = []

with open('user_info', 'r', encoding='utf-8') as f:
    for i in f:
        user_info_dict = {'name': i.split()[0], 'pwd': i.split()[1], "count": i.split()[2]}
        user_info.append(user_info_dict)
name_list = []
for i in user_info:
    name_list.append(i["name"])
while not q:
    choose = input(msg)
    if choose in dic:
        dic[choose]()
    else:
        print("输入的内容有误，请重新输入")

```

