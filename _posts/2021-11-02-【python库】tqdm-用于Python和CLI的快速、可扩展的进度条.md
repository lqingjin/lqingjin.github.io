---
layout: post
title: 'python库--tqdm-用于Python和CLI的快速、可扩展的进度条'
date: 2021-11-02
author: nangfeng-li
tags: python库
---

> A Fast, Extensible Progress Bar for Python and CLI <br>
> 参考：[github_tqdm](https://github.com/tqdm/tqdm)

简单使用，后续完善
```python
from tqdm import tqdm
from time import sleep

for i in tqdm(range(int(1000)), ncols=100):
    sleep(0.001)
```

效果

```python
 72%|███████████████████████████████████████████▎                | 721/1000 [00:11<00:04, 63.21it/s]
```