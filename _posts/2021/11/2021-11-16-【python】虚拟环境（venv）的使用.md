---
layout: post 
title: 'python--虚拟环境（venv）的使用' 
date: 2021-11-16 
author: nangfeng-li 
tags: python
---

> 激活虚拟环境后，使用pip install 会将对应的包安装到对应的虚拟环境。
>
> 虚拟环境互相隔离，互不影响。（可以让每一个python项目单独使用一个环境）

> 参考：[官方文档](https://docs.python.org/zh-cn/3/library/venv.html)

#### 安装virtualenv

```
pip install virtualenv
```

#### 创建虚拟环境

```
python -m venv  /path/venv   # 虚拟环境路径及文件夹名称
```

运行此命令将创建目标目录（父目录若不存在也将创建），并放置一个 pyvenv.cfg 文件在其中，文件中有一个 home 键，它的值指向运行此命令的 Python 安装（目标目录的常用名称是 .venv）。它还会创建一个 bin 子目录（在
Windows 上是 Scripts），其中包含 Python 二进制文件的副本或符号链接（视创建环境时使用的平台或参数而定）。它还会创建一个（初始为空的） lib/pythonX.Y/site-packages 子目录（在 Windows
上是 Lib\site-packages）。如果指定了一个现有的目录，这个目录就将被重新使用。

![](https://nanfeng-li.github.io/assets/img/2021/1116/venv_list.png)

venv3.8为Windows，venv3.9为mac

##### pycharm新建虚拟环境⬇️

![](https://nanfeng-li.github.io/assets/img/2021/1116/pycharm_venv.png)

```
#venv帮助
python -m venv -h
```

#### 激活虚拟环境

![](https://nanfeng-li.github.io/assets/img/2021/1116/activate_venv.png)

![](https://nanfeng-li.github.io/assets/img/2021/1116/activate_mac.png)

#### 退出虚拟环境

shell中输入 "deactivate" 可以退出虚拟环境。 Windows：venv\Scripts\deactivate.bat Mac：deactivate

![](https://nanfeng-li.github.io/assets/img/2021/1116/deactivate_mac.png)

