---
layout: post
title: "利用facebook/infer工具扫描oc代码"
date: 2015-12-31 17:52:53 +0800
comments: true
categories: test-tools
---
>最近在研究facebook的开源工具infer，它是一个静态扫描工具，可以分析 Objective-C， Java 或者 C 代码，我按照官方说明在本地进行了安装，遇到了很多环境的问题，把安装说明详细的记录下来，供大家参考。
###一、安装依赖
>需要安装如下依赖：

```
- opam >= 1.2.0 
- Python 2.7
- Java (only needed for the Java analysis)
- clang in Xcode command line tools. You can install them with the command：xcode-select --install
(only needed for the C/Objective-C analysis)
- Xcode >= 6.1 (only needed for the C/Objective-C analysis)
- autoconf >= 2.63 and automake >= 1.11.1 (if building from git)
```
>我是macx os环境，基本是用homebrew工具安装依赖的，建议大家使用该工具，省去了一系列配置环境变量的事。
###二、下载安装预编译包
####1.下载
>该预编译包包含clang and facebook-clang-plugins，减少自己编译clang和facebook-clang-plugins的时间。
>[下载链接](https://github.com/facebook/infer/releases)
>建议下载最新的包，格式为infer-osx-v0.5.0.tar.xz，解压后存到你想要放置的目录（我放在~/libtool）
<!-- more -->
####2.设置环境变量
>将/~/libtool/infer/infer/bin加到环境变量里
```
sudo vi /etc/profile
```
```
INFER_HOME=/～/libtool/infer/infer
PATH=$INFER_HOME/bin:$PATH
```
>将~替换成你的主目录路径
####3.build infer
```
cd /～/libtool/infer
./build-infer.sh
```
>大概等1分钟左右，没有报错的话，则infer安装完成。如果有报错，可能是少了某些依赖，需要根据补全相关的依赖，再重新build infer。
###三、运行example
####1.分析单个文件
```
cd /～/libtool/infer/examples/ios_hello/HelloWorldApp
infer -- clang -c Hello.m
```
>执行结果如下：
>![单个文件的扫描结果](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/infer/single.jpg)
####2.分析整个项目（本人做iOS的，以iOS为例）
```
cd /~/libtool/infer/examples/ios_hello
xcodebuild -target HelloWorldApp -configuration Debug -sdk iphonesimulator clean
infer -- xcodebuild -target HelloWorldApp -configuration Debug -sdk iphonesimulator
```
>执行结果如下：
>![项目的扫描结果](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/infer/project.jpg)
###四、执行inferTraceBugs查看问题
>切换到存在infer-out目录的文件夹，执行
```
inferTraceBugs --html
```
>点击打开生成的html，大致如图
>![html报告](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/infer/html.jpg)

>附录
>>1.[infer详细介绍](http://fbinfer.com/)
>>2.[facebook/infer源码](https://github.com/facebook/infer)

