# Phantomjs使用教程



## 1.实现简单爬虫

```
from selenium import webdriver
 

driver = webdriver.PhantomJS()
driver.get('http://www.baidu.com')   #加载网页
data = driver.page_source   #获取网页文本
driver.save_screenshot('1.png')   #截图保存
print(data)
driver.quit()
```

## 2.设置请求头

```
from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
 
 
dcap = dict(DesiredCapabilities.PHANTOMJS)  #设置useragent
dcap['phantomjs.page.settings.userAgent'] = ('Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:25.0) Gecko/20100101 Firefox/25.0 ')  #根据需要设置具体的浏览器信息
driver = webdriver.PhantomJS(desired_capabilities=dcap)  #封装浏览器信息
driver.get('http://www.baidu.com')   #加载网页
data = driver.page_source   #获取网页文本
driver.save_screenshot('1.png')   #截图保存
print(data)
driver.quit()
```







