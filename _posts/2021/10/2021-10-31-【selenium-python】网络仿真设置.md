---
layout: post
title: 'selenium-python--网络仿真设置'
date: 2021-10-31
author: nangfeng-li
tags: selenium-python
---

> 网络仿真设置(set_network_conditions)

```python
from selenium import webdriver

driver = webdriver.Chrome(executable_path=MAC_DRIVER_PATH, options=chrome_options)
driver.set_network_conditions(offline=False,latency=1000,throughput=500 * 1024)
```

### 参数设置

- > offline=False
  
  网络状态设置，默认为False(不断网），True(断网）
  
- > latency=5  # additional latency (ms)
    
    网络延迟设置，默认5ms(数值越大速度越慢)

- > download_throughput=500 * 1024,  # maximal throughput
  
  下载最大吞吐量500 * 1024 500KB

- > upload_throughput=500 * 1024)  # maximal throughput

  上行速率最大吞吐量500 * 1024 500KB

<br>Note: 'throughput' can be used to set both (for download and upload).

- > throughput=500 * 1024
  
  可同时设置上下行
