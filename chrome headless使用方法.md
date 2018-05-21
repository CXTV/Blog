# 无头浏览器用法使用方法

## 1. chromeheadless

```
from selenium import webdriver

option = webdriver.ChromeOptions()
option.add_argument('headless')
driver = webdriver.Chrome(chrome_options=option)
# driver = webdriver.Chrome()
# driver = webdriver.PhantomJS()
driver.get('https://www.baidu.com/')
print('打开浏览器')
print(driver.title)
driver.find_element_by_id('kw').send_keys('测试')
print('关闭')
driver.quit()
print('测试完成')
```

## 2. phantomjs

```
dcap = dict(DesiredCapabilities.PHANTOMJS)  # 设置useragent
dcap['phantomjs.page.settings.userAgent'] = (
    'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/44.0.2403.155 UBrowser/5.4.5426.1034 Safari/537.36')  # 根据需要设置具体的浏览器信息
driver = webdriver.PhantomJS(desired_capabilities=dcap)  # 封装浏览器信息
driver = webdriver.PhantomJS(desired_capabilities=dcap)
```

