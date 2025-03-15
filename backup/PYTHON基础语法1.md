

> [!important] ## 基础知识  




## 输入输出
+ input()函数：
	+ 变量，列表[]， 字符，字符串，
	+ 嵌套函数
		+ int()——转化整数int(input())
		+ ord()——转化ASCII码值 ord(input())
	+ 换行 input("请输入： \n")
+ 
+ 《python速查手册 基础卷》
	+ 需要反复阅读部分：P7~P8，P20，P22自己写一遍
	+ 

## 1.1 print玩法
- 三角形函数
```a,b,c = map(int,input("请输入三角形的三条变长,用空格间隔：").split())

if a+b>c and a+c>b and b+c>a:

    ans = "can be a triangle"

    if a==b and b==c:

        print("can be a equilateral triangle")

    elif a==b or b==c or a==c:

        print("can be a isosceles triangle")

        if a*a+b*b==c*c or b*b+c*c==a*a or c*c+a*a==b*b:

            print("can be a right triangle")

        else:

            print("can be a triangle")

    else:

        print("can be a normal triangle")

else:

    print("can not be a triangle")
```


+ 如何插入代码块
```
name="ada love & peace"  
```
name="ada love & peace"  
# title 函数是改变首字母大小写  
```
print(name.title())  
```
print(name.title())  
# upper函数是全部改为大写  
```
print(name.upper())  
```
print(name.upper())  
# lower函数是全部改为小写  
```
print(name.lower())  
```
print(name.lower())  
# 在字符串中使用变量,
注意变量赋值要有“”，使用f函数应是“{} {}”的结构，f是format函数的缩写  
```
first_name="ada"  
last_name="lovelace"  
full_name=f"{first_name} {last_name}"  
print(full_name)
print(f"x is {x}, y is {y}, name is {', '.join(name)}, a is {a}, b is {b}")
```
# f函数里面可以插入字符串 
可以嵌套“”的字符串结构，比如“hello”“，" "!"  
```
print(f"Hello, {full_name.title()}!!")  
```
# f字符串来创建消息  
```
message=f"HELLO, {full_name.upper()}! AD."  
print(message)  
```
# 字符串添加制表位
\t,注意第二个print和第三个print之间的区别，帮助我们了解格式化字符串的应用  
```
message=f"HELLO, {full_name.upper()}! AD & CONGTOU."  
print(message)  
print("\t message")  
print(f"\t{message}")  
```
  
# 字符串增加\t和\n的变形  
```
print(f"languages:\n
Python\nC\n{message}!")  
print(f"languages:\n\tPython\n\tC\n\t{message}!")  
```
  
# 字符串删除空白，
利用rstrip()可以批量删除空白  
```
favorite_language="python "  
favorite_language=favorite_language.rstrip()  
print(f"\t{favorite_language}!~~~!")  
```
  
# 字符串删除不同的空白形式，
可以采用rstrip，lstrip，strip不同的形式  
```
favorite_language=" python "  
favorite_language=favorite_language.lstrip()  
print(f"\t{favorite_language}!~~~!")  
  
favorite_language=" python "  
favorite_language=favorite_language.rstrip()  
print(f"\t{favorite_language}!~~~!")  
  
favorite_language=" python "  
favorite_language=favorite_language.strip()  
print(f"\t{favorite_language}!~~~!")  
```
  
# 变量反复的赋值和调用非常麻烦，
repr()是Python中的一个内置函数，它返回一个对象的“官方”字符串表示，也就是说，这个字符串表示  
通常可以用来重新创建该对象。当你调用repr()函数时，Python会尝试找到一个字符串，该字符串在传递给内置的eval()函数时，  能够产生和原始对象相同的对象。  
+ repr()的主要用途是调试和开发。它生成的字符串通常包含更多关于对象的信息，有时甚至是该对象的有效Python表达式。  
```
favorite_language="    python    "  
print(repr(favorite_language).rstrip())  
print(repr(favorite_language).strip()) 
``` 
# 括号取得不一样，
结果差别很大。注意括号的位置,repr可以调用原始变量  
```
print(repr(favorite_language.rstrip()))  
print(favorite_language)  
print(repr(favorite_language))  
print(repr(favorite_language.lstrip()))  
print(repr(favorite_language.strip())) 
``` 
  
# 删除前缀  
```
nostarch_url="http://nostarch.com"  
print(nostarch_url.removeprefix("http://"))
```

## 第五章 列表
# 课程5.4 if语句处理列表  
```
print("使用if处理列表")  
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']  
for requested_topping in requested_toppings:  
    print(f"Adding {requested_topping}.")  
print("\nFinished making your pizza!")
```

+ 列表循环调用，嵌套if语句进行判断，最后输出
```
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']  
for requested_topping in requested_toppings:  
    if requested_topping == 'green peppers':  
        print("Sorry, we are out of green peppers right now.")  
    else:  
        print(f"Adding {requested_topping}.")  
print("\nFinished making your pizza!")
```


+ 多个列表
```
print("使用多个列表")  
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']  
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']  
for requested_topping in requested_toppings:  
    if requested_topping in available_toppings:  
        print(f"Adding {requested_topping}.")  
    else:  
        print(f"Sorry, we don't have {requested_topping}.")  
print("\nFinished making your pizza!")
```

+ 不错的案例，关于如何判断用户是否注册了
	+ 这个名义上2个列表，实际都生成了user.lower的2个小写列表，相当于四个列表在里面参与计算。
```
# 当前已有的用户列表  
current_users = ['user1', 'admin', 'user3', 'user4', 'user5']  
  
# 希望注册的新用户列表  
new_users = ['user6', 'Admin', 'user7', 'User3', 'user8']  
  
# 创建一个包含current_users中用户名的小写版本的新列表,这个很重要！！！！确保比较时，不区分大小写。要多看几次！！！  
current_users_lower = [user.lower() for user in current_users]

# 遍历新用户列表，检查每个用户名是否已被使用  
for new_user in new_users:  
    if new_user.lower() in current_users_lower:  
        print(f"Username '{new_user}' has already been used. Please enter a different username.")  
    else:  
        print(f"Username '{new_user}' is available.")
```


## 六、列表
### 6.1 列表的基本操作
+ 列表的定义和读值
```
print("一个简单的字典")  
alien_0 = {'color': 'green', 'points': 5}  
print(alien_0['color'])  
print(alien_0['points'])  
  
new_points = alien_0['points']  
print(f"You just earned {new_points} points!")
```
+ 列表新增键值对
```
print("添加键对值")  
alien_0 = {'color': 'green', 'points': 5}  
print(alien_0)  
alien_0['x_position'] = 0   # 直接新增键值对  
alien_0['y_position'] = 25  # 直接新增第二组键值对  
print(alien_0)

# 6.2.4 修改字典中的值  
print("修改字典中的值")  
alien_0 = {'color': 'green'}  
print(f"The alien is {alien_0['color']}.")  
alien_0['color'] = 'yellow'     # 直接修改值  
print(f"The alien is now {alien_0['color']}.")
```

+ 字典中键值对的提取，计算的综合应用
```
#*** 非常好的例子，通过修改外星人字典的值，改变外星人的行为，通过调整speed，改变x_position的表现  
alien_0 = {'x_position': 0, 'y_position': 25, 'speed': 'medium'}  
print(f"Original position: {alien_0['x_position']}")   # 读字典初始值，original position不是新增变量，只是字符串，注意了  
 # 向右移动外星⼈  
 # 根据当前速度确定将外星⼈向右移动多远  
if alien_0['speed'] == 'slow':     # if语句+字典键对值提取+布尔表达式判定  
    x_increment = 1                # 新增变量，作为x_position的增量  
elif alien_0['speed'] == 'medium':  
    x_increment = 2  
else:  
 # 这个外星⼈的移动速度肯定很快  
    x_increment = 3  
 # 新位置为旧位置加上移动距离  
alien_0['x_position'] = alien_0['x_position'] + x_increment   #字典中的键对值的值是可以进行运算的。  
print(f"New position: {alien_0['x_position']}")
```


## 练习 6.1print("练习6.1")  
+ 遍历字典，提取key和value
```
person = {  
    'first_name': 'John',  
    'last_name': 'Doe',  
    'age': 30,  
    'city': 'New York'  
}  
  
# 遍历字典并打印每项信息  
for key, value in person.items():  
    print(f"{key}: {value}")
```

+ 提取key和value的语法，应该要熟悉
```
print("6.3 遍历字典")  
# 遍历所有的键对值  
favorite_languages = {  
 'jen': 'python',  
 'sarah': 'c',  
 'edward': 'rust',  
 'phil': 'python',  
 }  
for name, language in favorite_languages.items():  
    print(f"{name.title()}'s favorite language is {language.title()}.")
```

## 遍历字典中的所有键！！ .key()

```
print("遍历字典中的所有键-2！！")  
favorite_languages = {                  # 定义字典  
    'jen': 'python',  
    'sarah': 'c',  
    'edward': 'rust',  
    'phil': 'python',  
 }  
friends = ['phil', 'sarah']              # 新增一个列表friends  
for name in favorite_languages.keys():   # for循环，读取字典的键进入变量name  
    print(f"Hi {name.title()}.")         # 打印字典的键  
    if name in friends:                  # if语句，判定name在不在friends列表里  
        language = favorite_languages[name].title()     # 读取字典的值，并转化大写进入变量language  
        print(f"\t{name.title()}, I see you love {language}!")    #输出结果，打印出name和language
```


```
print("遍历字典中的所有值")  
favorite_languages = {  
    'jen': 'python',  
    'sarah': 'c',  
    'edward': 'rust',  
    'phil': 'python',  
    }  
print("The following languages have been mentioned:")  
for language in favorite_languages.values():  
    print(language.title())  
# set()集合，帮你找出独一无二的元素  
print("帮你找出独一无二的元素")  
favorite_languages = {  
    'jen': 'python',  
    'sarah': 'c',  
    'edward': 'rust',  
    'phil': 'python',  
    }  
print("The following languages have been mentioned:")  
for language in set(favorite_languages.values()):  
    print(language.title())
```

- 未完待续
