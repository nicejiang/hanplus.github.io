---
layout:     post
title:      "『Android』 将GitHub项目发布为远程依赖"
subtitle:   "从此可以使用自己的远程依赖库。"
date:       2019-04-29 12:00:00
author:     "HanPlus"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
	- GitHub
---

> 由于新的项目想依赖自己以前写的库，老是本地复制粘贴感觉很麻烦，然后学习了一下发布远程依赖，在此记录一下，也提供一些经验避免踩坑吧~



## 一、发布GitHub项目

> 如果已经了解发布*GitHub*项目请直接跳过这一步。

这里说一下*AS*上传项目到*GitHub*：

#### 1.下载并安装[Git](https://git-scm.com/)。

#### 2.在AS上配置*Git*，`File` > `Settings` > `Version Control` > `Git`。

![配置Git](https://upload-images.jianshu.io/upload_images/10515352-6a7cb290432d3915.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.`File` > `Settings` > `Version Control` > `GitHub`，配置*GitHub*账号：

![配置GitHub账号](https://upload-images.jianshu.io/upload_images/10515352-7c1f1f613b504d2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 4.`VCS` > `Import into Version Control` > `Create Git Repository...`，创建本地代码仓库，选定项目即可：

![创建本地代码仓库](https://upload-images.jianshu.io/upload_images/10515352-88c739c45883f8be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 5.项目上右键，添加文件到本地仓库，如需添加单个文件可在文件上右键然后 `Add`即可：

![添加文件到本地仓库](https://upload-images.jianshu.io/upload_images/10515352-8b71bea3769f1d52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 6.创建*GitHub*远程仓库：

![上传本地仓库到GitHub](https://upload-images.jianshu.io/upload_images/10515352-7ee0a6e7ef934adc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 输入仓库名和是否私有以及仓库描述等：

![QQ截图20191021191444.png](https://upload-images.jianshu.io/upload_images/10515352-639bdf8df04b298e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 7.提交文件到本地仓库并同步到*GitHub*

![提交文件或者文件夹](https://upload-images.jianshu.io/upload_images/10515352-ccf97dcf35630a45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 选择需要提交同步的文件并输入提交信息：

![选择提交文件](https://upload-images.jianshu.io/upload_images/10515352-06e2e1afac72b5dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-  `Commit` 只会上传到本地仓库选择，`Commit and Push` 会在提交到本地仓库的同时同步到*GitHub*，然后就可以在*GitHub*上看到项目了。

![Commit/Commit and Push](https://upload-images.jianshu.io/upload_images/10515352-1e4218c9f30a10ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

PS：关于命令行上传，可以百度或者看这里：[上传本地项目到Github](https://www.jianshu.com/p/083ab0de6808)。



## 二、发布GitHub项目的版本


- 当项目上传完成后，需要在GitHub上发布版本：

![查看版本](https://upload-images.jianshu.io/upload_images/10515352-023c153481d6d70b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![创建版本](https://upload-images.jianshu.io/upload_images/10515352-9d828da551dbf109.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 发布版本，并填写相关信息即可

![发布版本](https://upload-images.jianshu.io/upload_images/10515352-f3835646bdb6fc68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 发布后可查看改项目所有的发布版本

![查看版本](https://upload-images.jianshu.io/upload_images/10515352-190e07ba5e79a343.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 三、发布GitHub版本到[JitPack](https://jitpack.io/)

[JitPack](https://jitpack.io/)是一个远程仓库，将项目版本同步到*JitPack*，之后无需审核即可远程依赖。

- 进入[JitPack](https://jitpack.io/)，使用*GitHub*账号登录。

![GitHub账号登录](https://upload-images.jianshu.io/upload_images/10515352-6eb84656776e39c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 登陆之后可以看到已有的*GitHub*项目，右边是已有的版本，点击`Get it`则[JitPack](https://jitpack.io/)将会开始编译项目。

![开始编译项目](https://upload-images.jianshu.io/upload_images/10515352-d5e40903a364b97e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 是否编译成功可通过`Log`的颜色判断，红色则为失败，绿色为通过，当`Log`为红色的时候，通过远程依赖是找不到的，可以通过点击`Log`图标进行查看编译日志，排查失败的原因。

![是否编译成功](https://upload-images.jianshu.io/upload_images/10515352-0a699266dfeeda7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 编译成功之后，在*AS*中的根`build.gradle`中添加*maven*路径，然后在项目中添加依赖即可。

![添加依赖](https://upload-images.jianshu.io/upload_images/10515352-2a9a56d592d60a56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 如果*Gradle*工具版本大于等于`4.6`。

1) 在根`build.gradle`添加：

```
buildscript { 
  dependencies {
	classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1' // Add this line
  }
}
```

2) 在`library`的`build.gradle`中添加，`${YourUsername}`是远程依赖的项目名：

```
 apply plugin: 'com.github.dcendents.android-maven'  

 group='com.github.${YourUsername}'
```

3) 重新提交*GitHub*并发行版本，且同步到*JitPack*即可。



