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
## 显示等待与隐式等待
* 显示等待与隐式等待需要导入相关包
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
```
1. 显示等待:
显示等待主要语法:
```python
WebDriverWait(driver:self.driver,timeout(s):10).until(
            EC.presence_of_element_located((By.ID,"su"))
        )
```
* Expected Conditions(期待出现情况):
1. title_is(标题是)
2. title_contains(标题包含)
3. presence_of_element_located(元素加载即可,不需要互动)
4. visibility_of_element_located(元素需要能够互动和被用户看到)
5. presence_of_all_elements_located(符合特定条件的所有元素都要被看到)
6. text_to_be_present_in_element(文本出现在元素中)
7. invisibility_of_element_located(通过定位器元素消失)
8.  element_to_be_clickable(元素可点击)
9.  element_to_be_selected(元素可选择)
10. element_located_to_be_selected(通过定位器元素可选择)
11. alert_is_present(警告出现)
2. 隐式等待:
隐式等待主要语法:
```python
driver.implicitly_wait(10) # 隐式等待相当于等待一定的时间,等同于time.sleep(10)
```
## 测试网页对象设计样板
1. 测试用例(使用python unittest)
```python
# main.py
import unittest
from selenium import webdriver
import page

class PythonOrgSearch(unittest.TestCase):
    """测试python页面的搜索"""

    def setUp(self): #网页设置初始化
        self.driver = webdriver.Firefox()
        self.driver.get("http://www.python.org")

    def test_search_in_python_org(self):
        """测试搜索框搜索功能"""

        #加载主页.
        main_page = page.MainPage(self.driver)
        #检查标题
        self.assertTrue(main_page.is_title_matches(), "python.org title doesn't match.")
        #设置搜索框文本 "pycon"
        main_page.search_text_element = "pycon"
        main_page.click_go_button()
        search_results_page = page.SearchResultsPage(self.driver)
        #检验页面是否为空
        self.assertTrue(search_results_page.is_results_found(), "No results found.")

    def tearDown(self): #测试用例的结束
        self.driver.close()

if __name__ == "__main__": #运行测试用例
    unittest.main()
```
***
setUpClass：类级别的方法，只会执行一次，用于一些共享资源的初始化。
用途：适用于一些耗时较长或者只需要进行一次的初始化工作，例如：启动数据库连接、打开浏览器等。
setUp：实例级别的方法，会在每个测试用例执行前调用一次，用于每个测试用例的初始化操作。
用途：适用于那些每个测试用例都需要的初始化工作，例如：设置每个测试需要的环境状态，初始化对象等。
***
2. 网页对象类(每个页面看作一个类)
```python
# page.py
from element import BasePageElement
from locators import MainPageLocators

class BasePage(object):
    """Base class to initialize the base page that will be called from all
    pages"""

    def __init__(self, driver):
        self.driver = driver


class MainPage(BasePage):
    """Home page action methods come here. I.e. Python.org"""

    #Declares a variable that will contain the retrieved text
    search_text_element = SearchTextElement()

    def is_title_matches(self):
        """Verifies that the hardcoded text "Python" appears in page title"""

        return "Python" in self.driver.title

    def click_go_button(self):
        """Triggers the search"""

        element = self.driver.find_element(*MainPageLocators.GO_BUTTON)
        element.click()


class SearchResultsPage(BasePage):
    """Search results page action methods come here"""

    def is_results_found(self):
        # Probably should search for this text in the specific page
        # element, but as for now it works fine
        return "No results found." not in self.driver.page_source
```
3. 网页元素(不同的网页的一些元素)
```python
# element.py
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait


class BasePageElement(object):
    """Base page class that is initialized on every page object class."""

    def __set__(self, obj, value):
        """Sets the text to the value supplied"""

        driver = obj.driver
        WebDriverWait(driver, 100).until(
            lambda driver: driver.find_element(By.NAME, self.locator))
        driver.find_element(By.NAME, self.locator).clear()
        driver.find_element(By.NAME, self.locator).send_keys(value)

    def __get__(self, obj, owner):
        """Gets the text of the specified object"""

        driver = obj.driver
        WebDriverWait(driver, 100).until(
            lambda driver: driver.find_element(By.NAME, self.locator))
        element = driver.find_element(By.NAME, self.locator)
        return element.get_attribute("value")
```