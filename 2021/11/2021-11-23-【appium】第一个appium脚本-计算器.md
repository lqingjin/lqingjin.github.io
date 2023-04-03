---
layout: post
title: '【appium】第一个appium脚本-计算器'
date: 2021-11-23
author: nangfeng-li
tags: appium
---

> 简单使用,计算9+9

- 获取设备名称

```shell
adb devices
```

![](https://nanfeng-li.github.io/assets/img/2021/1123/devices_name.png)

- 获取调试应用信息

```shell
adb shell dumpsys window w|findstr \/|findstr name=
```

![](https://nanfeng-li.github.io/assets/img/2021/1123/find_appinfo.png)

- python脚本

```python
from appium import webdriver

def calculator():
    """9+9"""
    desired_caps = {
        "platformName": "Android",
        "deviceName": "52ec8347",
        "platformVersion": "8.0", 
        "appPackage": "com.oneplus.calculator",
        "appActivity": "com.oneplus.calculator.Calculator"
    }
    driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
    driver.find_element_by_id('com.oneplus.calculator:id/digit_9').click()
    driver.find_element_by_id('com.oneplus.calculator:id/op_add').click()
    driver.find_element_by_id('com.oneplus.calculator:id/digit_9').click()
    driver.find_element_by_id('com.oneplus.calculator:id/eq').click()

if __name__ == '__main__':
    calculator()
```
