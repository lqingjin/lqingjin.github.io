---
layout: post 
title: '【python】内置函数--map' 
date: 2021-11-19 
author: nangfeng-li 
tags: python
---

## map()

- 文档描述

        根据函数计算传入的每一个可迭代对象的元素，当最短的可迭代对象耗尽就停止。

- 语法

        map(func, *iterables) --> map object

- 参数

        function -- 函数
        *iterable -- 一个或多个可迭代对象

- 返回
  
        一个可迭代的map对象

- 实例

```python
    def sum(x,y,z):
        return x*y*z
    
    res = map(sum, [1,2,3,4],[10,20,30],[100,200])
    
    print(res)  # 返回可迭代map对象 <map object at 0x00000205313EF070>
    print(list(res))  # 转换为列表 [1000, 8000]
```
