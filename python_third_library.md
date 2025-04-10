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
|os.getcwd()|返回当前工作目录 |
|os.listdir(path)|返回path指定的文件夹包含的文件或文件夹的名字的列表|
|os.open(file, flags[, mode])|打开一个文件，并且设置需要的打开选项，mode参数是可选的|
|os.remove(path)|删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。|
|os.rename(src, dst)|重命名文件或目录，从 src 到 dst|
|os.rmdir(path)|删除path指定的空目录，如果目录非空，则抛出一个OSError异常。|