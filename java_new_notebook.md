# java新版笔记
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
java --version
javac --version
```
如显示版本信息则配置成功
## Java 基础语法

一个 Java 程序可以认为是一系列对象的集合，而这些对象通过调用彼此的方法来协同工作。下面简要介绍下类、对象、方法和实例变量的概念。

* 对象：对象是类的一个实例，有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
* 类：类是一个模板，它描述一类对象的行为和状态。
* 方法：方法就是行为，一个类可以有很多方法。逻辑运算、数据修改以及所有动作都是在方法中完成的。
* 实例变量：每个对象都有独特的实例变量，对象的状态由这些实例变量的值决定。

### 第一个Java程序

下面看一个简单的 Java 程序，它将输出字符串 Hello World
```java
public class HelloWorld {
    /* 第一个Java程序
     * 它将输出字符串 Hello World
     */
    public static void main(String[] args) {
        System.out.println("Hello World"); // 输出 Hello World
    }
}
```
![alt text](https://www.runoob.com/wp-content/uploads/2013/12/662E827A-FA32-4464-B0BD-40087F429E98.jpg)

下面将逐步介绍如何保存、编译以及运行这个程序：

* 打开代码编辑器，把上面的代码添加进去；
* 把文件名保存为：HelloWorld.java；
* 打开 cmd 命令窗口，进入目标文件所在的位置，假设是 C:\
* 在命令行窗口输入 javac HelloWorld.java 按下回车键编译代码。如果代码没有错误，cmd 命令提示符会进入下一行（假设环境变量都设置好了）。
* 再键输入 java HelloWorld 按下回车键就可以运行程序了

你将会在窗口看到 Hello World
```java
$ javac HelloWorld.java
$ java HelloWorld 
Hello World
```
如果遇到编码问题，我们可以使用 -encoding 选项设置 utf-8 来编译：
```java
javac -encoding UTF-8 HelloWorld.java 
java HelloWorld
```
### 基本语法

编写 Java 程序时，应注意以下几点：

* **大小写敏感**：Java 是大小写敏感的，这就意味着标识符 Hello 与 hello 是不同的。
* **类名**：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如 MyFirstJavaClass 。
* **方法名**：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。
* **源文件名**：源文件名必须和类名相同。当保存文件的时候，你应该使用类名作为文件名保存（切记 Java 是大小写敏感的），文件名的后缀为 .java。（如果文件名和类名不相同则会导致编译错误）。
* **主方法入口**：所有的 Java 程序由 public static void main(String[] args) 方法开始执行。

### Java 标识符

Java 所有的组成部分都需要名字。类名、变量名以及方法名都被称为标识符。

关于 Java 标识符，有以下几点需要注意：

* 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始
* 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合
* 关键字不能用作标识符
* 标识符是大小写敏感的
* 合法标识符举例：age、$salary、_value、__1_value
* 非法标识符举例：123abc、-salary

### Java修饰符

像其他语言一样，Java可以使用修饰符来修饰类中方法和属性。主要有两类修饰符：

* 访问控制修饰符 : default, public , protected, private
* 非访问控制修饰符 : final, abstract, static, synchronized

在后面的章节中我们会深入讨论 Java 修饰符。
### Java 变量
Java 中主要有如下几种类型的变量

* 局部变量
* 类变量（静态变量）
* 成员变量（非静态变量）

### Java 数组

数组是储存在堆上的对象，可以保存多个同类型变量。在后面的章节中，我们将会学到如何声明、构造以及初始化一个数组。
### Java 枚举

Java 5.0引入了枚举，枚举限制变量只能是预先设定好的值。使用枚举可以减少代码中的 bug。

例如，我们为果汁店设计一个程序，它将限制果汁为小杯、中杯、大杯。这就意味着它不允许顾客点除了这三种尺寸外的果汁。
```java
class FreshJuice {
   enum FreshJuiceSize{ SMALL, MEDIUM , LARGE }
   FreshJuiceSize size;
}
 
public class FreshJuiceTest {
   public static void main(String[] args){
      FreshJuice juice = new FreshJuice();
      juice.size = FreshJuice.FreshJuiceSize.MEDIUM  ;
   }
}
```
注意：枚举可以单独声明或者声明在类里面。方法、变量、构造函数也可以在枚举中定义。

### Java 关键字

下面列出了 Java 关键字。这些保留字不能用于常量、变量、和任何标识符的名称。 
| 类别                 | 关键字        | 说明                                  |
|----------------------|---------------|---------------------------------------|
| **访问控制**         | `private`     | 私有的                                |
|                      | `protected`   | 受保护的                              |
|                      | `public`      | 公共的                                |
|                      | `default`     | 默认                                  |
| **类、方法和变量修饰符** | `abstract`    | 声明抽象                              |
|                      | `class`       | 类                                    |
|                      | `extends`     | 扩充、继承                            |
|                      | `final`       | 最终值、不可改变的                    |
|                      | `implements`  | 实现（接口）                          |
|                      | `interface`   | 接口                                  |
|                      | `native`      | 本地、原生方法（非 Java 实现）        |
|                      | `new`         | 创建                                  |
|                      | `static`      | 静态                                  |
|                      | `strictfp`    | 严格浮点、精准浮点                    |
|                      | `synchronized`| 线程、同步                            |
|                      | `transient`   | 短暂                                  |
|                      | `volatile`    | 易失                                  |
| **程序控制语句**     | `break`       | 跳出循环                              |
|                      | `case`        | 定义一个值以供 `switch` 选择          |
|                      | `continue`    | 继续                                  |
|                      | `do`          | 运行                                  |
|                      | `else`        | 否则                                  |
|                      | `for`         | 循环                                  |
|                      | `if`          | 如果                                  |
|                      | `instanceof`  | 实例                                  |
|                      | `return`      | 返回                                  |
|                      | `switch`      | 根据值选择执行                        |
|                      | `while`       | 循环                                  |
| **错误处理**         | `assert`      | 断言表达式是否为真                    |
|                      | `catch`       | 捕捉异常                              |
|                      | `finally`     | 有没有异常都执行                      |
|                      | `throw`       | 抛出一个异常对象                      |
|                      | `throws`      | 声明一个异常可能被抛出                |
|                      | `try`         | 捕获异常                              |
| **包相关**           | `import`      | 引入                                  |
|                      | `package`     | 包                                    |
| **基本类型**         | `boolean`     | 布尔型                                |
|                      | `byte`        | 字节型                                |
|                      | `char`        | 字符型                                |
|                      | `double`      | 双精度浮点                            |
|                      | `float`       | 单精度浮点                            |
|                      | `int`         | 整型                                  |
|                      | `long`        | 长整型                                |
|                      | `short`       | 短整型                                |
| **变量引用**         | `super`       | 父类、超类                            |
|                      | `this`        | 本类                                  |
|                      | `void`        | 无返回值                              |
| **保留关键字**       | `goto`        | 是关键字，但不能使用                  |
|                      | `const`       | 是关键字，但不能使用                  |

**注意**：Java 的 `null` 不是关键字，类似于 `true` 和 `false`，它是一个字面常量，不允许作为标识符使用。

### Java 空行

空白行或者有注释的行，Java 编译器都会忽略掉。
### 继承

在 Java 中，一个类可以由其他类派生。如果你要创建一个类，而且已经存在一个类具有你所需要的属性或方法，那么你可以将新创建的类继承该类。

利用继承的方法，可以重用已存在类的方法和属性，而不用重写这些代码。被继承的类称为超类（super class），派生类称为子类（sub class）。
### 接口

在 Java 中，接口可理解为对象间相互通信的协议。接口在继承中扮演着很重要的角色。

接口只定义派生要用到的方法，但是方法的具体实现完全取决于派生类。
### Java 源程序与编译型运行区别
如下图所示：
![](https://www.runoob.com/wp-content/uploads/2013/12/ZSSDMld.png)

下一节介绍 Java 编程中的类和对象。之后你将会对 Java 中的类和对象有更清楚的认识。

## java注释
在计算机语言中，注释是计算机语言的一个重要组成部分，用于在源代码中解释代码的作用，可以增强程序的可读性，可维护性。

Java 注释是一种在 Java 程序中用于提供代码功能说明的文本。

注释不会被编译器包含在最终的可执行程序中，因此不会影响程序的运行。

注释是良好的编程习惯，它们帮助程序员更容易地理解代码的用途和功能，并且在团队协作中非常有用。

Java 注释主要有三种类型：

* 单行注释
* 多行注释
* 文档注释

### 单行注释
单行注释以双斜杠 // 开始：
```java
// 这是一个单行注释
int x = 10; // 初始化一个变量x为10
```
### 多行注释

多行注释以 /*开始，以 */结束：
```java
/*
这是一个多行注释
可以用来注释多行代码
*/
int y = 20; // 初始化一个变量y为20
```
### 文档注释

文档注释以 /** 开始，以 */ 结束，通常出现在类、方法、字段等的声明前面，用于生成代码文档，这种注释可以被工具提取并生成 API 文档，如 JavaDoc。
```java
/**
 * 这是一个文档注释示例
 * 它通常包含有关类、方法或字段的详细信息
 */
public class MyClass {
    // 类的成员和方法
}
```
文档注释的格式通常包含一些特定的标签，如 <kbd>@param</kbd>用于描述方法参数，<kbd>@return</kbd>用于描述返回值，<kbd>@throws</kbd>用于描述可能抛出的异常等等，这些标签有助于生成清晰的API文档，以便其他开发者能够更好地理解和使用你的代码。

## Java 对象和类

Java 作为一种面向对象的编程语言，支持以下基本概念：

1. 类（Class）：

* 定义对象的蓝图，包括属性和方法。
* 示例：public class Car { ... }

2. 对象（Object）：

* 类的实例，具有状态和行为。
* 示例：Car myCar = new Car();

3. 继承（Inheritance）：

* 一个类可以继承另一个类的属性和方法。
* 示例：public class Dog extends Animal { ... }

4. 封装（Encapsulation）：

* 将对象的状态（字段）私有化，通过公共方法访问。
* 示例：
```java
    private String name; 
    public String getName() { return name; }
```
5. 多态（Polymorphism）：

* 对象可以表现为多种形态，主要通过方法重载和方法重写实现。
* 示例：
    * 方法重载：public int add(int a, int b) { ... } 和 public double add(double a, double b) { ... }
    * 方法重写：@Override public void makeSound() { System.out.println("Meow"); }

6. 抽象（Abstraction）：

* 使用抽象类和接口来定义必须实现的方法，不提供具体实现。
* 示例：
    * 抽象类：public abstract class Shape { abstract void draw(); }
    * 接口：public interface Animal { void eat(); }

7. 接口（Interface）：

* 定义类必须实现的方法，支持多重继承。
* 示例：public interface Drivable { void drive(); }

8. 方法（Method）：

* 定义类的行为，包含在类中的函数。
* 示例：public void displayInfo() { System.out.println("Info"); }

9. 方法重载（Method Overloading）：

* 同一个类中可以有多个同名的方法，但参数不同。
* 示例：
```java
    public class MathUtils {
        public int add(int a, int b) {
            return a + b;
        }

        public double add(double a, double b) {
            return a + b;
        }
    }
```
本节我们重点研究对象和类的概念。

* 对象：对象是类的一个实例（对象不是找个女朋友），有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
* 类：类是一个模板，它描述一类对象的行为和状态。

下图中男孩（boy）、女孩（girl）为类（class），而具体的每个人为该类的对象（object）：

![](https://www.runoob.com/wp-content/uploads/2013/12/object-class.jpg)

下图中汽车为类（class），而具体的每辆车为该汽车类的对象（object），对象包含了汽车的颜色、品牌、名称等。

![](https://www.runoob.com/wp-content/uploads/2013/12/class-object2020-10-27.png)

### Java中的对象

现在让我们深入了解什么是对象。看看周围真实的世界，会发现身边有很多对象，车，狗，人等等。所有这些对象都有自己的状态和行为。

拿一条狗来举例，它的状态有：名字、品种、颜色，行为有：叫、摇尾巴和跑。

对比现实对象和软件对象，它们之间十分相似。

软件对象也有状态和行为。软件对象的状态就是属性，行为通过方法体现。

在软件开发中，方法操作对象内部状态的改变，对象的相互调用也是通过方法来完成。

### Java 中的类

类可以看成是创建 Java 对象的模板。

![](https://www.runoob.com/wp-content/uploads/2013/12/20210105-java-object-1.png)

通过上图创建一个简单的类来理解下 Java 中类的定义：
```java
public class Dog {
    String breed;
    int size;
    String colour;
    int age;
 
    void eat() {
    }
 
    void run() {
    }
 
    void sleep(){
    }
 
    void name(){
    }
}
```
一个类可以包含以下类型变量：

* 局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
* 成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
* 类变量：类变量也声明在类中，方法体之外，但必须声明为 static 类型。

一个类可以拥有多个方法，在上面的例子中：eat()、run()、sleep() 和 name() 都是 Dog 类的方法。
### 构造方法

每个类都有构造方法。如果没有显式地为类定义构造方法，Java 编译器将会为该类提供一个默认构造方法。

在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。

下面是一个构造方法示例：
```java
public class Puppy{
    public Puppy(){
    }
 
    public Puppy(String name){
        // 这个构造器仅有一个参数：name
    }
}
```
### 创建对象

对象是根据类创建的。在Java中，使用关键字 new 来创建一个新的对象。创建对象需要以下三步：

* 声明：声明一个对象，包括对象名称和对象类型。
* 实例化：使用关键字 new 来创建一个对象。
* 初始化：使用 new 创建对象时，会调用构造方法初始化对象。

下面是一个创建对象的例子：
```java
public class Puppy{
   public Puppy(String name){
      //这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }
   public static void main(String[] args){
      // 下面的语句将创建一个Puppy对象
      Puppy myPuppy = new Puppy( "tommy" );
   }
}
```
编译并运行上面的程序，会打印出下面的结果：
```java
小狗的名字是 : tommy
```
### 访问实例变量和方法

通过已创建的对象来访问成员变量和成员方法，如下所示：
```java
/* 实例化对象 */
Object referenceVariable = new Constructor();
/* 访问类中的变量 */
referenceVariable.variableName;
/* 访问类中的方法 */
referenceVariable.methodName();
```
使用 Object 类型声明变量只能在编译时访问 Object 类中的方法和属性，但在运行时，你可以通过强制类型转换将其转换为特定类型，以便访问特定类型的方法和属性。
### 实例

下面的例子展示如何访问实例变量和调用成员方法：
Puppy.java 文件代码：
```java
public class Puppy {
    private int age;
    private String name;
 
    // 构造器
    public Puppy(String name) {
        this.name = name;
        System.out.println("小狗的名字是 : " + name);
    }
 
    // 设置 age 的值
    public void setAge(int age) {
        this.age = age;
    }
 
    // 获取 age 的值
    public int getAge() {
        return age;
    }
 
    // 获取 name 的值
    public String getName() {
        return name;
    }
 
    // 主方法
    public static void main(String[] args) {
        // 创建对象
        Puppy myPuppy = new Puppy("Tommy");
 
        // 通过方法来设定 age
        myPuppy.setAge(2);
 
        // 调用另一个方法获取 age
        int age = myPuppy.getAge();
        System.out.println("小狗的年龄为 : " + age);
 
        // 也可以直接访问成员变量（通过 getter 方法）
        System.out.println("变量值 : " + myPuppy.getAge());
    }
}
```
编译并运行上面的程序，产生如下结果：
```java
小狗的名字是 : tommy
小狗的年龄为 : 2
变量值 : 2
```
### 源文件声明规则

在本节的最后部分，我们将学习源文件的声明规则。当在一个源文件中定义多个类，并且还有 import 语句和 package 语句时，要特别注意这些规则。

* 一个源文件中只能有一个 public 类
* 一个源文件可以有多个非 public 类
* 源文件的名称应该和 public 类的类名保持一致。例如：源文件中 public 类的类名是 Employee，那么源文件应该命名为Employee.java。
* 如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。
* 如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。
* import 语句和 package 语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。

类有若干种访问级别，并且类也分不同的类型：抽象类和 final 类等。这些将在访问控制章节介绍。

除了上面提到的几种类型，Java 还有一些特殊的类，如：内部类、匿名类。
### Java 包

包主要用来对类和接口进行分类。当开发 Java 程序时，可能编写成百上千的类，因此很有必要对类和接口进行分类。
### import 语句

在 Java 中，如果给出一个完整的限定名，包括包名、类名，那么 Java 编译器就可以很容易地定位到源代码或者类。import 语句就是用来提供一个合理的路径，使得编译器可以找到某个类。

例如，下面的命令行将会命令编译器载入 java_installation/java/io 路径下的所有类

import java.io.*;

### 一个简单的例子

在该例子中，我们创建两个类：Employee 和 EmployeeTest。

首先打开代码编辑器，把下面的代码粘贴进去，将文件保存为 Employee.java。

Employee 类有四个成员变量：name、age、designation 和 salary，该类显式声明了一个构造方法，该方法只有一个参数。
Employee.java 文件代码：
```java
import java.io.*;
 
public class Employee {
    private String name;
    private int age;
    private String designation;
    private double salary;
 
    // Employee 类的构造器
    public Employee(String name) {
        this.name = name;
    }
 
    // 设置 age 的值
    public void setAge(int age) {
        this.age = age;
    }
 
    // 获取 age 的值
    public int getAge() {
        return age;
    }
 
    // 设置 designation 的值
    public void setDesignation(String designation) {
        this.designation = designation;
    }
 
    // 获取 designation 的值
    public String getDesignation() {
        return designation;
    }
 
    // 设置 salary 的值
    public void setSalary(double salary) {
        this.salary = salary;
    }
 
    // 获取 salary 的值
    public double getSalary() {
        return salary;
    }
 
    // 打印信息
    public void printEmployee() {
        System.out.println(this);
    }
 
    // 重写 toString 方法
    @Override
    public String toString() {
        return "名字: " + name + "\n" +
               "年龄: " + age + "\n" +
               "职位: " + designation + "\n" +
               "薪水: " + salary;
    }
}
```
Java 程序都是从 main 方法开始执行，为了能运行这个程序，必须包含 main 方法并且创建一个实例对象。

下面给出 EmployeeTest 类，该类实例化 2 个 Employee 类的实例，并调用方法设置变量的值。

将下面的代码保存在 EmployeeTest.java文件中。
EmployeeTest.java 文件代码：
```java
import java.io.*;
 
public class EmployeeTest {
    public static void main(String[] args) {
        // 使用构造器创建两个对象
        Employee empOne = new Employee("RUNOOB1");
        Employee empTwo = new Employee("RUNOOB2");
 
        // 调用这两个对象的成员方法
        empOne.setAge(26);
        empOne.setDesignation("高级程序员");
        empOne.setSalary(1000);
        empOne.printEmployee();
 
        empTwo.setAge(21);
        empTwo.setDesignation("菜鸟程序员");
        empTwo.setSalary(500);
        empTwo.printEmployee();
    }
}
```

编译这两个文件并且运行 EmployeeTest 类，可以看到如下结果：
```java
$ javac EmployeeTest.java Employee.java
$ java EmployeeTest 
名字:RUNOOB1
年龄:26
职位:高级程序员
薪水:1000.0
名字:RUNOOB2
年龄:21
职位:菜鸟程序员
薪水:500.0
```
### java基本数据类型
变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。

内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。

![](https://www.runoob.com/wp-content/uploads/2013/12/2020-10-27-code-mem.png)

因此，通过定义不同类型的变量，可以在内存中储存整数、小数或者字符。

Java 的两大数据类型:

* 内置数据类型
* 引用数据类型

### 内置数据类型

Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

byte：

* byte 数据类型是8位、有符号的，以二进制补码表示的整数；
* 最小值是 -128（-2^7）；
* 最大值是 127（2^7-1）；
* 默认值是 0；
* byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一；
* 例子：byte a = 100，byte b = -50。

short：

* short 数据类型是 16 位、有符号的以二进制补码表示的整数
* 最小值是 -32768（-2^15）；
* 最大值是 32767（2^15 - 1）；
* Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
* 默认值是 0；
* 例子：short s = 1000，short r = -20000。

int：

* int 数据类型是32位、有符号的以二进制补码表示的整数；
* 最小值是 -2,147,483,648（-2^31）；
* 最大值是 2,147,483,647（2^31 - 1）；
* 一般地整型变量默认为 int 类型；
* 默认值是 0 ；
* 例子：int a = 100000, int b = -200000。

long：

* long 数据类型是 64 位、有符号的以二进制补码表示的整数；
* 最小值是 -9,223,372,036,854,775,808（-2^63）；
* 最大值是 9,223,372,036,854,775,807（2^63 -1）；
* 这种类型主要使用在需要比较大整数的系统上；
* 默认值是 0L；
* 例子： long a = 100000L，long b = -200000L。
    "L"理论上不分大小写，但是若写成"l"容易与数字"1"混淆，不容易分辩。所以最好大写。

float：

* float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
* float 在储存大型浮点数组的时候可节省内存空间；
* 默认值是 0.0f；
* 浮点数不能用来表示精确的值，如货币；
* 例子：float f1 = 234.5f。

double：

* double 数据类型是双精度、64 位、符合 IEEE 754 标准的浮点数；
* 浮点数的默认类型为 double 类型；
* double类型同样不能表示精确的值，如货币；
* 默认值是 0.0d；

* 例子：
```java
    double   d1  = 7D ;
    double   d2  = 7.; 
    double   d3  =  8.0; 
    double   d4  =  8.D; 
    double   d5  =  12.9867; 

    7 是一个 int 字面量，而 7D，7. 和 8.0 是 double 字面量。
```
boolean：

* boolean数据类型表示一位的信息；
* 只有两个取值：true 和 false；
* 这种类型只作为一种标志来记录 true/false 情况；
* 默认值是 false；
* 例子：boolean one = true。

char：

* char 类型是一个单一的 16 位 Unicode 字符；
* 最小值是 \u0000（十进制等效值为 0）；
* 最大值是 \uffff（即为 65535）；
* char 数据类型可以储存任何字符；
    例子：char letter = 'A';。

### 实例

对于数值类型的基本类型的取值范围，我们无需强制去记忆，因为它们的值都已经以常量的形式定义在对应的包装类中了。请看下面的例子：
```java
public class PrimitiveTypeTest {  
    public static void main(String[] args) {  
        // byte  
        System.out.println("基本类型：byte 二进制位数：" + Byte.SIZE);  
        System.out.println("包装类：java.lang.Byte");  
        System.out.println("最小值：Byte.MIN_VALUE=" + Byte.MIN_VALUE);  
        System.out.println("最大值：Byte.MAX_VALUE=" + Byte.MAX_VALUE);  
        System.out.println();  
  
        // short  
        System.out.println("基本类型：short 二进制位数：" + Short.SIZE);  
        System.out.println("包装类：java.lang.Short");  
        System.out.println("最小值：Short.MIN_VALUE=" + Short.MIN_VALUE);  
        System.out.println("最大值：Short.MAX_VALUE=" + Short.MAX_VALUE);  
        System.out.println();  
  
        // int  
        System.out.println("基本类型：int 二进制位数：" + Integer.SIZE);  
        System.out.println("包装类：java.lang.Integer");  
        System.out.println("最小值：Integer.MIN_VALUE=" + Integer.MIN_VALUE);  
        System.out.println("最大值：Integer.MAX_VALUE=" + Integer.MAX_VALUE);  
        System.out.println();  
  
        // long  
        System.out.println("基本类型：long 二进制位数：" + Long.SIZE);  
        System.out.println("包装类：java.lang.Long");  
        System.out.println("最小值：Long.MIN_VALUE=" + Long.MIN_VALUE);  
        System.out.println("最大值：Long.MAX_VALUE=" + Long.MAX_VALUE);  
        System.out.println();  
  
        // float  
        System.out.println("基本类型：float 二进制位数：" + Float.SIZE);  
        System.out.println("包装类：java.lang.Float");  
        System.out.println("最小值：Float.MIN_VALUE=" + Float.MIN_VALUE);  
        System.out.println("最大值：Float.MAX_VALUE=" + Float.MAX_VALUE);  
        System.out.println();  
  
        // double  
        System.out.println("基本类型：double 二进制位数：" + Double.SIZE);  
        System.out.println("包装类：java.lang.Double");  
        System.out.println("最小值：Double.MIN_VALUE=" + Double.MIN_VALUE);  
        System.out.println("最大值：Double.MAX_VALUE=" + Double.MAX_VALUE);  
        System.out.println();  
  
        // char  
        System.out.println("基本类型：char 二进制位数：" + Character.SIZE);  
        System.out.println("包装类：java.lang.Character");  
        // 以数值形式而不是字符形式将Character.MIN_VALUE输出到控制台  
        System.out.println("最小值：Character.MIN_VALUE="  
                + (int) Character.MIN_VALUE);  
        // 以数值形式而不是字符形式将Character.MAX_VALUE输出到控制台  
        System.out.println("最大值：Character.MAX_VALUE="  
                + (int) Character.MAX_VALUE);  
    }  
}
```

编译以上代码输出结果如下所示：
```java
基本类型：byte 二进制位数：8
包装类：java.lang.Byte
最小值：Byte.MIN_VALUE=-128
最大值：Byte.MAX_VALUE=127

基本类型：short 二进制位数：16
包装类：java.lang.Short
最小值：Short.MIN_VALUE=-32768
最大值：Short.MAX_VALUE=32767

基本类型：int 二进制位数：32
包装类：java.lang.Integer
最小值：Integer.MIN_VALUE=-2147483648
最大值：Integer.MAX_VALUE=2147483647

基本类型：long 二进制位数：64
包装类：java.lang.Long
最小值：Long.MIN_VALUE=-9223372036854775808
最大值：Long.MAX_VALUE=9223372036854775807

基本类型：float 二进制位数：32
包装类：java.lang.Float
最小值：Float.MIN_VALUE=1.4E-45
最大值：Float.MAX_VALUE=3.4028235E38

基本类型：double 二进制位数：64
包装类：java.lang.Double
最小值：Double.MIN_VALUE=4.9E-324
最大值：Double.MAX_VALUE=1.7976931348623157E308

基本类型：char 二进制位数：16
包装类：java.lang.Character
最小值：Character.MIN_VALUE=0
最大值：Character.MAX_VALUE=65535
```

Float和Double的最小值和最大值都是以科学记数法的形式输出的，结尾的"E+数字"表示E之前的数字要乘以10的多少次方。比如3.14E3就是3.14 × 103 =3140，3.14E-3 就是 3.14 x 10-3 =0.00314。

实际上，JAVA中还存在另外一种基本类型 void，它也有对应的包装类 java.lang.Void，不过我们无法直接对它们进行操作。

### 类型默认值

下表列出了 Java 各个类型的默认值：

数据类型|默认值
--|--
int|0
long|0L
short|0
char|'\u0000'
byte|0
float|0.0f
double|0.0d
boolean|false
引用类型（类、接口、数组）|null

说明：

* int, short, long, byte 的默认值是0。
* char 的默认值是 \u0000（空字符）。
* float 的默认值是 0.0f。
* double 的默认值是 0.0d。
* boolean 的默认值是 false。
* 引用类型（类、接口、数组）的默认值是 null。

实例

```java
public class Test {
    static boolean bool;
    static byte by;
    static char ch;
    static double d;
    static float f;
    static int i;
    static long l;
    static short sh;
    static String str;
 
    public static void main(String[] args) {
        System.out.println("Bool :" + bool);
        System.out.println("Byte :" + by);
        System.out.println("Character:" + ch);
        System.out.println("Double :" + d);
        System.out.println("Float :" + f);
        System.out.println("Integer :" + i);
        System.out.println("Long :" + l);
        System.out.println("Short :" + sh);
        System.out.println("String :" + str);
    }
}
```
实例输出结果为：
```java
Bool     :false
Byte     :0
Character:
Double   :0.0
Float    :0.0
Integer  :0
Long     :0
Short    :0
String   :null
```

### 引用类型

* 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
* 对象、数组都是引用数据类型。
* 所有引用类型的默认值都是null。
* 一个引用变量可以用来引用任何与之兼容的类型。
* 例子：Site site = new Site("Runoob")。

### Java 常量

常量在程序运行时是不能被修改的。

在 Java 中使用 final 关键字来修饰常量，声明方式和变量类似：
```java
final double PI = 3.1415927;
```
虽然常量名也可以用小写，但为了便于识别，通常使用大写字母表示常量。

字面量可以赋给任何内置类型的变量。例如：
```java
byte a = 68;
char a = 'A'
```
byte、int、long、和short都可以用十进制、16进制以及8进制的方式来表示。

当使用字面量的时候，前缀 0 表示 8 进制，而前缀 0x 代表 16 进制, 例如：
```java
int decimal = 100;
int octal = 0144;
int hexa =  0x64;
```
和其他语言一样，Java的字符串常量也是包含在两个引号之间的字符序列。下面是字符串型字面量的例子：
```java
"Hello World"
"two\nlines"
"\"This is in quotes\""
```
字符串常量和字符变量都可以包含任何 Unicode 字符。例如：
```java
char a = '\u0001';
String a = "\u0001";
```
Java语言支持一些特殊的转义字符序列。

符号 |字符含义
--|--
\n |换行 (0x0a)
\r |回车 (0x0d)
\f |换页符(0x0c)
\b |退格 (0x08)
\0 |空字符 (0x0)
\s |空格 (0x20)
\t |制表符
\" |双引号
\' |单引号
\\ |反斜杠
\ddd |八进制字符 (ddd)
\uxxxx |16进制Unicode字符 (xxxx)


### 自动类型转换

**整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。**

转换从低级到高级。
```java
低  ------------------------------------>  高

byte,short,char—> int —> long—> float —> double 
```
数据类型转换必须满足如下规则：

1. 不能对boolean类型进行类型转换。

2. 不能把对象类型转换成不相关类的对象。

3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

4. 转换过程中可能导致溢出或损失精度，例如：
```java
    int i =128;   
    byte b = (byte)i;
```
因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。

5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：
```java
    (int)23.7 == 23;        
    (int)-45.89f == -45
```
#### 自动类型转换

必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。
```java
public class ZiDongLeiZhuan{
        public static void main(String[] args){
            char c1='a';//定义一个char类型
            int i1 = c1;//char自动类型转换为int
            System.out.println("char自动类型转换为int后的值等于"+i1);
            char c2 = 'A';//定义一个char类型
            int i2 = c2+1;//char 类型和 int 类型计算
            System.out.println("char类型和int计算后的值等于"+i2);
        }
}
```
运行结果为:
```java
char自动类型转换为int后的值等于97
char类型和int计算后的值等于66
```
解析：c1 的值为字符 a ,查 ASCII 码表可知对应的 int 类型值为 97， A 对应值为 65，所以 i2=65+1=66。
### 强制类型转换

1. 条件是转换的数据类型必须是兼容的。

2. 格式：(type)value type是要强制类型转换后的数据类型 实例：
```java
    public class ForceTransform {
        public static void main(String[] args){
            int i1 = 123;
            byte b = (byte)i1;//强制类型转换为byte
            System.out.println("int强制类型转换为byte后的值等于"+b);
        }
    }
```
运行结果：
```java
int强制类型转换为byte后的值等于123
```
### 隐含强制类型转换

1. 整数的默认类型是 int。

2. 小数默认是 double 类型浮点型，在定义 float 类型时必须在数字后面跟上 F 或者 f。

这一节讲解了 Java 的基本数据类型。下一节将探讨不同的变量类型以及它们的用法。
## Java 变量类型

在 Java 语言中，所有的变量在使用前必须声明。

声明变量的基本格式如下：
type identifier [ = value][, identifier [= value] ...] ;

格式说明：

* type -- 数据类型。
* identifier -- 是变量名，可以使用逗号 , 隔开来声明多个同类型变量。

以下列出了一些变量的声明实例。注意有些包含了初始化过程。
```java
int a, b, c;         // 声明三个int型整数：a、 b、c
int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
byte z = 22;         // 声明并初始化 z
String s = "runoob";  // 声明并初始化字符串 s
double pi = 3.14159; // 声明了双精度浮点型变量 pi
char x = 'x';        // 声明变量 x 的值是字符 'x'。
```
Java 语言支持的变量类型有：

* 局部变量（Local Variables）：局部变量是在方法、构造函数或块内部声明的变量，它们在声明的方法、构造函数或块执行结束后被销毁，局部变量在声明时需要初始化，否则会导致编译错误。
```java
    public void exampleMethod() {
        int localVar = 10; // 局部变量
        // ...
    }
```
* 实例变量（Instance Variables）：实例变量是在类中声明，但在方法、构造函数或块之外，它们属于类的实例，每个类的实例都有自己的副本，如果不明确初始化，实例变量会被赋予默认值（数值类型为0，boolean类型为false，对象引用类型为null）。
```java
    public class ExampleClass {
        int instanceVar; // 实例变量
    }
```
* 静态变量或类变量（Class Variables）：类变量是在类中用 static 关键字声明的变量，它们属于类而不是实例，所有该类的实例共享同一个类变量的值，类变量在类加载时被初始化，而且只初始化一次。
```java
    public class ExampleClass {
        static int classVar; // 类变量
    }
```
* 参数变量（Parameters）：参数是方法或构造函数声明中的变量，用于接收调用该方法或构造函数时传递的值，参数变量的作用域只限于方法内部。
```java
    public void exampleMethod(int parameterVar) {
        // 参数变量
        // ...
    }
```
以下实例中定义了一个 RunoobTest 类，其中包含了一个成员变量 instanceVar 和一个静态变量 staticVar。

method() 方法中定义了一个参数变量 paramVar 和一个局部变量 localVar。在方法内部，我们将局部变量的值赋给成员变量，将参数变量的值赋给静态变量，然后打印出这些变量的值。

在 main() 方法中，我们创建了一个 RunoobTest 对象，并调用了它的 method() 方法。
```java
public class RunoobTest {
    // 成员变量
    private int instanceVar;
    // 静态变量
    private static int staticVar;
    
    public void method(int paramVar) {
        // 局部变量
        int localVar = 10;
        
        // 使用变量
        instanceVar = localVar;
        staticVar = paramVar;
        
        System.out.println("成员变量: " + instanceVar);
        System.out.println("静态变量: " + staticVar);
        System.out.println("参数变量: " + paramVar);
        System.out.println("局部变量: " + localVar);
    }
    
    public static void main(String[] args) {
        RunoobTest v = new RunoobTest();
        v.method(20);
    }
}
```
运行以上代码，输出如下：
```java
成员变量: 10
静态变量: 20
参数变量: 20
局部变量: 10
```
### Java 参数变量

Java 中的参数变量是指在方法或构造函数中声明的变量，用于接收传递给方法或构造函数的值。参数变量与局部变量类似，但它们只在方法或构造函数被调用时存在，并且只能在方法或构造函数内部使用。

Java 方法的声明语法如下：
```java
accessModifier returnType methodName(parameterType parameterName1, parameterType parameterName2, ...) {
    // 方法体
}
```
* parameterType -- 表示参数变量的类型。
* parameterName -- 表示参数变量的名称。

在调用方法时，我们必须为参数变量传递值，这些值可以是常量、变量或表达式。

方法参数变量的值传递方式有两种：**值传递**和**引用传递**。

* **值传递**：在方法调用时，传递的是实际参数的值的副本。当参数变量被赋予新的值时，只会修改副本的值，不会影响原始值。Java 中的基本数据类型都采用值传递方式传递参数变量的值。

* **引用传递**：在方法调用时，传递的是实际参数的引用（即内存地址）。当参数变量被赋予新的值时，会修改原始值的内容。Java 中的对象类型采用引用传递方式传递参数变量的值。

以下是一个简单的例子，展示了方法参数变量的使用：
```java
public class RunoobTest {
    public static void main(String[] args) {
        int a = 10, b = 20;
        swap(a, b); // 调用swap方法
        System.out.println("a = " + a + ", b = " + b); // 输出a和b的值
    }
   
    public static void swap(int x, int y) {
        int temp = x;
        x = y;
        y = temp;
    }
}
```
运行以上代码，输出如下：
```java
a = 10, b = 20
```
### Java 局部变量

Java 的局部变量是在方法、构造方法或语句块内部声明的变量，其作用域限制在声明它的代码块内部。

局部变量的声明语法为：
```java
type variableName;
```
* type -- 表示变量的类型。
* variableName -- 表示变量的名称。

说明：

* 作用域：局部变量的作用域限于它被声明的方法、构造方法或代码块内。一旦代码执行流程离开这个作用域，局部变量就不再可访问。

* 生命周期：局部变量的生命周期从声明时开始，到方法、构造方法或代码块执行结束时终止。之后，局部变量将被垃圾回收。

* 初始化：局部变量在使用前必须被初始化。如果不进行初始化，编译器会报错，因为 Java 不会为局部变量提供默认值。

* 声明：局部变量的声明必须在方法或代码块的开始处进行。声明时可以指定数据类型，后面跟着变量名，例如：int count;。

* 赋值：局部变量在声明后必须被赋值，才能在方法内使用。赋值可以是直接赋值，也可以是通过方法调用或表达式。

* 限制：局部变量不能被类的其他方法直接访问，它们只为声明它们的方法或代码块所私有。

* 内存管理：局部变量存储在 Java 虚拟机（JVM）的栈上，与存储在堆上的实例变量或对象不同。

* 垃圾回收：由于局部变量的生命周期严格限于方法或代码块的执行，它们在方法或代码块执行完毕后不再被引用，因此JVM的垃圾回收器会自动回收它们占用的内存。

* 重用：局部变量的名称可以在不同的方法或代码块中重复使用，因为它们的作用域是局部的，不会引起命名冲突。

* 参数和返回值：方法的参数可以视为一种特殊的局部变量，它们在方法被调用时初始化，并在方法返回后生命周期结束。

实例

以下是一个简单的例子，展示了局部变量的使用：
```java
public class LocalVariablesExample {
    public static void main(String[] args) {
        int a = 10; // 局部变量a的声明和初始化
        int b;     // 局部变量b的声明
        b = 20;    // 局部变量b的初始化
       
        System.out.println("a = " + a);
        System.out.println("b = " + b);
       
        // 如果在使用之前不初始化局部变量，编译器会报错
        // int c;
        // System.out.println("c = " + c);
    }
}
```
以上实例中我们声明并初始化了两个局部变量 a 和 b，然后打印出它们的值。注意，如果在使用局部变量之前不初始化它，编译器会报错。

在以下实例中 age 是一个局部变量，定义在 pupAge()方法中，它的作用域就限制在这个方法中：
```java
package com.runoob.test;
 
public class Test{ 
   public void pupAge(){
      int age = 0;
      age = age + 7;
      System.out.println("小狗的年龄是: " + age);
   }
   
   public static void main(String[] args){
      Test test = new Test();
      test.pupAge();
   }
}
```
以上实例编译运行结果如下:
```java
小狗的年龄是: 7
```
在下面的例子中 age 变量没有初始化，所以在编译时会出错：
```java
package com.runoob.test;
 
public class Test{ 
   public void pupAge(){
      int age;
      age = age + 7;
      System.out.println("小狗的年龄是 : " + age);
   }
   
   public static void main(String[] args){
      Test test = new Test();
      test.pupAge();
   }
}
```
以上实例编译运行结果如下:
```java
Test.java:4:variable number might not have been initialized
age = age + 7;
         ^
1 error
```
### 成员变量（实例变量）

* 成员变量声明在一个类中，但在方法、构造方法和语句块之外。
* 当一个对象被实例化之后，每个成员变量的值就跟着确定。
* 成员变量在对象创建的时候创建，在对象被销毁的时候销毁。
* 成员变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息。
* 成员变量可以声明在使用前或者使用后。
* 访问修饰符可以修饰成员变量。
* 成员变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把成员变量设为私有。通过使用访问修饰符可以使成员变量对子类可见。
* 成员变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是 false，引用类型变量的默认值是 null。变量的值可以在声明时指定，也可以在构造方法中指定；
* 成员变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName。

成员变量的声明语法为：
```java
accessModifier type variableName;
```
* accessModifier --表示访问修饰符，可以是 public、protected、private 或默认访问级别（即没有显式指定访问修饰符）。
* type -- 表示变量的类型。
* variableName -- 表示变量的名称。

与局部变量不同，成员变量的值在创建对象时被分配，即使未对其初始化，它们也会被赋予默认值，例如 int 类型的变量默认值为 0，boolean 类型的变量默认值为 false。

成员变量可以通过对象访问，也可以通过类名访问（如果它们是静态成员变量）。如果没有显式初始化成员变量，则它们将被赋予默认值。可以在构造函数或其他方法中初始化成员变量，或者通过对象或类名访问它们并设置它们的值。
#### 实例

以下实例我们声明了两个成员变量 a 和 b，并对其进行了访问和设置。注意，我们可以通过对象访问成员变量，也可以通过类名访问静态成员变量。
```java
public class RunoobTest {
      private int a; // 私有成员变量a
      public String b = "Hello"; // 公有成员变量b
     
      public static void main(String[] args) {
         RunoobTest obj = new RunoobTest(); // 创建对象
         
          obj.a = 10; // 访问成员变量a，并设置其值为10
          System.out.println("a = " + obj.a);
         
          obj.b = "World"; // 访问成员变量b，并设置其值为"World"
          System.out.println("b = " + obj.b);
      }
  }
```
以上实例编译运行结果如下:
```java
a = 10
b = World
```
以下实例我们声明了两个成员变量 name 和 salary，并对其进行了访问和设置。

Employee.java 文件代码：
```java
import java.io.*;
public class Employee{
   // 这个成员变量对子类可见
   public String name;
   // 私有变量，仅在该类可见
   private double salary;
   //在构造器中对name赋值
   public Employee (String empName){
      name = empName;
   }
   //设定salary的值
   public void setSalary(double empSal){
      salary = empSal;
   }  
   // 打印信息
   public void printEmp(){
      System.out.println("名字 : " + name );
      System.out.println("薪水 : " + salary);
   } 
   public static void main(String[] args){
      Employee empOne = new Employee("RUNOOB");
      empOne.setSalary(1000.0);
      empOne.printEmp();
   }
}
```
以上实例编译运行结果如下:
```java
$ javac Employee.java 
$ java Employee
名字 : RUNOOB
薪水 : 1000.0
```
### 类变量（静态变量）

Java 中的静态变量是指在类中定义的一个变量，它与类相关而不是与实例相关，即无论创建多少个类实例，静态变量在内存中只有一份拷贝，被所有实例共享。

静态变量在类加载时被创建，在整个程序运行期间都存在。
#### 定义方式

静态变量的定义方式是在类中使用 static 关键字修饰变量，通常也称为类变量。

以下实例中我们定义一个静态变量 count ，其初始值为 0：
```java
public class MyClass {
    public static int count = 0;
    // 其他成员变量和方法
}
```
#### 访问方式

由于静态变量是与类相关的，因此可以通过类名来访问静态变量，也可以通过实例名来访问静态变量。
```java
MyClass.count = 10; // 通过类名访问
MyClass obj = new MyClass();
obj.count = 20; // 通过实例名访问
```
#### 生命周期

静态变量的生命周期与程序的生命周期一样长，即它们在类加载时被创建，在整个程序运行期间都存在，直到程序结束才会被销毁。因此，静态变量可以用来存储整个程序都需要使用的数据，如配置信息、全局变量等。
#### 初始化时机

静态变量在类加载时被初始化，其初始化顺序与定义顺序有关。

如果一个静态变量依赖于另一个静态变量，那么它必须在后面定义。
```java
public class MyClass {
    public static int count1 = 0;
    public static int count2 = count1 + 1;
    // 其他成员变量和方法
}
```
上面的例子中，count1 要先于 count2 初始化，否则编译时会报错。
#### 常量和静态变量的区别

常量也是与类相关的，但它是用 final 关键字修饰的变量，一旦被赋值就不能再修改。与静态变量不同的是，常量在编译时就已经确定了它的值，而静态变量的值可以在运行时改变。另外，常量通常用于存储一些固定的值，如数学常数、配置信息等，而静态变量通常用于存储可变的数据，如计数器、全局状态等。

总之，静态变量是与类相关的变量，具有唯一性和共享性，可以用于存储整个程序都需要使用的数据，但需要注意初始化时机和与常量的区别。
#### 静态变量的访问修饰符

静态变量的访问修饰符可以是 public、protected、private 或者默认的访问修饰符（即不写访问修饰符）。

需要注意的是，静态变量的访问权限与实例变量不同，因为静态变量是与类相关的，不依赖于任何实例。
#### 静态变量的线程安全性

Java 中的静态变量是属于类的，而不是对象的实例。因此，当多个线程同时访问一个包含静态变量的类时，需要考虑其线程安全性。

静态变量在内存中只有一份拷贝，被所有实例共享。因此，如果一个线程修改了静态变量的值，那么其他线程在访问该静态变量时也会看到修改后的值。这可能会导致并发访问的问题，因为多个线程可能同时修改静态变量，导致不确定的结果或数据一致性问题。

为了确保静态变量的线程安全性，需要采取适当的同步措施，如同步机制、原子类或 volatile 关键字，以便在多线程环境中正确地读取和修改静态变量的值。
静态变量的命名规范

静态变量（也称为类变量）的命名规范通常遵循驼峰命名法，并且通常使用全大写字母，单词之间用下划线分隔，并且要用 static 关键字明确标识。

* 使用驼峰命名法： 静态变量的命名应该使用驼峰命名法，即首字母小写，后续每个单词的首字母大写。例如：myStaticVariable。

* 全大写字母： 静态变量通常使用全大写字母，单词之间用下划线分隔。这被称为"大写蛇形命名法"（Upper Snake Case）。例如：MY_STATIC_VARIABLE。

* 描述性： 变量名应该是有意义的，能够清晰地表达该变量的用途。避免使用单个字符或不具有明确含义的缩写。

* 避免使用缩写： 尽量避免使用缩写，以提高代码的可读性。如果使用缩写是必要的，确保广泛理解，并在注释中进行解释。

```java
public class MyClass {
    // 使用驼峰命名法
    public static int myStaticVariable;

    // 使用大写蛇形命名法
    public static final int MAX_SIZE = 100;

    // 避免使用缩写
    public static final String employeeName;

    // 具有描述性的变量名
    public static double defaultInterestRate;
}
```
#### 静态变量的使用场景

静态变量通常用于以下场景：

* 存储全局状态或配置信息
* 计数器或统计信息
* 缓存数据或共享资源
* 工具类的常量或方法
* 单例模式中的实例变量

#### 实例

以下实例定义了一个 AppConfig 类，其中包含了三个静态变量 APP_NAME、APP_VERSION 和 DATABASE_URL，用于存储应用程序的名称、版本和数据库连接URL。这些变量都被声明为 final，表示它们是不可修改的常量。

在 main() 方法中，我们打印出了这些静态变量的值。
AppConfig.java 文件代码：
```java
public class AppConfig {
    public static final String APP_NAME = "MyApp";
    public static final String APP_VERSION = "1.0.0";
    public static final String DATABASE_URL = "jdbc:mysql://localhost:3306/mydb";
    
    public static void main(String[] args) {
        System.out.println("Application name: " + AppConfig.APP_NAME);
        System.out.println("Application version: " + AppConfig.APP_VERSION);
        System.out.println("Database URL: " + AppConfig.DATABASE_URL);
    }
}
```
以上实例编译运行结果如下:
```java
Application name: MyApp
Application version: 1.0.0
Database URL: jdbc:mysql://localhost:3306/mydb
```
可以看到，这些静态变量存储的全局配置信息可以在整个程序中使用，并且不会被修改。这个例子展示了静态变量的另一个常见应用，通过它我们可以很方便地存储全局配置信息，或者实现其他需要全局共享的数据。

以下实例定义了一个 Counter 类，其中包含了一个静态变量 count，用于记录创建了多少个 Counter 对象。

每当创建一个新的对象时，构造方法会将计数器加一。静态方法 getCount() 用于获取当前计数器的值。

在 main() 方法中，我们创建了三个 Counter 对象，并打印出了计数器的值。
Counter.java 文件代码：
```java
public class Counter {
    private static int count = 0;
    
    public Counter() {
        count++;
    }
    
    public static int getCount() {
        return count;
    }
    
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();
        System.out.println("目前为止创建的对象数: " + Counter.getCount());
    }
}
```
以上实例编译运行结果如下:
```java
目前为止创建的对象数: 3
```
可以看到，计数器记录了创建了三个对象。这个例子展示了静态变量的一个简单应用，通过它我们可以很方便地统计对象的创建次数，或者记录其他需要全局共享的数据。

本章节中我们学习了Java的变量类型，下一章节中我们将介绍Java修饰符的使用。

## Java 变量命名规则

在 Java 中，不同类型的变量（例如实例变量、局部变量、静态变量等）有一些命名规则和约定。

遵循一些基本规则，这有助于提高代码的可读性和维护性。

以下是各种变量命名规则的概述：

* 使用有意义的名字： 变量名应该具有清晰的含义，能够准确地反映变量的用途。避免使用单个字符或无意义的缩写。

* 驼峰命名法（Camel Case）： 在变量名中使用驼峰命名法，即将每个单词的首字母大写，除了第一个单词外，其余单词的首字母都采用大写形式。例如：myVariableName。

* 避免关键字： 不要使用 Java 关键字（例如，class、int、boolean等）作为变量名。

* 区分大小写： Java 是大小写敏感的，因此变量名中的大小写字母被视为不同的符号。例如，myVariable 和 myvariable 是两个不同的变量。

* 不以数字开头： 变量名不能以数字开头，但可以包含数字。

* 遵循命名约定： 对于不同类型的变量（局部变量、实例变量、静态变量等），可以采用不同的命名约定，例如使用前缀或后缀来区分。

### 局部变量

* 使用驼峰命名法。
* 应该以小写字母开头。
* 变量名应该是描述性的，能够清晰地表示其用途。
```java
int myLocalVariable;
```
### 实例变量（成员变量）

* 使用驼峰命名法。
* 应该以小写字母开头。
* 变量名应该是描述性的，能够清晰地表示其用途。
```java
private int myInstanceVariable;
```
### 静态变量（类变量）

* 使用驼峰命名法，应该以小写字母开头。
* 通常也可以使用大写蛇形命名法，全大写字母，单词之间用下划线分隔。
* 变量名应该是描述性的，能够清晰地表示其用途。
```java
// 使用驼峰命名法
public static int myStaticVariable;

// 使用大写蛇形命名法
public static final int MAX_SIZE = 100;
```
### 常量

* 使用全大写字母，单词之间用下划线分隔。
* 常量通常使用 final 修饰。
```java
public static final double PI = 3.14;
```
### 参数

* 使用驼峰命名法。
* 应该以小写字母开头。
* 参数名应该是描述性的，能够清晰地表示其用途。
```java
public void myMethod(int myParameter) {
    // 方法体
}
```
### 类名

* 使用驼峰命名法。
* 应该以大写字母开头。
* 类名应该是描述性的，能够清晰地表示其用途。
```java
public class MyClass {
    // 类的成员和方法
}
```
## Java 修饰符

Java语言提供了很多修饰符，主要分为以下两类：

* 访问修饰符
* 非访问修饰符

修饰符用来定义类、方法或者变量，通常放在语句的最前端。我们通过下面的例子来说明：
```java
public class ClassName {
   // ...
}
private boolean myFlag;
static final double weeks = 9.5;
protected static final int BOXWIDTH = 42;
public static void main(String[] arguments) {
   // 方法体
}
```
### 访问控制修饰符

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

* default (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
* private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
* public : 对所有类可见。使用对象：类、接口、变量、方法
* protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

我们可以通过以下表来说明访问权限：

**访问控制** 

修饰符 |当前类 |同一包内 |子孙类(同一包) 	子孙类(不同包) |其他包
--|--|--|--|--
public |Y |Y |Y |Y|Y
protected |Y |Y |Y|	Y/N（说明） |N
default |Y|	Y |Y |N |N
private |Y |N |N |N |N

#### 默认访问修饰符-不使用任何关键字

如果在类、变量、方法或构造函数的定义中没有指定任何访问修饰符，那么它们就默认具有默认访问修饰符。

默认访问修饰符的访问级别是包级别（package-level），即只能被同一包中的其他类访问。

如下例所示，变量和方法的声明可以不使用任何修饰符。
```java
// MyClass.java
 
class MyClass {  // 默认访问修饰符
 
    int x = 10;  // 默认访问修饰符
 
    void display() {  // 默认访问修饰符
        System.out.println("Value of x is: " + x);
    }
}
 
// MyOtherClass.java
 
class MyOtherClass {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.display();  // 访问 MyClass 中的默认访问修饰符变量和方法
    }
}
```
以上实例中，MyClass 类和它的成员变量 x 和方法 display() 都使用默认访问修饰符进行了定义。MyOtherClass 类在同一包中，因此可以访问 MyClass 类和它的成员变量和方法。
#### 私有访问修饰符-private

私有访问修饰符是最严格的访问级别，所以被声明为 private 的方法、变量和构造方法只能被所属类访问，并且类和接口不能声明为 private。

声明为私有访问类型的变量只能通过类中公共的 getter 方法被外部类访问。

Private 访问修饰符的使用主要用来隐藏类的实现细节和保护类的数据。

下面的类使用了私有访问修饰符：
```java
public class Logger {
   private String format;
   public String getFormat() {
      return this.format;
   }
   public void setFormat(String format) {
      this.format = format;
   }
}
```
实例中，Logger 类中的 format 变量为私有变量，所以其他类不能直接得到和设置该变量的值。为了使其他类能够操作该变量，定义了两个 public 方法：getFormat() （返回 format的值）和 setFormat(String)（设置 format 的值）
#### 公有访问修饰符-public

被声明为 public 的类、方法、构造方法和接口能够被任何其他类访问。

如果几个相互访问的 public 类分布在不同的包中，则需要导入相应 public 类所在的包。由于类的继承性，类所有的公有方法和变量都能被其子类继承。

以下函数使用了公有访问控制：
```java
public static void main(String[] arguments) {
   // ...
}
```
Java 程序的 main() 方法必须设置成公有的，否则，Java 解释器将不能运行该类。
#### 受保护的访问修饰符-protected

protected 需要从以下两个点来分析说明：

*  子类与基类在同一包中：被声明为 protected 的变量、方法和构造器能被同一个包中的任何其他类访问；

* 子类与基类不在同一包中：那么在子类中，子类实例可以访问其从基类继承而来的 protected 方法，而不能访问基类实例的protected方法。

protected 可以修饰数据成员，构造方法，方法成员，不能修饰类（内部类除外）。

接口及接口的成员变量和成员方法不能声明为 protected。 可以看看下图演示：

![](https://www.runoob.com/wp-content/uploads/2013/12/java-protected.gif)

子类能访问 protected 修饰符声明的方法和变量，这样就能保护不相关的类使用这些方法和变量。

下面的父类使用了 protected 访问修饰符，子类重写了父类的 openSpeaker() 方法。

```java
class AudioPlayer {
   protected boolean openSpeaker(Speaker sp) {
      // 实现细节
   }
}
 
class StreamingAudioPlayer extends AudioPlayer {
   protected boolean openSpeaker(Speaker sp) {
      // 实现细节
   }
}
```
如果把 openSpeaker() 方法声明为 private，那么除了 AudioPlayer 外，其他类将不能访问该方法。

如果把 openSpeaker() 声明为 public，那么所有的类都能够访问该方法。

如果我们只想让该方法对其所在类的子类可见，则将该方法声明为 protected。

>protected 是最难理解的一种 Java 类成员访问权限修饰词，更多详细内容请查看 [Java protected 关键字详解](#Java-protected-关键字详解)。

#### 访问控制和继承

请注意以下方法继承的规则：

* 父类中声明为 public 的方法在子类中也必须为 public。

* 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。

* 父类中声明为 private 的方法，不能够被子类继承。

### 非访问修饰符

为了实现一些其他的功能，Java 也提供了许多非访问修饰符。

* static 修饰符，用来修饰类方法和类变量。

* final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

* abstract 修饰符，用来创建抽象类和抽象方法。

* synchronized 和 volatile 修饰符，主要用于线程的编程。
#### static 修饰符

* 静态变量：

    static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

* 静态方法：

    static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。 

对类变量和方法的访问可以直接使用 classname.variablename 和 classname.methodname 的方式访问。

如下例所示，static 修饰符用来创建类方法和类变量。
```java
public class InstanceCounter {
   private static int numInstances = 0;
   protected static int getCount() {
      return numInstances;
   }
 
   private static void addInstance() {
      numInstances++;
   }
 
   InstanceCounter() {
      InstanceCounter.addInstance();
   }
 
   public static void main(String[] arguments) {
      System.out.println("Starting with " +
      InstanceCounter.getCount() + " instances");
      for (int i = 0; i < 500; ++i){
         new InstanceCounter();
          }
      System.out.println("Created " +
      InstanceCounter.getCount() + " instances");
   }
}
```
以上实例运行编辑结果如下:
```java
Starting with 0 instances
Created 500 instances
```
#### final 修饰符

##### final 变量：

final 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须显式指定初始值。

final 修饰符通常和 static 修饰符一起使用来创建类常量。
```java
public class Test{
  final int value = 10;
  // 下面是声明常量的实例
  public static final int BOXWIDTH = 6;
  static final String TITLE = "Manager";
 
  public void changeValue(){
     value = 12; //将输出一个错误
  }
}
```
##### final 方法

父类中的 final 方法可以被子类继承，但是不能被子类重写。

声明 final 方法的主要目的是防止该方法的内容被修改。

如下所示，使用 final 修饰符声明方法。
```java
public class Test{
    public final void changeName(){
       // 方法体
    }
}
```
##### final 类

final 类不能被继承，没有类能够继承 final 类的任何特性。
```java
public final class Test {
   // 类体
}
```
#### abstract 修饰符

##### 抽象类：

抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。

抽象类可以包含抽象方法和非抽象方法。
```java
abstract class Caravan{
   private double price;
   private String model;
   private String year;
   public abstract void goFast(); //抽象方法
   public abstract void changeColor();
}
```
##### 抽象方法

抽象方法是一种没有任何实现的方法，该方法的具体实现由子类提供。

抽象方法不能被声明成 final 和 static。

任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。

抽象方法的声明以分号结尾，例如：public abstract sample();。
```java
public abstract class SuperClass{
    abstract void m(); //抽象方法
}
 
class SubClass extends SuperClass{
     //实现抽象方法
      void m(){
          .........
      }
}
```
#### synchronized 修饰符

synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。
```java
public synchronized void showDetails(){
.......
}
```
#### transient 修饰符

序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。

该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
```java
public transient int limit = 55;   // 不会持久化
public int b; // 持久化
```
#### volatile 修饰符

volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。

一个 volatile 对象引用可能是 null。
```java
public class MyRunnable implements Runnable
{
    private volatile boolean active;
    public void run()
    {
        active = true;
        while (active) // 第一行
        {
            // 代码
        }
    }
    public void stop()
    {
        active = false; // 第二行
    }
}
```
通常情况下，在一个线程调用 run() 方法（在 Runnable 开启的线程），在另一个线程调用 stop() 方法。 如果 第一行 中缓冲区的 active 值被使用，那么在 第二行 的 active 值为 false 时循环不会停止。

但是以上代码中我们使用了 volatile 修饰 active，所以该循环会停止。

## Java 运算符

计算机的最基本用途之一就是执行数学运算，作为一门计算机语言，Java也提供了一套丰富的运算符来操纵变量。我们可以把运算符分成以下几组：

* 算术运算符
* 关系运算符
* 位运算符
* 逻辑运算符
* 赋值运算符
* 其他运算符

### 算术运算符

算术运算符用在数学表达式中，它们的作用和在数学中的作用一样。下表列出了所有的算术运算符。

表格中的实例假设整数变量A的值为10，变量B的值为20：
操作符 |描述 |例子
--|--|--
+ |加法 - 相加运算符两侧的值 |A + B 等于 30
- |减法 - 左操作数减去右操作数 |A – B 等于 -10
* |乘法 - 相乘操作符两侧的值 |A * B等于200
/ |除法 - 左操作数除以右操作数 |B / A等于2
％ |取余 - 左操作数除以右操作数的余数 |B%A等于0
++ |自增: 操作数的值增加1 |B++ 或 ++B 等于 21（区别详见下文）
-- 	|自减: 操作数的值减少1 |B-- 或 --B 等于 19（区别详见下文）
#### 实例

下面的简单示例程序演示了算术运算符。复制并粘贴下面的 Java 程序并保存为 Test.java 文件，然后编译并运行这个程序：
```java
public class Test {
 
  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     int c = 25;
     int d = 25;
     System.out.println("a + b = " + (a + b) );
     System.out.println("a - b = " + (a - b) );
     System.out.println("a * b = " + (a * b) );
     System.out.println("b / a = " + (b / a) );
     System.out.println("b % a = " + (b % a) );
     System.out.println("c % a = " + (c % a) );
     System.out.println("a++   = " +  (a++) );
     System.out.println("a--   = " +  (a--) );
     // 查看  d++ 与 ++d 的不同
     System.out.println("d++   = " +  (d++) );
     System.out.println("++d   = " +  (++d) );
  }
}
```

以上实例编译运行结果如下：
```java
a + b = 30
a - b = -10
a * b = 200
b / a = 2
b % a = 0
c % a = 5
a++   = 10
a--   = 11
d++   = 25
++d   = 27
```
### 自增自减运算符

1. 自增（++）自减（--）运算符是一种特殊的算术运算符，在算术运算符中需要两个操作数来进行运算，而自增自减运算符是一个操作数。
```java
public class selfAddMinus{
    public static void main(String[] args){
        int a = 3;//定义一个变量；
        int b = ++a;//自增运算
        int c = 3;
        int d = --c;//自减运算
        System.out.println("进行自增运算后的值等于"+b);
        System.out.println("进行自减运算后的值等于"+d);
    }
}
```
运行结果为：
```java
进行自增运算后的值等于4
进行自减运算后的值等于2
```
解析：

* int b = ++a; 拆分运算过程为: a=a+1=4; b=a=4, 最后结果为b=4,a=4

* int d = --c; 拆分运算过程为: c=c-1=2; d=c=2, 最后结果为d=2,c=2

2. 前缀自增自减法(++a,--a): 先进行自增或者自减运算，再进行表达式运算。

3. 后缀自增自减法(a++,a--): 先进行表达式运算，再进行自增或者自减运算 实例：
```java
public class selfAddMinus{
    public static void main(String[] args){
        int a = 5;//定义一个变量；
        int b = 5;
        int x = 2*++a;
        int y = 2*b++;
        System.out.println("自增运算符前缀运算后a="+a+",x="+x);
        System.out.println("自增运算符后缀运算后b="+b+",y="+y);
    }
}
```
运行结果为：
```java
自增运算符前缀运算后a=6，x=12
自增运算符后缀运算后b=6，y=10
```
### 关系运算符

下表为Java支持的关系运算符

表格中的实例整数变量A的值为10，变量B的值为20：

运算符 |描述 |例子
--|--|--
== |检查如果两个操作数的值是否相等，如果相等则条件为真。 |（A == B）为假。
!= |检查如果两个操作数的值是否相等，如果值不相等则条件为真。|	(A != B) 为真。
\> |检查左操作数的值是否大于右操作数的值，如果是那么条件为真。|（A> B）为假。
< |检查左操作数的值是否小于右操作数的值，如果是那么条件为真。 |（A < B）为真。
\>= |检查左操作数的值是否大于或等于右操作数的值，如果是那么条件为真。|（A> = B）为假。
<= |检查左操作数的值是否小于或等于右操作数的值，如果是那么条件为真。 |（A <= B）为真。
#### 实例

下面的简单示例程序演示了关系运算符。复制并粘贴下面的Java程序并保存为Test.java文件，然后编译并运行这个程序：
Test.java 文件代码：
```java
public class Test {
 
  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     System.out.println("a == b = " + (a == b) );
     System.out.println("a != b = " + (a != b) );
     System.out.println("a > b = " + (a > b) );
     System.out.println("a < b = " + (a < b) );
     System.out.println("b >= a = " + (b >= a) );
     System.out.println("b <= a = " + (b <= a) );
  }
}
```
以上实例编译运行结果如下：
```java
a == b = false
a != b = true
a > b = false
a < b = true
b >= a = true
b <= a = false
```
#### 位运算符

Java定义了位运算符，应用于整数类型(int)，长整型(long)，短整型(short)，字符型(char)，和字节型(byte)等类型。

位运算符作用在所有的位上，并且按位运算。假设a = 60，b = 13;它们的二进制格式表示将如下：
```java
A = 0011 1100
B = 0000 1101
-----------------
A&B = 0000 1100
A | B = 0011 1101
A ^ B = 0011 0001
~A= 1100 0011
```
下表列出了位运算符的基本运算，假设整数变量 A 的值为 60 和变量 B 的值为 13：

操作符 |描述 |例子
--|--|--
＆ |如果相对应位都是1，则结果为1，否则为0 |（A＆B），得到12，即0000 1100
| |如果相对应位都是 0，则结果为 0，否则为 1 	|（A | B）得到61，即 0011 1101
^ |如果相对应位值相同，则结果为0，否则为1 |（A ^ B）得到49，即 0011 0001
〜 |按位取反运算符翻转操作数的每一位，即0变成1，1变成0。|	（〜A）得到-61，即1100 0011
<<  |按位左移运算符。左操作数按位左移右操作数指定的位数。 |A << 2得到240，即 1111 0000
\>>  |按位右移运算符。左操作数按位右移右操作数指定的位数。 |A >> 2得到15即 1111
\>>>  |按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。 |A>>>2得到15即0000 1111
#### 实例

下面的简单示例程序演示了位运算符。复制并粘贴下面的Java程序并保存为Test.java文件，然后编译并运行这个程序：
Test.java 文件代码：
```java
public class Test {
  public static void main(String[] args) {
     int a = 60; /* 60 = 0011 1100 */ 
     int b = 13; /* 13 = 0000 1101 */
     int c = 0;
     c = a & b;       /* 12 = 0000 1100 */
     System.out.println("a & b = " + c );
 
     c = a | b;       /* 61 = 0011 1101 */
     System.out.println("a | b = " + c );
 
     c = a ^ b;       /* 49 = 0011 0001 */
     System.out.println("a ^ b = " + c );
 
     c = ~a;          /*-61 = 1100 0011 */
     System.out.println("~a = " + c );
 
     c = a << 2;     /* 240 = 1111 0000 */
     System.out.println("a << 2 = " + c );
 
     c = a >> 2;     /* 15 = 1111 */
     System.out.println("a >> 2  = " + c );
  
     c = a >>> 2;     /* 15 = 0000 1111 */
     System.out.println("a >>> 2 = " + c );
  }
} 
```
以上实例编译运行结果如下：
```java
a & b = 12
a | b = 61
a ^ b = 49
~a = -61
a << 2 = 240
a >> 2  = 15
a >>> 2 = 15
```
#### 逻辑运算符

下表列出了逻辑运算符的基本运算，假设布尔变量A为真，变量B为假

操作符|	描述 |例子
--|--|--
&& |称为逻辑与运算符。当且仅当两个操作数都为真，条件才为真。 |（A && B）为假。
| | |称为逻辑或操作符。如果任何两个操作数任何一个为真，条件为真。 |（A | | B）为真。
！ |称为逻辑非运算符。用来反转操作数的逻辑状态。如果条件为true，则逻辑非运算符将得到false。 |！（A && B）为真。
#### 实例

下面的简单示例程序演示了逻辑运算符。复制并粘贴下面的Java程序并保存为Test.java文件，然后编译并运行这个程序：
```java
public class Test {
  public static void main(String[] args) {
     boolean a = true;
     boolean b = false;
     System.out.println("a && b = " + (a&&b));
     System.out.println("a || b = " + (a||b) );
     System.out.println("!(a && b) = " + !(a && b));
  }
}
```
以上实例编译运行结果如下：
```java
a && b = false
a || b = true
!(a && b) = true
```
### 短路逻辑运算符

当使用与逻辑运算符时，在两个操作数都为true时，结果才为true，但是当得到第一个操作为false时，其结果就必定是false，这时候就不会再判断第二个操作了。
```java
public class LuoJi{
    public static void main(String[] args){
        int a = 5;//定义一个变量；
        boolean b = (a<4)&&(a++<10);
        System.out.println("使用短路逻辑运算符的结果为"+b);
        System.out.println("a的结果为"+a);
    }
}
```
运行结果为：
```java
使用短路逻辑运算符的结果为false
a的结果为5
```
>解析： 该程序使用到了短路逻辑运算符(&&)，首先判断 a<4 的结果为 false，则 b 的结果必定是 false，所以不再执行第二个操作 a++<10 的判断，所以 a 的值为 5。 

### 赋值运算符

下面是Java语言支持的赋值运算符：

操作符|	描述 |例子
--|--|--
= |简单的赋值运算符，将右操作数的值赋给左侧操作数 |C = A + B将把A + B得到的值赋给C
+ = |加和赋值操作符，它把左操作数和右操作数相加赋值给左操作数 |C + = A等价于C = C + A
- = |减和赋值操作符，它把左操作数和右操作数相减赋值给左操作数 |C - = A等价于C = C - A
* = |乘和赋值操作符，它把左操作数和右操作数相乘赋值给左操作数 |C * = A等价于C = C * A
/ = |除和赋值操作符，它把左操作数和右操作数相除赋值给左操作数 |C / = A，C 与 A 同类型时等价于 C = C / A
（％）= |取模和赋值操作符，它把左操作数和右操作数取模后赋值给左操作数 |C％= A等价于C = C％A
<< = |左移位赋值运算符|	C << = 2等价于C = C << 2
\>> = |右移位赋值运算符 |C >> = 2等价于C = C >> 2
＆= |按位与赋值运算符 |C＆= 2等价于C = C＆2
^ = |按位异或赋值操作符 |C ^ = 2等价于C = C ^ 2
| = |按位或赋值操作符 |C | = 2等价于C = C | 2
#### 实例

下面的简单示例程序演示了赋值运算符。复制并粘贴下面的Java程序并保存为Test.java文件，然后编译并运行这个程序：
Test.java 文件代码：
```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        int c = 0;
        c = a + b;
        System.out.println("c = a + b = " + c );
        c += a ;
        System.out.println("c += a  = " + c );
        c -= a ;
        System.out.println("c -= a = " + c );
        c *= a ;
        System.out.println("c *= a = " + c );
        a = 10;
        c = 15;
        c /= a ;
        System.out.println("c /= a = " + c );
        a = 10;
        c = 15;
        c %= a ;
        System.out.println("c %= a  = " + c );
        c <<= 2 ;
        System.out.println("c <<= 2 = " + c );
        c >>= 2 ;
        System.out.println("c >>= 2 = " + c );
        c >>= 2 ;
        System.out.println("c >>= 2 = " + c );
        c &= a ;
        System.out.println("c &= a  = " + c );
        c ^= a ;
        System.out.println("c ^= a   = " + c );
        c |= a ;
        System.out.println("c |= a   = " + c );
    }
}
```
以上实例编译运行结果如下：
```java
c = a + b = 30
c += a  = 40
c -= a = 30
c *= a = 300
c /= a = 1
c %= a  = 5
c <<= 2 = 20
c >>= 2 = 5
c >>= 2 = 1
c &= a  = 0
c ^= a   = 10
c |= a   = 10
```
### 条件运算符（?:）

条件运算符也被称为三元运算符。该运算符有3个操作数，并且需要判断布尔表达式的值。该运算符的主要是决定哪个值应该赋值给变量。
```java
variable x = (expression) ? value if true : value if false
```
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args){
      int a , b;
      a = 10;
      // 如果 a 等于 1 成立，则设置 b 为 20，否则为 30
      b = (a == 1) ? 20 : 30;
      System.out.println( "Value of b is : " +  b );
 
      // 如果 a 等于 10 成立，则设置 b 为 20，否则为 30
      b = (a == 10) ? 20 : 30;
      System.out.println( "Value of b is : " + b );
   }
}
```
以上实例编译运行结果如下：
```java
Value of b is : 30
Value of b is : 20
```
### instanceof 运算符

该运算符用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）。

instanceof运算符使用格式如下：
```java
( Object reference variable ) instanceof  (class/interface type)
```
如果运算符左侧变量所指的对象，是操作符右侧类或接口(class/interface)的一个对象，那么结果为真。

下面是一个例子：
```java
String name = "James";
boolean result = name instanceof String; // 由于 name 是 String 类型，所以返回真
```
如果被比较的对象兼容于右侧类型，该运算符仍然返回 true。

看下面的例子：
```java
class Vehicle {}
 
public class Car extends Vehicle {
   public static void main(String[] args){
      Vehicle a = new Car();
      boolean result =  a instanceof Car;
      System.out.println( result);
   }
}
```
以上实例编译运行结果如下：
```java
true
```

### Java运算符优先级

当多个运算符出现在一个表达式中，谁先谁后呢？这就涉及到运算符的优先级别的问题。在一个多运算符的表达式中，运算符优先级不同会导致最后得出的结果差别甚大。

例如，（1+3）＋（3+2）*2，这个表达式如果按加号最优先计算，答案就是 18，如果按照乘号最优先，答案则是 14。

再如，x = 7 + 3 * 2;这里x得到13，而不是20，因为乘法运算符比加法运算符有较高的优先级，所以先计算3 * 2得到6，然后再加7。

下表中具有最高优先级的运算符在的表的最上面，最低优先级的在表的底部。

类别 |操作符 |关联性
--|--|--
后缀 |() [] . (点操作符) |左到右
一元 |expr++ expr-- |从左到右
一元 |++expr --expr + - ～ ！|从右到左
乘性  |* /％ |左到右
加性  |+ - |左到右
移位  |>> >>>  <<  |左到右
关系  |> >= < <=  |左到右
相等  |==  != |左到右
按位与 |＆ |左到右
按位异或 |^ |左到右
按位或 |\| |左到右
逻辑与 |&& |左到右
逻辑或 |\| \| |左到右
条件 |？： |从右到左
赋值 |= + = - = * = / =％= >> = << =＆= ^ = \| =|	从右到左
逗号 |， |左到右

## Java 循环结构 - for, while 及 do...while

顺序结构的程序语句只能被执行一次。

如果您想要同样的操作执行多次，就需要使用循环结构。

Java中有三种主要的循环结构：

* while 循环
* do…while 循环
* for 循环

在 Java5 中引入了一种主要用于数组的增强型 for 循环。
### while 循环

while是最基本的循环，它的结构为：
```java
while( 布尔表达式 ) {
  //循环内容
}
```
只要布尔表达式为 true，循环就会一直执行下去。
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args) {
      int x = 10;
      while( x < 20 ) {
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }
   }
}
```
以上实例编译运行结果如下：
```java
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```
### do…while 循环

对于 while 语句而言，如果不满足条件，则不能进入循环。但有时候我们需要即使不满足条件，也至少执行一次。

do…while 循环和 while 循环相似，不同的是，do…while 循环至少会执行一次。
```java
do {
       //代码语句
}while(布尔表达式);
```
注意：布尔表达式在循环体的后面，所以语句块在检测布尔表达式之前已经执行了。 如果布尔表达式的值为 true，则语句块一直执行，直到布尔表达式的值为 false。
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args){
      int x = 10;
 
      do{
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }while( x < 20 );
   }
}
```
以上实例编译运行结果如下：
```java
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```
### for循环

虽然所有循环结构都可以用 while 或者 do...while表示，但 Java 提供了另一种语句 —— for 循环，使一些循环结构变得更加简单。

for循环执行的次数是在执行前就确定的。语法格式如下：
```java
for(初始化; 布尔表达式; 更新) {
    //代码语句
}
```
关于 for 循环有以下几点说明：

* 最先执行初始化步骤。可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句。
* 然后，检测布尔表达式的值。如果为 true，循环体被执行。如果为false，循环终止，开始执行循环体后面的语句。
* 执行一次循环后，更新循环控制变量。
* 再次检测布尔表达式。循环执行上面的过程。

#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args) {
 
      for(int x = 10; x < 20; x = x+1) {
         System.out.print("value of x : " + x );
         System.out.print("\n");
      }
   }
}
```
以上实例编译运行结果如下：
```java
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```
### Java 增强 for 循环

Java5 引入了一种主要用于数组的增强型 for 循环。

Java 增强 for 循环语法格式如下:
```java
for(声明语句 : 表达式)
{
   //代码句子
}
```
声明语句：声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。

表达式：表达式是要访问的数组名，或者是返回值为数组的方法。
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args){
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ){
         System.out.print( x );
         System.out.print(",");
      }
      System.out.print("\n");
      String [] names ={"James", "Larry", "Tom", "Lacy"};
      for( String name : names ) {
         System.out.print( name );
         System.out.print(",");
      }
   }
}
``
以上实例编译运行结果如下：
```java
10,20,30,40,50,
James,Larry,Tom,Lacy,
```
### break 关键字

break 主要用在循环语句或者 switch 语句中，用来跳出整个语句块。

break 跳出最里层的循环，并且继续执行该循环下面的语句。
#### 语法

break 的用法很简单，就是循环结构中的一条语句：
```java
break;
```
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args) {
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ) {
         // x 等于 30 时跳出循环
         if( x == 30 ) {
            break;
         }
         System.out.print( x );
         System.out.print("\n");
      }
   }
}
``
以上实例编译运行结果如下：
```java
10
20
```
### continue 关键字

continue 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。

在 for 循环中，continue 语句使程序立即跳转到更新语句。

在 while 或者 do…while 循环中，程序立即跳转到布尔表达式的判断语句。
#### 语法

continue 就是循环体中一条简单的语句：
```java
continue;
```
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String[] args) {
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ) {
         if( x == 30 ) {
        continue;
         }
         System.out.print( x );
         System.out.print("\n");
      }
   }
}
```
以上实例编译运行结果如下：
```java
10
20
40
50
```
## Java 条件语句 - if...else
Java 中的条件语句允许程序根据条件的不同执行不同的代码块。

一个 if 语句包含一个布尔表达式和一条或多条语句。
### 语法

if 语句的语法如下：
```java
if(布尔表达式)
{
   //如果布尔表达式为true将执行的语句
}
```
如果布尔表达式的值为 true，则执行 if 语句中的代码块，否则执行 else 语句块后面的代码。

Test.java 文件代码：
```java
public class Test {
 
   public static void main(String args[]){
      int x = 10;
 
      if( x < 20 ){
         System.out.print("这是 if 语句");
      }
   }
}
```
以上代码编译运行结果如下：
```java
这是 if 语句
```
### if...else语句

if 语句后面可以跟 else 语句，当 if 语句的布尔表达式值为 false 时，else 语句块会被执行。
#### 语法

if…else 的用法如下：
```java
if(布尔表达式){
   //如果布尔表达式的值为true
}else{
   //如果布尔表达式的值为false
}
```
#### 实例
Test.java 文件代码：
```java
public class Test {
 
   public static void main(String args[]){
      int x = 30;
 
      if( x < 20 ){
         System.out.print("这是 if 语句");
      }else{
         System.out.print("这是 else 语句");
      }
   }
}
```
以上代码编译运行结果如下：
```java
这是 else 语句
```
### if...else if...else 语句

if 语句后面可以跟 else if…else 语句，这种语句可以检测到多种可能的情况。

使用 if，else if，else 语句的时候，需要注意下面几点：

* if 语句至多有 1 个 else 语句，else 语句在所有的 else if 语句之后。
* if 语句可以有若干个 else if 语句，它们必须在 else 语句之前。
* 一旦其中一个 else if 语句检测为 true，其他的 else if 以及 else 语句都将跳过执行。

#### 语法

if...else 语法格式如下:
```java
if(布尔表达式 1){
   //如果布尔表达式 1的值为true执行代码
}else if(布尔表达式 2){
   //如果布尔表达式 2的值为true执行代码
}else if(布尔表达式 3){
   //如果布尔表达式 3的值为true执行代码
}else {
   //如果以上布尔表达式都不为true执行代码
}
```
#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String args[]){
      int x = 30;
 
      if( x == 10 ){
         System.out.print("Value of X is 10");
      }else if( x == 20 ){
         System.out.print("Value of X is 20");
      }else if( x == 30 ){
         System.out.print("Value of X is 30");
      }else{
         System.out.print("这是 else 语句");
      }
   }
}
```
以上代码编译运行结果如下：
```java
Value of X is 30
```
### 嵌套的 if…else 语句

使用嵌套的 if…else 语句是合法的。也就是说你可以在另一个 if 或者 else if 语句中使用 if 或者 else if 语句。
#### 语法

嵌套的 if…else 语法格式如下：
```java
if(布尔表达式 1){
   ////如果布尔表达式 1的值为true执行代码
   if(布尔表达式 2){
      ////如果布尔表达式 2的值为true执行代码
   }
}
```
你可以像 if 语句一样嵌套 else if...else。
#### 实例
Test.java 文件代码：
```java
public class Test {
 
   public static void main(String args[]){
      int x = 30;
      int y = 10;
 
      if( x == 30 ){
         if( y == 10 ){
             System.out.print("X = 30 and Y = 10");
          }
       }
    }
}
```
以上代码编译运行结果如下：
```java
X = 30 and Y = 10
```
## Java switch case 语句

switch case 语句判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。
### 语法

switch case 语句语法格式如下：
```java
switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}
```
![](https://www.runoob.com/wp-content/uploads/2018/09/java-switch-case-flow-diagram.jpeg)

switch case 语句有如下规则：

* switch 语句中的变量类型可以是： byte、short、int 或者 char。从 Java SE 7 开始，switch 支持字符串 String 类型了，同时 case 标签必须为字符串常量或字面量。

* switch 语句可以拥有多个 case 语句。每个 case 后面跟一个要比较的值和冒号。

* case 语句中的值的数据类型必须与变量的数据类型相同，而且只能是常量或者字面常量。

* 当变量的值与 case 语句的值相等时，那么 case 语句之后的语句开始执行，直到 break 语句出现才会跳出 switch 语句。

* 当遇到 break 语句时，switch 语句终止。程序跳转到 switch 语句后面的语句执行。case 语句不必须要包含 break 语句。如果没有 break 语句出现，程序会继续执行下一条 case 语句，直到出现 break 语句。

* switch 语句可以包含一个 default 分支，该分支一般是 switch 语句的最后一个分支（可以在任何位置，但建议在最后一个）。default 在没有 case 语句的值和变量值相等的时候执行。default 分支不需要 break 语句。

**switch case 执行时，一定会先进行匹配，匹配成功返回当前 case 的值，再根据是否有 break，判断是否继续输出，或是跳出判断。**

#### 实例
Test.java 文件代码：
```java
public class Test {
   public static void main(String args[]){
      //char grade = args[0].charAt(0);
      char grade = 'C';
 
      switch(grade)
      {
         case 'A' :
            System.out.println("优秀"); 
            break;
         case 'B' :
         case 'C' :
            System.out.println("良好");
            break;
         case 'D' :
            System.out.println("及格");
            break;
         case 'F' :
            System.out.println("你需要再努力努力");
            break;
         default :
            System.out.println("未知等级");
      }
      System.out.println("你的等级是 " + grade);
   }
}
```
以上代码编译运行结果如下：
```java
良好
你的等级是 C
```
如果 case 语句块中没有 break 语句时，JVM 并不会顺序输出每一个 case 对应的返回值，而是继续匹配，匹配不成功则返回默认 case。

Test.java 文件代码：
```java
public class Test {
   public static void main(String args[]){
      int i = 5;
      switch(i){
         case 0:
            System.out.println("0");
         case 1:
            System.out.println("1");
         case 2:
            System.out.println("2");
         default:
            System.out.println("default");
      }
   }
}
```
以上代码编译运行结果如下：
```java
default
```
如果 case 语句块中没有 break 语句时，匹配成功后，从当前 case 开始，后续所有 case 的值都会输出。
Test.java 文件代码：
```java
public class Test {
   public static void main(String args[]){
      int i = 1;
      switch(i){
         case 0:
            System.out.println("0");
         case 1:
            System.out.println("1");
         case 2:
            System.out.println("2");
         default:
            System.out.println("default");
      }
   }
}
```
以上代码编译运行结果如下：
```java
1
2
default
```
如果当前匹配成功的 case 语句块没有 break 语句，则从当前 case 开始，后续所有 case 的值都会输出，如果后续的 case 语句块有 break 语句则会跳出判断。
Test.java 文件代码：
```java
public class Test {
   public static void main(String args[]){
      int i = 1;
      switch(i){
         case 0:
            System.out.println("0");
         case 1:
            System.out.println("1");
         case 2:
            System.out.println("2");
         case 3:
            System.out.println("3"); break;
         default:
            System.out.println("default");
      }
   }
}
```
以上代码编译运行结果如下：
```java
1
2
3
```
## Java Number & Math 类
### Java Number

一般地，当需要使用数字的时候，我们通常使用内置数据类型，如：byte、int、long、double 等。
#### 实例
```java
int a = 5000;
float b = 13.65f;
byte c = 0x4a;
```
然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情形。为了解决这个问题，Java 语言为每一个内置数据类型提供了对应的包装类。

所有的包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类 Number 的子类。

类名|对应基本类型|描述
--|--|--
Byte|byte|字节型包装类
Short|short|短整型包装类
Integer|int|整型包装类
Long|long|长整型包装类
Float|float|单精度浮点型包装类
Double|double|双精度浮点型包装类
BigInteger|-|不可变任意精度整数
BigDecimal|-|不可变任意精度有符号十进制数

![](https://www.runoob.com/wp-content/uploads/2013/12/OOP_WrapperClass.png)

这种由编译器特别支持的包装称为装箱，所以当内置数据类型被当作对象使用的时候，编译器会把内置类型装箱为包装类。相似的，编译器也可以把一个对象拆箱为内置类型。

Number 类属于 java.lang 包。

Number 是一个抽象类，主要作用是为各种数值类型提供统一的转换方法：

```java
public abstract class Number implements Serializable {
    // 抽象方法
    public abstract int intValue();
    public abstract long longValue();
    public abstract float floatValue();
    public abstract double doubleValue();
    
    // Java 8 新增
    public byte byteValue() {
        return (byte)intValue();
    }
    public short shortValue() {
        return (short)intValue();
    }
}
```
下面是一个使用 Integer 对象的实例：
```java
public class Test{
 
   public static void main(String[] args){
      Integer x = 5;
      x =  x + 10;
      System.out.println(x); 
   }
}
```

以上实例编译运行结果如下：
```java
15
```
当 x 被赋为整型值时，由于x是一个对象，所以编译器要对x进行装箱。然后，为了使x能进行加运算，所以要对x进行拆箱。

#### 常用方法示例
##### 基本类型转换
##### 实例
```java
Number num = 1234.56; // 实际是Double类型

System.out.println(num.intValue());    // 1234 (截断小数)
System.out.println(num.longValue());   // 1234
System.out.println(num.floatValue());  // 1234.56
System.out.println(num.doubleValue()); // 1234.56
```
#### 数值比较
##### 实例
```java
Integer x = 10;
Double y = 10.0;

// 正确比较方式：转换为同一类型后比较
System.out.println(x.doubleValue() == y.doubleValue()); // true
```
#### 特殊数值处理
##### 处理大数
##### 实例
```java
BigInteger bigInt = new BigInteger("12345678901234567890");
BigDecimal bigDec = new BigDecimal("1234567890.1234567890");

// 大数运算
BigInteger sum = bigInt.add(new BigInteger("1"));
BigDecimal product = bigDec.multiply(new BigDecimal("2"));
```
#### 数值格式化
##### 实例
```java
NumberFormat nf = NumberFormat.getInstance();
nf.setMaximumFractionDigits(2);

System.out.println(nf.format(1234.5678)); // "1,234.57"
```
#### 自动装箱与拆箱

Java 5+ 支持自动转换：
##### 实例
```java
// 自动装箱
Integer autoBoxed = 42; // 编译器转换为 Integer.valueOf(42)

// 自动拆箱
int autoUnboxed = autoBoxed; // 编译器转换为 autoBoxed.intValue()
```
### Java Math 类

Math 类是 Java 提供的数学工具类，位于 java.lang 包中，包含执行基本数值运算的静态方法。

Java 的 Math 包含了用于执行基本数学运算的属性和方法，如初等指数、对数、平方根和三角函数。

Math 的方法都被定义为 static 形式，通过 Math 类可以在主函数中直接调用。

Test.java 文件代码：
```java
public class Test {  
    public static void main (String []args)  
    {  
        System.out.println("90 度的正弦值：" + Math.sin(Math.PI/2));  
        System.out.println("0度的余弦值：" + Math.cos(0));  
        System.out.println("60度的正切值：" + Math.tan(Math.PI/3));  
        System.out.println("1的反正切值： " + Math.atan(1));  
        System.out.println("π/2的角度值：" + Math.toDegrees(Math.PI/2));  
        System.out.println(Math.PI);  
    }  
}
```
以上实例编译运行结果如下：
```java
90 度的正弦值：1.0
0度的余弦值：1.0
60度的正切值：1.7320508075688767
1的反正切值： 0.7853981633974483
π/2的角度值：90.0
3.141592653589793
```
#### 高级数学运算
1. 指数对数运算

实例
```java
Math.exp(1);    // e^1 ≈ 2.718
Math.log(Math.E); // ln(e) = 1
Math.log10(100); // log10(100) = 2
```
2. 随机数生成

实例
```java
// 生成[0.0, 1.0)之间的随机数
double random = Math.random();

// 生成[1, 100]的随机整数
int randomInt = (int)(Math.random() * 100) + 1;
```
3. 其他运算

实例
```java
Math.hypot(3, 4); // 计算sqrt(x²+y²) → 5.0
Math.IEEEremainder(10, 3); // IEEE余数 → 1.0
```
4. 常量字段

实例
```java
Math.PI;    // π ≈ 3.141592653589793
Math.E;     // 自然对数底数e ≈ 2.718281828459045
```
Number & Math 类方法

下面的表中列出的是 Number & Math 类常用的一些方法：
序号 |方法|描述
--|--|--
1 |xxxValue()|将 Number 对象转换为xxx数据类型的值并返回。
2 |compareTo()|将number对象与参数比较。
3 |equals()|判断number对象是否与参数相等。
4 |valueOf()|返回一个 Number 对象指定的内置数据类型
5 |toString()|以字符串形式返回值。
6 |parseInt()|将字符串解析为int类型。
7 |abs()|返回参数的绝对值。
8 |ceil()|返回大于等于( >= )给定参数的的最小整数，类型为双精度浮点型。
9 |floor()|返回小于等于（<=）给定参数的最大整数 。
10 |rint()|返回与参数最接近的整数。返回类型为double。
11 |round()|它表示四舍五入，算法为 Math.floor(x+0.5)，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11。
12 |min()|返回两个参数中的最小值。
13 |max()|返回两个参数中的最大值。
14 |exp()|返回自然数底数e的参数次方。
15 |log()|返回参数的自然数底数的对数值。
16 |pow()|返回第一个参数的第二个参数次方。
17 |sqrt()|求参数的算术平方根。
18 |sin()|求指定double类型参数的正弦值。
19 |cos()|求指定double类型参数的余弦值。
20 |tan()|求指定double类型参数的正切值。
21 |asin()|求指定double类型参数的反正弦值。
22 |acos()|求指定double类型参数的反余弦值。
23 |atan()|求指定double类型参数的反正切值。
24 |atan2()|将笛卡尔坐标转换为极坐标，并返回极坐标的角度值。
25 |toDegrees()|将参数转化为角度。
26 |toRadians()|将角度转换为弧度。
27 |random()|返回一个随机数。


floor,round 和 ceil 实例：
```java
public class Main {   
  public static void main(String[] args) {   
    double[] nums = { 1.4, 1.5, 1.6, -1.4, -1.5, -1.6 };   
    for (double num : nums) {   
      test(num);   
    }   
  }   
  
  private static void test(double num) {   
    System.out.println("Math.floor(" + num + ")=" + Math.floor(num));   
    System.out.println("Math.round(" + num + ")=" + Math.round(num));   
    System.out.println("Math.ceil(" + num + ")=" + Math.ceil(num));   
  }   
}
```
以上实例执行输出结果为：
```java
Math.floor(1.4)=1.0
Math.round(1.4)=1
Math.ceil(1.4)=2.0
Math.floor(1.5)=1.0
Math.round(1.5)=2
Math.ceil(1.5)=2.0
Math.floor(1.6)=1.0
Math.round(1.6)=2
Math.ceil(1.6)=2.0
Math.floor(-1.4)=-2.0
Math.round(-1.4)=-1
Math.ceil(-1.4)=-1.0
Math.floor(-1.5)=-2.0
Math.round(-1.5)=-1
Math.ceil(-1.5)=-1.0
Math.floor(-1.6)=-2.0
Math.round(-1.6)=-2
Math.ceil(-1.6)=-1.0
```

## Java Character 类

Character 类用于对单个字符进行操作。

Character 类在对象中包装一个基本类型 char 的值
### 实例
```java
char ch = 'a';
 
// Unicode 字符表示形式
char uniChar = '\u039A'; 
 
// 字符数组
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' };
```
然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情况。为了解决这个问题，Java语言为内置数据类型char提供了包装Character类。

Character类提供了一系列方法来操纵字符。你可以使用Character的构造方法创建一个Character类对象，例如：
```java
Character ch = new Character('a');
```
在某些情况下，Java编译器会自动创建一个Character对象。

例如，将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱。
### 实例
```java
// 原始字符 'a' 装箱到 Character 对象 ch 中
Character ch = 'a';
 
// 原始字符 'x' 用 test 方法装箱
// 返回拆箱的值到 'c'
char c = test('x');
```
### 转义序列

前面有反斜杠（\）的字符代表转义字符，它对编译器来说是有特殊含义的。

下面列表展示了Java的转义序列：
转义序列 |描述
--|--
\t |在文中该处插入一个tab键
\b|在文中该处插入一个后退键
\n |在文中该处换行
\r |在文中该处插入回车
\f |在文中该处插入换页符
\' |在文中该处插入单引号
\" |在文中该处插入双引号
\\ |在文中该处插入反斜杠
#### 实例

当打印语句遇到一个转义序列时，编译器可以正确地对其进行解释。

以下实例转义双引号并输出：
Test.java 文件代码：
```java
public class Test {
 
   public static void main(String[] args) {
      System.out.println("访问\"菜鸟教程!\"");
   }
}
```
以上实例编译运行结果如下：
```java
访问"菜鸟教程!"
```
### Character 方法

下面是Character类的方法：
序号 |方法与描述
--|--
1 |isLetter()是否是一个字母
2 |isDigit()是否是一个数字字符
3 |isWhitespace()是否是一个空白字符
4 |isUpperCase()是否是大写字母
5 |isLowerCase()是否是小写字母
6 |toUpperCase()指定字母的大写形式
7 |toLowerCase()指定字母的小写形式
8 |toString()返回字符的字符串形式，字符串的长度仅为1

对于方法的完整列表，请参考的 java.lang.Character API 规范。

## Java String 类

字符串广泛应用 在 Java 编程中，在 Java 中字符串属于对象，Java 提供了 String 类来创建和操作字符串。
创建字符串

创建字符串最简单的方式如下:
```java
String str = "Runoob";
```
在代码中遇到字符串常量时，这里的值是 "Runoob"，编译器会使用该值创建一个 String 对象。

和其它对象一样，可以使用关键字和构造方法来创建 String 对象。

用构造函数创建字符串：
```java
String str2=new String("Runoob");
```
String 创建的字符串存储在公共池中，而 new 创建的字符串对象在堆上：
```java
String s1 = "Runoob";              // String 直接创建
String s2 = "Runoob";              // String 直接创建
String s3 = s1;                    // 相同引用
String s4 = new String("Runoob");   // String 对象创建
String s5 = new String("Runoob");   // String 对象创建
```

![](https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png)

String 类有 11 种构造方法，这些方法提供不同的参数来初始化字符串，比如提供一个字符数组参数:
StringDemo.java 文件代码：
```java
public class StringDemo{
   public static void main(String args[]){
      char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
      String helloString = new String(helloArray);  
      System.out.println( helloString );
   }
}
```
以上实例编译运行结果如下：
```java
runoob
```
注意:String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了（详看笔记部分解析）。

如果需要对字符串做很多修改，那么应该选择使用 [StringBuffer & StringBuilder 类](#StringBuffer-&-StringBuilder-类)。


### 字符串长度

用于获取有关对象的信息的方法称为访问器方法。

String 类的一个访问器方法是 length() 方法，它返回字符串对象包含的字符数。

下面的代码执行后，len 变量等于 14:
StringDemo.java 文件代码：
```java
public class StringDemo {
    public static void main(String args[]) {
        String site = "www.runoob.com";
        int len = site.length();
        System.out.println( "菜鸟教程网址长度 : " + len );
   }
}
```
以上实例编译运行结果如下：
```java
菜鸟教程网址长度 : 14
```
### 连接字符串

String 类提供了连接两个字符串的方法：
string1.concat(string2);

返回 string2 连接 string1 的新字符串。也可以对字符串常量使用 concat() 方法，如：
```java
"我的名字是 ".concat("Runoob");
```
更常用的是使用'+'操作符来连接字符串，如：
```java
"Hello," + " runoob" + "!"
```
结果如下:
```java
"Hello, runoob!"
```
下面是一个例子:

StringDemo.java 文件代码：
```java
public class StringDemo {
    public static void main(String args[]) {     
        String string1 = "菜鸟教程网址：";     
        System.out.println("1、" + string1 + "www.runoob.com");  
    }
}
```
以上实例编译运行结果如下：
```java
1、菜鸟教程网址：www.runoob.com
```
### 创建格式化字符串

我们知道输出格式化数字可以使用 printf() 和 format() 方法。

String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

如下所示：
```java
System.out.printf("浮点型变量的值为 " +
                  "%f, 整型变量的值为 " +
                  " %d, 字符串变量的值为 " +
                  "is %s", floatVar, intVar, stringVar);
```
你也可以这样写
```java
String fs;
fs = String.format("浮点型变量的值为 " +
                   "%f, 整型变量的值为 " +
                   " %d, 字符串变量的值为 " +
                   " %s", floatVar, intVar, stringVar);
```
### String 方法
下面是 String 类支持的方法，更多详细，参看 Java String API 文档:
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


<a id="StringBuffer-&-StringBuilder-类"></a>

## Java StringBuffer和StringBuilder 类
当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。 
![](https://www.runoob.com/wp-content/uploads/2013/12/java-string-20201208.png)

在使用 StringBuffer 类时，每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象，所以如果需要对字符串进行修改推荐使用 StringBuffer。

StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。

```java
public class RunoobTest{
    public static void main(String[] args){
        StringBuilder sb = new StringBuilder(10);
        sb.append("Runoob..");
        System.out.println(sb);  
        sb.append("!");
        System.out.println(sb); 
        sb.insert(8, "Java");
        System.out.println(sb); 
        sb.delete(5,8);
        System.out.println(sb);  
    }
}
```
![](https://www.runoob.com/wp-content/uploads/2013/12/2021-03-01-java-stringbuffer.svg)

以上实例编译运行结果如下：
```java
Runoob..
Runoob..!
Runoob..Java!
RunooJava!
```
然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。
Test.java 文件代码：
```java
public class Test{
  public static void main(String[] args){
    StringBuffer sBuffer = new StringBuffer("菜鸟教程官网：");
    sBuffer.append("www");
    sBuffer.append(".runoob");
    sBuffer.append(".com");
    System.out.println(sBuffer);  
  }
}
```
以上实例编译运行结果如下：
```java
菜鸟教程官网：www.runoob.com
```
## StringBuffer 方法

以下是 StringBuffer 类支持的主要方法：
序号 |方法描述
--|--
1 |public StringBuffer append(String s)将指定的字符串追加到此字符序列。
2 |public StringBuffer reverse()将此字符序列用其反转形式取代。
3 |public delete(int start, int end)移除此序列的子字符串中的字符。
4 |public insert(int offset, int i)将 int 参数的字符串表示形式插入此序列中。
5 |insert(int offset, String str)将 str 参数的字符串插入此序列中。
6 |replace(int start, int end, String str)使用给定 String 中的字符替换此序列的子字符串中的字符。

以下列表列出了 StringBuffer 类的其他常用方法：

序号|	方法描述
--|--
1 |int capacity()返回当前容量。
2 |char charAt(int index)返回此序列中指定索引处的 char 值。
3 |void ensureCapacity(int minimumCapacity)确保容量至少等于指定的最小值。
4 |void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)将字符从此序列复制到目标字符数组 dst。
5 |int indexOf(String str)返回第一次出现的指定子字符串在该字符串中的索引。
6 |int indexOf(String str, int fromIndex)从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。
7 |int lastIndexOf(String str)返回最右边出现的指定子字符串在此字符串中的索引。
8 |int lastIndexOf(String str, int fromIndex)返回 String 对象中子字符串最后出现的位置。
9 |int length()返回长度（字符数）。
10 |void setCharAt(int index, char ch)将给定索引处的字符设置为 ch。
11 |void setLength(int newLength)设置字符序列的长度。
12 |CharSequence subSequence(int start, int end)返回一个新的字符序列，该字符序列是此序列的子序列。
13 |String substring(int start)返回一个新的 String，它包含此字符序列当前所包含的字符子序列。
14 |String substring(int start, int end)返回一个新的 String，它包含此序列当前所包含的字符子序列。
15 |String toString()返回此序列中数据的字符串表示形式。

## Java 数组

数组对于每一门编程语言来说都是重要的数据结构之一，当然不同语言对数组的实现及处理也不尽相同。

Java 语言中提供的数组是用来存储固定大小的同类型元素。

你可以声明一个数组变量，如 numbers[100] 来代替直接声明 100 个独立变量 number0，number1，....，number99。

本教程将为大家介绍 Java 数组的声明、创建和初始化，并给出其对应的代码。
***
### 声明数组变量

首先必须声明数组变量，才能在程序中使用数组。下面是声明数组变量的语法：
```java
dataType[] arrayRefVar;   // 首选的方法
 
或
 
dataType arrayRefVar[];  // 效果相同，但不是首选方法
```
注意: 建议使用 dataType[] arrayRefVar 的声明风格声明数组变量。 dataType arrayRefVar[] 风格是来自 C/C++ 语言 ，在Java中采用是为了让 C/C++ 程序员能够快速理解java语言。
### 实例

下面是这两种语法的代码示例：
```java
double[] myList;         // 首选的方法
 
或
 
double myList[];         //  效果相同，但不是首选方法
```
### 创建数组

Java语言使用new操作符来创建数组，语法如下：
```java
arrayRefVar = new dataType[arraySize];
```
上面的语法语句做了两件事：

*  一、使用 dataType[arraySize] 创建了一个数组。
*  二、把新创建的数组的引用赋值给变量 arrayRefVar。

数组变量的声明，和创建数组可以用一条语句完成，如下所示：
```java
dataType[] arrayRefVar = new dataType[arraySize];
```
另外，你还可以使用如下的方式创建数组。
```java
dataType[] arrayRefVar = {value0, value1, ..., valuek};
```
数组的元素是通过索引访问的。数组索引从 0 开始，所以索引值从 0 到 arrayRefVar.length-1。
### 实例

下面的语句首先声明了一个数组变量 myList，接着创建了一个包含 10 个 double 类型元素的数组，并且把它的引用赋值给 myList 变量。

TestArray.java 文件代码：
```java
public class TestArray {
   public static void main(String[] args) {
      // 数组大小
      int size = 10;
      // 定义数组
      double[] myList = new double[size];
      myList[0] = 5.6;
      myList[1] = 4.5;
      myList[2] = 3.3;
      myList[3] = 13.2;
      myList[4] = 4.0;
      myList[5] = 34.33;
      myList[6] = 34.0;
      myList[7] = 45.45;
      myList[8] = 99.993;
      myList[9] = 11123;
      // 计算所有元素的总和
      double total = 0;
      for (int i = 0; i < size; i++) {
         total += myList[i];
      }
      System.out.println("总和为： " + total);
   }
}
```
以上实例输出结果为：
```java
总和为： 11367.373
```
下面的图片描绘了数组 myList。这里 myList 数组里有 10 个 double 元素，它的下标从 0 到 9。

![](https://www.runoob.com/wp-content/uploads/2013/12/12-130Q0221Q5602.jpg)

### 处理数组

数组的元素类型和数组的大小都是确定的，所以当处理数组元素时候，我们通常使用基本循环或者 For-Each 循环。
#### 示例

该实例完整地展示了如何创建、初始化和操纵数组：
TestArray.java 文件代码：
```java
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
 
      // 打印所有数组元素
      for (int i = 0; i < myList.length; i++) {
         System.out.println(myList[i] + " ");
      }
      // 计算所有元素的总和
      double total = 0;
      for (int i = 0; i < myList.length; i++) {
         total += myList[i];
      }
      System.out.println("Total is " + total);
      // 查找最大元素
      double max = myList[0];
      for (int i = 1; i < myList.length; i++) {
         if (myList[i] > max) max = myList[i];
      }
      System.out.println("Max is " + max);
   }
}
```
以上实例编译运行结果如下：
```java
1.9
2.9
3.4
3.5
Total is 11.7
Max is 3.5
```
### For-Each 循环

JDK 1.5 引进了一种新的循环类型，被称为 For-Each 循环或者加强型循环，它能在不使用下标的情况下遍历数组。

语法格式如下：
```java
for(type element: array)
{
    System.out.println(element);
}
```
实例
```java
该实例用来显示数组 myList 中的所有元素：
TestArray.java 文件代码：
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
 
      // 打印所有数组元素
      for (double element: myList) {
         System.out.println(element);
      }
   }
}
```
以上实例编译运行结果如下：
```java
1.9
2.9
3.4
3.5
```
### 数组作为函数的参数

数组可以作为参数传递给方法。

例如，下面的例子就是一个打印 int 数组中元素的方法:
```java
public static void printArray(int[] array) {
  for (int i = 0; i < array.length; i++) {
    System.out.print(array[i] + " ");
  }
}
```
下面例子调用 printArray 方法打印出 3，1，2，6，4 和 2：
printArray(new int[]{3, 1, 2, 6, 4, 2});
### 数组作为函数的返回值
```java
public static int[] reverse(int[] list) {
  int[] result = new int[list.length];
 
  for (int i = 0, j = result.length - 1; i < list.length; i++, j--) {
    result[j] = list[i];
  }
  return result;
}
```
以上实例中 result 数组作为函数的返回值。
### 多维数组

多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素都是一个一维数组，例如：
```java
String[][] str = new String[3][4];
```
#### 多维数组的动态初始化（以二维数组为例）

1. 直接为每一维分配空间，格式如下：
```java
type[][] typeName = new type[typeLength1][typeLength2];
```
type 可以为基本数据类型和复合数据类型，typeLength1 和 typeLength2 必须为正整数，typeLength1 为行数，typeLength2 为列数。

例如：
```java
int[][] a = new int[2][3];
```
解析：
```java
二维数组 a 可以看成一个两行三列的数组。
```
2. 从最高维开始，分别为每一维分配空间，例如：
String[][] s = new String[2][];
s[0] = new String[2];
s[1] = new String[3];
s[0][0] = new String("Good");
s[0][1] = new String("Luck");
s[1][0] = new String("to");
s[1][1] = new String("you");
s[1][2] = new String("!");

解析：

s[0]=new String[2] 和 s[1]=new String[3] 是为最高维分配引用空间，也就是为最高维限制其能保存数据的最长的长度，然后再为其每个数组元素单独分配空间 s0=new String("Good") 等操作。
多维数组的引用（以二维数组为例）

对二维数组中的每个元素，引用方式为 arrayName[index1][index2]，例如：
```java
num[1][0];
```
### Arrays 类

java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。

具有以下功能：

* 给数组赋值：通过 fill 方法。
* 对数组排序：通过 sort 方法,按升序。
* 比较数组：通过 equals 方法比较数组中元素值是否相等。
* 查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

具体说明请查看下表：
序号 |方法和说明
--|--
1|public static int binarySearch(Object[] a, Object key)用二分查找算法在给定数组中搜索给定值的对象(Byte,Int,double等)。数组在调用前必须排序好的。如果查找值包含在数组中，则返回搜索键的索引；否则返回 (-(插入点) - 1)。
2 |public static boolean equals(long[] a, long[] a2)如果两个指定的 long 型数组彼此相等，则返回 true。如果两个数组包含相同数量的元素，并且两个数组中的所有相应元素对都是相等的，则认为这两个数组是相等的。换句话说，如果两个数组以相同顺序包含相同的元素，则两个数组是相等的。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。
3 |public static void fill(int[] a, int val)将指定的 int 值分配给指定 int 型数组指定范围中的每个元素。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。
4|public static void sort(Object[] a)对指定对象数组根据其元素的自然顺序进行升序排列。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。

<a id="Java-protected-关键字详解"></a>

## Java protected 关键字详解



