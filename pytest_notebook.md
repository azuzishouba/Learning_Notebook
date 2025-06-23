# pytest笔记
## pytest安装与运行
1. 安装pytest
```python
pip install pytest
```
2. 编写测试用例：
* 测试函数以<kbd>test_</kbd>开头。
* 测试类以<kbd>Test</kbd>开头。
3. 运行测试
```python
pytest 
```
## 简单的断言测试
```python
#my_functions.py
def add(num1,num2):
    return num1+num2
def divide(num1,num2):
    return num1/num2
```
```python
# test_my_functions.py
import pytest
import source.my_functions as my_functions
def test_add():
    result = my_functions.add(2, 3)
    assert result == 5 #断言时直接使用assert来判断

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError): #使用pytest.raises来简单抛出异常,测试时算通过
        result = my_functions.divide(10, 0)
```
## 面向对象的测试
```python
#shapes.py
import math
class Shape:
    def area(self):
        pass
    def perimeter(self):
        pass

class Circle(Shape):
    def __init__(self,radius):
        self.radius=radius
    def area(self):
        return math.pi*self.radius **2
    def perimeter(self):
        return  2*math.pi*self.radius

```
```python
#test_circles.py
import math

import source.shapes as shapes


class TestCircle:
    def setup_method(self, method):#setup_method方法级别在方法前都会执行一遍,teardown同理在方法后执行一遍
        print(f"Setting up{method}")
        self.circle = shapes.Circle(10)

    def teardown_method(self, method):
        print(f"Tearing down {method}")
        del self.circle

    def test_area(self):
        assert self.circle.area()==math.pi*self.circle.radius**2
```
***pytest -s能够详细输出信息***
### 类级别的 setup 和 teardown

如果你需要在类级别执行初始化和清理操作，可以使用 pytest 的 setup_class 和 teardown_class 钩子函数。
示例：
```python
class TestExample:
    @classmethod
    def setup_class(cls):
        print("Setup class: Initialize class-level resources")

    @classmethod
    def teardown_class(cls):
        print("Teardown class: Clean up class-level resources")

    def test_1(self):
        assert True

    def test_2(self):
        assert True
```
## fixture夹具
夹具(Fixture)在 pytest 中确实可以看作是一个函数，它会被当作参数传递给测试函数。夹具的主要作用是提供一种机制，用于在测试运行之前准备测试环境（如初始化数据、创建对象等），并在测试结束后清理资源。
夹具的基本用法
1. 定义一个夹具

使用 @pytest.fixture 装饰器定义一个夹具函数。
```python
import pytest

@pytest.fixture
def my_fixture():
    return "Hello, Fixture!"
```
2. 在测试函数中使用夹具

将夹具名称作为参数传递给测试函数,pytest 会自动调用夹具函数并将其返回值传递给测试函数。
```python
def test_example(my_fixture):
    assert my_fixture == "Hello, Fixture!"
```
```python
#shapes.py
import math


class Shape:
    def area(self):
        pass

    def perimeter(self):
        pass


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def perimeter(self):
        return 2 * math.pi * self.radius


class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.width * self.length

    def perimeter(self):
        return 2 * (self.length + self.width)
```
```python
import pytest

from source import shapes


@pytest.fixture
def my_rectangle():
    return shapes.Rectangle(10,20)

def test_area(my_rectangle):
    assert my_rectangle.area()==10*20
def test_perimeter(my_rectangle):
    assert my_rectangle.perimeter()==2*(10+20)
```
### fixture夹具的范围
| Scope 类型   | 生命周期 | 适用场景| 示例 |
|:--|:--|:--|:--
| `function`   | 每个函数  | 每个测试函数独立使用，不共享状态或上下文。           | 每个测试函数都重新创建一个数据库连接。如果你希望每个测试函数都使用新的 fixture 实例，例如某些不需要共享状态或上下文的测试。                            |
| `module`     | 每个文件  | 共享状态，但只在当前文件中使用。                   | 每个文件中所有测试函数共享同一个数据库连接。                        |
| `class`      | 每个类    | 每个测试类内共享状态。                           | 每个测试类共享同一个配置对象。                                    |
| `session`    | 整个会话  | 整个测试会话中共享状态，适用于跨文件共享资源。         | 所有测试文件共享同一个 web 服务实例。 当你希望整个测试会话（通常是测试套件）中共享某些资源，比如数据库连接、远程服务、外部API连接等，可以选择此作用范围。 |
## pytest 标记与参数化
在 pytest 中，标记（Marking） 是一种强大的功能，允许你为测试函数或测试类添加元数据（metadata），从而控制测试的执行方式。标记可以用于分类测试、跳过测试、参数化测试等。
1. @pytest.mark.skip：跳过测试

标记某个测试为跳过，不执行。
```python

import pytest

@pytest.mark.skip(reason="This test is not ready yet")
def test_skip():
    assert 1 + 1 == 3
```
2. @pytest.mark.skipif：条件跳过

根据条件跳过测试。
```python
import sys
import pytest

@pytest.mark.skipif(sys.platform == "win32", reason="Does not run on Windows")
def test_skipif():
    assert 1 + 1 == 2
```
3. @pytest.mark.xfail：预期失败

标记某个测试为预期失败。如果测试失败，pytest 不会将其视为失败；如果测试通过，会将其视为意外通过。
```python
import pytest

@pytest.mark.xfail(reason="This test is expected to fail")
def test_xfail():
    assert 1 + 1 == 3
```
4. @pytest.mark.parametrize：参数化测试

为测试提供多组参数，生成多个测试用例。
```python
import pytest

@pytest.mark.parametrize("a, b, expected", [(1, 2, 3), (4, 5, 9)])
def test_parametrize(a, b, expected):
    assert a + b == expected
```
### 参数化测试

你可以使用 @pytest.mark.parametrize 在类中实现参数化测试。
示例：
```python
import pytest

class TestMath:
    @pytest.mark.parametrize("a, b, expected", [(1, 2, 3), (4, 5, 9)])
    def test_addition(self, a, b, expected):
        assert a + b == expected
```
### hook函数
pytest 的 hook 函数就是一套“事件监听器”，让你能在测试执行的各个阶段“挂钩干预”，比如：启动前、用例执行前后、生成报告等。

| Hook 函数名                                    | 触发时机    | 能干啥              |
| ------------------------------------------- | ------- | ---------------- |
| `pytest_configure(config)`                  | 初始化时    | 设置全局配置、添加 marker |
| `pytest_sessionstart(session)`              | 会话开始    | 打印欢迎语、初始化数据库     |
| `pytest_runtest_setup(item)`                | 每个用例运行前 | 登录、准备数据          |
| `pytest_runtest_call(item)`                 | 执行用例时   | 动态处理断言或异常        |
| `pytest_runtest_teardown(item)`             | 用例运行后   | 清理资源、断开连接        |
| `pytest_sessionfinish(session, exitstatus)` | 所有用例跑完  | 发送报告、关闭服务        |
### confest.py文件作用
集中管理测试的“公共资源”与“钩子逻辑”，比如共享的 fixture、插件配置、hook 函数等

| 功能类型          | 举个栗子 🌰                                   | 用途说明                  |
| ------------- | ----------------------------------------- | --------------------- |
| 🔧 Fixture 共享 | 数据库连接、登录态、token等                          | 不用每个测试文件都写一遍          |
| 🪝 Hook 函数    | `pytest_runtest_setup`、`pytest_configure` | 控制测试前后行为，比如自动截图、失败重跑等 |
| 🧩 插件配置       | 配置 pytest-html、allure等插件                  | 集中设置，统一管理             |

## allure-pytest的安装与使用
1. 安装 Allure 命令行工具

Allure 是一个独立的工具，需要单独安装。以下是安装方法：
Windows 系统

   1. 下载 Allure 命令行工具：
      * 访问 Allure 的 GitHub 发布页面。
      * 下载最新版本的 .zip 文件（例如 allure-2.23.0.zip）。
   2. 解压下载的文件到一个目录，例如 C:\allure。
   3. 将 Allure 的 bin 目录添加到系统的环境变量中：
      * 右键点击“此电脑”或“我的电脑”，选择“属性”。
      * 点击“高级系统设置” -> “环境变量”。
      * 在“系统变量”中找到 Path，点击“编辑”。
      * 添加 Allure 的 bin 目录路径（例如 C:\allure\bin）。
      * 点击“确定”保存。

   4. 打开一个新的命令提示符窗口，运行以下命令验证安装：
```bash
    allure --version
```
    如果显示版本号，说明安装成功。
2. 安装pytest-Allure
   1. 安装 Allure 和插件：
```bash
    pip install allure-pytest
```
   2. 运行测试并生成 Allure 数据：
```bash
    pytest --alluredir=./allure-results
```
   3. 生成并查看报告：
```bash
    allure serve ./allure-results
```
## allure报告的详细使用
### 常用allure标注
1. @allure.feature("模块/功能")

表示这个测试用例属于哪个功能模块，报告中会以模块为维度进行分组。

```python
@allure.feature("Sign Up Flow")
```
2. @allure.story("用户故事 / 场景")

表示测试用例背后的用户行为或功能场景，更细粒度地划分。
```python
@allure.story("User Sign Up")
```
3. @allure.severity(...)

标记这个测试用例的重要程度（对业务或系统影响），用于优先级分类。

可选等级：
```python
allure.severity_level.BLOCKER      # 阻塞整个功能
allure.severity_level.CRITICAL     # 关键功能出错
allure.severity_level.NORMAL       # 正常优先级
allure.severity_level.MINOR        # 次要问题
allure.severity_level.TRIVIAL      # 可忽略的小问题
```
例子：
```python
@allure.severity(allure.severity_level.CRITICAL)
```
4. @allure.step("步骤说明")

这个可以包裹你测试代码中的逻辑步骤，让报告里显示出你执行的详细操作步骤（一步步展开看，非常清晰）。
```python
with allure.step("填写注册表单"):
    loginpage.input_name()
    loginpage.input_email()
```
5. @allure.title("报告标题")
配置当前报告的标题
```python
@allure.title("测试报告")
```