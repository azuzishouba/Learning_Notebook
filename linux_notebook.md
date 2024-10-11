# Linux笔记
## Linux简介
Linux是一种开源操作系统,它是由Linus Torvalds在1991年首次发布的。Linux的内核是其核心部分,负责管理硬件和软件之间的交互。由于其开源特性,用户可以自由修改和分发Linux的代码,这使得许多不同的Linux发行版(如Ubuntu、Fedora、Debian等)应运而生。
### Linux发行版
Linux发行版是基于Linux内核的操作系统版本,通常包含内核、系统工具和应用软件。每个发行版可能有不同的目标用户和特性,例如:

1. Ubuntu:用户友好,适合初学者,广泛用于桌面和服务器。
2. Fedora:强调最新技术,适合开发者和技术爱好者。
3. Debian:稳定性强,适合服务器环境,软件库丰富。
4. Arch Linux:灵活性高,适合高级用户,采用滚动更新模式。
### Linux系统启动过程
1. BIOS/UEFI:
  * 当计算机启动时,BIOS(基本输入输出系统)或UEFI(统一可扩展固件接口)首先进行自检,确保硬件正常运行。这一过程包括检查内存、硬盘和其他硬件组件。完成后,BIOS/UEFI会查找启动设备,通常是硬盘或USB驱动器。

2. 引导加载程序(Bootloader):
  * 一旦BIOS/UEFI找到启动设备,引导加载程序(如GRUB)被加载到内存中。GRUB允许用户选择要启动的操作系统(如果有多个)并加载相应的内核。在此阶段,引导加载程序会读取配置文件,确定内核的位置和启动参数。

3. 加载内核:
    * 引导加载程序加载内核到内存,并初始化基本的硬件控制。内核会执行一系列初始化任务,包括检测和配置硬件设备(如硬盘、网络接口等)。接着,它会挂载根文件系统,通常是一个包含系统文件的分区。

4. 初始化进程(init):
    * 一旦内核完成初始化,它会启动init进程(或systemd)。init是系统中的第一个用户空间进程,负责启动和管理其他进程。根据Linux的版本,可能会使用不同的初始化系统,例如SysVinit、Upstart或systemd。
      * 运行级别:
        >运行级别0:系统停机状态,系统默认运行级别不能设为0,否则不能正常启动

        >运行级别1:单用户模式(Single-user mode):用于系统维护,只有超级用户可以登录,没有网络服务。

        >运行级别2:多用户模式(Multi-user mode without networking):允许多个用户登录,但没有网络服务。

        >运行级别3:完整的多用户模式(Full multi-user mode):允许多个用户登录,并且提供网络服务(通常是文本模式)。

        >运行级别4:未使用(Unused):通常保留给用户自定义用途。

        >运行级别5:图形用户界面(Graphical mode):与运行级别3类似,但启动图形用户界面(如X Window)。

        >运行级别6:重启(Reboot):重新启动系统。

5. 启动服务:
    * init或systemd根据其配置文件(如/etc/inittab或/etc/systemd/system)启动系统服务。这些服务包括网络服务、登录管理器、图形界面等。systemd使用目标(targets)来管理不同的运行级别,使得服务的启动顺序更为高效。

6. 登录界面:
    * 系统启动完成后,用户会看到登录提示或图形用户界面,允许他们输入用户名和密码进行登录。一旦登录成功,用户会进入他们的桌面环境或命令行界面,开始使用系统。
## Linux的安装
1. 下载VMware:
   * https://ubuntu.com/download/desktop
2. 下载ubuntu ISO镜像:
   * https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Player
3. 启动VMware并创建新的虚拟机:
   * 选择下载好的Ubuntu ISO文件
4. 设置硬盘容量至少30GB,运行CPU核数4核,运行内存8GB
5. 按照默认安装软件
## 升级管理软件
* 通过应用商店管理软件
* Ubuntu可以用过synaptic package manager来管理
## COMMAND LINE
### 定位文件
* which (filename) 
查找文件的路径
  >which python
* whereis (filename) 查找二进制文件、源代码和手册页
  >whereis gcc
* grep "pattern" filename 命令用于在文件中搜索特定模式或字符串
  >grep "error" file.txt

  >ls -l | grep "txt"
  * | 表示前面命令的输出作为后面命令的输入,可以理解为执行两个命令
* locate:用于快速查找文件名，依赖于数据库，通常会定期更新。
  >locate example.txt
  * locate 的速度比 find 快，它并不是真的查找，而是查数据库，一般文件数据库在 /var/lib/slocate/slocate.db 中，所以 locate 的查找并不是实时的，而是以数据库的更新为准，一般是系统自己维护，也可以手工升级数据库 ，命令为:
    >sudo updatedb
* find:用于在指定目录下递归查找文件和目录。
  >find . -name "example.txt"

查找当前目录及其子目录下名为example.txt的文件, . 用于查找当前目录
### 变更目录
* pwd 展示当前目录
* cd 切换工作目录
  * cd ~ ~代表当前用户主目录
  * cd .. 切换到父工作目录 ..代表父类
  * cd - 切换到之前的工作目录 -代表之前
* pushd /(directory name) 将当前目录压入堆栈并切换到当前目录
* popd 将栈顶目录弹出并切换到弹出后栈顶目录
* dirs 显示当前堆栈内容
* dir 作用类似于ls,是简略版
  > cd ~

  切换到当前用户的主目录

  > pwd

  /homebrain

  显示当前目录

  >pushd /tmp 

  将tmp目录压入堆栈中并切换到tmp目录

  >dirs

  /tmp ~

  显示当前堆栈,tmp表示栈顶,~表示栈底

  >popd

  >pwd

  ~ 显示的是弹出后栈顶的目录
#### 绝对路径与相对路径
绝对路径:路径的写法,由根目录 / 写起,例如: /usr/share/doc 这个目录。

相对路径:路径的写法,不是由 / 写起,例如由 /usr/share/doc 要到 /usr/share/man 底下时,可以写成: cd ../man 这就是相对路径的写法。
### 文件与目录的处理
* >pwd 显示当前目录
* >ls 列出目录的所有文件
  * >ls -a 列出所有文件,包括隐藏文件 -a代表all所有
  * >ls -d 只列出文件目录,-d代表directory目录
  * >ls -l 列出文件的长形式,-l代表long长形式
  * >tree 列出系统的目录结构
  * >mkdir (directory_name) 创建新的目录
  * >rmdir (directory_name) 删除目录
  * >cp (filename or directory_name) 复制文件或目录
  * >rm (filename or directory_name) 删除文件或目录
    * >rm -f -f代表强制
    * >rm -r -r代表递归
    * >rm-rf 强制递归删除,非常危险的选项
  * >mv (filename) (new directory) 移动文件到新目录
    * >mv (filename or directory name) (new filename or new directory name) 重命名文件或目录
#### Linux文件内容的查看
* >cat (filename) 从第一行显示文件的内容
  * >cat -b 列出行号,仅针对非空白行
  * >cat -n 列出行号,对所有行
* >tac (filename) 从文件的最后显示文件的内容
* >more (filename) 一页一页的显示内容
* >less (filename) 一页一页显示内容可以往前翻页,按q退出
* >head (filename) 只看头十行
* >tail (filename) 只看尾十行
### 改变文件时间戳
* >touch (filename) 修改文件时间戳为当前系统时间戳,如果没有该文件将创建文件
### 硬链接和软链接(符号链接)
硬链接:硬链接指向文件的物理位置。使用硬链接时,两个文件共享相同的 inode。
* >ln (原文件) (链接名)
* >ln -i  -i代表interaction交互模式,文件存在则提示用户是否覆盖
* >ln -f -f代表force强制执行

软链接(符号链接):符号链接是指向另一个文件或目录的引用,可以跨文件系统。
* >ln -s  (原文件) (链接名)
### 输入输出重定向
大多数 UNIX 系统命令从你的终端接受输入并将所产生的输出发送回​​到您的终端。
一个命令通常从一个叫标准输入的地方读取输入,默认情况下,这恰好是你的终端。
同样,一个命令通常将其输出写入到标准输出,默认情况下,这也是你的终端。
重定向命令列表如下:
|命令|说明|
|:--:|:--|
|command > file|将输出重定向到 file。|
|command < file |将输入重定向到 file。|
|command >> file |将输出以追加的方式重定向到 file。|
|n > file|将文件描述符为 n 的文件重定向到 file。|
|n >> file|将文件描述符为 n 的文件以追加的方式重定向到 file。|
|n >& m |将输出文件 m 和 n 合并。|
|n <& m |将输入文件 m 和 n 合并。|
*需要注意的是文件描述符 0 通常是标准输入(STDIN),1 是标准输出(STDOUT),2 是标准错误输出(STDERR)。*
1. 标准输出重定向：
    > command > file：将 command 的标准输出重定向到 file，如果文件已存在，会被覆盖。

    >command >> file：将 command 的标准输出追加到 file，而不是覆盖。

2. 标准错误重定向：
    >command 2> file：将 command 的标准错误重定向到 file。

    >command 2>> file：将 command 的标准错误追加到 file。

3. 同时重定向标准输出和标准错误：
    >command > file 2>&1：将标准输出和标准错误都重定向到同一个文件。

    >command &> file：在某些shell（如Bash）中，等同于上面的命令，重定向标准输出和标准错误到同一个文件。

4. 将输出丢弃：
    >command > /dev/null 2>&1：将标准输出和标准错误都丢弃，通常用于不希望看到任何输出的情况。

5. 管道：
    >command | another_command：将 command 的输出通过管道传递给 another_command。
### 通配符
1. *：匹配零个或多个字符。
例如：*.txt 匹配所有文本文件。

2. ?：匹配一个字符。
例如：file?.txt 匹配 file1.txt、fileA.txt 等。

3. [...]：匹配括号内的任意一个字符。
例如：file[1-3].txt 匹配 file1.txt、file2.txt 和 file3.txt。

4. {...}：匹配指定的任意选项。
例如：file{1,2}.txt 匹配 file1.txt 和 file2.txt。
### apt命令
apt（Advanced Packaging Tool）是一个在 Debian 和 Ubuntu 中的 Shell 前端软件包管理器。

apt 命令提供了查找、安装、升级、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

apt 命令执行需要超级管理员权限(root)。
1. 列出所有可更新的软件清单命令：

>sudo apt update

2. 升级已安装的包：

>sudo apt upgrade
  * 列出可更新的软件包及版本信息：
   
    > apt list --upgradable

3. 安装新包：

>sudo apt install package_name

4. 删除已安装的包：

>sudo apt remove package_name

5. 查找包：

>apt search package_name

6. 显示包的信息：

>apt show package_name
### man命令
Linux man 命令是 "manual" 单词的缩写，用于查看各种命令、函数和配置文件的手册页面。

通过 man 命令，您可以获取关于特定命令或主题的详细信息。
查看ls命令的手册页：
>man ls

对于函数（如库函数），可以使用man命令查看，例如man printf。手册页通常分为多个节，包括用户命令、系统调用、库函数等。要查看特定节，可以使用：
>man (option)(section)(number) (function_name)
* option:
  *  -f：显示与指定关键字相关的手册页面。
  *  -k：搜索手册页中与关键字匹配的条目。
  *  -a：显示所有匹配的手册页面。
  *  -w：仅显示手册页的位置，而不显示其内容。
* section:
  * 1：用户命令
  * 2：系统调用
  * 3：C库函数
  * 4：设备和特殊文件
  * 5：文件格式和约定
  * 6：游戏和演示
  * 7：杂项
  * 8：系统管理命令
### help命令
> (command) --help 查询命令行帮助
### process进程相关命令
* >ps 显示当前运行的进程信息
  * >ps aux 显示所有用户的进程信息
  * >ps -lf 显示进程的长格式信息
* F: 进程的标志位，显示进程的状态和特性。
* S: 进程状态（如 S - 睡眠，R - 运行，Z - 僵尸等）。
* UID: 进程所有者的用户 ID。
* PID: 进程 ID，系统分配给每个进程的唯一标识符。
* PPID: 父进程 ID，指向创建该进程的进程。
* C: CPU 使用率（在某些情况下表示进程的 CPU 时间百分比）。
* PRI: 进程的优先级。
* NI: 进程的 nice 值，影响其优先级。
* ADDR: 进程的内存地址（通常在现代系统中不常用）。
* SZ: 进程使用的虚拟内存大小，以页面为单位。
* WCHAN: 进程等待的内核函数名，如果进程在等待某个事件。
* TTY: 进程的终端类型，表示进程所连接的终端。
* TIME: 进程使用的 CPU 时间总和（以分秒形式表示）。
* CMD: 运行的命令或进程名称。 
* >top 查看进程和资源使用情况
  * PID: 进程ID，系统分配给每个进程的唯一标识符。
  * USER: 运行进程的用户或所有者。
  * PR: 进程的优先级（Priority）。
  * NI: 进程的“nice”值，影响进程的优先级。
  * VIRT: 进程使用的虚拟内存总量，包括所有映射的内存。
  * RES: 进程使用的常驻内存（物理内存）量。
  * SHR: 进程使用的共享内存量。
  * S: 进程的状态（如 R - 运行，S - 睡眠，Z - 僵尸等）。
  * %CPU: 进程占用的 CPU 百分比。
  * %MEM: 进程占用的物理内存百分比。
  * TIME+: 进程使用的 CPU 时间总和（以分秒形式表示）。
  * COMMAND: 运行的命令或进程名称。
* >htop 更加友好界面需要安装
* >kill (pid) 杀死指定进程号的进程
  * kill -9 (pid) 强制终止进程
* >renice 更改进程的优先级
  * >用法:renice priority PID

    >>renice -10 4368 将进程号为4368的进程优先级设置为-10
### Linux文件系统图示
![系统文件结构][https://image.baidu.com/search/detail?ct=503316480&z=undefined&tn=baiduimagedetail&ipn=d&word=Linux%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E5%9B%BE%E7%89%87&step_word=&lid=9315845612771150588&ie=utf-8&in=&cl=2&lm=-1&st=undefined&hd=undefined&latest=undefined&copyright=undefined&cs=2589106027,4202593476&os=3650427162,2531212261&simid=2589106027,4202593476&pn=0&rn=1&di=7410818322373017601&ln=1653&fr=&fmq=1728627783407_R&fm=&ic=undefined&s=undefined&se=&sme=&tab=0&width=undefined&height=undefined&face=undefined&is=0,0&istype=0&ist=&jit=&bdtype=0&spn=0&pi=0&gsm=1e&objurl=https%3A%2F%2Fdeveloper.qcloudimg.com%2Fhttp-save%2Fyehe-11039852%2Fa52d0e5bcc6e3d129e0a5a7b158ea783.png&rpstart=0&rpnum=0&adpicid=0&nojc=undefined&dyTabStr=MCwzLDEsMiwxMyw3LDYsNSwxMiw5&ctd=1728627785229^3_1920X919%1]