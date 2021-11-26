---
layout: post 
title: '【requests】获取请求体的Content-Length' 
date: 2021-11-24
author: nangfeng-li 
tags: requests
---

> 接口测试时，有的接口要求传：Content-Length。但len会报错


在 Python 中，不同的字符所占的字节数不同，数字、英文字母、小数点、下划线以及空格，各占一个字节，
而一个汉字可能占 2~4 个字节，具体占多少个，取决于采用的编码方式。
例如，汉字在 GBK/GB2312 编码中占用 2 个字节，而在 UTF-8 编码中一般占用 3 个字节

```python
data = '人生苦短，我用Python'
print(len(data))
print(data.__len__())
print(len(data.encode()))
print(len(data.encode('gbk')))
```
