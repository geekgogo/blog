---
title: "Windows右键添加自定义菜单选项"
date: 2019-06-17T10:05:04+08:00
draft: false
tags: ["windows"]
---

> 这篇博客简单介绍如何给 windows 鼠标右键添加自定义的菜单选项，操作步骤如下:

1. 打开运行输入 regedit（打开注册表）

2. 依次定位：`HKEY_CLASSES_ROOT*\shell`

3. 在 shell 项右键新建项，名字为右键时显示的名称

4. 在第 3 步新建的项下继续新建项：`command`

5. 在`command`右侧双击默认，数值数据填写软件的路径与执行文件，例如：

    `“D:\Program Files (x86)\Sublime Text 3\sublime_text.exe” “%1”`

    **%1 是必须的**

![如图](/images/2019-06-11-006tNbRwly1fw818hc3v5j30qn09n75v.jpg)
