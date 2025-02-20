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
## random函数
1. 导入包
```java
import java.util.Random
```
2. 创建对象
```java
Random random=new random();
```
3. 生成随机数
```java
int number;
number =random.nextInt(1,6);
System.out.println(number)
//左闭右开取1-5的值
double number;
number =random.nextDouble();
System.out.println(number)
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
1. 幂运算和开方
* 幂运算:Math.pow()
    ```java
    double result = Math.pow(2, 3); // 2的3次方，result = 8.0
    ```
* 平方根:Math.sqrt()
    ```java
    double sqrtValue = Math.sqrt(16); // sqrtValue = 4.0
    ```
1. 随机数
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
4. 字符串查找
* charAt(int index)：返回指定索引处的字符。
    ```java
    char ch = str1.charAt(1); // ch = 'e'
    ```
* indexOf(String str)：返回指定子字符串第一次出现的索引。
    ```java
    int index = str1.indexOf("lo"); // index = 3
    ```
* lastIndexOf(String str)：返回指定子字符串最后一次出现的索引。
    ```java
    int lastIndex = str1.lastIndexOf("l"); // lastIndex = 3
    ```
* contains(CharSequence s)：检查字符串是否包含指定子字符串。
    ```java
    boolean contains = str1.contains("ell"); // contains = true
    ```
5. 字符串截取
* substring(int beginIndex)：从指定索引开始截取字符串。
    ```java
    String subStr = str1.substring(1); // subStr = "ello"
    ```
* substring(int beginIndex, int endIndex)：截取指定索引范围内的字符串。
    ```java
    String subStr = str1.substring(1, 4); // subStr = "ell"
    ```
6. 字符串替换
* replace(char oldChar, char newChar)：替换字符串中的字符。
    ```java
    String newStr = str1.replace('l', 'L'); // newStr = "HeLLo"
    ```
7. 字符串大小写转换
* toLowerCase()：将字符串转换为小写。
   ```java
    String lowerStr = str1.toLowerCase(); // lowerStr = "hello"
    ```
* toUpperCase()：将字符串转换为大写。
    ```java
    String upperStr = str1.toUpperCase(); // upperStr = "HELLO"
    ```
8. 字符串修剪
* trim()：去除字符串两端的空白字符。
    ```java
    String str = "  Hello  ";
    String trimmedStr = str.trim(); // trimmedStr = "Hello"
    ```

9. 字符串分割
* split(String regex)：根据正则表达式分割字符串。
    ```java
    String str = "Hello,World,Java";
    String[] parts = str.split(","); // parts = ["Hello", "World", "Java"]
    ```
10. 字符串检查
* isEmpty()：检查字符串是否为空。
    ```java
    boolean isEmpty = str1.isEmpty(); // isEmpty = false
    ```
* startsWith(String prefix)：检查字符串是否以指定前缀开头。
    ```java
    boolean startsWith = str1.startsWith("He"); // startsWith = true
    ```
* endsWith(String suffix)：检查字符串是否以指定后缀结尾。
    ```java
    boolean endsWith = str1.endsWith("lo"); // endsWith = true
    ```
11. 字符串重复
* repeat(int count)（Java 11+）：重复字符串指定次数。
    ```java
    String repeatedStr = str1.repeat(3); // repeatedStr = "HelloHelloHello"
    ```
## switch...case判断
在 Java 中，switch-case 是一种多分支选择结构，用于根据变量的值执行不同的代码块。它比多个 if-else 语句更简洁和易读，特别适合处理多个固定值的场景。
```java
switch (expression) {
    case value1:
        // 当 expression 等于 value1 时执行的代码
        break;
    case value2:
        // 当 expression 等于 value2 时执行的代码
        break;
    // 可以有任意数量的 case 语句
    default:
        // 当 expression 不匹配任何 case 时执行的代码
}
```
* expression：可以是 byte、short、int、char、String（Java 7+）或枚举类型。
* case：每个 case 后面跟一个常量值，用于与 expression 进行比较。
* break：用于退出 switch 语句。如果没有 break，程序会继续执行后续的 case 代码（称为“贯穿”）。
* default：当 expression 不匹配任何 case 时执行的代码块（可选）。
Java 12+ 的增强 switch 表达式

示例 ：贯穿现象

如果没有 break，程序会继续执行后续的 case 代码，直到遇到 break 或 switch 结束。
```java
int num = 2;
String result;

switch (num) {
    case 1:
    case 2:
    case 3:
        result = "Small number";
        break;
    case 4:
    case 5:
    case 6:
        result = "Medium number";
        break;
    default:
        result = "Large number";
}

System.out.println(result); // 输出：Small number
```
### 从 Java 12 开始，switch 支持更简洁的语法，并且可以作为表达式返回值。
```java
int day = 3;
String dayName = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    case 4 -> "Thursday";
    case 5 -> "Friday";
    case 6 -> "Saturday";
    case 7 -> "Sunday";
    default -> "Invalid day";
};

System.out.println("Day: " + dayName); // 输出：Day: Wednesday
```
在 Java 的增强 switch 表达式（Java 12+）中，如果某个 case 需要执行多行代码，可以使用 {} 包裹代码块，并通过 yield 返回值。这种方式既保留了增强 switch 表达式的简洁性，又支持复杂的逻辑。
```java
result = switch (expression) {
    case value -> {
        // 多行代码
        yield resultValue; // 使用 yield 返回值
    }
    // 其他 case
};
```
```java
int day = 2;
String message = switch (day) {
    case 1 -> {
        System.out.println("It's Monday!");
        yield "Start of the week"; // 使用 yield 返回值
    }
    case 2 -> {
        System.out.println("It's Tuesday!");
        yield "Second day of the week";
    }
    case 3 -> {
        System.out.println("It's Wednesday!");
        yield "Midweek";
    }
    default -> "Invalid day";
};

System.out.println(message);
```
* <kbd>{}</kbd>:用于包裹多行代码。

* <kbd>yield</kbd>:用于返回结果值（类似于 return，但专门用于 switch 表达式）。
## 逻辑运算符
常用逻辑运算符

|运算符|名称|描述|
|:--:|:--:|:--:|
|<kbd>&&</kbd>|逻辑与|两个条件都为 true 时，结果为 true；否则为 false。
|<kbd>\|\|</kbd>|逻辑或|至少一个条件为 true 时，结果为 true；否则为 false。|
|<kbd>!</kbd>|逻辑非|对条件取反，true 变 false，false 变 true。
## while循环与do-while循环
在 Java 中，while 循环是一种条件循环，它会重复执行一段代码，直到指定的条件不再满足为止。while 循环适合在不确定循环次数的情况下使用。
1. 基本语法
```java
while (条件) {
    // 循环体（需要重复执行的代码）
}
```
* 条件：一个布尔表达式。如果条件为 true，则执行循环体；如果为 false，则退出循环。
* 循环体：需要重复执行的代码块。
2. 执行流程
    1. 检查条件是否为 true。
    2. 如果条件为 true，执行循环体。
    3. 执行完循环体后，再次检查条件。
    4. 重复上述步骤，直到条件为 false，退出循环。
3. 示例

    示例 1：打印 1 到 5
    ```java
    int i = 1;
    while (i <= 5) {
        System.out.println(i);
        i++; // 更新条件变量
    }
    ```
    输出：
    ```java
    1
    2
    3
    4
    5
    ```
4. do-while 循环

do-while 循环是 while 循环的变体，它会先执行一次循环体，再检查条件。即使条件一开始就不满足，循环体也会至少执行一次。

语法
```java
do {
    // 循环体
} while (条件);
```
示例
```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```
输出：
```java
1
2
3
4
5
```
## for循环
在 Java 中，for 循环是一种计数循环，用于在已知循环次数的情况下重复执行一段代码。for 循环的语法简洁明了，适合遍历数组、集合或执行固定次数的操作。
1. 基本语法
```java
for (初始化; 条件; 更新) {
    // 循环体（需要重复执行的代码）
}
```
* 初始化：在循环开始前执行一次，通常用于初始化循环变量。
* 条件：一个布尔表达式。如果条件为 true，则执行循环体；如果为 false，则退出循环。
* 更新：在每次循环结束后执行，通常用于更新循环变量。
* 循环体：需要重复执行的代码块。

示例 1：打印 1 到 5
```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```
输出：
```java
1
2
3
4
5
```

for 循环可以嵌套使用，常用于处理多维数组或复杂的逻辑。

示例：打印九九乘法表
```java
for (int i = 1; i <= 9; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j + "×" + i + "=" + (i * j) + "\t");
    }
    System.out.println();
}
```
输出：
```java
1×1=1	
1×2=2	2×2=4	
1×3=3	2×3=6	3×3=9	
...
1×9=9	2×9=18	3×9=27	...	9×9=81
```
2. break 终止循环：
     ```java
     int count = 0
     while(True){
         count += 1;
     if(count == 5){
        break;s
        }
     } 
     ```
3. continue 跳过当前迭代：
<kbd>continue</kbd>语句可以跳过当前循环的其余部分，直接开始下一次迭代。

## 方法

在Java中，方法（Method）是类或对象的行为的体现，用于执行特定的任务或操作。方法可以接受输入参数并返回结果。以下是Java方法的基本结构和一些关键概念：
1. 方法的基本结构
```java
[访问修饰符] [返回类型] 方法名([参数列表]) {
    // 方法体
    // 执行具体的操作
    return [返回值]; // 如果返回类型不是void
}
```
* 访问修饰符：控制方法的访问权限，如 public、private、protected 或默认（无修饰符）。
* 返回类型：方法返回的数据类型，如 int、String、void（表示不返回任何值）等。
* 方法名：方法的名称，遵循标识符命名规则。
* 参数列表：方法接受的输入参数，可以有多个参数，用逗号分隔。
* 方法体：包含具体的执行代码。
* return 语句：用于返回方法的结果（如果返回类型不是 void）。
2. 示例
```java
public class Calculator {

    // 一个简单的加法方法
    public int add(int a, int b) {
        return a + b;
    }

    // 一个没有返回值的方法
    public void printMessage(String message) {
        System.out.println(message);
    }

    // 主方法，程序的入口
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        int result = calc.add(5, 3); // 调用add方法
        System.out.println("5 + 3 = " + result);

        calc.printMessage("Hello, Java!"); // 调用printMessage方法
    }
}
```
3. 方法的重载（Overloading）

Java允许在同一个类中定义多个同名方法，只要它们的参数列表不同（参数类型、数量或顺序不同）。这称为方法重载。
```java
public class MathOperations {

    // 重载的add方法
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        MathOperations math = new MathOperations();
        System.out.println(math.add(2, 3)); // 调用int add(int, int)
        System.out.println(math.add(2.5, 3.5)); // 调用double add(double, double)
        System.out.println(math.add(2, 3, 4)); // 调用int add(int, int, int)
    }
}
```
4. 静态方法

静态方法属于类而不是类的实例，可以通过类名直接调用。静态方法不能访问非静态成员（变量或方法）。
```java
public class MathUtils {

    // 静态方法
    public static int square(int num) {
        return num * num;
    }

    public static void main(String[] args) {
        int result = MathUtils.square(4); // 直接通过类名调用
        System.out.println("4的平方是: " + result);
    }
}
```
5. 可变参数（Varargs）

Java支持可变参数，允许方法接受不定数量的参数。
```java
public class VarargsExample {

    // 可变参数方法
    public int sum(int... numbers) {
        int sum = 0;
        for (int num : numbers) {
            sum += num;
        }
        return sum;
    }

    public static void main(String[] args) {
        VarargsExample example = new VarargsExample();
        System.out.println("Sum: " + example.sum(1, 2, 3)); // 输出 6
        System.out.println("Sum: " + example.sum(1, 2, 3, 4, 5)); // 输出 15
    }
}
```
6. 方法的调用

方法可以通过对象实例调用，如果是静态方法，则可以通过类名直接调用。
```java
ClassName obj = new ClassName();
obj.methodName(arguments); // 实例方法调用

ClassName.staticMethodName(arguments); // 静态方法调用
```
7. 方法的返回值

方法可以返回一个值，返回值的类型必须与方法声明中的返回类型匹配。如果方法返回类型为 void，则不需要<kbd>return</kbd>语句，或者可以使用<kbd>return</kbd>; 来提前结束方法。
```java
public int getMax(int a, int b) {
    return (a > b) ? a : b;
}
```
## 变量范围

变量的作用域指的是变量在程序中可以被访问的范围。Java中的变量作用域可以分为以下几种：

1. 局部变量：在方法、构造函数或块中声明的变量。它们只在声明它们的块中有效。
```java
public class LocalVariableExample {
    public void printNumber() {
        // 局部变量
        int num = 10; // num 只在 printNumber 方法中有效
        System.out.println("局部变量 num: " + num);
    }

    public static void main(String[] args) {
        LocalVariableExample obj = new LocalVariableExample();
        obj.printNumber(); // 输出: 局部变量 num: 10

        // 以下代码会报错，因为 num 是局部变量，不能在方法外访问
        // System.out.println(num);
    }
}
```
2. 实例变量：在类中声明但在方法、构造函数或块之外的变量。它们属于对象的实例，每个对象都有其自己的实例变量副本。
```java
public class InstanceVariableExample {
    // 实例变量
    int num; // 默认值为 0

    public void setNumber(int num) {
        this.num = num; // 使用 this 关键字引用当前对象的实例变量
    }

    public void printNumber() {
        System.out.println("实例变量 num: " + num);
    }

    public static void main(String[] args) {
        InstanceVariableExample obj1 = new InstanceVariableExample();
        InstanceVariableExample obj2 = new InstanceVariableExample();

        obj1.setNumber(10); // 设置 obj1 的 num
        obj2.setNumber(20); // 设置 obj2 的 num

        obj1.printNumber(); // 输出: 实例变量 num: 10
        obj2.printNumber(); // 输出: 实例变量 num: 20
    }
}
```
3. 类变量（静态变量）：使用static关键字声明的变量。它们属于类，而不是类的任何特定实例。所有实例共享同一个类变量。
```java
public class StaticVariableExample {
    // 类变量（静态变量）
    static int num; // 默认值为 0

    public void setNumber(int num) {
        StaticVariableExample.num = num; // 使用类名访问静态变量
    }

    public void printNumber() {
        System.out.println("类变量 num: " + num);
    }

    public static void main(String[] args) {
        StaticVariableExample obj1 = new StaticVariableExample();
        StaticVariableExample obj2 = new StaticVariableExample();

        obj1.setNumber(10); // 设置类变量 num
        obj2.setNumber(20); // 修改类变量 num

        obj1.printNumber(); // 输出: 类变量 num: 20
        obj2.printNumber(); // 输出: 类变量 num: 20

        // 直接通过类名访问静态变量
        System.out.println("直接访问类变量 num: " + StaticVariableExample.num); // 输出: 20
    }
}
```
## 数组
在Java中，数组是一种用于存储固定数量同类型元素的数据结构。数组中的元素可以通过索引访问，索引从0开始。以下是关于Java数组的一些基本概念和操作：

1. 声明数组

你可以通过以下方式声明一个数组：
```java
// 声明一个整型数组
int[] myArray;

// 声明一个字符串数组
String[] stringArray;
```
2. 创建数组

声明数组后，你需要使用new关键字来创建数组，并指定数组的大小：
```java

// 创建一个可以存储5个整数的数组
myArray = new int[5];

// 创建一个可以存储3个字符串的数组
stringArray = new String[3];
//也可以创建一个数组来隐式指定数组大小
int[] myArray = {1,2,3,4,5} //数组大小为5
```
你也可以在声明数组的同时进行初始化：
```java
// 声明并初始化一个整型数组
int[] myArray = {1, 2, 3, 4, 5};

// 声明并初始化一个字符串数组
String[] stringArray = {"Hello", "World", "Java"};
```
3. 访问数组元素

你可以通过索引访问数组中的元素。数组的索引从0开始：
```java
int[] myArray = {10, 20, 30, 40, 50};

// 访问第一个元素
int firstElement = myArray[0]; // 10

// 访问第三个元素
int thirdElement = myArray[2]; // 30
```
4. 修改数组元素

你可以通过索引修改数组中的元素：
```java
int[] myArray = {10, 20, 30, 40, 50};

// 修改第二个元素
myArray[1] = 25;

// 现在数组变为 {10, 25, 30, 40, 50}
```
5. 数组的长度

你可以使用length属性来获取数组的长度：
```java

int[] myArray = {10, 20, 30, 40, 50};

int arrayLength = myArray.length; // 5
```
6. 遍历数组

你可以使用for循环或for-each循环来遍历数组：
```java
int[] myArray = {10, 20, 30, 40, 50};

// 使用for循环遍历数组
for (int i = 0; i < myArray.length; i++) {
    System.out.println(myArray[i]);
}

// 使用for-each循环遍历数组
for (int num : myArray) {
    System.out.println(num);
}
```
7. 多维数组

Java也支持多维数组，最常见的是二维数组：
```java

// 声明并初始化一个二维数组
int[][] twoDArray = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// 访问二维数组中的元素
int element = twoDArray[1][2]; // 6
// 遍历输出二维数组元素
for(int[] row:twoDArray){
    for(int num:row){
        System.out.print(num + " ")
    }
    System.out.println()
}
```
8. 数组的常见操作
* 数组排序:可以使用<kbd>Arrays.sort()</kbd>方法对数组进行排序。
* 数组复制:可以使用<kbd>System.arraycopy()</kbd>或<kbd>Arrays.copyOf()</kbd>方法复制数组。
* 数组填充:可以使用<kbd>Arrays.fill()</kbd>方法填充数组。

```java
import java.util.Arrays;

public class ArrayExample {
    public static void main(String[] args) {
        int[] myArray = {5, 3, 1, 4, 2};

        // 排序数组
        Arrays.sort(myArray); // {1, 2, 3, 4, 5}

        // 复制数组
        int[] copiedArray = Arrays.copyOf(myArray, myArray.length);

        // 填充数组
        Arrays.fill(myArray, 0); // {0, 0, 0, 0, 0}
    }
}
```
***
***通过用户输入转为数组输出***

```java
 public static void main(String[] args)throws IOException{
        BufferedReader reader=new BufferedReader(new InputStreamReader(System.in));
        String[] foods;
        int num;
        System.out.print("input a number you want input");
        num= Integer.parseInt(reader.readLine());
        foods=new String[num];
        for(int i=0;i<foods.length;i++){
            System.out.println("input a food ");
            foods[i] = reader.readLine();
        }
        for(String food:foods){
            System.out.println(food +" " );
        }
        reader.close();
    }
```
***
### 在数组内搜索元素
```java
public class Helloworld {
    public static void main(String[] args)throws IOException{
        BufferedReader reader=new BufferedReader(new InputStreamReader(System.in));
        String[] fruits={"apple","orange","banana"};
        int[] num={1,2,3,4,5};
        boolean isFound=false;
        System.out.print("input a fruit you wang to search: ");
        String fruit = reader.readLine();
        for(int i=0;i<fruits.length;i++){
            if (fruits[i].equals(fruit)){
                System.out.print("element found in index: "+ i);
                isFound=true;
            }
        }
        if (!isFound){
            System.out.print("element not found!");
        }

        reader.close();
    }
}
```
## 面向对象编程
Java 面向对象编程（OOP，Object-Oriented Programming）是 Java 编程语言的一种编程范式，它将程序组织成由类和对象构成的结构。面向对象编程有四大基本特性
1. 类（Class）和对象（Object）
   * 类：类是对象的模板或蓝图，定义了对象的属性和行为。类包含字段（属性）和方法（行为）。
   * 对象：对象是类的实例，具有类定义的属性和行为。

示例：
```java
// 定义一个类
class Dog {
    // 属性（字段）
    String name;
    int age;

    // 行为（方法）
    void bark() {
        System.out.println(name + " is barking!");
    }
}

// 创建对象
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog(); // 创建Dog类的对象
        myDog.name = "Buddy";  // 设置属性
        myDog.age = 3;
        myDog.bark();          // 调用方法
    }
}
```
2. 封装（Encapsulation）
   * 封装是将数据（属性）和行为（方法）绑定在一起，并隐藏内部实现细节，只暴露必要的接口。
   * 通过访问修饰符（private、protected、public）控制对类的属性和方法的访问。

示例：
```java
class Person {
    // 私有属性，外部不能直接访问
    private String name;
    private int age;

    // 公共方法，提供访问和修改属性的接口
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 0) { // 数据校验
            this.age = age;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Alice");
        person.setAge(25);
        System.out.println("Name: " + person.getName() + ", Age: " + person.getAge());
    }
}
```
3. 继承（Inheritance）
   * 继承允许一个类（子类）继承另一个类（父类）的属性和方法，从而实现代码复用。
   * 子类可以扩展或重写父类的功能。

示例：
```java
// 父类
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// 子类
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // 继承自Animal类
        dog.bark(); // Dog类自己的方法
    }
}

1. 多态（Polymorphism）
   * 多态是指同一个方法在不同对象中有不同的实现。
   * 多态可以通过方法重写（Override）和接口实现来实现。

示例：
```java

// 父类
class Animal {
    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

// 子类1
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks.");
    }
}

// 子类2
class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("The cat meows.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal(); // 父类对象
        Animal myDog = new Dog();       // 子类对象
        Animal myCat = new Cat();       // 子类对象

        myAnimal.sound(); // 输出: Animal makes a sound.
        myDog.sound();    // 输出: The dog barks.
        myCat.sound();    // 输出: The cat meows.
    }
}
```

1. 抽象类（Abstract Class）和接口（Interface）
   * 抽象类：用abstract关键字定义，不能实例化，可以包含抽象方法（没有实现的方法）和具体方法。
   * 接口：用interface关键字定义，只能包含抽象方法（Java 8 以后可以包含默认方法和静态方法），用于定义行为规范。

抽象类示例：
```java
abstract class Shape {
    abstract void draw(); // 抽象方法
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape shape = new Circle();
        shape.draw(); // 输出: Drawing a circle.
    }
}
```
接口示例：
```java
interface Drawable {
    void draw(); // 抽象方法
}

class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing a circle.");
    }
}

public class Main {
    public static void main(String[] args) {
        Drawable drawable = new Circle();
        drawable.draw(); // 输出: Drawing a circle.
    }
}
```
面向对象代码示例:
```java
//Main.java文件
public class Main{
    public static void main(String[] args){
        Car car1=new Car();
        Car car2=new Car();
        System.out.println(car1.make+ " " + car1.model);
        System.out.println(car2.make+ " " + car2.model);
    }
}
//Car.java文件
public class Car {
    String make="ford";
    String model="mustang";
    int year=2025;
    double price=58000.9;
    boolean inRunning=false;
    void start(){
        System.out.println(" you start the engine");
    }
    void stop(){
        System.out.println(" you stop the engine");
    }
}
/*
如果一个类声明为 public，那么它所在的文件名必须与该类名完全一致，包括大小写。例如，如果类名是 Person，那么文件名必须是Person.java。
在一个文件中只能有一个 public 类，因为 Java 不允许一个文件包含多个 public 类。如果文件中有多个类，只有一个类可以是 public，其他的类可以是默认访问修饰符（包访问级别）或者是 private 或 protected。
*/
```
访问权限：
   * 默认访问修饰符（package-private）：如果类或类的成员（字段、方法）没有显式的访问修饰符（如 public、private、protected），它们的访问权限默认是 包访问权限，即只要是同一包中的类，都可以直接访问和创建对象。
   * public 类：如果类是 public，它不仅可以在同一个包中创建对象，也可以在其他包中创建对象（前提是导入该类）。
   * private 类：如果类是 private（通常适用于内部类），则它只能在定义该类的外部类中访问，不能在同一包的其他类中访问。
   * protected 类：protected 类通常适用于继承关系，允许同一包中的类或子类访问。
## 构造方法
构造方法是用于在创建对象时初始化对象的状态。构造方法与类同名，并且没有返回类型（连 void 也没有）。
```java
public class Person {
    private String name;
    private int age;

    // 构造函数
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
使用构造函数来创建对象：
```java
Person person = new Person("John", 30);
```
## 构造方法的重载
构造方法是可以重载的，也就是说，可以定义多个构造方法，它们的参数不同。Java 会根据传递给构造方法的参数类型和数量来决定使用哪个构造方法。
```java
//User.java文件
public class User{
    String username;
    String email;
    int age;
    User(){
        this.name="guest";
        this.email="not provided";
        this.age=0;
    }
    User(String username){
        this.name=username;
        this.email="not provided";
        this.age=0;
    }
    User(String username,String email){
        this.name=username;
        this.email=email;
        this.age=0;
    }
    User(String username,String email,int age){
        this.name=name;
        this.email=email;
        this.age=age;
    }
}
//Main.java文件
public class Main{
    public static void main(String[] args){
        User user1=new User("Spongebob");
        User user2=new User("patrick","pstar@email.com");
        User user3=new User("sandy","scheeks@gmail.com",27);
        User user4=new User();
        System.out.println(user1.username)
        System.out.println(user1.email)
        System.out.println(user1.age)
        System.out.println(user2.username)
        System.out.println(user2.email)
        System.out.println(user2.age)
        System.out.println(user3.username)
        System.out.println(user3.email)
        System.out.println(user3.age)
        System.out.println(user4.username)
        System.out.println(user4.email)
        System.out.println(user4.age)
    }
}
```
## 对象数组
在 Java 中，对象数组是指一个数组，其中的每个元素都是一个对象（即类的实例）。Java 中的数组是固定长度的，对象数组可以存储同一类型的多个对象。

假设我们有一个 User 类，表示用户信息：
```java
class User {
    int id;
    String name;
    int age;

    // 构造方法
    public User(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    // 重写 toString 方法，方便打印对象信息
    @Override
    public String toString() {
        return "User{id=" + id + ", name='" + name + "', age=" + age + "}";
    }
}
```
我们可以创建一个 User 类型的对象数组：
```java
public class Main {
    public static void main(String[] args) {
        // 创建一个 User 对象数组
        User[] users = new User[3];

        // 初始化数组中的每个元素
        users[0] = new User(1, "Alice", 25);
        users[1] = new User(2, "Bob", 30);
        users[2] = new User(3, "Charlie", 35);

        // 遍历数组并打印每个对象
        for (User user : users) {
            System.out.println(user);
        }
    }
}
```
输出结果
```java
User{id=1, name='Alice', age=25}
User{id=2, name='Bob', age=30}
User{id=3, name='Charlie', age=35}
```
## static关键字
在Java中，static 关键字用于声明类级别的成员，而不是对象级别的成员。通过使用 static，可以让某个变量、方法或代码块属于类本身，而不是某个特定的对象实例。这样可以提高内存的利用率，减少资源的浪费。
1. static 变量（静态变量）

静态变量属于类，而不属于任何对象。也就是说，无论类创建多少个实例，静态变量只有一份拷贝，并且所有对象都共享这份数据。
```java
class Example {
    static int count = 0; // 静态变量

    Example() {
        count++; // 每创建一个实例，count增加
    }
}

public class Main {
    public static void main(String[] args) {
        Example obj1 = new Example();
        Example obj2 = new Example();
        System.out.println(Example.count); // 输出2，因为有两个实例
    }
}
```
2. static 方法（静态方法）

静态方法属于类，可以直接通过类名调用，而不需要实例化对象。静态方法只能访问静态变量或调用其他静态方法。它不能访问实例变量和实例方法，因为它不依赖于对象的状态。
```java
class Example {
    static void greet() {
        System.out.println("Hello, world!");
    }
}

public class Main {
    public static void main(String[] args) {
        Example.greet(); // 直接调用静态方法
    }
}
```
3. static 块（静态初始化块）

静态块是在类加载时执行的代码块。它通常用于类级别的初始化操作，比如设置静态变量的初始值。静态块会在类第一次加载时执行一次。
```java
class Example {
    static {
        System.out.println("静态块执行");
    }
}

public class Main {
    public static void main(String[] args) {
        new Example(); // 只要类被加载，静态块就会执行一次
    }
}
```
## 继承
在Java中，继承（Inheritance）是面向对象编程的核心特性之一。它允许一个类从另一个类继承属性和方法，从而实现代码的重用和扩展。继承通过创建一个子类（subclass）来扩展现有的父类（superclass）的功能。

继承的基本概念

* 父类（SuperClass 或 BaseClass）：提供被继承的属性和方法。
* 子类（SubClass 或 DerivedClass）：继承父类的属性和方法，并可以添加新的属性和方法，或者重写父类的方法。
1. 使用 extends 关键字

子类通过 extends 关键字继承父类。
```java
// 父类
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

// 子类
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // 从父类继承的方法
        dog.bark(); // 子类的方法
    }
}
```
2. 方法重写（Overriding）

子类可以重写父类的方法，以提供自己的实现。重写时，方法的签名（方法名、参数类型、返回类型）必须与父类中的方法完全相同。
```java
// 父类
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

// 子类
class Dog extends Animal {
    @Override  // 可选的注解，用来检查是否正确重写了方法
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal();
        Dog dog = new Dog();

        animal.sound(); // 输出: Animal makes a sound
        dog.sound();    // 输出: Dog barks
    }
}
```
3. super 关键字

super 关键字用于引用父类的成员（属性、方法）。它通常用于：
* 调用父类的构造方法。
* 调用父类的实例方法。
* 访问父类的成员变量。
```java
// 父类
class Animal {
    String name;

    Animal(String name) {
        this.name = name;
    }

    void greet() {
        System.out.println("Hello, I am " + name);
    }
}

// 子类
class Dog extends Animal {
    Dog(String name) {
        super(name); // 调用父类构造方法
    }

    void greet() {
        super.greet(); // 调用父类的方法
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Rex");
        dog.greet();
    }
}
```
4. 构造方法和继承

构造方法不会被继承，但子类可以通过 super() 调用父类的构造方法。如果父类没有无参构造方法，子类必须显式调用父类的构造方法。
```java
// 父类
class Animal {
    Animal(String name) {
        System.out.println("Animal's name is " + name);
    }
}

// 子类
class Dog extends Animal {
    Dog(String name) {
        super(name); // 调用父类构造方法
        System.out.println("Dog's name is " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy");
    }
}
```
5. 单继承与多重继承

在Java中，类支持单继承，即一个类只能继承一个父类。这是为了避免多重继承可能带来的复杂性（比如方法冲突）。

如果想实现多重继承的效果，可以通过\*\*接口（interface）\*\*来实现，接口支持多重实现。
```java
interface Animal {
    void sound();
}

interface Pet {
    void play();
}

class Dog implements Animal, Pet {
    public void sound() {
        System.out.println("Dog barks");
    }

    public void play() {
        System.out.println("Dog plays");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();  // Dog barks
        dog.play();   // Dog plays
    }
}
```
## super
super的作用是明确区分父类与子类的成员，特别是在子类和父类有相同的成员（例如构造方法、属性或方法）时，super能够确保你访问的是父类的版本。这对于避免命名冲突和控制继承行为非常重要。
1. 访问父类的构造方法

当子类的构造方法需要调用父类的构造方法时，必须使用super()，尤其是父类没有默认构造方法（无参构造方法）时。
```java
class Parent {
    Parent(int x) {
        System.out.println("Parent constructor with x = " + x);
    }
}

class Child extends Parent {
    Child(int x) {
        super(x);  // 调用父类的构造方法
        System.out.println("Child constructor with x = " + x);
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child(10);
    }
}
```
2. 访问父类的成员变量

当子类和父类有相同的成员变量时，子类会隐藏父类的成员变量。此时，使用super可以访问父类的变量，而不是子类中的同名变量。
```java
class Parent {
    int num = 10;
}

class Child extends Parent {
    int num = 20;

    void printNums() {
        System.out.println("Child num: " + num);        // 访问子类的num
        System.out.println("Parent num: " + super.num); // 访问父类的num
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.printNums();
    }
}
```
3. 调用父类的被重写方法

如果子类重写了父类的方法，使用super可以调用父类被重写的方法，而不是子类的重写版本。
```java
class Parent {
    void display() {
        System.out.println("Parent's display");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child's display");
    }

    void callParentDisplay() {
        super.display();  // 调用父类的display方法
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.callParentDisplay();  // 输出 "Parent's display"
    }
}
```
总结来说，super的作用是明确区分父类与子类的成员，特别是在子类和父类有相同的成员（例如构造方法、属性或方法）时，super能够确保你访问的是父类的版本。这对于避免命名冲突和控制继承行为非常重要。
## 重写override
方法重写（Method Overriding）是面向对象编程（OOP）中的一个重要特性，允许子类对从父类继承过来的方法进行修改和扩展。通过方法重写，子类可以提供自己的实现来替代父类中已经定义的方法。
1. 方法重写的基本规则

    方法名、参数列表、返回类型必须相同：子类重写父类方法时，方法名、参数列表和返回类型必须与父类中的方法完全相同。
    访问修饰符：子类重写的方法的访问修饰符不能比父类的更严格。例如，父类的 public 方法，子类重写时不能使用 private，但可以使用相同的 public 或更宽松的 protected。
    抛出的异常：子类重写父类方法时，可以抛出比父类方法更多的异常，但不能抛出父类方法没有声明的异常。

2. 方法重写的目的

方法重写的主要目的是让子类能够修改父类的方法实现，以便符合子类的实际需求。方法重写也支持多态，使得同一个方法在不同的对象上表现出不同的行为。
3. 方法重写的示例

假设有一个父类 Animal，它有一个 makeSound() 方法，子类 Dog 和 Cat 重写这个方法，分别实现自己的声音。
```java
class Animal {
    // 父类的makeSound方法
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // 子类Dog重写makeSound方法
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    // 子类Cat重写makeSound方法
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();   // 创建Dog对象
        Animal myCat = new Cat();   // 创建Cat对象

        myDog.makeSound();  // 输出: Dog barks
        myCat.makeSound();  // 输出: Cat meows
    }
}
```
在这个例子中，Dog 和 Cat 类分别重写了 Animal 类中的 makeSound() 方法，实现了不同的声音。
4. @Override 注解

@Override 是一个注解，它用于标记方法是对父类方法的重写。使用 @Override 可以帮助编译器检查方法签名是否正确（例如，方法名和参数列表是否匹配），如果没有正确重写父类方法，编译器会给出错误提示。

虽然 @Override 不是必需的，但它是一个良好的编程实践，能帮助捕捉潜在的错误。
5. 方法重写与多态

方法重写是实现多态的一个重要部分。在Java中，通过父类引用指向子类对象时，调用的方法是运行时决定的，即会调用子类重写的方法，而不是父类的方法。这被称为动态方法分派。
```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();  // 父类引用指向子类对象
        animal.makeSound();         // 输出: Dog barks
    }
}
```
这里，animal 是 Animal 类型的引用，但它指向的是 Dog 类型的对象。由于方法是重写的，所以调用 makeSound() 时，会执行 Dog 类中的版本，而不是 Animal 类中的版本，这就是多态的体现。
6. 注意事项

* 构造方法不能被重写：构造方法属于类的一部分，而方法重写是针对类的方法的，因此构造方法不能被重写。
* 静态方法不能被重写：静态方法是类级别的方法，它们在类加载时就已经被确定，不属于对象实例，因此不能被重写。如果子类定义了一个与父类静态方法签名相同的方法，它实际上是方法隐藏（方法覆盖），而不是方法重写。
```java
class Animal {
    static void staticMethod() {
        System.out.println("Animal static method");
    }
}

class Dog extends Animal {
    static void staticMethod() {
        System.out.println("Dog static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal.staticMethod();  // 输出: Animal static method
        Dog.staticMethod();     // 输出: Dog static method
    }
}
```
## tostring方法
在 Java 中，toString() 方法是 Object 类中的一个方法。因为所有的 Java 类都直接或间接继承自 Object 类，所以每个 Java 对象都有一个 toString() 方法。默认情况下，toString() 方法返回的是该对象的类名和它的哈希码，但是你通常会在你的类中重写该方法，以便返回更有意义的对象信息。

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public static void main(String[] args) {
        Person person = new Person("Alice", 30);
        System.out.println(person.toString());
    }
}
```
**重写tostring()方法**
```java
@Override
public String toString() {
    return "Person{name='" + name + "', age=" + age + "}";
}
```
**默认的 toString() 方法**

默认情况下，toString() 方法返回的是该对象的类名以及对象的哈希码，例如：
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public static void main(String[] args) {
        Person person = new Person("Alice", 30);
        System.out.println(person.toString());
    }
}
```
如果你没有重写 toString()，输出可能类似于：
```java
Person@15db9742
```
这个输出包括了类名 Person 和对象的哈希码的十六进制表示。
## abstract抽象类
在 Java 中,抽象类(Abstract Class)和接口(Interface)是两种不同的机制,用于实现多态性和封装性。它们都用于定义类的行为，但有一些关键的区别。
1. 抽象类（Abstract Class）

    定义: 抽象类是一个不能实例化的类，它可以包含抽象方法（没有方法体）和具体方法（有方法体）。抽象类主要用于被其他类继承。
    特性:
    * 可以有构造方法。
    * 可以有成员变量。
    * 可以有抽象方法，也可以有具体方法（有方法体）。
    * 继承抽象类的子类必须实现所有的抽象方法（除非子类本身也是抽象类）。
        一个类只能继承一个抽象类（Java 支持单继承）。

示例:
```java
abstract class Animal {
    // 抽象方法
    abstract void sound();
    
    // 具体方法
    void sleep() {
        System.out.println("This animal is sleeping.");
    }
}

class Dog extends Animal {
    // 实现抽象方法
    @Override
    void sound() {
        System.out.println("Bark");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();  // 输出 "Bark"
        dog.sleep();  // 输出 "This animal is sleeping."
    }
}
```
## interface接口
2. 接口（Interface）

    定义: 接口是一个纯粹的抽象类型，只能包含常量、抽象方法（Java 8 及以后版本支持默认方法和静态方法）和默认方法。接口用于定义类必须遵循的契约。
    特性:
    * 不能有构造方法。
    * 不能有实例变量（只能有静态常量）。
    * 接口中的方法默认是 public abstract（可以省略）。
    * 一个类可以实现多个接口（Java 支持多重继承）。
    * 接口不提供实现，只有方法签名，实际的实现由实现类提供。

示例:
```java
//在创建时选择创建接口文件
interface Animal {
    // 抽象方法
    void sound();
    
    // 默认方法
    default void sleep() {
        System.out.println("This animal is sleeping.");
    }
}

class Dog implements Animal {
    // 实现接口中的抽象方法
    @Override
    public void sound() {
        System.out.println("Bark");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();  // 输出 "Bark"
        dog.sleep();  // 输出 "This animal is sleeping."
    }
}
```
主要区别
||||
|:--|:--|:--|
|特性|抽象类|接口|
|成员|可以包含字段、方法（有实现）|只能包含常量、抽象方法（Java 8 后可有默认方法和静态方法）|
|构造方法|可以有构造方法|不能有构造方法|
|继承|类只能继承一个抽象类|类可以实现多个接口|
|方法实现|可以有具体方法（有方法体）|只能包含抽象方法（除非是 Java 8 及以上版本）|
|访问修饰符|方法可使用任何访问修饰符|所有方法默认都是 public|
## 多态
   * 多态是指同一个方法在不同对象中有不同的实现。
   * 多态可以通过方法重写（Override）和接口实现来实现。
```java

// 父类
class Animal {
    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

// 子类1
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks.");
    }
}

// 子类2
class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("The cat meows.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal(); // 父类对象
        Animal myDog = new Dog();       // 子类对象
        Animal myCat = new Cat();       // 子类对象

        myAnimal.sound(); // 输出: Animal makes a sound.
        myDog.sound();    // 输出: The dog barks.
        myCat.sound();    // 输出: The cat meows.
    }
}
```
## 运行时多态
运行时多态性的特点：

* 方法重写：子类重写了父类的方法。
* 父类引用指向子类对象：可以通过父类的引用类型来调用子类重写的方法。
*  方法调用在运行时决定：方法的具体调用取决于对象的实际类型，而不是声明类型。

运行时多态性的示例
```java
class Animal {
    // 父类的speak方法
    public void speak() {
        System.out.println("Animal speaks");
    }
}

class Dog extends Animal {
    // 子类Dog重写了父类的speak方法
    @Override
    public void speak() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    // 子类Cat重写了父类的speak方法
    @Override
    public void speak() {
        System.out.println("Cat meows");
    }
}

public class TestPolymorphism {
    public static void main(String[] args) {
        Animal animal;  // 父类引用

        animal = new Dog();  // 父类引用指向子类对象Dog
        animal.speak();  // 输出 "Dog barks" 由于运行时多态性，调用的是Dog类的speak方法

        animal = new Cat();  // 父类引用指向子类对象Cat
        animal.speak();  // 输出 "Cat meows" 由于运行时多态性，调用的是Cat类的speak方法
    }
}
```
## getter 和setter方法
在Java中，getter 和 setter 方法用于访问和修改对象的私有成员变量。通过这两个方法，类的外部可以安全地访问和修改对象的属性，同时保持封装性（Encapsulation）和数据的控制。
1. Getter方法：
   * 作用：用于获取对象的属性值。
   * 命名规则：通常以get开头，后跟属性名，首字母大写。
   * 返回类型：与属性类型相同。

2. Setter方法：
   * 作用：用于设置对象的属性值。
   * 命名规则：通常以set开头，后跟属性名，首字母大写。
   * 参数类型：与属性类型相同。
```java
class Person {
    // 私有成员变量
    private String name;
    private int age;

    // Getter方法：获取name
    public String getName() {
        return name;
    }

    // Setter方法：设置name
    public void setName(String name) {
        this.name = name;
    }

    // Getter方法：获取age
    public int getAge() {
        return age;
    }

    // Setter方法：设置age
    public void setAge(int age) {
        if (age > 0) {  // 增加条件判断来确保设置的年龄有效
            this.age = age;
        } else {
            System.out.println("年龄必须大于0");
        }
    }
}

public class TestGetterSetter {
    public static void main(String[] args) {
        Person person = new Person();
        
        // 使用setter方法设置属性
        person.setName("Alice");
        person.setAge(25);

        // 使用getter方法获取属性
        System.out.println("Name: " + person.getName());  // 输出 "Name: Alice"
        System.out.println("Age: " + person.getAge());    // 输出 "Age: 25"
    }
}
//在Person类中，name和age是私有的 (private)，这意味着它们不能直接从类外部访问。
```
它们允许类的外部访问和修改私有成员变量，同时提供了控制数据合法性和修改逻辑的机会。
## 聚合
在 Java 中，"聚合"（Aggregation）是面向对象编程中的一个概念，表示一种对象之间的"整体-部分"关系。它通常是指一个类（整体）包含或拥有另一个类（部分）的实例，但这些部分可以独立于整体存在。聚合通常被视为比组合（Composition）关系更为松散，因为部分对象可以在多个整体对象之间共享。

在代码中，聚合通常通过引用其他对象的实例来实现。
```java
class Employee {
    private String name;
    private int id;

    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }
}

class Department {
    private String departmentName;
    private Employee[] employees;  // 使用数组来替代 List

    public Department(String departmentName, Employee[] employees) {
        this.departmentName = departmentName;
        this.employees = employees;
    }

    public String getDepartmentName() {
        return departmentName;
    }

    public Employee[] getEmployees() {
        return employees;
    }
}

public class Main {
    public static void main(String[] args) {
        // 创建 Employee 对象
        Employee emp1 = new Employee("Alice", 1);
        Employee emp2 = new Employee("Bob", 2);

        // 创建 Employee 数组
        Employee[] employees = {emp1, emp2};

        // 创建 Department 对象，传入 Employee 数组
        Department dept = new Department("HR", employees);

        // 打印部门信息及员工
        System.out.println("Department: " + dept.getDepartmentName());
        for (Employee emp : dept.getEmployees()) {
            System.out.println("Employee: " + emp.getName());
        }
    }
}
```
聚合是对象间的一种关系，强调对象间的关联而非生命周期的依赖性。它可以在不影响部分对象独立性的情况下，实现对象间的组合。
## 结合
在 Java 中，组合（Composition）是面向对象编程中的一种“整体-部分”关系。与聚合不同，组合具有更强的关联性，其中 部分对象 的生命周期由 整体对象 控制。也就是说，如果整体对象被销毁，那么它包含的部分对象也会被销毁。组合关系比聚合关系更加紧密，部分对象不能在多个整体对象间共享。
```java
class Engine {
    private String type;

    public Engine(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

class Car {
    private String model;
    private Engine engine;  // 组合关系，Car 包含一个 Engine

    public Car(String model, String engineType) {
        this.model = model;
        this.engine = new Engine(engineType);  // 创建 Engine 对象
    }

    public void start() {
        System.out.println(model + " is starting with a " + engine.getType() + " engine.");
    }

    // Getter
    public Engine getEngine() {
        return engine;
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "V8");

        // 启动汽车
        car.start();
    }
}

```
## 封装类
在Java中，Wrapper 类是用于将基本数据类型（如 int、char 等）封装成对象的类。Java 中的基本数据类型（原始类型）不能直接作为对象传递或操作，因此我们使用包装类来实现这一点。每个基本数据类型都有一个对应的包装类。
基本数据类型与对应的包装类如下：
|基本数据类型|对应的包装类|
|:--:|:--:|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|
```java
public class WrapperExample {
    public static void main(String[] args) {
        // 自动装箱
        Integer intWrapper = 100;  // 自动将int类型转换为Integer对象
        
        // 自动拆箱
        int num = intWrapper;  // 自动将Integer对象转换为int类型
        
        // 使用包装类的方法
        String intStr = intWrapper.toString();  // Integer对象转为字符串
        System.out.println("Integer as String: " + intStr);
        
        // 从字符串转换回包装类
        Integer parsedInt = Integer.parseInt("200");
        System.out.println("Parsed Integer: " + parsedInt);
        
        // 比较两个包装类对象
        Integer a = 10;
        Integer b = 10;
        System.out.println("a == b: " + (a == b));  // true，因为Integer缓存池的原因
        
        // 手动装箱
        Integer manualBoxing = Integer.valueOf(123);
        System.out.println("Manually boxed value: " + manualBoxing);
    }
}
```
**自动装箱与拆箱：**
```java
Integer num1 = 5; // 自动装箱，将基本类型5转换为Integer对象
int num2 = num1;  // 自动拆箱，将Integer对象转换为基本类型int
```
## arraylist
ArrayList 是 Java 集合框架中的一个类，它提供了一个可变大小的数组，用于存储元素。ArrayList 是基于动态数组实现的，能够自动调整大小，因此在存储元素时非常灵活。它属于 java.util 包，并且实现了 List 接口，意味着它维护元素的插入顺序，允许重复的元素，并提供对元素的访问。
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        // 创建一个 ArrayList
        ArrayList<String> list = new ArrayList<>();
        
        // 添加元素
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        
        // 获取元素
        System.out.println("Element at index 1: " + list.get(1));  // 输出: Banana
        
        // 修改元素
        list.set(1, "Blueberry");
        System.out.println("Modified element at index 1: " + list.get(1));  // 输出: Blueberry
        
        // 删除元素
        list.remove("Apple");  // 删除 Apple
        System.out.println("After removal: " + list);
        
        // 获取 ArrayList 大小
        System.out.println("Size of list: " + list.size());  // 输出: 2
        
        // 检查是否包含某个元素
        boolean containsCherry = list.contains("Cherry");
        System.out.println("Contains 'Cherry': " + containsCherry);  // 输出: true
        
        // 清空列表
        list.clear();
        System.out.println("After clear, size: " + list.size());  // 输出: 0
    }
}
```
## 异常处理
在Java中，异常处理是通过try、catch、finally、throw和throws等关键字来实现的。异常处理机制允许程序在出现错误时进行优雅的处理，而不是直接崩溃。
1. try-catch 块

try块用于包裹可能会抛出异常的代码，catch块用于捕获并处理异常。
```java
try {
    // 可能会抛出异常的代码
    int result = 10 / 0; // 这里会抛出 ArithmeticException
} catch (ArithmeticException e) {
    // 处理异常
    System.out.println("捕获到算术异常: " + e.getMessage());
}
```
2. finally 块

finally块中的代码无论是否发生异常都会执行，通常用于释放资源。
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("捕获到算术异常: " + e.getMessage());
} finally {
    System.out.println("finally 块执行");
}
```
3. throw 关键字

throw关键字用于手动抛出异常。
```java
if (someCondition) {
    throw new IllegalArgumentException("参数不合法");
}
```
4. throws 关键字

throws关键字用于在方法签名中声明该方法可能会抛出的异常，调用者需要处理这些异常。
```java
public void myMethod() throws IOException {
    // 可能会抛出 IOException 的代码
    throw new IOException("IO 异常");
}
```
5. 自定义异常

你可以通过继承Exception类或RuntimeException类来创建自定义异常。
```java
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}

public void myMethod() throws MyCustomException {
    throw new MyCustomException("自定义异常");
}
```
6. 多重 catch 块

你可以使用多个catch块来捕获不同类型的异常。
```java
try {
    // 可能会抛出多种异常的代码
} catch (ArithmeticException e) {
    System.out.println("捕获到算术异常: " + e.getMessage());
} catch (NullPointerException e) {
    System.out.println("捕获到空指针异常: " + e.getMessage());
} catch (Exception e) {
    System.out.println("捕获到其他异常: " + e.getMessage());
}
```
## 读写文件
1. 使用 FileReader 和 FileWriter（适用于字符文件）

这是用于读取和写入文本文件的最简单方式。

**读取文件**
```java
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
**写入文件**
```java
import java.io.FileWriter;
import java.io.BufferedWriter;
import java.io.IOException;

public class FileWriteExample {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"))) {
            writer.write("Hello, World!");
            writer.newLine();
            writer.write("This is a Java file write example.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
2. 使用Files类（Java 7及以上）

Java 7引入了java.nio.file.Files类，提供了更简洁的文件读写方式。
**读取文件**
```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.io.IOException;
import java.util.List;

public class ReadFileWithFilesExample {
    public static void main(String[] args) {
        try {
            List<String> lines = Files.readAllLines(Paths.get("input.txt"));
            for (String line : lines) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
**写入文件**
```java

import java.nio.file.Files;
import java.nio.file.Paths;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class WriteFileWithFilesExample {
    public static void main(String[] args) {
        List<String> lines = Arrays.asList("Hello, World!", "This is a new line.");
        try {
            Files.write(Paths.get("output.txt"), lines);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
``` 
## 日期与时间
现代日期时间类（java.time 包）： 从 Java 8 开始，java.time 包提供了更好的日期和时间处理方式，遵循 ISO-8601 标准。主要的类包括：
* LocalDate: 表示没有时间的日期（年、月、日）。
* LocalTime: 表示没有日期的时间（小时、分钟、秒）。
* LocalDateTime: 包含日期和时间，表示某个时刻（无时区）。
* ZonedDateTime: 表示带时区的日期和时间。
* Instant: 精确到纳秒的时间戳。
* Duration: 表示时间的量度（持续时间）。
* Period: 表示日期之间的差异（年月日）。

获取当前日期和时间：
```java
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;

public class Main {
    public static void main(String[] args) {
        LocalDate currentDate = LocalDate.now(); // 获取当前日期
        LocalTime currentTime = LocalTime.now(); // 获取当前时间
        LocalDateTime currentDateTime = LocalDateTime.now(); // 获取当前日期时间

        System.out.println("当前日期: " + currentDate);
        System.out.println("当前时间: " + currentTime);
        System.out.println("当前日期时间: " + currentDateTime);
    }
}
```
日期和时间格式化：
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Main {
    public static void main(String[] args) {
        LocalDateTime dateTime = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

        String formattedDateTime = dateTime.format(formatter);
        System.out.println("格式化后的日期时间: " + formattedDateTime);
    }
}
```
## 匿名类
在 Java 中，匿名类（Anonymous Class）是一种没有名字的类，它是在表达式中定义和使用的。匿名类通常用于简化代码，尤其是在只需要一个实现某个接口或继承某个类的实例时，而不必单独定义一个类。
匿名类的定义

匿名类可以实现接口或继承一个类，并且可以直接在创建对象时进行实现。其语法结构如下：
```java
new 接口或类() {
    // 实现接口或类的方法
}
```
* 如果是实现接口，则可以直接在匿名类中实现接口的所有方法。
* 如果是继承类，则可以覆盖父类的方法。
例子

1. 实现接口的匿名类

假设有一个接口 Animal，我们可以使用匿名类来实现这个接口：
```java
interface Animal {
    void sound();
}

public class Main {
    public static void main(String[] args) {
        // 使用匿名类实现 Animal 接口
        Animal dog = new Animal() {
            @Override
            public void sound() {
                System.out.println("Woof!");
            }
        };

        dog.sound();  // 输出: Woof!
    }
}
```
在这个例子中，我们创建了一个匿名类来实现 Animal 接口，并覆盖了 sound() 方法。

2. 继承类的匿名类

我们也可以用匿名类来继承一个类，并覆写其中的方法。比如，假设有一个 Animal 类：
```java
class Animal {
    public void sound() {
        System.out.println("Some sound");
    }
}

public class Main {
    public static void main(String[] args) {
        // 使用匿名类继承 Animal 类
        Animal dog = new Animal() {
            @Override
            public void sound() {
                System.out.println("Woof!");
            }
        };

        dog.sound();  // 输出: Woof!
    }
}
```
在这个例子中，Animal 是一个类，我们通过匿名类继承了它，并覆写了 sound() 方法。

3. 匿名类作为事件监听器（常见用法）

匿名类常常用于事件监听器的实现，特别是在图形用户界面（GUI）编程中。例如，在 Java Swing 中，我们可以用匿名类来处理按钮点击事件：
```java
import javax.swing.*;
import java.awt.event.ActionListener;

public class Main {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Anonymous Class Example");
        JButton button = new JButton("Click me");

        // 使用匿名类实现按钮点击事件的监听器
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(java.awt.event.ActionEvent e) {
                System.out.println("Button clicked!");
            }
        });

        frame.add(button);
        frame.setSize(200, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```
## timertask
在Java中，TimerTask 是一个抽象类，继承自 java.util.TimerTask，用于表示一个可以由 Timer 执行的任务。你可以通过继承这个类并重写它的 run() 方法，来定义任务的具体执行内容。

通常，TimerTask 和 Timer 类一起使用，其中 Timer 用于安排定时任务的执行。你可以设置任务在未来某个特定时间点执行，或者周期性地执行。

```java
public class Main{
    public static void main[String[] args]{
        Timer timer=new timer();
        TimerTask TimerTask=new timertask(){
            int count=3;
            @override
            public void run(){
                System.out.println("hello!");
                count--;
                if(count<=0){
                    System.out.println("task complete!");
                    timer.cancel();
                }
            }
        };
        // 安排任务在延迟 2 秒后执行，每隔 1 秒执行一次
        timer.schedule(task,2000,1000)
    }
}
```
## 泛式
在Java中，\*\*泛型（Generics）\*\*是一种允许在类、接口和方法中使用类型参数的机制。泛型提供了一种强大的方式来提高代码的重用性、类型安全性以及可读性。泛型使得代码可以在不指定具体类型的情况下进行操作，从而在编译时提供类型检查，减少了运行时错误。
```java
1. 泛型类

泛型类是指在类定义时使用类型参数的类。类型参数可以在实例化时指定。
示例：

// 定义一个泛型类
public class Box<T> {
    private T value;
    
    public void setValue(T value) {
        this.value = value;
    }
    
    public T getValue() {
        return value;
    }
}

// 使用泛型类
public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.setValue(100);
        System.out.println(intBox.getValue());  // 输出 100
        
        Box<String> strBox = new Box<>();
        strBox.setValue("Hello");
        System.out.println(strBox.getValue());  // 输出 Hello
    }
}

在上面的代码中，Box<T> 是一个泛型类，T 是一个类型参数。在实例化时，可以指定类型，比如 Box<Integer> 或 Box<String>。
```
2. 泛型方法

泛型方法是指方法声明时使用类型参数，可以在方法调用时指定类型。
示例：
```java
public class GenericMethodExample {

    // 泛型方法
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4};
        String[] strArray = {"Hello", "World"};

        // 调用泛型方法
        printArray(intArray);  // 输出 1 2 3 4
        printArray(strArray);  // 输出 Hello World
    }
}
```
在这个例子中，<T> 使得 printArray 方法可以处理不同类型的数组。
3. 泛型接口

泛型接口是指接口声明时包含类型参数的接口，接口的实现类可以指定具体的类型。
示例：
```java
// 定义一个泛型接口
interface Pair<K, V> {
    K getKey();
    V getValue();
}

// 实现泛型接口
public class OrderedPair<K, V> implements Pair<K, V> {
    private K key;
    private V value;
    
    public OrderedPair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    @Override
    public K getKey() {
        return key;
    }

    @Override
    public V getValue() {
        return value;
    }
}

// 使用泛型接口
public class Main {
    public static void main(String[] args) {
        Pair<String, Integer> pair = new OrderedPair<>("One", 1);
        System.out.println(pair.getKey() + ": " + pair.getValue());  // 输出 One: 1
    }
}
```
4. 泛型边界

在定义泛型时，可以使用extends来指定泛型类型的上限，限制泛型的类型范围。
示例：
```java
public class BoundedTypeParameter {

    // 只允许Number及其子类作为T的类型
    public static <T extends Number> void printNumber(T number) {
        System.out.println(number);
    }

    public static void main(String[] args) {
        printNumber(100);     // 可以传入Integer
        printNumber(10.5);    // 可以传入Double
        // printNumber("Hello");  // 编译错误，String不是Number的子类
    }
}
```
在这个例子中，<T extends Number> 限制了类型 T 必须是 Number 类及其子类（如 Integer 和 Double）。