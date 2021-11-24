---
layout: post 
title: '【python】内置函数--filter' 
date: 2021-11-19 
author: nangfeng-li 
tags: python
---

## filter()

- 文档描述

        根据函数计算传入的每一个可迭代对象的元素进行判断，返回True或False，将返回为True的元素放到新列表中。
        如果函数为None，则返回为True的元素

- 语法

        filter(function or None, iterable) --> filter object

- 参数

        function -- 函数
        *iterable -- 可迭代对象

- 返回

        一个可迭代的filter对象

- 实例

```python
    def is_equal_one(x):
        return x % 2 == 1
    
    res = filter(is_equal_one, [1,2,3,4])
    
    print(res)  # 返回可迭代filter对象 <filter object at 0x000001CE73A6E250>
    print(list(res))  # 转换为列表 [1, 3]
```
