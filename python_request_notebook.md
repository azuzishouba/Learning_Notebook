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
