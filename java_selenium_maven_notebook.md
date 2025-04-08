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
        <!-- https://mvnrepository.com/artifact/org.testng/testng -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.11.0</version>
            <scope>test</scope>
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
## 创建面向对象的maven-selenium项目
1. 创建maven project
![maven project interface](/screen_shot/maven_project_interface.png)
2. 安装selenium-java selenium-manager(selenium-java在4.6.0后无需安装) testng依赖
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.test.automation</groupId>
    <artifactId>selenium-framework</artifactId>
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
        <!-- https://mvnrepository.com/artifact/org.testng/testng -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.11.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <properties>
        <maven.compiler.source>22</maven.compiler.source>
        <maven.compiler.target>22</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```
3. 项目结构
![project_structure](/screen_shot/project_structure.png)
* base包表示主函数测试类
* pages包表示页面类
* utils包表示工具类
* tests包表示测试函数
4. 创建basetest.java
```java
package base;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;

public class BaseTest {
    protected WebDriver driver;
    @BeforeMethod //注解向解释器解释执行过程
    public void setUp(){
        driver=new FirefoxDriver();
        driver.get("http://admin-demo.nopcommerce.com/login");
        driver.manage().window().maximize();
    }
    @AfterMethod
    public void tearDown(){
        if (driver!=null){
            driver.quit();
        }
    }
}
```
5. 创建loginpage.java(设计思想是在page包中一个页面视为一个类)
```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class LoginPage{
    private WebDriver driver;
    public LoginPage(WebDriver driver){//每个页面需要使用构造方法初始化driver
        this.driver=driver;
    }
    public void input_email(){
        WebElement emailbox = driver.findElement(By.id("Email"));//在Java中元素前面需要声明WebElement
        emailbox.clear();
        emailbox.sendKeys("admin@yourstore.com");
    }
    public void input_password(){
        WebElement passwordbox=driver.findElement(By.id("Password"));
        passwordbox.clear();
        passwordbox.sendKeys("admin");
    }
    public void click_login_button(){
        WebElement loginbutton=driver.findElement(By.xpath("//button[contains(text(), 'Log in')]"));
        loginbutton.click();
    }
}

```
6. 创建LoginTest.java
```java
package tests;

import base.BaseTest;
import org.openqa.selenium.WebDriver;
import org.testng.Assert;
import org.testng.annotations.Test;
import pages.LoginPage;

import java.time.Duration;

public class LoginTest extends BaseTest {
    @Test//需要注解为Test
    public void test_valid_login(){
        LoginPage loginPage=new LoginPage(driver);
        loginPage.input_email();
        loginPage.input_password();
        loginPage.click_login_button();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(8));
        Assert.assertEquals(driver.getTitle(),"Dashboard / nopCommerce administration");
    }
}
```
## 使用extent reports输出个性化报告
1. 安装extent reports依赖
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.test.automation</groupId>
    <artifactId>selenium-framework</artifactId>
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
        <!-- https://mvnrepository.com/artifact/org.testng/testng -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.11.0</version>
        </dependency>
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-api</artifactId>
            <version>4.30.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.aventstack/extentreports -->
        <dependency>
            <groupId>com.aventstack</groupId>
            <artifactId>extentreports</artifactId>
            <version>5.1.2</version>
        </dependency>
    </dependencies>
    <properties>
        <maven.compiler.source>22</maven.compiler.source>
        <maven.compiler.target>22</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>
```
2. 编写报告输出ExtentReportManager
```java
package utils;

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;

import java.text.SimpleDateFormat;
import java.util.Date;

public class ExtentReportManager {
    private static ExtentReports extent;
    private static ExtentTest test;
    public static String reportPath;
    public static ExtentReports getReportInstance(){
        if(extent==null){
            String timestamp=new SimpleDateFormat("yyyy-MM-dd_HH-mm-ss").format(new Date());
            reportPath = "reports/ExtentReport_"+timestamp+".html";
            ExtentSparkReporter reporter = new ExtentSparkReporter(reportPath);
            reporter.config().setDocumentTitle("Automation Test Report");
            reporter.config().setReportName("Test Execution Report");
            extent = new ExtentReports();
            extent.attachReporter(reporter);
        }
        return extent;
    }
    public  static ExtentTest createTest(String testName){
        test = getReportInstance().createTest(testName);
        return test;
    }

}

```
3. 编写基准测试文件BaseTest.java
```java
package base;
import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.BeforeSuite;
import utils.ExtentReportManager;

public class BaseTest {
    protected WebDriver driver;
    protected static ExtentReports extent;
    protected ExtentTest test;
    @BeforeSuite
    public void setupReport(){
        extent= ExtentReportManager.getReportInstance();
    }
    @AfterSuite
    public void teardownReport(){
        extent.flush();
    }
    @BeforeMethod
    public void setUp(){
        driver=new FirefoxDriver();
        driver.get("http://admin-demo.nopcommerce.com/login");
        driver.manage().window().maximize();
    }
    @AfterMethod
    public void tearDown(){
        if (driver!=null){
            driver.quit();
        }
    }
}
```
4. 编写登录页面测试文件LoginTest.java
```java
package tests;

import base.BaseTest;
import org.openqa.selenium.WebDriver;
import org.testng.Assert;
import org.testng.annotations.Test;
import pages.LoginPage;
import utils.ExtentReportManager;

import java.time.Duration;

public class LoginTest extends BaseTest {
    @Test
    public void test_valid_login(){
        test= ExtentReportManager.createTest("Login test");
        LoginPage loginPage=new LoginPage(driver);
        test.info("navigate to website");
        loginPage.input_email();
        loginPage.input_password();
        loginPage.click_login_button();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(8));
        test.info("verify index title");
        Assert.assertEquals(driver.getTitle(),"Dashboard / nopCommerce administration");
        test.info("test pass!");
    }
}
```
## 使用pagefactory简化元素的定位
1. 安装selenium依赖
2. 将原本find方法变为注解
```java
@FindBy(id="Email")
WebElement emailbox;
@FindBy(id="Password")
WebElement passwordbox;
@FindBy(xpath = "//button[@type='submit']")
WebElement loginbutton;
```
3. 在页面进行pagefactory初始化
```java
public LoginPage(WebDriver driver){
        this.driver=driver;
        PageFactory.initElements(driver, this);
    }
```
## 数据驱动自动化测试
### 创建xlsx形式的excel表格
1. 安装poi依赖
```xml
<!-- https://mvnrepository.com/artifact/org.apache.poi/poi -->
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi</artifactId>
            <version>5.4.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.poi/poi-ooxml -->
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi-ooxml</artifactId>
            <version>5.4.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.24.0</version>
        </dependency>
```
2. 创建并编写ExcelUtils
```java
package utils;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.CellType;
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Workbook;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

public class ExcelUtils {

	private static Workbook workbook;
	private static Sheet sheet;

	public static void loadExcel(String filePath, String sheetName) throws IOException {

		FileInputStream file = new FileInputStream(filePath);
		workbook = new XSSFWorkbook(file);
		sheet = workbook.getSheet(sheetName);
	}

	public static String getCellData(int row, int col) {
		Cell cell = sheet.getRow(row).getCell(col);
		if (cell.getCellType() == CellType.STRING) {
			return cell.getStringCellValue();
		} else if (cell.getCellType() == CellType.NUMERIC) {
			return String.valueOf((int) cell.getNumericCellValue());
		}
		return "";
	}

	public static int getRowCount() {
		return sheet.getPhysicalNumberOfRows();
	}

	public static void closeExcel() throws IOException {
		workbook.close();
	}

}
```
3. 编写logintest文件
```java
package tests;

import base.BaseTest;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;
import pages.LoginPage;
import utils.ExcelUtils;
import utils.ExtentReportManager;

import java.io.IOException;
import java.time.Duration;

public class LoginTest extends BaseTest {
    /**
     * 获取表格中的数据
     * @return 返回文件中用户名 密码
     * @throws IOException
     */
    @DataProvider(name="LoginData")//@dataprovider注解表示数据提供的对象 name表示名称
    public Object[][] getLoginData() throws IOException {

        String filePath = System.getProperty("user.dir")+"/testdata/TestData.xlsx";
        ExcelUtils.loadExcel(filePath, "Sheet1");
        int rowCount = ExcelUtils.getRowCount();
        Object[][] data = new Object[rowCount-1][2];

        for(int i=1; i<rowCount; i++) {

            data[i-1][0] = ExcelUtils.getCellData(i, 0);	// Username
            data[i-1][1] = ExcelUtils.getCellData(i, 1);	// Password
        }
        ExcelUtils.closeExcel();
        return data;
    }
    @DataProvider(name="LoginData2")
    public Object[][] getData(){

        return new Object[][] {
                {"user1","pass1"},
                {"user2","pass2"},
                {"user3","pass3"}
        };
    }
    @Test(dataProvider = "LoginData")//dataprovider里面填写名称表示数据来源
    public void test_valid_login(String username,String password){

        test= ExtentReportManager.createTest("Login test");
        LoginPage loginPage=new LoginPage(driver);
        test.info("navigate to website");
        loginPage.input_email(username);
        loginPage.input_password(password);
        loginPage.click_login_button();
        test.info("verify index title");
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(3));
        wait.until(ExpectedConditions.titleIs("Dashboard / nopCommerce administration"));
        Assert.assertEquals(driver.getTitle(),"Dashboard / nopCommerce administration","");
        test.info("test pass!");
    }
}
```
### 使用数据提供方法提供数据
1. 在测试文件logintest文件写注解表示数据提供方法
```java
@DataProvider(name="LoginData2")
    public Object[][] getData(){

        return new Object[][] {
                {"user1","pass1"},
                {"user2","pass2"},
                {"user3","pass3"}
        };
    }
```
2. 测试方法时编写注解表明使用此方法
```java
    @Test(dataProvider = "LoginData2")//dataprovider里面填写名称表示数据来源
    public void test_valid_login(String username,String password){

        test= ExtentReportManager.createTest("Login test");
        LoginPage loginPage=new LoginPage(driver);
        test.info("navigate to website");
        loginPage.input_email(username);
        loginPage.input_password(password);
        loginPage.click_login_button();
        test.info("verify index title");
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(3));
        wait.until(ExpectedConditions.titleIs("Dashboard / nopCommerce administration"));
        Assert.assertEquals(driver.getTitle(),"Dashboard / nopCommerce administration","");
        test.info("test pass!");
    }
```
## 通过邮件发送测试报告
1. 安装邮件依赖
```xml
<!-- https://mvnrepository.com/artifact/com.sun.mail/jakarta.mail -->
        <dependency>
            <groupId>com.sun.mail</groupId>
            <artifactId>jakarta.mail</artifactId>
            <version>2.0.1</version>
        </dependency>
``` 
2. 编写邮件工具类文件EmailUtils
```java
package utils;

import java.io.File;
import java.util.Properties;

import jakarta.mail.Authenticator;
import jakarta.mail.Message;
import jakarta.mail.PasswordAuthentication;
import jakarta.mail.Session;
import jakarta.mail.Transport;
import jakarta.mail.internet.InternetAddress;
import jakarta.mail.internet.MimeBodyPart;
import jakarta.mail.internet.MimeMessage;
import jakarta.mail.internet.MimeMultipart;

public class EmailUtils {

    public static void sendTestReport(String reportPath) {
        final String senderEmail = "z2510668237@gmail.com";//自己的gmail邮箱
        final String appPassword = "dljvxzaxwuodarfc";//创建应用密码
        final String recipientEmail = "z2510668237@gmail.com";

        // SMTP Server Properties
        Properties prop = new Properties();
        prop.put("mail.smtp.auth", "true");
        prop.put("mail.smtp.host", "smtp.gmail.com");
        prop.put("mail.smtp.starttls.enable", "true");
        prop.put("mail.smtp.port", "587");

        // Create session with Authentication
        Session session = Session.getInstance(prop, new Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication(senderEmail, appPassword);
            }
        });
        session.setDebug(true);

        try {
            // Create Email message
            Message message = new MimeMessage(session);
            message.setFrom(new InternetAddress(senderEmail));
            message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(recipientEmail));
            message.setSubject("Test Email From QA Automation");
//					message.setText("Hello \n This is a test email from Java \n Regards,\nQA Team");

            // Email Body Part
            MimeBodyPart textPart = new MimeBodyPart();
            textPart.setText("Hello \n\n This is a test email from Java \n\n Regards,\nQA Team");

            // Attachment Part
            MimeBodyPart attachmentPart = new MimeBodyPart();
//			String filePath = System.getProperty("user.dir") + "/reports/ExtentReport.html";
            System.out.println("Attachment path is - " + reportPath);
            attachmentPart.attachFile(new File(reportPath));

            // Combine body and attachment parts
            MimeMultipart multipart = new MimeMultipart();
            multipart.addBodyPart(textPart);
            multipart.addBodyPart(attachmentPart);
            message.setContent(multipart);

            // Send Email
            Transport.send(message);
            System.out.println("Email Sent Successfully ***");

        } catch (Exception e) {
            e.printStackTrace();
        }

    }

}
```
## 注解的使用
|注解|触发时机|适用场景|推荐使用时机|
|--|--|--|--|
|@BeforeSuite|在整个测试套件执行前|用于全局初始化（如数据库连接、启动服务器等）|需要在所有测试之前做一次性准备工作，比如启动服务器或配置全局变量。
|@BeforeTest|在 <test> 标签下的所有测试方法执行前|用于为 <test> 标签下的所有测试做准备工作|需要对 <test> 标签下的所有测试方法进行初始化。|
|@BeforeClass|在当前类中的第一个测试方法执行前|用于类级别的初始化，如 WebDriver 或数据库连接|需要为整个测试类进行初始化工作，并且不需要在每个方法前执行。
|@BeforeMethod|在每个 @Test 方法执行前|用于方法级别的初始化，如每个测试方法前都要清理或初始化	|需要在每个测试方法前进行独立的初始化，确保测试之间互不干扰。|
|@BeforeGroups|在特定测试组执行前|用于对特定测试组的初始化操作|	需要对某个特定的测试组进行初始化，通常适用于功能分组的情况。|