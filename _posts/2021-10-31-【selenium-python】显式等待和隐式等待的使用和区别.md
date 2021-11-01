---
layout: post
title: 'selenium-python--显式等待和隐式等待的使用和区别'
date: 2021-10-31
author: nangfeng-li
tags: selenium-python
---

> 网上教程挺多，看完还是没太理解，看了官方文档稍微理解了一些，在此记录。<br>
> 部分观点为个人理解，请批判性阅读。如有错误，请指正，万分感谢。<br>
> 参考：<br>
> [webdriver_waits](https://www.selenium.dev/zh-cn/documentation/webdriver/waits/) <br>
> [When to use explicit wait vs implicit wait in Selenium Webdriver?](https://stackoverflow.com/questions/10404160/when-to-use-explicit-wait-vs-implicit-wait-in-selenium-webdriver) <br>
> [Selenium - Is it okay to mix implicit wait and explicit wait like this?](https://stackoverflow.com/questions/60762906/selenium-is-it-okay-to-mix-implicit-wait-and-explicit-wait-like-this) <br>
> [ selenium-python中文文档  5.等待事件](https://python-selenium-zh.readthedocs.io/zh_CN/latest/5.Waits/)


# Explicit Waits（显式等待）

> 显示等待 是Selenium客户可以使用的命令式过程语言。它们允许您的代码暂停程序执行，或冻结线程，直到满足通过的 条件 。这个条件会以一定的频率一直被调用，直到等待超时。这意味着只要条件返回一个假值，它就会一直尝试和等待

> 由于显式等待允许您等待条件的发生，所以它们非常适合在浏览器及其DOM和WebDriver脚本之间同步状态。

> 为了弥补我们之前的错误指令集，我们可以使用等待来让 findElement 调用等待直到脚本中动态添加的元素被添加到DOM中:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.get("https://www.baidu.com/")
try:
    WebDriverWait(driver, timeout=5, poll_frequency=1, ignored_exceptions=None).until(
        EC.visibility_of_element_located((By.ID, "kw")), message='显式等待超时')
finally:
    driver.quit()
```

### 参数

- timeout：超时时间（最大等待时间）
- poll_frequency：轮询间隔（默认0.5s）
- ignored_exceptions：忽略例外情况（None默认忽略NoSuchElementException）
- message：自定义报错信息

> 如果条件失败，例如从未得到条件为真实的返回值，等待将会抛出/引发一个叫 TimeoutException 的错误/异常。

> 参考源码自己写了一个等待，实现显式等待的功能。

```python
from selenium.common.exceptions import TimeoutException
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time


def explicit_wait(driver, timeout, poll_frequency=0.5, message: str = None):
    end_time = time.time() + timeout
    while True:
        try:
            return driver.find_element_by_id("kw").is_displayed()
        except Exception as msg:
            error_msg = repr(msg)
        time.sleep(poll_frequency)
        if time.time() > end_time:
            break
    raise TimeoutException(message)


driver = webdriver.Chrome()
driver.get("https://www.baidu.com/")
try:
    explicit_wait(driver, 5, 1, '显式等待超时')
finally:
    driver.quit()
```

# Implicit Waits（隐式等待）

> 隐式等待是告诉WebDriver如果在查找一个或多个不是立即可用的元素时轮询DOM一段时间。<br>
> 默认设置为0，表示禁用。一旦设置好，隐式等待就被设置为会话的生命周期(适用于所有driver.find_element_by_*())。

```python
from selenium import webdriver

driver = Chrome()
driver.implicitly_wait(10)
driver.get("http://somedomain/url_that_delays_loading")
my_dynamic_element = driver.find_element(By.ID, "myDynamicElement")
```

> 如超过最大时间失败，等待将会抛出/引发一个叫 NoSuchElementException 的错误/异常。


# 区别

### 显式等待

> 检查存在性、可见性、交互性和许多其他东西——动态地等待<br>
> 明确的行为表现 在本地的selenium运行(你选择的编程语言) 可以在任何你能想到的条件下工作 返回成功或者超时 可以定义元素的缺失为条件 可以定制重试间隔，可以忽略某些异常

- 记录和定义行为。
- 在selenium的本地部分运行（使用您的代码语言）。
- 在任何你能想到的情况下都能工作。
- 返回成功或超时错误。
- 可以将缺少元素定义为成功条件。
- 可以自定义要忽略的重试和异常之间的延迟。

### 隐式等待

> 只关心元素是否存在<br>
> 不明确的行为表现，同一个问题依赖于不同的操作系统，不同的浏览器，不同的selenium版本会有各种不同的表现 在远程的selenium上运行(控制浏览器的那部分). 只能在寻找元素的函数上工作 返回找到元素或者（在超时以后）没有找到 如果检查元素缺失那么总是会等待到超时 除了时间啥都不能指定

- 未记录和实际上未定义的行为。
- 运行在selenium的远程部分（控制浏览器的部分）。
- 仅适用于查找元素方法。
- 返回找到的元素或（超时后）找不到。
- 如果检查是否缺少元素，则必须一直等到超时。
- 除全局超时外，无法自定义。

> 两个代码示例执行相同的操作。找到某个元素，10秒后找不到就放弃。隐式等待只能做到这一点。它只能尝试查找超时的元素。显式等待的优势在于它可以等待各种条件。还可以自定义超时并忽略某些异常。

# 警告:
> 不要混合使用隐式和显式等待。这样做会导致不可预测的等待时间。例如，将隐式等待设置为10秒，将显式等待设置为15秒，可能会导致在20秒后发生超时。

混合使用可参考：[Selenium - Is it okay to mix implicit wait and explicit wait like this?](https://stackoverflow.com/questions/60762906/selenium-is-it-okay-to-mix-implicit-wait-and-explicit-wait-like-this)
