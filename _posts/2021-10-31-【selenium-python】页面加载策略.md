---
layout: post
title: '【selenium-python】页面加载策略'
date: 2021-10-31
author: nangfeng-li
tags: selenium-python webdriver
---

> 参考：[webdriver_页面加载策略](https://www.selenium.dev/zh-cn/documentation/webdriver/page_loading_strategy/)


定义当前会话的页面加载策略. 默认情况下, 当Selenium WebDriver加载页面时, 遵循 normal 的页面加载策略. 始终建议您在页面加载缓慢时, 停止下载其他资源 (例如图片, css, js) .

document.readyState 属性描述当前页面的加载状态. 默认情况下, 在页面就绪状态是 complete 之前, WebDriver都将延迟 driver.get() 的响应或 driver.navigate().to() 的调用.

在单页应用程序中 (例如Angular, React, Ember) , 一旦动态内容加载完毕 (即pageLoadStrategy状态为COMPLETE) , 则点击链接或在页面内执行某些操作的行为将不会向服务器发出新请求, 因为内容在客户端动态加载, 无需刷新页面.

单页应用程序可以动态加载许多视图, 而无需任何服务器请求, 因此页面加载策略将始终显示为 COMPLETE 的状态, 直到我们执行新的 driver.get() 或 driver.navigate().to() 为止.

WebDriver的 页面加载策略 支持以下内容:

# normal

> 下载并解析html内容和子资源(如图像，css，js，但不包括ajax）

此配置使Selenium WebDriver等待整个页面的加载. 设置为 normal 时, Selenium WebDriver将保持等待, 直到 返回 [load](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/load_event) 事件

默认情况下, 如果未设置页面加载策略, 则设置 normal 为初始策略.

```python
from selenium import webdriver

chrome_options = webdriver.ChromeOptions()
chrome_options.page_load_strategy = 'normal'
driver = webdriver.Chrome(options=chrome_options)
try:
    driver.get("http://www.baidu.com")
finally:
    driver.quit()
```

```python
from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities

desired_capabilities = DesiredCapabilities.CHROME
desired_capabilities['pageLoadStrategy'] = 'normal'
driver = webdriver.Chrome()
try:
    driver.get("http://www.baidu.com")
finally:
    driver.quit()
```


# eager

> 仅下载和解析html内容

这将使Selenium WebDriver保持等待, 直到完全加载并解析了HTML文档, 该策略无关样式表, 图片和subframes的加载.

设置为 eager 时, Selenium WebDriver保持等待, 直至返回 [DOMContentLoaded](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/DOMContentLoaded_event) 事件.

```python
chrome_options.page_load_strategy = 'eager'
# or
desired_capabilities['pageLoadStrategy'] = 'eager'
```

# none

> 仅下载html内容

设置为 none 时, Selenium WebDriver仅等待至初始页面下载完成.

```python
chrome_options.page_load_strategy = 'none'
# or
desired_capabilities['pageLoadStrategy'] = 'none'
```

# 实践

```python
from selenium import webdriver
import time 

for type in ('normal', 'eager', 'none'):
    chrome_options = webdriver.ChromeOptions()
    chrome_options.page_load_strategy = type
    driver = webdriver.Chrome(options=chrome_options)
    start = time.time()
    try:
        driver.get("https://www.baidu.com/")
        print(type, time.time() - start)
    finally:
        driver.quit()
```

对比一下耗时，并看不出来差距。。