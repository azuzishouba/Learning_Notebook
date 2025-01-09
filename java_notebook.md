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
           * 在“系统变量”区域点击“新建”，输入以下内容：
               变量名：JAVA_HOME
               变量值：JDK 安装路径（例如 C:\Program Files\Java\jdk-17）。
       2. 配置 PATH 变量
           在“系统变量”区域找到 Path 变量，点击编辑。
           添加 JDK 的 bin 目录路径，例如 C:\Program Files\Java\jdk-17\bin。

3. 验证安装
在命令提示符中输入：
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
1. 变量类型
   1. 基本数据类型
   2. 引用数据类型