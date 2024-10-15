# Shell笔记
## 第一个shell程序
打开文本编辑器(可以使用 vi/vim 命令来创建文件)，新建一个文件 test.sh，扩展名为 sh（sh代表shell），扩展名并不影响脚本执行，见名知意就好，如果你用 php 写 shell 脚本，扩展名就用 php 好了。 
>#!/bin/bash

>echo "Hello World !"
## 运行shell脚本
作为可执行程序

将上面的代码保存为 test.sh，并 cd 到相应目录：
>chmod +x ./test.sh  #使脚本具有执行权限

>./test.sh  #执行脚本
## Shell变量
在 Shell 编程中，变量是用于存储数据值的名称。
定义变量时，变量名不加美元符号（$，PHP语言中变量需要），如：
>your_name="runoob"
### 使用变量
使用一个定义过的变量，只要在变量名前面加美元符号即可，如：
>your_name="qinjx"

>echo $your_name

>echo ${your_name}

***尽量使用花括号***
### 只读变量
使用 readonly 命令可以将变量定义为只读变量，只读变量的值不能被改变。
>myUrl="https://www.google.com"

>readonly myUrl

>myUrl="https://www.runoob.com"

### 删除变量
变量被删除后不能再次使用。unset 命令不能删除只读变量。
>#!/bin/sh

>myUrl="https://www.runoob.com"

>unset myUrl

>echo $myUrl
以上实例执行将没有任何输出。
### 变量类型
* 字符串类型:在 Shell中，变量通常被视为字符串。你可以使用单引号 ' 或双引号 " 来定义字符串，例如：
    >my_string='Hello, World!'

    或者

    >my_string="Hello, World!"
* 整数类型:在一些Shell中，你可以使用 declare 或 typeset 命令来声明整数变量。这样的变量只包含整数值，例如：
    >declare -i my_integer=42

    -i代表integer，整形 
* 数组变量: Shell 也支持数组，允许你在一个变量中存储多个值。数组可以是整数索引数组或关联数组，以下是一个简单的整数索引数组的例子：
    >my_array=(1 2 3 4 5)

    或者关联数组

    >declare -A associative_array

    >associative_array["name"]="John"

    > associative_array["age"]=30
* 环境变量:这些是由操作系统或用户设置的特殊变量，用于配置 Shell 的行为和影响其执行环境。例如，PATH 变量包含了操作系统搜索可执行文件的路径：
    >echo $PATH
* 特殊变量:有一些特殊变量在 Shell 中具有特殊含义，例如 $0 表示脚本的名称，$1, $2, 等表示脚本的参数。$#表示传递给脚本的参数数量，$? 表示上一个命令的退出状态等。
### Shell字符串
字符串是shell编程中最常用最有用的数据类型（除了数字和字符串，也没啥其它类型好用了），字符串可以用单引号，也可以用双引号，也可以不用引号。 
#### 单引号
>str='this is a string'

单引号字符串的限制：
  * 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
  * 单引号字符串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。
#### 双引号
```shell
your_name="runoob"

str="Hello, I know you are \"$your_name\"! \n"

echo -e $str -e代表识别特殊字符
```

输出结果为：

>Hello, I know you are "runoob"! 

双引号的优点：
  * 双引号里可以有变量
  * 双引号里可以出现转义字符
```
your_name="runoob"

#使用双引号拼接

greeting="hello, "$your_name" !"

greeting_1="hello, ${your_name} !"

echo $greeting  $greeting_1

#使用单引号拼接

greeting_2='hello, '$your_name' !'

greeting_3='hello, ${your_name} !'

echo $greeting_2  $greeting_3
```

输出结果为：

>hello, runoob ! hello, runoob !

>hello, runoob ! hello, ${your_name} !
#### 获取字符串长度

>string="abcd"

>echo ${#string}   # 输出 4
变量为字符串时，\${#string} 等价于 ${#string[0]}:

>string="abcd"

>echo ${#string[0]}   # 输出 4
#### 提取子字符串
以下实例从字符串第 2 个字符开始截取 4 个字符：
>string="runoob is a great site"

>echo ${string:1:4} # 输出 unoo
#### 查找子字符串
查找字符i或o的位置(哪个字母先出现就计算哪个)：
>string="runoob is a great site"

>echo `expr index "$string" io`  # 输出 4

注意： 以上脚本中 ` 是反引号，而不是单引号 '，不要看错了哦。
#### Shell数组
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

类似于 C 语言，数组元素的下标由 0 开始编号。获取数组中的元素要利用下标，下标可以是整数或算术表达式，其值应大于或等于 0。 
##### 定义数组
在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。定义数组的一般形式为： 
>数组名=(值1 值2 ... 值n)
例如:
>array_name=(value0 value1 value2 value3)
或者

```shell
array_name=(

value0

value1

value2

value3

)
```
还可以单独定义数组的各个分量：
```shell
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```
可以不使用连续的下标，而且下标的范围没有限制。
##### 读取数组
读取数组元素值的一般格式是：
>${数组名[下标]}

例如：
>valuen=${array_name[n]}

使用 @ 符号可以获取数组中的所有元素，例如：
>echo ${array_name[@]}
##### 获取数组的长度
获取数组长度的方法与获取字符串长度的方法相同，例如：
```shell
# 取得数组元素的个数
length=${#array_name[@]}

# 或者
length=${#array_name[*]}

# 取得数组单个元素的长度
length=${#array_name[n]}
```
#### Shell 注释
以 # 开头的行就是注释，会被解释器忽略。
通过每一行加一个 # 号设置多行注释，像这样：
```shell
#--------------------------------------------
# 这是一个注释
# author：菜鸟教程
# site：www.runoob.com
# slogan：学的不仅是技术，更是梦想！
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
#
#
##### 用户配置区 结束  #####
``` 
如果在开发过程中，遇到大段的代码需要临时注释起来，过一会儿又取消注释，怎么办呢？

每一行加个#符号太费力了，可以把这一段要注释的代码用一对花括号括起来，定义成一个函数，没有地方调用这个函数，这块代码就不会执行，达到了和注释一样的效果。
##### 多行注释
使用 Here 文档

多行注释还可以使用以下格式： 
```shell
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```
以上例子中，: 是一个空命令，用于执行后面的 Here 文档，<<'EOF' 表示开启 Here 文档，COMMENT 是 Here 文档的标识符，在这两个标识符之间的内容都会被视为注释，不会被执行。

EOF 也可以使用其他符号:
```shell
: <<'COMMENT'
这是注释的部分。
可以有多行内容。
COMMENT
```
```shell
:<<'
注释内容...
注释内容...
注释内容...
'
```
```shell
:<<!
注释内容...
注释内容...
注释内容...
!
```
