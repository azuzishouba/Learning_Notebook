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
![google_name_locate](/screen_shot/google_name_locate.png)

```python
locate_element_by_name=driver.get_element(By.name,"q")
```
### 通过元素的id定位
