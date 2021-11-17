---
layout: post
title: 'appium--安装与配置（windows）'
date: 2021-10-29
author: nangfeng-li
cover: 'https://nanfeng-li.github.io/assets/img/2021/1029/appium.png'
tags: appium
---

> 需提前安装jdk,可查询其他教程

## appium-desktop（免安装）

地址：[https://github.com/appium/appium-desktop/releases](https://github.com/appium/appium-desktop/releases)

下载解压到自定目录即可

![](https://nanfeng-li.github.io/assets/img/2021/1029/appium_desktop.png)

## appium-inspector（免安装）

地址：[https://github.com/appium/appium-inspector/releases](https://github.com/appium/appium-inspector/releases)

同appium-desktop

## 安装android-sdk

ps：免安装版无tools（可能姿势不对），此处选择安装版

地址：[https://www.androiddevtools.cn/](https://www.androiddevtools.cn/)

![](https://nanfeng-li.github.io/assets/img/2021/1029/sdk_tools.png)

### 环境变量配置

系统变量：

```
ANDROID_HOME：D:\Android\android-sdk （sdk安装目录）
```

用户变量PATH：

```
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\tools
```

## 安装Appium-Python-Client

```
pip install Appium-Python-Client
```



