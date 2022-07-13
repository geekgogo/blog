---
title: "Pycharm将设置导入至github"
date: 2019-06-17T10:46:09+08:00
draft: false
tags: ["pycharm"]
---

### 前言

> 每个程序员对于自己的 ide 都有独特的审美。每次在新的环境中都要配置一次熟悉的 ide 界面尤其麻烦。拿
> pycharm 来举例，传统的做法是将配置好的 ide 设置导出，保存一份，然后再在新的环境中导出。这样也会增
> 加新的麻烦，导出的配置文件丢失咋办？这时就需要用到 github 了，pycharm 有专门的选项将设置保存到
> github 上。

#### 操作步骤如下

1. 在 github 上新建一个仓库

2. 申请一个 github 的 Access token，点
   击[这里](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line)查
   看申请步骤，申请成功后记得妥善保管，此 access token 只显示一次。

3. 如下图，找到 pycharm 的 settings repository

    ![](/images/2019-06-11-006tNbRwly1fygr24eh9qj30ga0hxwm3.jpg)

4. 出现让你输入仓库地址，将第一步的地址填入即可。

5. 第一次设置会出现输入 access token 框，将第 2 步申请到的填入。

6. 之后选择<strong>Overwrite Remote</strong>，覆盖到远程地址，这里相当于 git 的 push 操作

    ![](/images/2019-06-11-006tNbRwly1fygre9ym58j30b7038q36.jpg)

7. 在新的环境上同步时选择<strong>Overwrite Local</strong>即可。

**ps：以上参考[此文档](https://yuhao.space/blog/2017/10/pycharm-setting-base/)，里面有记录更详细的内
容，若有疑问可移步阅读参考**
