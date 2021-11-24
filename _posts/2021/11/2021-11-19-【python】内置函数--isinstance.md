---
layout: post 
title: '【python】内置函数--isinstance' 
date: 2021-11-19 
author: nangfeng-li 
tags: python
---

## isinstance()

- 文档描述

        判断一个对象是否是一个已知的类型，类似 type()。
  
        isinstance() 与 type() 区别：
        type() 不会认为子类是一种父类类型，不考虑继承关系。
        isinstance() 会认为子类是一种父类类型，考虑继承关系。
        如果要判断两个类型是否相同推荐使用 isinstance()。

- 语法

        isinstance(object, classinfo)

- 参数

        object -- 判断对象
        *iterable -- 直接或间接类名、基本类型或者由它们组成的元组。

- 返回

        True or False

- 实例

```python
    a = 2
    isinstance (a,int)  # True
    isinstance (a,str)  # False
    isinstance (a,(str,int,list)) # True
```

