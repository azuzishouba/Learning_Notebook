# java_selenium_maven笔记
## Windows上Maven的安装
1. 下载 Maven：
   * 访问 Maven 官方网站。
   * 在 "Files" 部分，下载 Binary zip archive（例如，apache-maven-3.x.x-bin.zip）。

2. 解压文件：
    * 下载完成后，解压 .zip 文件到你选择的目录，例如 C:\Program Files\Apache\maven。

3. 配置环境变量：
   * 打开 系统属性 > 高级系统设置 > 环境变量。
   * 在系统变量中，点击 Path 变量，然后点击 编辑，添加 Maven 的 bin 目录路径（例如 C:\Program Files\Apache\maven\apache-maven-3.x.x\bin）。

4. 设置 MAVEN_HOME 环境变量：
   * 在系统变量中，点击 新建，设置变量名为 MAVEN_HOME，变量值为 Maven 的安装路径（例如 C:\Program Files\Apache\maven\apache-maven-3.x.x）。

5. 验证安装：
   * 打开 命令提示符（Command Prompt），输入以下命令来验证是否安装成功：
```shell
mvn -version
```
如果一切正常，你应该看到 Maven 的版本信息。
## 创建maven-selenium项目
1. 创建maven项目 
![创建maven项目](/screen_shot/maven_project.png)
* groupId=com.example：设置你的组织或公司名（例如，com.example）。
* artifactId=selenium-project：设置项目名称。
2. 设置pom.xml依赖(添加selenium-java依赖,添加selenium-manager依赖)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.selenium.framework</groupId>
    <artifactId>selenium-automation</artifactId>
    <version>1.0-SNAPSHOT</version>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.30.0</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-manager -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-manager</artifactId>
            <version>4.30.0</version>
        </dependency>
    </dependencies>
    <properties>
        <maven.compiler.source>22</maven.compiler.source>
        <maven.compiler.target>22</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```
***报错时执行强制更新***
```bash
mvn clean install -U
```
## 编写第一个java测试脚本
```java
package test;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class TestMain {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();

        driver.get("https://selenium.dev");

        driver.quit();
    }
}
```
## java在selenium与python的不同
1. 驱动需要生成实例再调用
```java
WebDriver driver = new ChromeDriver();
driver.get("https://selenium.dev");
driver.quit();
```
```python
driver = webdriver.Chrome()
```
2. 元素定位需要声明WebElement
```java
WebElement textBox = driver.findElement(By.name("my-text"));
WebElement submitButton = driver.findElement(By.cssSelector("button"));
```
```python
text_box = driver.find_element(by=By.NAME, value="my-text")
submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")
```
3. 显示等待
```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import java.util.concurrent.TimeUnit;

WebDriver driver = new ChromeDriver();
WebDriverWait wait = new WebDriverWait(driver, 10);
WebElement element = wait.until(ExpectedConditions.presenceOfElementLocated(By.name("q")));
```
```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

element = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.NAME, "q"))
)
```
4. 隐式等待
```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(2));
```
```python
driver.implicitly_wait(2)
```
6. select选择
```java
WebElement selectElement = driver.findElement(By.name("selectomatic"));
Select select = new Select(selectElement);
```
```python
dropdown2 = self.driver.find_element(By.ID, 'months')
select2 = Select(dropdown2)
select2.select_by_visible_text('January')
```
   1. 通过可视文本选择选项
```java
        select.selectByVisibleText("Four");
```
   2. 通过值选择选项
```java
        select.selectByValue("two");
```
   3. 通过索引index选择选项
```java
        select.selectByIndex(3);
```