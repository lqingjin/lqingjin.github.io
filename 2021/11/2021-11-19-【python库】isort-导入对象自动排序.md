---
layout: post
title: '【python库】isort-导入对象自动排序'
date: 2021-11-19
author: nangfeng-li
cover: 'https://nanfeng-li.github.io/assets/img/2021/1119/isort.png'
tags: python库
---


> isort your imports, so you don't have to.
> 
> 将导入的对象按类型及字母顺序排序分为多个部分。
> 
> 参考：[isort](https://github.com/PyCQA/isort)


Before isort:

```shell
from my_lib import Object
import os
from my_lib import Object3
from my_lib import Object2
import sys
from third_party import lib15, lib1, lib2, lib3, lib4, lib5, lib6, lib7, lib8, lib9, lib10, lib11, lib12, lib13, lib14
import sys
from __future__ import absolute_import
from third_party import lib3

print("Hey")
print("yo")
```

After isort:

```shell
from __future__ import absolute_import

import os
import sys

from third_party import (lib1, lib2, lib3, lib4, lib5, lib6, lib7, lib8,
                         lib9, lib10, lib11, lib12, lib13, lib14, lib15)

from my_lib import Object, Object2, Object3

print("Hey")
print("yo")
```

### 安装isort

```shell
pip install isort
```

### 使用isort

- 执行指定的文件

```shell
isort pythonfile.py
```

- 当前目录所有文件

```shell
isort .
```

- 查看修改建议但不执行

```shell
isort pythonfile.py --diff

```





