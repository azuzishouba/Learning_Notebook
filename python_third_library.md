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