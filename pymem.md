## 设置selenium各种webdriver设置useragent
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
