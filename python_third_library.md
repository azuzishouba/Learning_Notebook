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
## python-OS模块
OS 模块方法
OS模块提供了非常丰富的方法用来处理文件和目录。常用的方法如下表所示：
|方法|描述|
|:--|:--|
|os.chdir(path)|改变当前工作目录|
|os.chmod(path, mode)|更改权限|
|os.chown(path, uid, gid)|更改文件所有者|
|os.chroot(path)|改变当前进程的根目录|
|os.getcwd()|(get current directory)返回当前工作目录 |
|os.listdir(path)|返回path指定的文件夹包含的文件或文件夹的名字的列表|
|os.open(file, flags[, mode])|打开一个文件，并且设置需要的打开选项，mode参数是可选的|
|os.remove(path)|删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。|
|os.rename(src, dst)|重命名文件或目录，从 src 到 dst|
|os.rmdir(path)|删除path指定的空目录，如果目录非空，则抛出一个OSError异常。|
## python-file模块
### open() 方法
Python<kbd>open()</kbd>方法用于打开一个文件，并返回文件对象。

在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。

注意：使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open() 函数常用形式是接收两个参数：文件名(file)和模式(mode)。
```python
open(file, mode='r')
```
完整的语法格式为：
```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```
推荐与<kbd>with</kbd>搭配使用

with 自动调用 \_\_enter__() 和 \_\_exit__()，常用于自动释放资源，如文件、数据库连接、线程锁等。
```python
with open("test.txt", "w") as f:
    f.write("hello")

print(f.closed)
```
参数说明:
* file: 必需，文件路径（相对或者绝对路径）。
* mode: 可选，文件打开模式
* buffering: 设置缓冲
* encoding: 一般使用utf8
* errors: 报错级别
* newline: 区分换行符
* closefd: 传入的file参数类型
* opener: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符。

mode 参数有：
|模式|描述|
|:--|:--|
|t|文本模式 (默认)。
|x|写模式，新建一个文件，如果该文件已存在则会报错。
|b|二进制模式。
|+|打开一个文件进行更新(可读可写)。
|r|以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。
rb|以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。
r+|打开一个文件用于读写。文件指针将会放在文件的开头。
rb+|以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。
|w|打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
w|打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
wb|以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。
w+|打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
|a|打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。

### file 对象
file 对象使用 open 函数来创建，下表列出了 file 对象常用的函数：

|序号|方法及描述
|:--|:--|
|1|***file.close()关闭文件。关闭后文件不能再进行读写操作。***
|2|file.flush()刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。
|3|file.fileno()返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。
|4|file.isatty()如果文件连接到一个终端设备返回 True，否则返回 False。
|5|file.next()***Python 3 中的 File 对象不支持 next() 方法***。返回文件下一行。
|6|***file.read([size])从文件读取指定的字节数，如果未给定或为负则读取所有。***
|7|***file.readline([size])读取整行，包括 "\n" 字符。***
|8|file.readlines([sizeint])读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比 sizeint 较大, 因为需要填充缓冲区。
|9|***file.tell()返回文件当前位置。***
|10|file.truncate([size])从文件的首行首字符开始截断，截断文件为 size 个字符，无 size 表示从当前位置截断；截断之后后面的所有字符被删除，其中 windows 系统下的换行代表2个字符大小。
|11|***file.write(str)将字符串写入文件，返回的是写入的字符长度。***
|12|***file.writelines(sequence)向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。***
## python-csv模块
CSV（Comma-Separated Values）文件是一种常见的文件格式，用于存储表格数据。

CSV 文件由纯文本组成，每一行代表表格中的一行数据，而每一列则通过逗号（或其他分隔符）分隔。

CSV 文件通常用于数据交换，因为它简单且易于处理。

Python 提供了一个内置的 csv 模块，用于读取和写入 CSV 文件。这个模块简化了处理 CSV 文件的过程，使得开发者可以轻松地操作表格数据。
1. 读取 CSV 文件

要读取 CSV 文件，可以使用 csv.reader 对象。以下是一个简单的示例：
实例
```python
import csv
# 打开 CSV 文件
with open('data.csv', mode='r', encoding='utf-8') as file:
    # 创建 csv.reader 对象
    csv_reader = csv.reader(file)
   
    # 逐行读取数据
    for row in csv_reader:
        print(row)
```
代码解释：

* open('data.csv', mode='r', encoding='utf-8')：以只读模式打开名为 data.csv 的文件，并指定编码为 UTF-8。
* csv.reader(file)：创建一个 csv.reader 对象，用于读取文件内容。
* for row in csv_reader：逐行读取文件内容，每一行数据会被解析为一个列表。

2. 写入 CSV 文件

要写入 CSV 文件，可以使用 csv.writer 对象。以下是一个示例：
实例
```python
import csv

# 要写入的数据
data = [
    ['Name', 'Age', 'City'],
    ['Alice', '30', 'New York'],
    ['Bob', '25', 'Los Angeles']
]

# 打开 CSV 文件
with open('output.csv', mode='w', encoding='utf-8', newline='') as file:
    # 创建 csv.writer 对象
    csv_writer = csv.writer(file)
   
    # 写入数据
    for row in data:
        csv_writer.writerow(row)
```
代码解释：
* open('output.csv', mode='w', encoding='utf-8', newline='')：以写入模式打开名为 output.csv 的文件，并指定编码为 UTF-8。newline='' 用于避免在 Windows 系统中出现空行。
* csv.writer(file)：创建一个 csv.writer 对象，用于写入文件内容。
* csv_writer.writerow(row)：将每一行数据写入文件。

3. 使用字典读取和写入 CSV 文件

csv 模块还提供了 DictReader 和 DictWriter 类，它们可以将 CSV 文件的每一行解析为字典，或者将字典写入 CSV 文件。

**使用 DictReader 读取 CSV 文件：**

实例
```python
import csv

with open('data.csv', mode='r', encoding='utf-8') as file:
    csv_dict_reader = csv.DictReader(file)
   
    for row in csv_dict_reader:
        print(row)
```
**使用 DictWriter 写入 CSV 文件：**

实例
```python
import csv

data = [
    {'Name': 'Alice', 'Age': '30', 'City': 'New York'},
    {'Name': 'Bob', 'Age': '25', 'City': 'Los Angeles'}
]

with open('output.csv', mode='w', encoding='utf-8', newline='') as file:
    fieldnames = ['Name', 'Age', 'City']
    csv_dict_writer = csv.DictWriter(file, fieldnames=fieldnames)
   
    # 写入表头
    csv_dict_writer.writeheader()
   
    # 写入数据
    for row in data:
        csv_dict_writer.writerow(row)
```
**常用的属性和方法**

**csv 模块核心方法**

|方法|说明|示例
|:--|:--|:--
csv.reader()|从文件对象读取 CSV 数据|reader = csv.reader(file)
csv.writer()|将数据写入 CSV 文件|writer = csv.writer(file)
csv.DictReader()|将 CSV 行读取为字典（带表头）	|dict_reader = csv.DictReader(file)
csv.DictWriter()|将字典写入 CSV 文件（需指定字段名）|dict_writer = csv.DictWriter(file, fieldnames)
csv.register_dialect()|注册自定义 CSV 格式（如分隔符）	|csv.register_dialect('mydialect', delimiter='|')
csv.unregister_dialect()|删除已注册的方言|csv.unregister_dialect('mydialect')
csv.list_dialects()|列出所有已注册的方言|print(csv.list_dialects())

**csv.reader 和 csv.writer 对象常用方法**

方法|说明|适用对象
|:--|:--|:--
__next__()|迭代读取下一行（或使用 for 循环）|reader
writerow(row)|写入单行数据|writer
writerows(rows)|写入多行数据（列表的列表）|writer

**csv.DictReader 和 csv.DictWriter 对象特性**

特性/方法|说明|示例
:--|:--|:--
fieldnames|字段名列表（DictReader 自动从首行获取）|dict_reader.fieldnames
writeheader()|写入表头行（DictWriter 专用）	|dict_writer.writeheader()
## python-json库
**Python3 JSON 数据解析**

JSON (JavaScript Object Notation) 是一种轻量级的数据交换格式。

如果你还不了解 JSON，可以先阅读我们的 JSON 教程。

Python3 中可以使用 json 模块来对 JSON 数据进行编解码，它包含了两个函数：
* json.dumps(): 对数据进行编码。
* json.loads(): 对数据进行解码。

![json图解](https://www.runoob.com/wp-content/uploads/2016/04/json-dumps-loads.png)

在 json 的编解码过程中，Python 的原始类型与 json 类型会相互转换，具体的转化对照如下：

**Python 编码为 JSON 类型转换对应表：**
|Python |JSON
|:--|:--
dict |object
list, tuple |array
str |string
int, float, int- & float-derived Enums |number
True|true
False|false
None |null
JSON 解码为 Python 类型转换对应表：
JSON |Python
|:--|:--
object 	|dict
array 	|list
string |	str
number (int) |	int
number (real) 	|float
true 	|True
false |	False
null 	|None

json.dumps 与 json.loads 实例

以下实例演示了 Python 数据结构转换为JSON：
实例(Python 3.0+)
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'https://www.runoob.com'
}
 
json_str = json.dumps(data)
print ("Python 原始数据：", repr(data))
print ("JSON 对象：", json_str)

执行以上代码输出结果为：

Python 原始数据： {'no': 1, 'name': 'Runoob', 'url': 'https://www.runoob.com'}
JSON 对象： {"no": 1, "name": "Runoob", "url": "https://www.runoob.com"}

通过输出的结果可以看出，简单类型通过编码后跟其原始的repr()输出结果非常相似。

接着以上实例，我们可以将一个JSON编码的字符串转换回一个Python数据结构：
实例(Python 3.0+)
```python
#!/usr/bin/python3
 
import json
 
# Python 字典类型转换为 JSON 对象
data1 = {
    'no' : 1,
    'name' : 'Runoob',
    'url' : 'http://www.runoob.com'
}
 
json_str = json.dumps(data1)
print ("Python 原始数据：", repr(data1))
print ("JSON 对象：", json_str)
 
# 将 JSON 对象转换为 Python 字典
data2 = json.loads(json_str)
print ("data2['name']: ", data2['name'])
print ("data2['url']: ", data2['url'])
```
执行以上代码输出结果为：
```python
Python 原始数据： {'name': 'Runoob', 'no': 1, 'url': 'http://www.runoob.com'}
JSON 对象： {"name": "Runoob", "no": 1, "url": "http://www.runoob.com"}
data2['name']:  Runoob
data2['url']:  http://www.runoob.com
```
如果你要处理的是文件而不是字符串，你可以使用 json.dump() 和 json.load() 来编码和解码JSON数据。例如：
实例(Python 3.0+)
```python
# 写入 JSON 数据
with open('data.json', 'w') as f:
    json.dump(data, f)
 
# 读取数据
with open('data.json', 'r') as f:
    data = json.load(f)
```
## python-tenacity库
tenacity 是一个 Python 库，用于实现重试机制，通常用于处理可能会失败的操作，比如网络请求、数据库操作等。它的核心功能是通过设置重试次数、间隔时间和其他策略，帮助你自动重试失败的操作，从而提高程序的可靠性。

安装：
```python
pip install tenacity
```
基本使用：

1. 最简单的重试： 默认情况下，tenacity 会重试失败的函数，直到成功为止。
```python
from tenacity import retry

@retry
def test_function():
    print("尝试中...")
    raise Exception("发生错误")

test_function()
```
这个代码会反复尝试调用 test_function()，直到没有错误为止。

2. 控制最大重试次数： 你可以指定最多重试多少次，之后抛出异常。
```python
from tenacity import retry, stop_after_attempt

@retry(stop=stop_after_attempt(3))
def test_function():
    print("尝试中...")
    raise Exception("发生错误")

test_function()
```
3. 设置重试间隔： 可以自定义重试之间的间隔时间，支持固定间隔、指数回退等。
```python
from tenacity import retry, wait_fixed

@retry(wait=wait_fixed(2))  # 每次重试等待2秒
def test_function():
    print("尝试中...")
    raise Exception("发生错误")

test_function()
```
4. 根据异常类型进行重试： 你可以指定哪些异常类型触发重试。
```python
from tenacity import retry, retry_if_exception_type

@retry(retry=retry_if_exception_type(ValueError))
def test_function():
    print("尝试中...")
    raise ValueError("发生错误")

test_function()
```
5. 自定义重试逻辑： tenacity 还允许你定义复杂的重试逻辑，控制何时重试以及如何处理不同的情况。
```python
from tenacity import retry, wait_exponential, stop_after_attempt

@retry(wait=wait_exponential(multiplier=1, min=4, max=10), stop=stop_after_attempt(5))
def test_function():
    print("尝试中...")
    raise Exception("发生错误")

test_function()
```
Selenium应用示例：

* 等待页面完全加载： 如果页面加载非常缓慢，可以使用 tenacity 重试等待页面加载，直到某个标志性元素（如页面标题或某个特定的 DOM 元素）加载完成。
```python
@retry(wait=wait_fixed(3), stop=stop_after_attempt(5))
def wait_for_page_to_load():
    driver.get('https://www.example.com')
    element = driver.find_element(By.TAG_NAME, 'h1')  # 假设页面有一个 h1 标签
    assert element.text == '欢迎访问 Example 页面'  # 确保页面加载完成
```
等待元素可见并进行交互： 假设页面上的某些元素只有在 AJAX 请求完成后才会可见。可以通过 tenacity 重试查找元素直到它出现。
```python
@retry(wait=wait_fixed(1), stop=stop_after_attempt(10))
def wait_for_element_to_be_visible():
    driver.get('https://www.example.com')
    element = driver.find_element(By.ID, 'dynamic_element')
    assert element.is_displayed()  # 确保元素可见
    element.click()  # 执行点击
```
## python 正则表达式
正则表达式是一个特殊的字符序列，它能帮助你方便的检查一个字符串是否与某种模式匹配。

在 Python 中，使用 re 模块来处理正则表达式。

re 模块提供了一组函数，允许你在字符串中进行模式匹配、搜索和替换操作。

re 模块使 Python 语言拥有完整的正则表达式功能。
1. 元字符

| 元字符  | 含义 | 示例|
|:--|:--|:--
| `.`  | 匹配除换行符外的任意一个字符| `a.b` 匹配 `acb`, `a9b`|||
| `^`  | 匹配字符串的开头| `^abc` 匹配 `abc123`|||
| `$`  | 匹配字符串的结尾         | `abc$` 匹配 `123abc`|||
| `*`  | 匹配前一个字符 0 次或1次或多次   | `ab*c` 匹配 `ac`, `abc`, `abbbc` |       |                    |
| `+`  | 匹配前一个字符 1 次或多次   | `ab+c` 匹配 `abc`, `abbbc`|       | |
| `?`  | 匹配前一个字符 0 次或 1 次 | `ab?c` 匹配 `ac`, `abc`|||
|`{3}`|匹配前一个字符的次数|`abc{2}`匹配`abcc`|
|`{2,4}` |匹配前一个字符最少的次数和最多的次数|`abc{2,4}`表示前面2到4个
| `[]` | 匹配括号内的任意一个字符     | `[abc]` 匹配 `a`, `b`, `c`|||
|`[^]`| 匹配不在括号内的字符|`[^abc]`匹配的字符非abc|
| \`   | \`| 表示“或” | \`abc | def`匹配`abc`或`def\` |
| `()` | 分组（可用于提取）| `(abc)+` 匹配 `abc`, `abcabc`|||
2. 转义字符

| 转义字符 | 含义          | 示例                 |
| ---- | ----------- | ------------------ |
| `\d` | 匹配任意数字（0-9） | `\d+` 匹配 `123`     |
| `\D` | 匹配非数字字符     | `\D+` 匹配 `abc`     |
| `\w` | 匹配字母数字下划线   | `\w+` 匹配 `hello_1` |
| `\W` | 匹配非 \w 的字符  | `\W+` 匹配 `@#$`     |
| `\s` | 匹配任意空白字符    | `\s+` 匹配空格、制表      |
| `\S` | 匹配非空白字符     | `\S+` 匹配 `abc123`  |

```python
import re

# 1. re.match：从字符串开头匹配
re.match(r"\d+", "123abc")  # ✅匹配成功

# 2. re.search：从任意位置查找第一个匹配
re.search(r"\d+", "abc123")  # ✅匹配成功

# 3. re.findall：找出所有匹配
re.findall(r"\d+", "a1b22c333")  # ['1', '22', '333']

# 4. re.sub：替换匹配内容
re.sub(r"\d+", "X", "abc123def456")  # 'abcXdefX'

# 5. 分组提取
m = re.search(r"(\d{4})-(\d{2})-(\d{2})", "今天是 2025-06-04")
print(m.group(1), m.group(2), m.group(3))  # 2025 06 04

```