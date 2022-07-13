---
title: "关闭Adobe Creative Cloud自启动"
date: 2019-06-17T10:51:36+08:00
draft: false
tags: ["Mac"]
---
### 前言

> macOS 系统安装adobe家的软件时（如photoshop）会自动安装adobe creative cloud，令人厌烦的是这玩意儿会随着电脑自启动，最新的版本已经无法在界面找到关闭自启动的选项了，所以需要使用命令行来关闭，几个命令就可搞定。

### 操作如下

#### 打开终端，按照需要输入以下命令

**禁用**

```
launchctl unload -w /Library/LaunchAgents/com.adobe.AdobeCreativeCloud.plist
```

**启用**

```
launchctl load -w /Library/LaunchAgents/com.adobe.AdobeCreativeCloud.plist
```
