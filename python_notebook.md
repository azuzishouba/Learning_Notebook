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
* <kbd>math.fabs(x)</kbd> — 返回x的绝对值
* <kbd>math.factorial(x)</kbd> — 返回x的阶乘(x必须为非负整数)
* <kbd>math.gcd(x, y)</kbd> — 返回x和y的最大公约数
```python
import math
print(math.ceil(3.2))  # 输出：4
print(math.floor(3.8))  # 输出：3
print(math.trunc(3.7))  # 输出：3
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