## 设置selenium各种webdriver设置useragent
```
# @firefox
from selenium import webdriver
profile = webdriver.FirefoxProfile()
profile.set_preference("general.useragent.override", user_agent)
driver = webdriver.Firefox(profile)
```
