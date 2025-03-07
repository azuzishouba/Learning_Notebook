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
            EC.presence_of_element_located((By.NAME, self.locator))
        )
        driver.find_element(By.NAME, self.locator).clear()
        driver.find_element(By.NAME, self.locator).send_keys(value)

    def __get__(self, obj, owner):
        """Gets the text of the specified object"""

        driver = obj.driver
        WebDriverWait(driver, 100).until(
            EC.presence_of_element_located((By.NAME, self.locator))
        )
        element = driver.find_element(By.NAME, self.locator)
        return element.get_attribute("value")
```
4. 定位器(locators)
```python
from selenium.webdriver.common.by import By

class MainPageLocators(object):
    """A class for main page locators. All main page locators should come here"""

    GO_BUTTON = (By.ID, 'submit')

class SearchResultsPageLocators(object):
    """A class for search results locators. All search results locators should
    come here"""

    pass
```
## select(多项选择)
![select_option](/screen_shot/select_option.png)
```python
def select_months(self):
        dropdown2 = self.driver.find_element(By.ID, 'months')
        select2 = Select(dropdown2)
        select2.select_by_visible_text('January')
```
### select常用方法
索引从0开始
* select_by_index(index: int) → None

  * Select the option at the given index. This is done by examining the “index” attribute of an element, and not merely by counting.

  * Args:

    * index - The option at this index will be selected

    throws NoSuchElementException If there is no option with specified index in SELECT

* select_by_value(value: str) → None

  * Select all options that have a value matching the argument. That is, when given “foo” this would select an option like:

    <option value=”foo”>Bar</option>

  * Args:

    * value - The value to match against

    throws NoSuchElementException If there is no option with specified value in SELECT

* select_by_visible_text(text: str) → None

  * Select all options that display text matching the argument. That is, when given “Bar” this would select an option like:

        <option value=”foo”>Bar</option>

  * Args:

    * text - The visible text to match against

        throws NoSuchElementException If there is no option with specified text in SELECT

## actionchains(复杂链式操作)
ActionChains 在链模式的使用:
```python
menu = driver.find_element(By.CSS_SELECTOR, ".nav")
hidden_submenu = driver.find_element(By.CSS_SELECTOR, ".nav #submenu1")

ActionChains(driver).move_to_element(menu).click(hidden_submenu).perform()
```
也可以一个动作一个动作执行, 然后 performed.:
```python
menu = driver.find_element(By.CSS_SELECTOR, ".nav")
hidden_submenu = driver.find_element(By.CSS_SELECTOR, ".nav #submenu1")

actions = ActionChains(driver)
actions.move_to_element(menu)
actions.click(hidden_submenu)
actions.perform()
```
常用actions函数:

* click(on_element: WebElement | None = None) → ActionChains

    Clicks an element.

    * Args:

        * on_element: The element to click.  If None, clicks on current mouse position.

* click_and_hold(on_element: WebElement | None = None) → ActionChains

    Holds down the left mouse button on an element.

    * Args:

        * on_element: The element to mouse down. If None, clicks on current mouse position.

* double_click(on_element: WebElement | None = None) → ActionChains

    Double-clicks an element.

    * Args:

        * on_element: The element to double-click. If None, clicks on current mouse position.

* drag_and_drop(source: WebElement, target: WebElement) → ActionChains
    
    \#这里的down和up代表的按键按下去,松按键

    Holds down the left mouse button on the source element, then moves to the target element and releases the mouse button.

    * Args:

        * source: The element to mouse down.

        * target: The element to mouse up.

* drag_and_drop_by_offset(source: WebElement, xoffset: int, yoffset: int) → ActionChains

    Holds down the left mouse button on the source element, then moves to the target offset and releases the mouse button.

    * Args:

        * source: The element to mouse down.

        * xoffset: X offset to move to.

        * yoffset: Y offset to move to.

* key_down(value: str, element: WebElement | None = None) → ActionChains
    \#按下按键不松开应该仅用于控制按键
    Sends a key press only, without releasing it. Should only be used with modifier keys (Control, Alt and Shift).

    * Args:

        * value: The modifier key to send. Values are defined in Keys class.

        * element: The element to send keys. If None, sends a key to current focused element.

    Example, pressing ctrl+c:
    ```python
        ActionChains(driver).key_down(Keys.CONTROL).send_keys('c').key_up(Keys.CONTROL).perform()
    ```
* key_up(value: str, element: WebElement | None = None) → ActionChains

    Releases a modifier key.

    * Args:

        * value: The modifier key to send. Values are defined in Keys class.

        * element: The element to send keys. If None, sends a key to current focused element.

    Example, pressing ctrl+c:
    ```python
        ActionChains(driver).key_down(Keys.CONTROL).send_keys('c').key_up(Keys.CONTROL).perform()
    ```
* move_by_offset(xoffset: int, yoffset: int) → ActionChains

    Moving the mouse to an offset from current mouse position.

    * Args:

        * xoffset: X offset to move to, as a positive or negative integer.

        * yoffset: Y offset to move to, as a positive or negative integer.

* move_to_element(to_element: WebElement) → ActionChains

    Moving the mouse to the middle of an element.

    * Args:

        * to_element: The WebElement to move to.

* ***perform() → None(常用)***

    Performs all stored actions.
    用法:
    ```
    actions.perform()
    ```

* scroll_to_element(element: WebElement) → ActionChains

    If the element is outside the viewport, scrolls the bottom of the element to the bottom of the viewport.

    * Args:

        * element: Which element to scroll into the viewport.

* send_keys(*keys_to_send: str) → ActionChains

    Sends keys to current focused element.

    * Args:

        * keys_to_send: The keys to send. Modifier keys constants can be found in the ‘Keys’ class.
## alert(警告框)
1. 接受,取消警示
    ```python
    Alert(driver).accept()
    Alert(driver).dismiss()
    ```
2. 警示框输入
    ```python
    name_prompt = Alert(driver)
    name_prompt.send_keys("Willian Shakesphere")
    name_prompt.accept()
    ```
3. 获取警示框文本
   ```python
   alert_text = Alert(driver).text
    self.assertEqual("Do you wish to quit?", alert_text)
   ```
## 截屏
    ```python
    self.driver.get_screenshot_as_file('homepage.png')
    ```
## Selenium的文件下载与上传
### 文件上传操作

文件上传是 Web 应用程序中常见的功能之一。

在 Selenium 中，文件上传通常通过\<input type="file">元素实现。

以下是实现文件上传的步骤：

定位文件上传元素：首先，我们需要定位到文件上传的输入框元素。通常，这个元素是一个\<input>标签，类型为file。
实例
```python
file_input = driver.find_element(By.XPATH, "//input[@type='file']")
```
发送文件路径：一旦定位到文件上传元素，我们可以使用send_keys()方法将文件的绝对路径发送到该元素。
```python
file_input.send_keys("/path/to/your/file.txt")
```
这将触发文件选择对话框，并自动选择指定的文件。

提交表单：在某些情况下，文件上传后需要提交表单。你可以通过点击提交按钮来完成这一操作。
```python
submit_button = driver.find_element(By.XPATH, "//input[@type='submit']")
submit_button.click()
```
注意事项
* 确保文件路径是正确的，并且文件存在。
* 如果文件上传元素是隐藏的，可能需要使用 JavaScript 来使其可见。
### 文件下载操作
文件下载操作在 Selenium 中稍微复杂一些，因为涉及到浏览器的下载对话框。

以下是实现文件下载的步骤：

设置下载路径：首先，我们需要设置浏览器的下载路径。这可以通过设置浏览器的首选项来实现。
```python
from selenium.webdriver.chrome.options import Options

chrome_options = Options()
chrome_options.add_experimental_option("prefs", {
    "download.default_directory": "/path/to/download/directory",
    "download.prompt_for_download": False,
    "download.directory_upgrade": True,
    "safebrowsing.enabled": True
})

driver = webdriver.Chrome(options=chrome_options)
```
这将设置浏览器的默认下载路径，并禁用下载提示。

触发下载：接下来，我们需要找到触发下载的链接或按钮，并点击它。
```python
download_link = driver.find_element(By.XPATH, "//a[@id='downloadLink']")
download_link.click()
```
这将触发文件下载，并自动保存到之前设置的下载路径中。

等待下载完成：为了确保文件下载完成，我们可以使用time.sleep()或更智能的等待机制。
```python
import time
time.sleep(10)  # 等待10秒，确保文件下载完成
```
注意事项

* 确保下载路径是可写的。
* 如果下载的文件较大，可能需要增加等待时间。

处理下载对话框

在某些情况下，浏览器可能会弹出下载对话框，询问用户是否保存文件。为了自动化处理这种情况，我们可以使用以下方法：

使用浏览器首选项：如上所述，通过设置浏览器的首选项，可以禁用下载对话框。
```python
chrome_options.add_experimental_option("prefs", {
    "download.prompt_for_download": False
})
```
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from selenium.webdriver.common.by import By
import time
import os

# 设置下载路径
download_dir = "/path/to/download/directory"

# 配置 Chrome 选项
chrome_options = webdriver.ChromeOptions()
prefs = {
    "download.default_directory": download_dir,  # 设置下载路径
    "download.prompt_for_download": False,       # 禁用下载提示
    "download.directory_upgrade": True,          # 允许下载到指定目录
    "safebrowsing.enabled": True                 # 启用安全浏览
}
chrome_options.add_experimental_option("prefs", prefs)

# 启动浏览器
service = ChromeService(executable_path="/path/to/chromedriver")
driver = webdriver.Chrome(service=service, options=chrome_options)

# 打开网页
driver.get("https://www.example.com/download")

# 点击下载按钮
download_button = driver.find_element(By.ID, "download-button")
download_button.click()

# 等待文件下载完成
time.sleep(10)  # 根据文件大小调整等待时间

# 检查文件是否下载成功
files = os.listdir(download_dir)
print("下载的文件列表:", files)

# 关闭浏览器
driver.quit()
```
## Selenium异常处理
在使用 Selenium 进行自动化测试时，异常处理非常重要。Selenium 提供了多种异常类型来帮助我们处理不同的错误情况。常见的异常包括 <kbd>NoSuchElementException</kbd>、<kbd>TimeoutException</kbd>、<kbd>ElementNotInteractableException</kbd>等。
1. 捕获元素未找到的异常

NoSuchElementException 在找不到某个元素时会抛出。可以使用 try-except 块来捕获该异常。
```python
from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException

driver = webdriver.Chrome()

try:
    element = driver.find_element_by_id("non_existent_id")
except NoSuchElementException:
    print("元素未找到")
```
2. 元素未可交互异常

ElementNotInteractableException 在元素存在，但无法与之交互时抛出（例如，元素不可见或不可点击）。
```python
from selenium import webdriver
from selenium.common.exceptions import ElementNotInteractableException

driver = webdriver.Chrome()

try:
    element = driver.find_element_by_id("element_id")
    element.click()  # 假设元素不可点击
except ElementNotInteractableException:
    print("元素不可交互")
```
例子:
(a) 页面元素查找时的异常处理

例如，当页面元素无法找到时，使用 NoSuchElementException 捕获异常。
```python
from selenium.common.exceptions import NoSuchElementException

try:
    loginpage.click_sign_up_button()
except NoSuchElementException:
    print("无法找到“注册”按钮，可能是页面未加载完全")
```
3. 超时异常

TimeoutException 通常发生在等待某个元素时超出设定的超时时间。例如，当我们使用 WebDriverWait 等待一个元素可见时，若超时未能找到该元素，就会抛出此异常。
```python
from selenium import webdriver
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()

try:
    WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "some_id")))
except TimeoutException:
    print("超时，未能找到元素")
```
(b) 使用 WebDriverWait 进行智能等待

很多情况下，使用 WebDriverWait 来确保元素加载完成可以避免由于加载延迟而导致的异常。
例子:
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

try:
    element = WebDriverWait(self.driver, 10).until(
        EC.presence_of_element_located((By.ID, "some_element_id"))
    )
except TimeoutException:
    print("等待元素超时，元素未能在指定时间内加载")
```