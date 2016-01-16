---
layout: post
title: "OCLint(静态扫描工具)介绍"
date: 2016-01-14 12:47:57 +0800
comments: true
categories: 测试工具
---
###一、OCLint是什么
  OCLint是一款静态扫描工具，可以扫描C,C++,OC。扫描出的主要问题包括：<br>
空的if/else/try/catch/finally 语句<br>
未使用的代码，包括未使用的局部变量、传参<br>
复杂的代码<br>
switch语句里break未加 等<br>
###二、 OCLint安装
####1.下载编译包
附上下载
[OCLint官方包](https://github.com/oclint/oclint/releases)、
[本人整理后的包，筛选了自定义规则](https://raw.githubusercontent.com/qiuhm/Resource/master/download/oclint.zip)<br>
下载后解压存到某个文件夹，我是放到~/libtool,所以我的OCLINT_HOME为~/libtool/oclint
####2.配置环境变量
修改~/.bash_profile(或/etc/profile)文件（如无,可创建一个）,添加如下脚本<br>
OCLINT_HOME=~/libtool/oclint<br>
PATH=$OCLINT_HOME/bin:$PATH
####3.配置ocLint配置文件（非必须）
#####a.全局配置文件
该文件存储在```$(/path/to/bin/oclint)/../etc/oclint```，对整个系统生效，由于我的oclint路径为```~/libtool/oclint/bin/oclint```,则我的全局oclint文件路径为```~/libtool/oclint/bin/etc/oclint```
#####b.用户配置文件
新建.oclint文件，存于～目录下，该配置文件对该用户生效
#####c.项目级配置文件
新建oclint文件，放在project的主目录
#####d.配置文件优先级
项目级配置文件>用户配置文件>全局配置文件
###三、OCLint安装目录解析
oclint<br>
|-bin<br>
|-lib<br>
|---clang<br>
|-----3.7.0<br>
|-------include<br>
|-------lib<br>
|---oclint<br>
|-----rules #oclint默认的规则目录<br>
|-----customRules  #我配置的自定义规则文件夹<br>
|-----reporters
###四、OCLint使用
####1、OCLint直接嵌入xcode工程
[OCLint嵌入到Xcode IDE](http://qiuhm.github.io/blog/2016/01/16/oclintqian-ru-dao-xcodejiao-cheng/)
####2、OCLint接入jenkins持续集成
（未完待续）
####3、OCLint配置文件解析
（未完待续）
####4、OCLint规则解析
（未完待续）