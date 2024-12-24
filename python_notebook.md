# python笔记
## python的安装
1. 前往python.org,下载python3,click add python to path
2. 下载pycharm,安装
3. 点击创建项目
## 第一个python项目
1. 右击项目
2. 创建.py文件
3. 使用print函数
    ```python
    print("hello,world!")
    print('*' * 10)
    ```
python逐行执行,从上到下
## 变量
    ```python
    x=10
    print(x)
    ```
1. 变量的命名规则

    变量名在 Python 中有一定的规则和约定：

   * 变量名只能包含字母、数字和下划线 (_)，但不能以数字开头。
   * 变量名区分大小写，例如<kbd>name</kbd>和<kbd>Name</kbd>是两个不同的变量。
   * 变量名不能是 Python 的保留字（关键字），例如<kbd>if</kbd>、<kbd>else</kbd>、<kbd>for</kbd> 等。
2. 赋值操作

    在 Python 中，赋值是通过 = 运算符完成的。例如：
    ```python
    x = 10
    y = 20
    ```
3. 变量类型

    Python 是一种动态类型语言，意味着变量的类型在运行时由解释器根据赋给变量的值自动推断，而不需要显式声明类型。常见的变量类型包括：

   1. 整数 (int)：用于存储整数值。
        ```python
        age = 25
        ```
   2. 浮点数 (float)：用于存储带有小数部分的数字。
        ```python
        price = 19.99
        ```
   3. 字符串 (str)：用于存储文本数据。
        ```python
        name = "Alice"
        ```
   4. 布尔值 (bool)：用于存储 True 或 False。
        ```python
        is_active = True
        ```
   5. 列表 (list)：用于存储多个元素，元素可以是不同类型。
        ```python
        fruits = ["apple", "banana", "cherry"]
        ```
   6. 字典 (dict)：用于存储键值对。
        ```python
        person = {"name": "Alice", "age": 25}
        ```
   7. 元组 (tuple)：与列表类似，但元组是不可变的。
        ```python
        coordinates = (10, 20)
        ```
   8. 集合 (set)：用于存储唯一元素的集合。
        ```python
        unique_numbers = {1, 2, 3, 4}
        ```
## input函数
    ```python
    name=input('what is your name? ')
    print('Hi' + name)
    ```
    eg:

    ```python
    name=input('what is your name? ')
    favourite_color=input('what is your favourite color?')
    print(name + 'likes' + favourite_color)
    ```
## 类型转换
```python
#input输入的都是字符串
birth_year=input('Birth year: ')
#可以通过int()类型转换
birth_year=int(input('Birth year: '))
#可以通过type()查看类型
print(type(birth_year))
age=2019-int(birth_year)
print(type(age))
print(age)
```
eg:
```python
weight_lbs=input('weight(lbs): ')
weight_kg=int(weight_lbs) * 0.45
print(weight_kg)
```
## 字符串
```python
#在python中双引号单引号表示字符串都可以,但在想输出单引号时就用双引号来表示,同样想输出双引号就用单引号表示
course="python's course for beginners"
course='python course for "beginers"'
print(course)
#多行输出时用'''来输出
course='''
hi john
thank you 
the support team
'''
#取字符串字母用数组的方法
course="python's course for beginners"
#下标从0开始,-1代表最后一个
print(course[0])
print(course[-1])
#[start:end:step]表示从几位取到end-1位,左闭右开,step代表每隔几个step元素取一个值
name= 'Jennifer'
print(name[1:-1]) #这里输出就是ennife,r取不到
```
***常用字符串方法:***
***
**基本操作方法:**
* ***len(s)
返回字符串的长度（字符数）。***
    
```python
s = "Hello"
print(len(s))  # 输出: 5
```
* ***str.lower()
返回字符串的小写版本。***
```python
s = "Hello World"
print(s.lower())  # 输出: "hello world"
```
* ***str.upper()
返回字符串的大写版本。***
```python
s = "Hello World"
print(s.upper())  # 输出: "HELLO WORLD"
```
* ***str.capitalize()
返回字符串的首字母大写，其余字母小写。***
```python
s = "hello world"
print(s.capitalize())  # 输出: "Hello world"
```
* ***str.title()
返回标题化的字符串（每个单词的首字母大写）。***
```python
s = "hello world"
print(s.title())  # 输出: "Hello World"
```
* ***str.strip()
去除字符串两侧的空白字符（默认空格、换行符等）。***
```python
s = "  Hello World  "
print(s.strip())  # 输出: "Hello World"
```
***
**查找和替换:**
* ***str.find(sub)
返回子字符串 sub 第一次出现的位置，如果未找到返回 -1。***
```python
s = "Hello World"
print(s.find("World"))  # 输出: 6
print(s.find("Python"))  # 输出: -1
```
* ***str.index(sub)
返回子字符串 sub 第一次出现的位置，如果未找到则引发 ValueError。***
```python
s = "Hello World"
print(s.index("World"))  # 输出: 6
```
* ***str.replace(old, new)
将字符串中的 old 替换为 new，并返回新的字符串。***
```python
s = "Hello World"
print(s.replace("World", "Python"))  # 输出: "Hello Python"
```
* ***str.count(sub)
统计子字符串 sub 在字符串中出现的次数。***
```python
s = "Hello Hello World"
print(s.count("Hello"))  # 输出: 2
```
***
**格式化方法:**
* <kbd>f-string</kbd>（Python 3.6+）
更简洁的格式化方法，使用大括号 {} 和 f 前缀。
```python
name = "Alice"
age = 30
s = f"My name is {name} and I am {age} years old."
print(s)  # 输出: "My name is Alice and I am 30 years old."
```
***
**字符检测和检查:**
* str.isdigit()
判断字符串是否由数字字符组成。
```python
s = "12345"
print(s.isdigit())  # 输出: True
```
* str.isalpha()
判断字符串是否仅包含字母字符。
```python
s = "Hello"
print(s.isalpha())  # 输出: True
```
* ***str.islower()
判断字符串是否全为小写字母。***
```python
s = "hello"
print(s.islower())  # 输出: True
```
* ***str.isupper()
判断字符串是否全为大写字母。***
```python
s = "HELLO"
print(s.isupper())  # 输出: True
```
* ***str.startswith(prefix)
判断字符串是否以指定的 prefix 开头。***
```python
s = "Hello World"
print(s.startswith("Hello"))  # 输出: True
```
* ***str.endswith(suffix)
判断字符串是否以指定的 suffix 结尾。***
```python
s = "Hello World"
print(s.endswith("World"))  # 输出: True
```
***
**字符串拆分和连接:**
* ***str.split(sep)
将字符串根据分隔符 sep 拆分成多个子字符串，返回一个列表。如果未指定 sep，默认以空格为分隔符。***
```python
s = "Hello World Python"
print(s.split())  # 输出: ['Hello', 'World', 'Python']
print(s.split(" "))  # 输出: ['Hello', 'World', 'Python']
```
* ***str.join(iterable)
将可迭代对象中的元素连接成一个字符串，元素之间使用原字符串作为分隔符。***
```python
words = ["Hello", "World", "Python"]
print(" ".join(words))  # 输出: "Hello World Python"
```
## 格式化字符串
```python
first='John'
last='Smith'
#格式话字符串用f''或f""里面{}引用变量
msg=f'{first} {last} is a coder' #输出 john smith is a coder
```
## 算术运算符
1. 加法:+
```python
x=10
#以下方法同样使用,也适用于其他运算符
x+=3
```
2. 减法:-
3. 乘法:*
4. 除法:/
```python
a = 5
b = 2
result = a / b  # 结果为 2.5
```
5. 取整除://
```python
a = 5
b = 2
result = a // b  # 结果为 2
```
6. 取余:%
```python
a = 5
b = 2
result = a % b  # 结果为 1
```
7. 幂运算:**
```python
a = 5
b = 2
result = a ** b  # 结果为 25 (5的2次方)
```
**运算优先级**
运算符优先级表
|运算符|描述|优先级|
|:--:|:--:|:--:|
|<kbd>**</kbd>|幂运算|最高|
|<kbd>+x</kbd>,<kbd> -x</kbd>,<kbd> ~x</kbd>|一元加法、减法、按位取反|高|
|<kbd>*</kbd>,<kbd> /</kbd>, <kbd>//</kbd>,<kbd>%</kbd>|乘法、除法、取整除、取余|中等|
|<kbd>+</kbd>,<kbd>-</kbd>|加法、减法|低|
|<kbd>= (赋值运算符)</kbd>|赋值操作|最低|
结合性说明:

    乘法 (*)、除法 (/) 等是左结合的，因此在有多个乘法或除法运算时，它们从左到右依次执行。
    幂运算 (**) 是右结合的，因此在有多个幂运算时，它们从右到左依次执行。例如：2 ** 3 ** 2 会先计算 3 ** 2，然后再计算 2 ** 9。

在 Python 中，幂运算的优先级最高，而加法和减法的优先级最低。其他算术运算符如乘法、除法、取余等按顺序从高到低排列。如果要明确控制计算顺序，可以使用括号来改变默认的优先级计算顺
## 数学函数