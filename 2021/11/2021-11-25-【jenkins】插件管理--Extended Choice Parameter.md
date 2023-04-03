---
layout: post 
title: '【jenkins】插件管理--Extended Choice Parameter' 
date: 2021-11-25
author: nangfeng-li 
tags: jenkins
---

> [Extended Choice Parameter(扩展选择参数插件)](https://plugins.jenkins.io/extended-choice-parameter/)
>
> 仅部分有使用到的功能记录，后续完善

### 起因

    测试和准生产各应用目前都是通过jenkins部署，部署顺序需按各应用之间依赖执行。
    预期利用jenkins去调用部署，失败发消息并自动重试，因无jenkins权限，故使用
    本地jenkins调用部署jenkins服务。
    后已实现自动获取git改动应用自动部署，在此记录此插件的一些使用过程，以后的场景
    可能会使用到

### 效果

    勾选待部署环境（单选），和待部署服务（多选）。

![](https://nanfeng-li.github.io/assets/img/2021/1125/jenkins_effect.png)
    
### 配置

![](https://nanfeng-li.github.io/assets/img/2021/1125/jenkins_config_env.png)

![](https://nanfeng-li.github.io/assets/img/2021/1125/jenkins_config_services.png)

### 在pipeline中将参数设置为环境变量

    流水线脚本中设置环境变量，根据环境变量进行一些处理判断，也可以将变量传给
    python脚本执行

![](https://nanfeng-li.github.io/assets/img/2021/1125/jenkins_pipeline.png)



