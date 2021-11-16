---
layout: post 
title: "python--r'', b'', u'', f'' 的使用"
date: 2021-11-16 
author: nangfeng-li 
tags: python
---


> r'', b'', u'', f'' 的使用


### r/R:非转义的原始字符串

```python
print(r'input\nxx')

# input\nxx
```

### b:bytes

```python
print(b'input\nxx')

# b'input\nxx'
```

### u/U:表示unicode字符串

```python
print(u'input\nxx')

# input
# xx
```

### f/format():格式化操作

```python
x = 'test'
print(f'input:{x}')

# input:test
```

同

```python
x = 'test'
print('input:%s' % x)
print('input:{}'.format(x))

# input:test
```