# Selenium笔记
## Selenium的安装
1. 首先安装selenium框架
>pip install selenium 
2. 下载并安装对应浏览器所需的webdriver(网页驱动)
* Google chrome 下载安装 chromedriver
![chromedriver_interface](/screen_shot/chromedriver_interface.png)

    https://googlechromelabs.github.io/chrome-for-testing/
* firefox 下载安装geckodriver
![geckodriver_interface](/screen_shot/geckodriver_interface.png)

    https://github.com/mozilla/geckodriver/releases

***注意:浏览器最好升级到最新的版本***
## Selenium的初始化
1. 导入selenium包
```python
from selenium import webdriver #导入驱动包
from selenium.webdriver.chrome.service import Service #导入服务
```
2. 指定webdriver的位置和启动服务
```python
# 设置浏览器驱动的路径
PATH = r"D:\geckodriver-v0.35.0-win64\geckodriver.exe"
service = Service(executable_path=PATH)
driver = webdriver.Firefox(service=service)
```
3. 验证是否初始化成功
```python
 # 打开谷歌搜索首页
driver.get("https://www.google.com")

 # 等待搜索框出现
input_element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.NAME, "q"))
)
# 输入搜索内容并执行搜索
input_element.send_keys("brain" + Keys.ENTER)

# 打印网页标题
print(driver.title)
time.sleep(10)

driver.quit()
```
## 元素的定位
* 元素的定位需要导入对应的包
```python
from selenium.webdriver.common.by import By
```
### 通过元素的name定位
1. 通过元素name定位
```python
locate_element_by_name=driver.get_element(By.name,"q")
```
![google_name_locate](/screen_shot/google_name_locate.png)
### 通过元素的id定位
1. 通过元素的id定位
```python
baidu_button=self.driver.find_element(By.ID,"su")
```
![locate_element_by_id](/screen_shot/locate_element_by_id.png)
### 通过元素的Xpath定位
#### Xpath的语法
1. 选取节点
    1. /:从根节点选取所有子节点
    2. //:选取所有符合标签的所有子节点(常用)
    
        eg://tagname 代表选取所有符合tagname的子节点
    3. @:选取属性(常用)
    ***进一步的有选取节点下的节点,用法://tagname1/tagname2(常用)***
2. xpath运算符
   1. =:返回等于条件的元素
   2. or:返回符合条件之一的元素
   3. and:返回符合所有条件的元素
    eg:
        //h2[(@attribute="")or(@attribute="")]
        //h2[(@attribute="")and(@attribute="")]
#### Xpath定位元素的实例
* @属性定位:
    ```xpath
    //button[@data-qa="signup-button"]
    ```
    python代码:
    ```python
    sign_up_button = (By.XPATH, '// button[@data-qa="login-button"]')
    ```
    ![locate_element_by_xpath1](/screen_shot/locate_element_by_xpath1.png)
    类似的还有:
    ```python
    check_box1 = (By.XPATH, '//label[@for="newsletter"]')
    check_box2 = (By.XPATH, '//label[@for="optin"]')
    ```
* @属性contains定位:
    ```xpath
    //h2[contains(text(), 'New User Signup!')]
    ```
    ```python
    login_title = (By.XPATH, "//h2[contains(text(), 'New User Signup!')]")
    ```
    ![locate_element_by_xpath2](/screen_shot/locate_element_by_xpath2.png)