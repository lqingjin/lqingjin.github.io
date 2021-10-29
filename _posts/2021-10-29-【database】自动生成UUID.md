---
layout: post
title: '【database】自动生成UUID'
date: 2021-10-29
author: nangfeng-li
tags: database PostgreSQL
---

# PostgreSQL

```
create extension "uuid-ossp" ：安装 uuid_generate_v4() 扩展函数
select uuid_generate_v4() 
```

![](https://nanfeng-li.github.io/assets/img/2021/1029/postgresql_uuid.png)