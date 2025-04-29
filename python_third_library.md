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
|w|打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
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
|12|file.writelines(sequence)向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。
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