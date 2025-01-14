# java笔记
## 配置Java环境
1. 下载JDK
   * 访问Oracle官网下载对应系统版本的JDK安装包
   * 选择合适的版本（推荐LTS版本如JDK 8或JDK 11）
   * 运行安装程序，记住安装路径
2. 设置环境变量
   1. Windows 环境变量配置

       1. 设置 JAVA_HOME
           * 右键点击“此电脑”或“我的电脑”，选择“属性”。
           * 点击“高级系统设置” → “环境变量”。
           * 在“系统变量”区域点击“新建”，输入以下内容:
               变量名:JAVA_HOME
               变量值:JDK 安装路径（例如 C:\Program Files\Java\jdk-17）。
       2. 配置 PATH 变量
           在“系统变量”区域找到 Path 变量，点击编辑。
           添加 JDK 的 bin 目录路径，例如 C:\Program Files\Java\jdk-17\bin。

3. 验证安装
在命令提示符中输入:
```bash
java *version
javac *version
```
如显示版本信息则配置成功
## 第一个java程序
1. 创建project
2. 创建java文件
```java
public class Helloworld {
    public static void main(String[] args){
        System.out.println("helloworld!");
        System.out.print("helloworld!\n");//\n表示在输出后换行
    }
}
```
***//表示单行注释,/\*\*\/表示多行注释***
## 变量
1. 变量初始化

变量可以在声明时直接初始化，也可以在声明后单独初始化。语法如下:
```java
数据类型 变量名 = 初始值;
```
例如:
```java
int age = 25;
String name = "John Doe";
double salary = 50000.0;
```
2. 变量类型
   1. 基本数据类型

    |数据类型|大小(字节)|默认值|描述|
    |:--:|:--:|:--:|:--:|
    |byte|1|0|8位有符号整数|
    |short|2|0|16位有符号整数|
    |int|4|0|32位有符号整数|
    |long|8|0L|64位有符号整数|
    |float|4|0.0f|32位单精度浮点数|
    |double|8|0.0d|64位双精度浮点数
    |char|2|'\u0000'|16位Unicode字符|
    |boolean|1|false|布尔值(true或false)|
   1. 引用数据类型

    引用数据类型是指向对象的引用（类似于指针）。常见的引用数据类型包括:

    * 类:如<kbd>String</kbd>、<kbd>Integer</kbd>等。

    * 接口:如<kbd>List</kbd>、Map等。

    * 数组:如int[]、String[]等。
3. 变量的作用域

变量的作用域指的是变量在程序中可以被访问的范围。Java中的变量作用域可以分为以下几种:

* 局部变量:在方法、构造函数或块中声明的变量。它们只在声明它们的块中有效。

* 实例变量:在类中声明但在方法、构造函数或块之外的变量。它们属于对象的实例，每个对象都有其自己的实例变量副本。

* 类变量（静态变量）:使用static关键字声明的变量。它们属于类，而不是类的任何特定实例。所有实例共享同一个类变量。
    ```java
    public class VariableExample {
        // 实例变量
        int instanceVar = 10;

        // 类变量（静态变量）
        static int classVar = 20;

        public void method() {
            // 局部变量
            int localVar = 30;
            System.out.println("局部变量: " + localVar);
        }

        public static void main(String[] args) {
            VariableExample obj = new VariableExample();
            System.out.println("实例变量: " + obj.instanceVar);
            System.out.println("类变量: " + classVar);
            obj.method();
        }
    }
    ```

***变量的命名应遵循命名规范,通常使用驼峰命名法(如myVariableName).***
***类名使用大写字母开头（帕斯卡命名法）。(如MyClass)*** 
## java输入
1. 使用 Scanner 类

Scanner 类是Java中最常用的输入工具，它可以从控制台、文件或其他输入源读取数据。

步骤:

   1. 导入java.util.Scanner。

   2. 创建Scanner对象。

   3. 使用Scanner的方法读取输入。

常用方法:

* <kbd>next()</kbd>:读取一个字符串（以空格或换行符分隔）。

* <kbd>nextInt()</kbd>:读取一个整数。

* <kbd>nextDouble()</kbd>:读取一个双精度浮点数。

* <kbd>nextLine()</kbd>:读取一行字符串（包括空格）。

示例代码:
```java

import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        // 创建 Scanner 对象
        Scanner scanner = new Scanner(System.in);

        // 读取整数
        System.out.print("请输入一个整数: ");
        int num = scanner.nextInt();
        System.out.println("你输入的整数是: " + num);

        // 读取浮点数
        System.out.print("请输入一个浮点数: ");
        double decimal = scanner.nextDouble();
        System.out.println("你输入的浮点数是: " + decimal);

        // 读取字符串（单个单词）
        System.out.print("请输入一个单词: ");
        String word = scanner.next();
        System.out.println("你输入的单词是: " + word);

        // 读取一行字符串
        scanner.nextLine(); // 清除缓冲区
        System.out.print("请输入一行文字: ");
        String line = scanner.nextLine();
        System.out.println("你输入的文字是: " + line);

        // 关闭 Scanner
        scanner.close();
    }
}
```
***(不换行时候)在使用nextInt()或nextDouble()后，如果紧接着使用nextLine()，可能会读取到空行。这是因为nextInt()不会读取换行符，而nextLine()会读取换行符。处理嫌麻烦输出时println换行即可***
2. 使用 BufferedReader 类

BufferedReader 类是一个更高效的输入工具，通常与InputStreamReader一起使用。它适合读取大量数据。
步骤:

* 导入java.io.BufferedReader和java.io.InputStreamReader。

* 创建BufferedReader对象。

* 使用readLine()方法读取输入。

示例代码:
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class BufferedReaderExample {
    public static void main(String[] args) throws IOException {
        // 创建 BufferedReader 对象
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

        // 读取字符串
        System.out.print("请输入你的名字: ");
        String name = reader.readLine();
        System.out.println("你好, " + name + "!");

        // 读取整数
        System.out.print("请输入你的年龄: ");
        int age = Integer.parseInt(reader.readLine());
        System.out.println("你的年龄是: " + age);

        // 读取浮点数
        System.out.print("请输入你的身高: ");
        double height = Double.parseDouble(reader.readLine());
        System.out.println("你的身高是: " + height);

        // 关闭 BufferedReader
        reader.close();
    }
}
```
## java 数学运算
1. 加法:+
2. 减法:-
3. 乘法:*
4. 除法:/
5. 取整除://
6. 取余:%
7. 幂运算:
```java
double result = Math.pow(2, 3); // result = 8.0 (2的3次方)
```
8. 自增运算符 (++)
* 用于将变量的值增加1。

```java
int a = 5;
a++; // a = 6
```
* 前缀自增 (++a) 和后缀自增 (a++) 的区别:
  * 前缀自增:先增加，再使用。
  * 后缀自增:先使用，再增加。

```java
int a = 5;
int b = ++a; // a = 6, b = 6

int c = 5;
int d = c++; // c = 6, d = 5
```
9. 自减运算符 (--)
* 用于将变量的值减少1。

```java
int a = 5;
a--; // a = 4
```
* 前缀自减 (<kbd>--a</kbd>) 和后缀自减 (<kbd>a--</kbd>) 的区别:

    * 前缀自减:先减少，再使用。

    * 后缀自减:先使用，再减少。

```java
int a = 5;
int b = --a; // a = 4, b = 4

int c = 5;
int d = c--; // c = 4, d = 5
```
10. 三元运算符 (? :)
* 虽然不是严格的数学运算符，但它可以用于条件判断。
```java
int a = 5;
int b = 3;
int max = (a > b) ? a : b; // max = 5
```
## if 语句
1. <kbd>if</kbd>语句

* 如果条件为<kbd>true</kbd>，则执行 if 块中的代码。

```java
int a = 10;
if (a > 5) {
    System.out.println("a 大于 5");
}
```
2. <kbd>if-else</kbd>语句
* 如果 if 条件为 true，执行 if 块中的代码；否则执行 else 块中的代码。

```java
int a = 3;
if (a > 5) {
    System.out.println("a 大于 5");
} else {
    System.out.println("a 小于或等于 5");
}
```
3. <kbd>if-else if-else</kbd>语句

* 用于多个条件的判断。如果第一个 if 条件为 false，则检查下一个 else if 条件；如果所有条件都为 false，则执行 else 块中的代码。

```java
int a = 7;
if (a > 10) {
    System.out.println("a 大于 10");
} else if (a > 5) {
    System.out.println("a 大于 5 但小于或等于 10");
} else {
    System.out.println("a 小于或等于 5");
}
```
## 数学类
1. 基本数学运算
* 绝对值:<kbd>Math.abs()</kbd>
    ```java
    int a = -10;
    int absValue = Math.abs(a); // absValue = 10
    ```
* 最大值和最小值:<kbd>Math.max()</kbd>和<kbd>Math.min()</kbd>
    ```java
    int max = Math.max(5, 10); // max = 10
    int min = Math.min(5, 10); // min = 5
    ```
* 四舍五入:<kbd>Math.round()</kbd>
    ```java
    double num = 3.6;
    long rounded = Math.round(num); // rounded = 4
    ```
* 向上取整:Math.ceil()
    ```java
    double num = 3.2;
    double ceilValue = Math.ceil(num); // ceilValue = 4.0
    ```
* 向下取整:Math.floor()
    ```java
    double num = 3.9;
    double floorValue = Math.floor(num); // floorValue = 3.0
    ```
2. 幂运算和开方
* 幂运算:Math.pow()
    ```java
    double result = Math.pow(2, 3); // 2的3次方，result = 8.0
    ```
* 平方根:Math.sqrt()
    ```java
    double sqrtValue = Math.sqrt(16); // sqrtValue = 4.0
    ```
3. 随机数
* 生成随机数:Math.random()
  * 返回一个 [0.0, 1.0) 之间的随机浮点数。
    ```java
    double randomValue = Math.random(); // 例如:0.123456
    ```
  * 生成指定范围的随机整数(例如 1 到 100):
    ```java
    int randomInt = (int) (Math.random() * 100) + 1; // 1 到 100 之间的随机整数
    ```
## printf函数
printf 是 Java 中用于格式化输出的方法,属于PrintStream类(如 System.out).它允许你使用格式化字符串来控制输出的格式,类似于 C 语言中的 printf 函数。
基本语法
```java
System.out.printf(String format, Object... args);
```
* format:格式化字符串,包含普通文本和格式说明符。
* args:可变参数,用于替换格式说明符。
常用格式说明符

|格式说明符|说明|
|:--:|:--:|
|%d|十进制整数|
|%f|浮点数|
|%s|字符串|
|%c|字符|
|%b|布尔值|
|%n|换行符|
|%%|百分号|
```java
public class PrintfExample {
    public static void main(String[] args) {
        int age = 25;
        double height = 1.75;
        String name = "Alice";

        // 格式化输出
        System.out.printf("Name: %s, Age: %d, Height: %.2f meters%n", name, age, height);

        // 输出布尔值
        boolean isStudent = true;
        System.out.printf("Is student: %b%n", isStudent);

        // 输出字符
        char grade = 'A';
        System.out.printf("Grade: %c%n", grade);

        // 输出百分号
        System.out.printf("Progress: %d%%%n", 75);
    }
}
```
输出结果
```java
Name: Alice, Age: 25, Height: 1.75 meters
Is student: true
Grade: A
Progress: 75%
```
格式化选项

* 宽度：指定最小字段宽度，如 %10s 表示字符串至少占 10 个字符宽度。

* 精度：对于浮点数，可以指定小数点后的位数，如 %.2f 表示保留两位小数。

* 对齐：使用 - 表示左对齐，如 %-10s。

示例：宽度和精度
```java
System.out.printf("%-10s %5d %6.2f%n", "Alice", 25, 1.75);
System.out.printf("%-10s %5d %6.2f%n", "Bob", 30, 1.80);
```

输出结果
```java
Alice      25   1.75
Bob        30   1.80
```
## if嵌套
4. 嵌套的 if 语句

可以在一个 if 或 else 块中嵌套另一个 if 语句。

```java
int a = 12;
if (a > 10) {
    if (a > 15) {
        System.out.println("a 大于 15");
    } else {
        System.out.println("a 大于 10 但小于或等于 15");
    }
} else {
    System.out.println("a 小于或等于 10");
}
```
## 字符串方法
1. 字符串长度

* length()：返回字符串的长度。
    ```java
    String str = "Hello";
    int len = str.length(); // len = 5
    ```

2. 字符串拼接

* concat(String str)：将指定字符串连接到当前字符串的末尾。
    ```java
    String str1 = "Hello";
    String str2 = "World";
    String result = str1.concat(" ").concat(str2); // result = "Hello World"
    ```
* \+ 运算符：也可以用于字符串拼接。
    ```java
    String result = str1 + " " + str2; // result = "Hello World"
    ```
3. 字符串比较
* equals(Object obj)：比较字符串内容是否相等（区分大小写）。
    ```java
    String str1 = "Hello";
    String str2 = "hello";
    boolean isEqual = str1.equals(str2); // isEqual = false
    ```
* equalsIgnoreCase(String str)：比较字符串内容是否相等（不区分大小写）。
    ```java
    boolean isEqualIgnoreCase = str1.equalsIgnoreCase(str2); // isEqualIgnoreCase = true
    ```