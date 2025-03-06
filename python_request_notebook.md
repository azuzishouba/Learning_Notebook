# python requests笔记
## request库
Python requests 是一个常用的 HTTP 请求库，可以方便地向网站发送 HTTP 请求，并获取响应结果。
1. 安装request库
```python
pip install requests
```
2. 发送get请求
```python
import requests

response=requests.get(self.urls['product_list'])
self.assertEqual(response.status_code,200)#response.status_code 返回状态码
response_data=response.json()#response.json()返回json格式的数据
```
3. 发送post请求
```python
import requests

data = {'key': 'value'}
response = requests.post('https://api.example.com/submit', data=data)

print(response.status_code)
print(response.text)
```
**更多请求的访问信息**
|属性或方法 |说明|
|:--|:--|
|apparent_encoding|编码方式|
|content|返回响应的内容，以字节为单位|
|cookies|返回一个 CookieJar 对象，包含了从服务器发回的 cookie|
|headers|返回响应头，字典格式|
|json()|返回结果的 JSON 对象 (结果需要以 JSON 格式编写的，否则会引发错误)|
|reason|响应状态的描述，比如 "Not Found" 或 "OK"|
|status_code|返回 http 的状态码，比如 404 和 200（200 是 OK，404 是 Not Found）|
|text|返回响应的内容，unicode 类型数据|
实例
```python
# 导入 requests 包
import requests

# 发送请求
x = requests.get('https://www.runoob.com/')

# 返回 http 的状态码
print(x.status_code)

# 响应状态的描述
print(x.reason)

# 返回编码
print(x.apparent_encoding)
```
输出结果如下：
```python
200
OK
utf-8
```
请求 json 数据文件，返回 json 内容：
实例
```python
# 导入 requests 包
import requests

# 发送请求
x = requests.get('https://www.runoob.com/try/ajax/json_demo.json')

# 返回 json 数据
print(x.json())
```
输出结果如下：
```python
{'name': '网站', 'num': 3, 'sites': [{'name': 'Google', 'info': ['Android', 'Google 搜索', 'Google 翻译']}, {'name': 'Runoob', 'info': ['菜鸟教程', '菜鸟工具', '菜鸟微信']}, {'name': 'Taobao', 'info': ['淘宝', '网购']}]}
```
### requests 方法

requests方法如下表：
|方法|描述|
|:--:|:--|
|delete(url, args) |发送 DELETE 请求到指定 url|
|get(url, params, args) |发送 GET 请求到指定 url|
|head(url, args) |发送 HEAD 请求到指定 url|
|patch(url, data, args) |发送 PATCH 请求到指定 url|
|post(url, data, json, args) |发送 POST 请求到指定 url|
|put(url, data, args) |发送 PUT 请求到指定 url|
|request(method, url, args) |向指定的 url 发送指定的请求方法|
* url 请求 url。
* data 参数为要发送到指定 url 的字典、元组列表、字节或文件对象。
* json 参数为要发送到指定 url 的 JSON 对象。
* args 为其他参数，比如 cookies、headers、verify等。
* **params 参数接收一个字典或字符串，字典类型会自动转换为 URL 编码的格式。**
示例：kw = {'s': 'python 教程'}

假设你使用 requests.get("https://www.runoob.com/", params=kw)，那么最终的 URL 会变成：
<kbd>https://www.runoob.com/?s=python+教程</kbd>

* ? 后面的 s=python+教程 就是查询字符串，s 是键，python 教程 是值。

* python 教程 中的空格会被自动编码为 + 或 %20，这是 URL 编码的一部分。

查询参数params的作用：

查询参数params是 URL 的一部分，通常用于：
* 过滤数据：比如在搜索时?s=python+教程,?s就是搜索的关键字，告诉服务器你要搜索的关键词。
* 分页：比如 ?page=2 表示获取第二页的数据。
* 排序：比如 ?sort=date 表示按日期排序。
* 其他操作：比如 ?action=delete 表示执行删除操作。
```python
import unittest
import requests

class TestApi(unittest.TestCase):
    def setUp(self):
        self.urls={
            'product_list': 'https://automationexercise.com/api/productsList',
            'brand_list': ' https://automationexercise.com/api/brandsList',
            'search_product': ' https://automationexercise.com/api/searchProduct',
            'verify_login': 'https://automationexercise.com/api/verifyLogin'
        }
    def test_get_all_products_list(self):
        response=requests.get(self.urls['product_list'])
        self.assertEqual(response.status_code,200)
        response_data=response.json()
        print(response_data)
    def test_post_to_all_products_list(self):
        response = requests.post(self.urls['product_list'])
        print(response.status_code)
        response_data = response.text
        print(response_data)
    def test_get_all_brand_list(self):
        response=requests.get(self.urls['brand_list'])
        self.assertEqual(response.status_code,200)
        response_data=response.json()
        print(response_data)
    def test_put_to_all_brand_list(self):
        response=requests.put(self.urls['brand_list'])
        self.assertEqual(response.status_code,200)
        response_data = response.json()
        print(response_data)
    def test_post_to_search_product(self):
        response=requests.post(self.urls['search_product'])
        print(response.json())
    def test_post_to_search_product_without_search_product_parameter(self):
        response=requests.post(self.urls['search_product'])
        response_data=response.json()
        self.assertEqual(response_data['message'],'Bad request, search_product parameter is missing in POST request.')
        print(response_data)
    def test_delete_to_verify_login(self):
        response = requests.get(self.urls[ 'verify_login'])
        response_data = response.json()
        self.assertIn('This request method is not supported.', response_data.values())
        self.assertEqual(response_data['responseCode'],405)
        print(response_data['responseCode'])


    def tearDown(self):
        pass
```
