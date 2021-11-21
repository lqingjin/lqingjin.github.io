---
layout: post 
title: '【selenium-python】浏览器启动选项（options）设置' 
date: 2021-11-19 
author: nangfeng-li 
tags: selenium-python
---

```python
from selenium import webdriver

# 加启动配置
chrome_options = webdriver.ChromeOptions()
prefs = {"credentials_enable_service": False, "profile.password_manager_enabled": False}
chrome_options.add_experimental_option("prefs", prefs)  # 关掉密码弹窗
chrome_options.add_argument('--disable-gpu')  # 谷歌文档提到需要加上这个属性来规避bug
chrome_options.add_argument('lang=zh_CN.UTF-8')  # 设置默认编码为utf-8
chrome_options.add_argument('--window-size=1920,1080') # 设置窗口大小
chrome_options.add_argument('--start-maximized')  # 设置浏览器最大化运行
chrome_options.add_argument('--headless')  # 无头模式
chrome_options.add_experimental_option('useAutomationExtension', False)  # 取消chrome受自动控制提示
chrome_options.add_experimental_option("excludeSwitches", ['enable-automation'])  # 取消chrome受自动控制提示
# 模拟手机启动
mobile_emulation = {'deviceName': 'iPhone 6'}
chrome_options.add_experimental_option("mobileEmulation", mobile_emulation)
# 启动浏览器时打开F12
chrome_options.add_argument("--auto-open-devtools-for-tabs")
# 打开浏览器
driver = webdriver.Chrome(options=chrome_options)
```