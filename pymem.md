## selenium各种webdriver设置useragent
```python
# @firefox
from selenium import webdriver
profile = webdriver.FirefoxProfile()
profile.set_preference("general.useragent.override", user_agent)
driver = webdriver.Firefox(profile)

# @chrome
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('user-agent=' + user_agent)
driver = webdriver.Chrome(chrome_options=chrome_options)

# @phantomjs
dcap = dict(webdriver.DesiredCapabilities.PHANTOMJS)
dcap["phantomjs.page.settings.userAgent"] = (
                "Mozilla/5.0 (Linux; U; Android 2.3.6; en-us; Nexus S Build/GRK39F) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1"
            )
browser = webdriver.PhantomJS(desired_capabilities=dcap)            

```

## selenium获取cookie
```python
from selenium import webdriver
browser=webdriver.Firefox()
browser.get("xxx") #要登陆页面
sleep(100) #这个时间自己去手动登陆
cookie={}
for elem in browser.get_cookies():
    cookie[elem['name']] = elem['value']
print(json.dumps(cookie)) #字典转字符串
```

## 计算list中相同字串的个数
`''.join(list).count(sameStr)`python
