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
***
```python
#inf表示无穷大,类型为float
a = float('inf')  # 正无穷大
b = float('-inf') # 负无穷大
print(type(float('inf')))  # 输出 <class 'float'>
```
***
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
首先需要导入 math 模块：
```python
import math
```
**常用数学函数**
1. 数学常数
* <kbd>math.pi</kbd> — 圆周率(π)
* <kbd>math.e</kbd> — 自然常数(e)
```python
import math
print(math.pi)  # 输出：3.141592653589793
print(math.e)   # 输出：2.718281828459045
```
2. 幂与对数
* <kbd>math.pow(x, y)</kbd> — 返回x的y次幂
* <kbd>math.sqrt(x)</kbd> — 返回x的平方根
```python
import math
print(math.pow(2, 3))  # 输出:8.0
print(math.sqrt(16))   # 输出:4.0
```
3. 取整和舍入
* <kbd>math.ceil(x)</kbd> — 返回大于或等于x的最小整数
* <kbd>math.floor(x)</kbd> — 返回小于或等于x的最大整数
* <kbd>math.trunc(x)</kbd> — 返回x的整数部分
* <kbd>round(x)</kbd> — 进行四舍五入后,返回x的整数部分
* <kbd>math.fabs(x)</kbd> — 返回x的绝对值
* <kbd>math.factorial(x)</kbd> — 返回x的阶乘(x必须为非负整数)
* <kbd>math.gcd(x, y)</kbd> — 返回x和y的最大公约数
```python
import math
print(math.ceil(3.2))  # 输出：4
print(math.floor(3.8))  # 输出：3
print(math.trunc(3.7))  # 输出：3
print(round(3.7))#输出:4
print(math.fabs(-5))    # 输出：5.0
print(math.factorial(5))  # 输出：120
print(math.gcd(36, 60))  # 输出：12
```
## 条件判断(if语句,match...case)
1. if 语句

     基本的条件判断语法如下：
     ```python
     if condition:
     # 如果条件成立，执行这个代码块
     ```
     示例：判断一个数是否为正数
     ```python
     number = 5
     if number > 0:
     print("这是一个正数")
     ```
2. if...else 语句

     如果 if 的条件不成立，可以使用 else 语句执行另一个代码块。
     ```python
     if condition:
     # 如果条件成立，执行这个代码块
     else:
     # 如果条件不成立，执行这个代码块
     ```
     示例：判断一个数是正数还是负数
     ```python
     number = -3
     if number > 0:
     print("这是一个正数")
     else:
     print("这是一个负数")
     ```
3. if...elif...else 语句

     如果有多个条件需要判断，可以使用 elif 语句，它是 else if 的简写。elif 用于判断多个条件中的一个。如果条件不成立，程序会继续判断下一个 elif 条件。如果没有满足的条件，则执行 else 代码块。
     ```python
     if condition1:
     # 如果条件1成立，执行这部分
     elif condition2:
     # 如果条件1不成立，但条件2成立，执行这部分
     else:
     # 如果所有条件都不成立，执行这部分
     ```
     示例：判断一个数是正数、负数还是零
     ```python
     number = 0
     if number > 0:
     print("这是一个正数")
     elif number < 0:
     print("这是一个负数")
     else:
     print("这是零")
     ```
4. 条件表达式(Ternary Operator)

     Python 支持条件表达式（也叫三元运算符）。它的基本语法为：
     ```python
     value_if_true if condition else value_if_false
     ```
     它在 if 和 else 语句中经常被用来简化代码。
     示例：使用条件表达式
     ```python
     age = 20
     status = "成年人" if age >= 18 else "未成年人"
     print(status)  # 输出：成年人
     ```
4. match...case语句

Python 3.10 增加了<kbd>match...case</kbd>的条件判断，不需要再使用一连串的 if-else 来判断了。
match 后的对象会依次与 case 后的内容进行匹配,如果匹配成功,则执行匹配到的表达式,否则直接跳过,<kbd>_</kbd>可以匹配一切。

基本语法:
```python
match expression:
    case pattern1:
        # 当 expression 匹配 pattern1 时执行的代码
    case pattern2:
        # 当 expression 匹配 pattern2 时执行的代码
    case _:
        # 任何其他情况，通常作为默认情况
```
<kbd>case _</kbd>: 类似于 C 和 Java 中的<kbd>default</kbd>:，当其他 case 都无法匹配时，匹配这条，保证永远会匹配成功。
实例:
```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"

mystatus=400
print(http_error(400))
```
以上是一个输出 HTTP 状态码的实例，输出结果为：
```python
Bad request
```
一个 case 也可以设置多个匹配条件，条件使用<kbd>|</kbd>隔开，例如：
```python
...
    case 401|403|404:
        return "Not allowed"
```
## 逻辑运算符
|运算符|说明|示例|
|:--:|:--:|:--:|
|<kbd>and</kbd>|连接多个条件，**只有所有条件都为真**时，结果为真| `<kbd>x > 5 and y > 10</kbd>` 结果为 `True`，当 `x = 6` 和 `y = 12` 时 |
|<kbd>or</kbd>|连接多个条件，**只要有一个条件为真**，结果就为真| `<kbd>x > 5 or y > 10</kbd>` 结果为 `True`，当 `x = 3` 和 `y = 12` 时 |
|<kbd>not</kbd>|对条件取反，将 `True` 转为 `False`，将 `False` 转为 `True` | `<kbd>not x > 5</kbd>` 结果为 `True`，当 `x = 3` 时 |
|<kbd>in</kbd>|判断一个值是否存在于容器（如列表、字符串等）中| `<kbd>'a' in 'apple'</kbd>` 结果为 `True`|
|<kbd>not in</kbd>|判断一个值是否不存在于容器中| `<kbd>'b' not in 'apple'</kbd>` 结果为 `True`|
|<kbd>is</kbd>|判断两个对象是否是同一个对象（内存地址相同）| `<kbd>a is b</kbd>` 结果为 `True`，当 `a = [1, 2]` 和 `b = a` 时|
|<kbd>is not</kbd>|判断两个对象是否不是同一个对象| `<kbd>a is not b</kbd>` 结果为 `True`，当 `a = [1, 2]` 和 `b = [1, 2]` 时|
## 比较运算符
|运算符|说明|示例|
|:--:|:--:|:--:|
| <kbd>==</kbd>   | **等于**：判断两个值是否相等 | `<kbd>3 == 3</kbd>` 结果为 `True`|
| <kbd>!=</kbd>   | **不等于**：判断两个值是否不相等 | `<kbd>3 != 4</kbd>` 结果为 `True`|
| <kbd>></kbd> | **大于**：判断左边的值是否大于右边的值| `<kbd>5 &gt; 3</kbd>` 结果为 `True`|
| <kbd><</kbd> | **小于**：判断左边的值是否小于右边的值| `<kbd>3 &lt; 5</kbd>` 结果为 `True`|
| <kbd>>=</kbd> | **大于等于**：判断左边的值是否大于或等于右边的值| `<kbd>5 &gt;= 5</kbd>` 结果为 `True` |
| <kbd><=</kbd> | **小于等于**：判断左边的值是否小于或等于右边的值| `<kbd>3 &lt;= 4</kbd>` 结果为 `True`|
| <kbd>is</kbd>    | **身份运算符**：判断两个对象是否是同一个对象（内存地址相同） | `<kbd>a is b</kbd>` 结果为 `True`，当 `a` 和 `b` 指向同一个对象时 |
| <kbd>is not</kbd>| **非身份运算符**：判断两个对象是否不是同一个对象| `<kbd>a is not b</kbd>` 结果为 `True`，当 `a` 和 `b` 指向不同对象时 |
## while循环
Python 的 while 循环用于在条件为 True 时重复执行代码块，直到条件变为 False。
基本语法
```python
while condition:
    # 执行的代码块

    condition：布尔表达式，当为 True 时循环执行。
    # 执行的代码块：每次迭代执行的代码。
```
示例

1. 基本用法：
     ```python
     count = 0
     while count < 5:
     print(count)
     count += 1
     ```
2. 无限循环：
     ```python
     while True:
     print("This will run forever")
     ```
3. break 终止循环：
     ```python
     count = 0
     while True:
     count += 1
     if count == 5:
          break
     ```
4. continue 跳过当前迭代：
<kbd>continue</kbd>语句可以跳过当前循环的其余部分，直接开始下一次迭代。
     
```python
     count = 0
     while count < 5:
     count += 1
     if count == 3:
          continue
     print(count)
```
5. else 块：在循环正常结束时执行。

while 循环还可以带有 else 块。else 块中的代码会在循环正常结束时执行（即没有因为 break 语句而提前退出）。

如果循环是因为 break 被终止的,else 部分将不会执行。
```python 
     count = 0
     while count < 5:
     print(count)
     count += 1
     else:
     print("Loop finished.")
```
## for循环
在 Python 中，for 循环是一种迭代器，可以用于遍历任何序列（如列表、元组、字符串等）或其他可迭代对象。其基本语法结构如下：
```python
for variable in iterable:
    # 执行代码块
```
详细解释：

* <kbd>variable</kbd>是循环中使用的临时变量，代表当前迭代的元素。
* <kbd>iterable</kbd>是任何可以迭代的对象（如列表、元组、字典、字符串、范围等）。
* 每次循环，<kbd>variable</kbd>会依次取<kbd>iterable</kbd>中的每个元素，直到迭代完所有元素。
```python
# 示例 1: 遍历列表
fruits = ["apple", "banana", "cherry"]
print("遍历列表:")
for fruit in fruits:
    print(fruit)

# 示例 2: 遍历字符串
word = "Python"
print("\n遍历字符串:")
for letter in word:
    print(letter)

# 示例 3: 使用 range() 生成数字序列
#range(start, stop, step)
#start: 序列的起始值（默认值为 0）。如果省略，则默认为 0。
#stop: 序列的结束值（不包括该值）。这是必须指定的参数。
#step: 每次增加的步长（默认值为 1）。如果省略，则默认为 1。
print("\n遍历数字序列:")
for i in range(5):
    print(i)

# 示例 4: 遍历字典
person = {"name": "Alice", "age": 25, "city": "New York"}
print("\n遍历字典:")
for key, value in person.items():
    print(f"{key}: {value}")
```
运行结果:
```python
遍历列表:
apple
banana
cherry

遍历字符串:
P
y
t
h
o
n

遍历数字序列:
0
1
2
3
4

遍历字典:
name: Alice
age: 25
city: New York
n
```
但如果在循环中使用<kbd>break</kbd>提前退出,<kbd>else</kdb>代码块就不会执行：
```python
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("循环结束")

#输出：
0
1
2
```
## 循环嵌套
```python
for i in range(start1, stop1, step1):
    for j in range(start2, stop2, step2):
        # 执行的操作
```
示例:
```python
# 示例 1: 打印二维数组的元素
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print("示例 1: 打印二维数组的元素")
for row in matrix:
    for value in row:
        print(value, end=' ')
    print()
print()

# 示例 2: 打印九九乘法表
print("示例 2: 打印九九乘法表")
for i in range(1, 10):
    for j in range(1, i+1):
        print(f'{j}*{i}={i*j}', end=' ')
    print()
print()

# 示例 3: 打印矩阵的坐标
rows = 3
cols = 4

print("示例 3: 打印矩阵的坐标")
for i in range(rows):
    for j in range(cols):
        print(f'({i}, {j})', end=' ')
    print()
print()

# 示例 4: 计算二维数组的和
total = 0
print("示例 4: 计算二维数组的和")
for row in matrix:
    for value in row:
        total += value

print("Total sum:", total)
```
输出:
```python
示例 1: 打印二维数组的元素
1 2 3 
4 5 6 
7 8 9 

示例 2: 打印九九乘法表
1*1=1 
1*2=2 2*2=4 
1*3=3 2*3=6 3*3=9 
1*4=4 2*4=8 3*4=12 4*4=16 
1*5=5 2*5=10 3*5=15 4*5=20 5*5=25 
1*6=6 2*6=12 3*6=18 4*6=24 5*6=30 6*6=36 
1*7=7 2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49 
1*8=8 2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64 
1*9=9 2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81 

示例 3: 打印矩阵的坐标
(0, 0) (0, 1) (0, 2) (0, 3) 
(1, 0) (1, 1) (1, 2) (1, 3) 
(2, 0) (2, 1) (2, 2) (2, 3) 

示例 4: 计算二维数组的和
Total sum: 45
```
## 列表
1. 创建列表

    你可以通过方括号<kbd>[]</kbd>来创建一个列表,元素之间用逗号<kbd>,</kbd>分隔。
    ```python
    # 示例
    my_list = [1, 2, 3, 4, 5]
    ```
2. 访问列表元素

    列表的元素是通过索引来访问的，Python的索引从 0 开始。

    ```python
    print(my_list[0])  # 输出 1
    print(my_list[1])  # 输出 2

    # 你也可以使用负数索引来从列表的末尾访问元素，-1 表示最后一个元素,-2 表示倒数第二个元素，以此类推。

    print(my_list[-1])  # 输出 5
    print(my_list[-2])  # 输出 4
    ```
3. 修改列表

    列表是可变的，这意味着你可以直接修改列表中的元素。
    ```python
    my_list[2] = 10
    print(my_list)  # 输出 [1, 2, 10, 4, 5]
    ```
4. 列表切片

    切片（Slicing）是从列表中提取一个子列表。你可以通过 start:stop:step 来获取子列表。
    列表切片不改变原列表,返回一个新的列表
    ```python
    # 获取索引2到4之间的元素
    sublist = my_list[2:4]
    print(sublist)  # 输出 [4, 5]

    # 从索引1开始，每隔1个元素取一个
    sublist = my_list[1::2]
    print(sublist)  # 输出 [2, 5]
    
    #反转列表:切片可以通过步长为 -1 来反转列表，且这不会改变原列表。
    my_list = [1, 2, 3, 4, 5]
    reversed_list = my_list[::-1]
    print(reversed_list)  # 输出 [5, 4, 3, 2, 1]
    ```
5. 列表嵌套

    列表可以包含其他列表，这称为嵌套列表。
    ```python
    nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    print(nested_list[0])  # 输出 [1, 2, 3]
    print(nested_list[1][2])  # 输出 6
    ```
6. 列表推导式（List Comprehension）

    列表推导式是一种简洁的方式来生成新列表。它允许你从一个已有的列表创建一个新的列表，同时可以进行条件筛选或变换。
    ```python
    # 示例：将my_list中的每个元素乘以2
    new_list = [x * 2 for x in my_list]
    print(new_list)  # 输出 [2, 4, 8, 10]

    # 示例：筛选出大于3的元素
    filtered_list = [x for x in my_list if x > 3]
    print(filtered_list)  # 输出 [4, 5]
    ```
### 列表常用方法
1. <kbd>append()</kbd>

    <kbd>append()</kbd>方法将元素添加到列表的末尾。
    ```python
    my_list = [1, 2, 3]
    my_list.append(4)
    print(my_list)  # 输出: [1, 2, 3, 4]
    ```
2. extend()

    <kbd>extend()</kbd>方法将一个可迭代对象（如列表、元组、字符串等）的元素添加到列表的末尾。
    ```python
    my_list = [1, 2, 3]
    my_list.extend([4, 5])
    print(my_list)  # 输出: [1, 2, 3, 4, 5]

    # 也可以扩展其他可迭代对象
    my_list.extend("abc")
    print(my_list)  # 输出: [1, 2, 3, 4, 5, 'a', 'b', 'c']
    ```
3. <kbd>insert()</kbd>

    <kbd>insert()</kbd>方法将元素插入到列表的指定位置。
    ```python
    my_list = [1, 2, 3]
    my_list.insert(1, 10)  # 在索引 1 处插入元素 10
    print(my_list)  # 输出: [1, 10, 2, 3]
    ```
4. <kbd>remove()</kbd>

    <kbd>remove()</kbd>方法删除列表中第一个匹配的元素。如果该元素不存在，Python 会抛出 ValueError 异常。
    ```python
    my_list = [1, 2, 3, 4, 5]
    my_list.remove(3)  # 删除值为 3 的元素
    print(my_list)  # 输出: [1, 2, 4, 5]
    ```
5. <kbd>clear()</kbd>

    <kbd>clear()</kbd>方法删除列表中的所有元素，使列表变为空列表。
    ```python
    my_list = [1, 2, 3]
    my_list.clear()
    print(my_list)  # 输出: []
    ```
6. <kbd>index()</kbd>

    <kbd>index()</kbd>方法返回列表中某个元素的第一个匹配项的索引。如果元素不存在，会抛出 ValueError 异常。
    ```python
    my_list = [10, 20, 30, 40]
    index_of_20 = my_list.index(20)
    print(index_of_20)  # 输出: 1
    ```
7. <kbd>count()</kbd>

    <kbd>count()</kbd>方法返回某个元素在列表中出现的次数。
    ```python
    my_list = [1, 2, 2, 3, 2, 4]
    count_of_2 = my_list.count(2)
    print(count_of_2)  # 输出: 3
    ```
8. <kbd>sort()</kbd>

    <kbd>sort()</kbd>方法将列表中的元素按升序排序，默认是按照元素的值排序。可以通过 reverse=True 参数反向排序，也可以通过 key 参数提供自定义排序规则。

    ***sort() 方法没有返回值（即返回 None）,它是在原地对列表进行排序。用于对原始列表进行排序,并且会修改原列表。***
    ```python
    my_list = [3, 1, 4, 2, 5]
    my_list.sort()
    print(my_list)  # 输出: [1, 2, 3, 4, 5]

    # 反向排序
    my_list.sort(reverse=True)
    print(my_list)  # 输出: [5, 4, 3, 2, 1]

    # 按绝对值排序
    my_list = [-3, 1, -4, 2, -5]
    my_list.sort(key=abs)
    print(my_list)  # 输出: [1, 2, -3, -4, -5]
    ```
9. <kbd>sorted</kbd>
    <kbd>sorted()</kbd>是一个内建函数,可以对任何可迭代对象进行排序（不仅限于列表）,并返回一个新的已排序的列表,而不修改原始数据。
    
    ***返回一个新的排序后的列表。***
#### sort与sorted主要区别
|特性|sort()|sorted()|
|:--:|:--:|:--:|
|修改原列表|是，排序是原地进行的|否，返回一个新的排序后的列表|
|返回值|<kbd>None</kbd>|返回排序后的新列表|
|适用范围|只能用于列表对象|可以用于任何可迭代对象|
|性能|原地排序(较高效)|需要额外的空间来存储新列表|

***如果你想就地修改原始列表，使用 sort() 方法。如果你需要保持原始列表不变，或者希望对其他可迭代对象进行排序，使用 sorted() 函数。***
1.  <kbd>reverse()</kbd>

    <kbd>reverse()</kbd>方法将列表中的元素反向排列。这个方法会直接修改原列表。
    ```python
    my_list = [1, 2, 3, 4, 5]
    my_list.reverse()
    print(my_list)  # 输出: [5, 4, 3, 2, 1]
    ```
2.  <kbd>max()</kbd>和<kbd>min()</kbd>

    max() 和 min() 方法分别返回列表中的最大值和最小值。
    ```python
    my_list = [1, 2, 3, 4, 5]
    print(max(my_list))  # 输出: 5
    print(min(my_list))  # 输出: 1
    ```
3.  <kbd>list()</kbd>

    list() 方法用于将其他类型（如元组、字符串、字典等）转换为列表。
    ```python
    # 从元组转换为列表
    tuple_data = (1, 2, 3)
    my_list = list(tuple_data)
    print(my_list)  # 输出: [1, 2, 3]

    # 从字符串转换为列表
    string_data = "hello"
    my_list = list(string_data)
    print(my_list)  # 输出: ['h', 'e', 'l', 'l', 'o']
    ```
## 元组
在Python中，元组（Tuple）是一种内置的数据结构，类似于列表（List），但与列表不同的是，元组是不可变的（immutable）。一旦创建，元组的元素就不能被修改、添加或删除。这使得元组通常用于存储那些不需要修改的数据。
1. 元组的创建
    
    元组可以通过圆括号 () 创建，元素之间使用逗号 , 分隔。
    ```python
    # 创建一个包含三个元素的元组
    my_tuple = (1, 2, 3)

    # 创建一个包含不同数据类型的元组
    mixed_tuple = (1, "hello", 3.14)

    # 单元素元组需要一个逗号
    single_element_tuple = (5,)
    ```
2. 访问元组中的元素

    你可以通过索引访问元组中的元素,索引从0开始。
    ```python
    my_tuple = (10, 20, 30)

    # 访问第一个元素
    print(my_tuple[0])  # 输出: 10

    # 访问最后一个元素
    print(my_tuple[-1])  # 输出: 30
    ```
## 解包(元组解包和参数解包)
在Python中,元组解包(Tuple Unpacking)是指将元组中的元素分配给多个变量。通过元组解包，可以轻松地将元组中的每个元素提取到相应的变量中，这是一种非常方便且常见的操作。
1. 在元组解包中使用 *

   <kbd>*</kbd>在元组解包中的使用主要体现在 捕获多余的元素。它将元组中剩余的元素打包成一个列表，然后赋值给一个变量。

   示例 1:捕获剩余的元素

    ```python
    my_tuple = (1, 2, 3, 4, 5)

    # 使用 * 来捕获剩余的元素
    a, b, *rest = my_tuple

    print(a)      # 输出: 1
    print(b)      # 输出: 2
    print(rest)   # 输出: [3, 4, 5]
    ```
2. <kbd>*</kbd>在函数参数中

    <kbd>*</kbd>也用于 函数定义和调用时解包 元组或列表。你可以将一个元组或列表中的元素解包并将它们作为函数的参数传递。

    示例 3:函数参数中的 *
    ```python
    # 定义一个函数
    def add(a, b, c):
        return a + b + c

    # 创建一个元组
    my_tuple = (1, 2, 3)

    # 使用 * 来解包元组并传递给函数
    result = add(*my_tuple)

    print(result)  # 输出: 6
    ```
    在这个例子中，*my_tuple 将元组中的元素解包并传递给函数 add，分别作为 a, b 和 c。

    示例4:selenium下的函数解包
    
    ```python
    element = self.driver.find_element(*MainPageLocators.GO_BUTTON)
    element.click()

    class MainPageLocators(object):
    """A class for main page locators. All main page locators should come here"""
    
    GO_BUTTON = (By.ID, 'submit')
    
    ```
    ***在 self.driver.find_element(*MainPageLocators.GO_BUTTON) 中，<kbd>*</kbd>是用于 解包 元组的语法。这个语法将 MainPageLocators.GO_BUTTON 元组中的两个元素 By.ID 和 'submit' 解包并分别传递给 find_element 方法。***
## map函数
map() 是 Python 内置的一个函数，用于对可迭代对象（如列表、元组等）中的每个元素应用一个指定的函数，并返回一个迭代器。这个迭代器生成应用该函数后的结果。
语法：
```python
map(function, iterable, ...)
```
* function：一个函数，这个函数会被应用到可迭代对象中的每个元素。
* iterable：一个或多个可迭代对象（如列表、元组等），map 会对每个可迭代对象中的元素依次应用 function。

如果提供多个可迭代对象，function 必须接受多个参数，且 map 会将每个可迭代对象的元素一一对应地传递给 function。
* 返回值：

map() 返回一个迭代器对象，它是一个惰性求值的对象，意味着它不会立即计算结果，而是当你遍历它时才会计算每个元素。如果你想要得到具体的结果，可以使用 list() 或 tuple() 等函数将其转换为列表或元组。
示例 1：单个可迭代对象
```python
numbers = [1, 2, 3, 4, 5]

# 使用 lambda 表达式对每个元素进行平方运算
squared_numbers = map(lambda x: x ** 2, numbers)

# 将 map 对象转换为列表并输出
print(list(squared_numbers))  # 输出 [1, 4, 9, 16, 25]
```
在这个示例中，lambda x: x ** 2 对列表 numbers 中的每个元素进行平方处理，最终返回一个新的列表。
示例 2：多个可迭代对象
```python
numbers1 = [1, 2, 3]
numbers2 = [4, 5, 6]

# 使用 lambda 表达式对两个列表的对应元素进行加法运算
summed_numbers = map(lambda x, y: x + y, numbers1, numbers2)

# 将 map 对象转换为列表并输出
print(list(summed_numbers))  # 输出 [5, 7, 9]
```
在这个示例中，map() 同时处理两个列表 numbers1 和 numbers2，将它们的对应元素相加。

示例 3：使用函数而非 lambda

你也可以传递一个已经定义的函数，而不是 lambda 表达式：
```python
def square(x):
    return x ** 2

numbers = [1, 2, 3, 4, 5]

# 使用定义好的函数对每个元素进行平方运算
squared_numbers = map(square, numbers)

# 将 map 对象转换为列表并输出
print(list(squared_numbers))  # 输出 [1, 4, 9, 16, 25]
```
## 字典
Python 中的字典(dict)是一种内置的数据结构,它是一个无序的键值对集合。字典中的每个元素都是由一个键(key)和值(value)组成,键是唯一的,而值则可以是任何数据类型。
1. 字典的创建
    你可以使用大括号 {} 或者 dict() 构造函数来创建字典。
    使用大括号创建字典：
    ```python
    my_dict = {"name": "Alice", "age": 25, "city": "New York"}
    ```
    使用 dict() 构造函数：
    ```python
    my_dict = dict(name="Alice", age=25, city="New York")
    ```
2. 访问字典中的元素
      
    可以通过键来访问字典中的值。如果键不存在，会抛出 KeyError 异常。
    ```python
    print(my_dict["name"])  # 输出: Alice
    ```
    使用 .get() 方法访问值

    get() 方法允许你在键不存在时返回 None 或者你指定的默认值，而不是抛出异常。
    ```python
    print(my_dict.get("age"))  # 输出: 25
    print(my_dict.get("address", "Not Found"))  # 输出: Not Found
    ```
3. 修改字典中的元素

    你可以通过键来修改字典中的值。如果键不存在，则会添加一个新的键值对。
    ```python
    my_dict["age"] = 26
    print(my_dict)  # 输出: {'name': 'Alice', 'age': 26, 'city': 'New York'}
    
    # 添加新的键值对
    my_dict["address"] = "123 Street"
    print(my_dict)  # 输出: {'name': 'Alice', 'age': 26, 'city': 'New York', 'address': '123 Street'}
    ```
4. 删除字典中的元素

    你可以使用 del 语句或 .pop() 方法删除字典中的元素。
    使用 del 删除
    ```python
    del my_dict["age"]
    print(my_dict)  # 输出: {'name': 'Alice', 'city': 'New York', 'address': '123 Street'}
    ```
    使用 .pop() 删除并返回值
    ```python
    value = my_dict.pop("city")
    print(value)  # 输出: New York
    print(my_dict)  # 输出: {'name': 'Alice', 'address': '123 Street'}
    ```
    5. 字典的方法

    ***遍历字典**

    可以使用 for 循环遍历字典中的键、值或键值对。

    * 遍历键：
    ```python
    for key in my_dict:
        print(key)
    ```
   * 遍历值：
    ```python
    for value in my_dict.values():
        print(value)
    ```
   * 遍历键值对：
    ```python
    for key, value in my_dict.items():
        print(key, value)
    ```
### 字典常用函数
1. <kbd>.clear()</kbd>

    清空字典，删除所有的键值对。
    ```python
    my_dict = {'a': 1, 'b': 2}
    my_dict.clear()
    print(my_dict)  # 输出: {}
    ```
2. <kbd>.copy()</kbd>

    返回字典的浅拷贝，即创建一个新的字典，内容与原字典相同。
    ```python
    original_dict = {'a': 1, 'b': 2}
    new_dict = original_dict.copy()
    print(new_dict)  # 输出: {'a': 1, 'b': 2}
    ```
3. <kbd>.get(key, default=None)</kbd>

    获取指定键的值。如果键不存在，返回 default（默认为 None）。
    ```python
    my_dict = {'a': 1, 'b': 2}
    print(my_dict.get('a'))  # 输出: 1
    print(my_dict.get('c'))  # 输出: None
    print(my_dict.get('c', 'Not Found'))  # 输出: Not Found
    ```
4. <kbd>.items()</kbd>

    返回一个包含所有键值对的视图对象（dict_items），它是一个包含 (key, value) 元组的可迭代对象。
    ```python
    my_dict = {'a': 1, 'b': 2}
    print(my_dict.items())  # 输出: dict_items([('a', 1), ('b', 2)])
    for key, value in my_dict.items():
        print(key, value)
    ```
5. <kbd>.keys()</kbd>

    返回字典中所有键的视图对象（dict_keys），可以用来遍历所有的键。
    ```python
    my_dict = {'a': 1, 'b': 2}
    print(my_dict.keys())  # 输出: dict_keys(['a', 'b'])
    for key in my_dict.keys():
        print(key)
    ```
6. <kbd>.values()</kbd>

    返回字典中所有值的视图对象（dict_values），可以用来遍历所有的值。
    ```python
    my_dict = {'a': 1, 'b': 2}
    print(my_dict.values())  # 输出: dict_values([1, 2])
    for value in my_dict.values():
        print(value)
    ```
## python-random模块
random 模块方法

random 模块方法如下：
|方法|描述|
|:--|:--|
|randrange() |从 range(start, stop, step) 返回一个随机选择的元素。左闭右开|
|randint(a, b) |返回随机整数 N 满足 a <= N <= b。|
|choice(seq) |从非空序列 seq 返回一个随机元素。 如果 seq 为空，则引发 IndexError。|
|shuffle(x[, random]) |将序列 x 随机打乱位置。|
|random() |返回 [0.0, 1.0) 范围内的下一个随机浮点数。|

## python函数
1. 函数的定义和调用
    ```python
    def greet_user():
        print('Hi there!')
        print('welcome aboard')

    print("start")
    greet_user()
    prinf("Finish")
    ```
2. 带参数的函数
    ```python
    def greet_user(name):
        print(f'Hi {name}!')
        print('welcome aboard')

    print("start")
    greet_user('john')
    greet_user('mary')
    prinf("Finish")
    ```
    ```python
    def greet_user(first_name,last_name):
        print(f'Hi {first_name,},{last_name}!')
        print('welcome aboard')

    print("start")
    greet_user('john','smith')
    prinf("Finish")
    ```
3. 带关键字参数函数

当同时使用位置参数和关键字参数时，位置参数必须先传递，关键字参数可以根据名称传递。

***关键字参数应该置于位置参数后***


```python
def greet_user(first_name,last_name):
    print(f'Hi {first_name,},{last_name}!')
    print('welcome aboard')

print("start")
greet_user(first_name='john',last_name='smith')
prinf("Finish")
```
```python
def greet(name, age, city="Unknown"):
    print(f"Hello, my name is {name}, I am {age} years old, and I live in {city}.")

# 使用位置参数和关键字参数
greet("Alice", 25, city="New York")  # 输出: Hello, my name is Alice, I am 25 years old, and I live in New York.

# 只使用位置参数，使用默认值
greet("Bob", 30)  # 输出: Hello, my name is Bob, I am 30 years old, and I live in Unknown.
```
4. 使用可变参数(<kbd>*args</kbd>和<kbd>**kwargs</kbd>)
* <kbd>*args</kbd>用于接收任意数量的位置参数（以元组形式传递）。
* <kbd>**kwargs</kbd>用于接收任意数量的关键字参数(以字典形式传递)。
```python
 # 使用 *args 接收多个位置参数
def add_numbers(*args):
    return sum(args)

print(add_numbers(1, 2, 3))  # 输出: 6
print(add_numbers(5, 10, 15, 20))  # 输出: 50

# 使用 **kwargs 接收多个关键字参数
def greet_person(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

greet_person(name="Alice", age=25, city="New York")
# 输出:
# name: Alice
# age: 25
# city: New York
```
5. lambda函数(匿名函数)
用法:
```python
lambda 参数: 表达式
```
```python
# 定义一个lambda函数
multiply = lambda x, y: x * y
print(multiply(3, 4))  # 输出: 12
```
## python装饰器
装饰器（decorators）是 Python 中的一种高级功能，它允许你动态地修改函数或类的行为。

***简单来说就是在函数前注解的时候(即使用装饰器的时候),装饰器能够作为一个整体函数作为使用装饰器的此函数的函数,使用装饰器的函数作为参数***

举个直观的例子：
```python
def decorator(func):  # func 就是被 @ 装饰的函数
    def wrapper():
        print("调用前")
        func()   # 调用原始函数
        print("调用后")
    return wrapper

@decorator
def greet():
    print("Hello!")

# 相当于：
# greet = decorator(greet)

greet()
```

输出：
```python
调用前
Hello!
调用后
```
所以你说的没错，@decorator 就是把 greet 传给 decorator 函数，相当于：
```python
greet = decorator(greet)
```
而 decorator 函数返回了 wrapper 这个函数对象，它替代了原始的 greet 函数。
## 函数的返回(return)
在 Python 中,函数的返回值是指函数执行完毕后,将结果返回到函数,以便下次继续调用.
```python
def square(number):
    return number * number
print(square(3)) #输出9
```
在以下情况下无返回值默认返回None
```python
def square(number):
    print(number * number)
print(square(3)) 
#输出9
#输出None
```
## yield关键字
在Python中，yield是一个用于创建生成器的关键字。生成器是一种特殊类型的迭代器，它允许你逐个生成值，而不是一次性生成所有值。使用yield可以让你在一个函数中暂停执行并返回一个值，然后继续从暂停的地方继续执行，直到函数结束。

1. 基本用法

当你在一个函数中使用yield时，该函数不再是一个普通的函数，而变成了一个生成器函数。每次调用生成器时，都会执行到yield语句，并返回一个值，暂停函数的执行，直到下次通过next()重新启动函数。
```python
def count_up_to(max):
    count = 1
    while count <= max:
        yield count  # 暂停并返回count
        count += 1

counter = count_up_to(5)
print(next(counter))  # 输出 1
print(next(counter))  # 输出 2
```
2. yield与return的区别

   * yield会暂停函数的执行，并保存函数的状态，而return会终止函数的执行并返回一个值。
   * 生成器函数使用yield返回多个值，而return只能返回一个值。

3. 示例：用yield实现斐波那契数列
```python
def fibonacci(n):
    a, b = 0, 1
    while n > 0:
        yield a
        a, b = b, a + b
        n -= 1

fib = fibonacci(5)
for num in fib:
    print(num)  # 输出 0, 1, 1, 2, 3
```
## if \_\_name\_\_=='main':
最直接根本的作用就是判断是否作为主函数运行,当其他文件作为模块导入该文件时不执行代码

***平常的时候很多的导入包代码并没有执行是因为一些包都是方法没有调用是无法执行的***
1. <kbd>\_\_name\_\_</kbd> 变量：
   * 每个 Python 模块（即 .py 文件）都有一个内建的 \_\_name\_\_ 变量.
   * 当你直接运行一个 Python 文件时,\_\_name\_\_ 的值被设置为 '\_\_main\_\_'.
   * 如果这个 Python 文件被作为模块导入到其他脚本中，\_\_name\_\_ 的值将是该模块的名字(即文件名，不包括扩展名 .py).
2. <kbd>if \_\_name\_\_ == '\_\_main\_\_':</kbd>：
   * 这行代码的作用是判断当前脚本是否是直接执行的。
   * 如果是直接执行的，则 \_\_name__ == '\_\_main\_\_' 为真，代码块内的内容会被执行。
   * 如果是作为模块被导入，\_\_name\_\_ == '\_\_main\_\_' 为假，代码块内的内容不会执行。
## python 魔术方法
Python 中的魔术方法(Magic Methods)，也叫做特殊方法或双下方法(dunder methods)，是以双下划线(<kbd>__</kbd>)包围的方法，用来实现 Python 类的特殊功能和行为。这些方法可以让你自定义对象的行为，使其在特定情况下表现得像内建类型一样。例如，你可以让你的对象支持加法、减法、索引、字符串表示等操作。
1. 对象创建与初始化

    * <kbd>\_\_new\_\_(cls, ...)</kbd>:

      * 用于创建并返回一个新的对象实例。

      * 在 \_\_init\_\_ 之前调用。

    * <kbd>\_\_init\_\_(self, ...)</kbd>:

      * 用于初始化对象实例。

      * 在对象创建后调用。

    * <kbd>\_\_del\_\_(self)</kbd>:

      * 在对象被销毁（垃圾回收）时调用。
    ```python
    class MyClass:
        def __new__(cls, *args, **kwargs):
            print("Creating instance")
            return super().__new__(cls)

        def __init__(self, value):
            print("Initializing instance")
            self.value = value

        def __del__(self):
            print("Deleting instance")

    obj = MyClass(10)  # 输出: Creating instance, Initializing instance
    del obj            # 输出: Deleting instance
    ```
2. 字符串表示

    * <kbd>\_\_str\_\_(self)</kbd>:

      * 定义对象的“非正式”字符串表示，通常用于用户友好的输出。

      * 调用 str(obj) 或 print(obj) 时触发。

    * <kbd>\_\_repr\_\_(self)</kbd>:

      * 定义对象的“正式”字符串表示，通常用于调试和开发。

      * 调用 repr(obj) 或在交互式环境中直接输入对象时触发。

    ```python
    class MyClass:
        def __init__(self, value):
            self.value = value

        def __str__(self):
            return f"MyClass with value: {self.value}"

        def __repr__(self):
            return f"MyClass({self.value})"

    obj = MyClass(10)
    print(str(obj))   # 输出: MyClass with value: 10
    print(repr(obj))  # 输出: MyClass(10)
    ```
3. 属性访问

    * <kbd>\_\_getattr\_\_(self, name)</kbd>:

      * 当访问不存在的属性时调用。

    * <kbd>\_\_setattr\_\_(self, name, value)</kbd>:

      * 当设置属性时调用。

    * <kbd>\_\_delattr\_\_(self, name)</kbd>:

      * 当删除属性时调用。

    ```python
    class MyClass:
        def __getattr__(self, name):
            return f"Attribute {name} not found"

        def __setattr__(self, name, value):
            print(f"Setting {name} to {value}")
            super().__setattr__(name, value)

    obj = MyClass()
    print(obj.x)  # 输出: Attribute x not found
    obj.x = 10    # 输出: Setting x to 10
    ```
5. 运算符重载

    * <kbd>\_\_add\_\_(self, other)</kbd>:

       * 定义加法行为，调用 obj1 + obj2 时触发。

    * <kbd>\_\_sub\_\_(self, other)</kbd>:

       * 定义减法行为，调用 obj1 - obj2 时触发。

    * <kbd>\_\_eq\_\_(self, other)</kbd>:

       * 定义相等比较行为，调用 obj1 == obj2 时触发。

    * <kbd>\_\_lt\_\_(self, other)</kbd>:

       * 定义小于比较行为，调用 obj1 < obj2 时触发。

    ```python
    class Point:
        def __init__(self, x, y):
            self.x = x
            self.y = y

        def __add__(self, other):
            return Point(self.x + other.x, self.y + other.y)

        def __eq__(self, other):
            return self.x == other.x and self.y == other.y

    p1 = Point(1, 2)
    p2 = Point(3, 4)
    p3 = p1 + p2
    print(p3.x, p3.y)  # 输出: 4 6
    print(p1 == p2)    # 输出: False
    ```
## 错误处理
在 Python 中，错误处理主要通过<kbd>try</kbd>、<kbd>except</kbd>、<kbd>else</kbd>和<kbd>finally</kbd>语句来实现.这些语句允许你捕获和处理代码中可能发生的异常,从而避免程序崩溃。
```python
try:
    # 尝试执行的代码
    risky_code()
except SomeException as e:
    # 如果发生 SomeException 异常，执行这里的代码
    handle_exception(e)
else:
    # 如果没有异常发生，执行这里的代码
    no_exceptions()
finally:
    # 无论是否发生异常，都会执行这里的代码
    always_execute()
```
eg:
```python
try:
    # 尝试打开一个文件
    with open('non_existent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError as e:
    # 如果文件不存在，捕获 FileNotFoundError 异常
    print(f"Error: {e}")
else:
    # 如果没有异常发生，打印文件内容
    print(content)
finally:
    # 无论是否发生异常，都会执行这里的代码
    print("Execution complete.")
```
1. 捕获多个异常

    你可以捕获多个不同类型的异常，并对它们进行不同的处理：
    ```python
    try:
        age =int(input('age: '))
        income=20000
        risk= income / age
        print(age)  
    except ZeroDivisionError:
        print('Age cannot be 0')
    except ValueError:
        print('Invalid value')

    ```
    ```python
    try:
        # 尝试执行的代码
        risky_code()
    except FileNotFoundError as e:
        # 处理文件未找到异常
        print(f"File not found: {e}")
    except PermissionError as e:
        # 处理权限错误
        print(f"Permission denied: {e}")
    except Exception as e:
        # 处理其他所有异常
        print(f"An unexpected error occurred: {e}")
    ```
2. 捕获所有异常

    如果你想要捕获所有可能的异常，可以使用 Exception 类：
    ```python
    try:
        # 尝试执行的代码
        risky_code()
    except Exception as e:
        # 处理所有异常
        print(f"An error occurred: {e}")
    ```
3. 自定义异常

    你还可以定义自己的异常类，并在代码中抛出这些异常：
    ```python
    class MyCustomError(Exception):
        pass

    def risky_function():
        raise MyCustomError("Something went wrong!")

    try:
        risky_function()
    except MyCustomError as e:
        print(f"Custom error caught: {e}")
    ```
### raise关键字
在 Python 中，raise 关键字用于触发（或抛出）一个异常。它可以用来手动引发一个异常，从而停止程序的正常执行并跳转到异常处理机制（如 try 和 except 语句块）。
1. 抛出一个特定的异常： 你可以使用 raise 抛出一个已经存在的异常类，例如 ValueError、TypeError 等。可以传递一个错误信息来帮助解释异常的原因。
```python
raise ValueError("Invalid value provided")
```
这将抛出一个 ValueError 异常，并附带消息 "Invalid value provided"。

2. 重新抛出当前异常： 在 except 块中，可以使用 raise 重新抛出当前捕获的异常。
```python
try:
    x = 10 / 0
except ZeroDivisionError as e:
    print("Caught an exception:", e)
    raise  # 重新抛出当前异常
```
3. 这会在打印错误消息后重新抛出 ZeroDivisionError。

自定义异常： 你还可以创建自己的异常类，并用 raise 抛出它们。
```python
    class MyCustomError(Exception):
        pass

    raise MyCustomError("Something went wrong")
```
总的来说，raise 关键字使得你可以在程序中控制错误流，触发或重新抛出异常，帮助开发者处理特殊情况或错误。
### 常见错误
|异常类型|描述|处理方法|
|:--:|:--:|:--:|
|FileNotFoundError|文件未找到|检查文件路径，捕获异常|
|ZeroDivisionError|除零错误|检查除数，捕获异常|
|TypeError|类型错误|检查变量类型，捕获异常|
|IndexError|索引错误|检查索引范围，捕获异常|
|KeyError|键错误|检查字典键值，捕获异常|
|AttributeError|属性错误|检查对象属性或方法，捕获异常|
|ValueError|值错误|检查输入值，捕获异常|
|KeyboardInterrupt|用户中断|捕获异常并优雅退出|
|自定义异常|自定义逻辑错误|定义异常类，抛出并捕获|
## 类
在 Python 中,类(Class)是面向对象编程（OOP）的核心概念。类用于创建对象，对象是类的实例。类可以包含属性（变量）和方法(函数),用于描述对象的行为和状态。
1. 基本语法
定义类

使用 class 关键字定义类，类名通常采用驼峰命名法（如 MyClass）。
```python
class MyClass:
    pass  # 空类
```
创建对象

通过类名加括号 () 创建类的实例（对象）。
python
复制

obj = MyClass()

1. 属性和方法
实例属性

实例属性是绑定到对象上的变量，通常在 __init__ 方法中初始化。
```python

class Person:
    def __init__(self, name, age):
        self.name = name  # 实例属性
        self.age = age

# 创建对象
person = Person("Alice", 25)
print(person.name)  # 输出: Alice
print(person.age)   # 输出: 25
```
实例方法

实例方法是绑定到对象上的函数，第一个参数通常是 self，表示对象本身。
```python


class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, my name is {self.name} and I am {self.age} years old."

# 创建对象并调用方法
person = Person("Alice", 25)
print(person.greet())  # 输出: Hello, my name is Alice and I am 25 years old.
```
3. 类属性和类方法
类属性

类属性是绑定到类本身的变量，所有实例共享。
```python

class Person:
    species = "Human"  # 类属性

    def __init__(self, name, age):
        self.name = name
        self.age = age

# 访问类属性
print(Person.species)  # 输出: Human

# 实例也可以访问类属性
person = Person("Alice", 25)
print(person.species)  # 输出: Human
```
类方法

类方法是绑定到类本身的方法，使用 @classmethod 装饰器定义，第一个参数是 cls，表示类本身。
```python

class Person:
    species = "Human"

    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def get_species(cls):
        return cls.species

# 调用类方法
print(Person.get_species())  # 输出: Human
```
4. 静态方法

静态方法与类和实例无关，使用 @staticmethod 装饰器定义，不需要 self 或 cls 参数。
```python

class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

# 调用静态方法
print(MathUtils.add(3, 5))  # 输出: 8
```
5. 继承

继承允许一个类（子类）继承另一个类（父类）的属性和方法。
基本语法
```python

class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Unknown sound"

class Dog(Animal):  # 继承 Animal 类
    def speak(self):
        return "Woof!"

# 创建子类对象
dog = Dog("Buddy")
print(dog.name)      # 输出: Buddy
print(dog.speak())   # 输出: Woof!
```
方法重写

子类可以重写父类的方法。
调用父类方法

使用 super() 调用父类的方法。
```python

class Cat(Animal):
    def speak(self):
        return super().speak() + " Meow!"

cat = Cat("Whiskers")
print(cat.speak())  # 输出: Unknown sound Meow!
```
7. 多态

多态是指不同类的对象可以调用相同的方法，但表现出不同的行为。
```python

class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

def animal_sound(animal):
    return animal.speak()

dog = Dog()
cat = Cat()

print(animal_sound(dog))  # 输出: Woof!
print(animal_sound(cat))  # 输出: Meow!
```
