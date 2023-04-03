---
layout: post 
title: '【jenkins】python脚本获取jenkins变量' 
date: 2021-11-25
author: nangfeng-li 
tags: jenkins
---

> 将jenkins变量传给python脚本

- python脚本

```python
import os

def get_jenkins_env(env_name):
    return os.environ[env_name]

if __name__ == '__main__':
    print('---------------------')
    print('jenkins_environment',get_jenkins_env('SERVICES'))
    print('---------------------')
```

- bat脚本

```shell
@echo off
path\python.exe path/get_jenkins_env.py
pause
```

- pipeline配置

```shell
pipeline {
    agent any
    environment {
        SERVICES = "myservices"
    }
    stages {
        stage('执行bat文件'){
            steps {
              bat '''path\\batname.bat'''
              }
        }
    }
}
```

![](https://nanfeng-li.github.io/assets/img/2021/1125/jenkins_pipeline_env.png)

- 结果

![](https://nanfeng-li.github.io/assets/img/2021/1125/result.png)
