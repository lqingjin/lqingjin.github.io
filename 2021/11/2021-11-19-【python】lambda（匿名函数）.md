---
layout: post 
title: '【python】lambda（匿名函数）' 
date: 2021-11-19 
author: nangfeng-li 
tags: python
---


> lambda是一个表达式，一次性使用，函数体比def简单。
>> 优点：减少不能复用的单行函数定义，使代码更加简洁，但是损失了一些易读性。不熟悉的可能会无法理解。


格式： 冒号前是参数，可以有多个，用逗号隔开，冒号右边的为表达式。
lambda返回值是一个函数的地址，也就是函数对象。

```python
sum_res = (lambda x,y:x+y)(1,10)
print(sum_res)
```

or

```python
sum = lambda x,y:x+y
print(sum(1,10))
```

返回lambda函数对象

```python
sum = lambda x,y:x+y
print(sum)
```

用def实现
```python
def sum(x,y):
    return x+y
print(sum(1,10))
```