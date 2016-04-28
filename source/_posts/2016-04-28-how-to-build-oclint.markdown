---
layout: post
title: "本地编译oclint包"
date: 2016-04-28 17:59:42 +0800
comments: true
categories: oclint test-tools
---
进行自定义规则开发，必须在本地编译oclint的release包或debug包。
### 1、 编译release包
- 进入checkout的oclint目录，再进入到oclint-scripts目录
- 执行```make```

### 2、编译debug包
- 进入checkout的oclint目录，再进入到oclint-scripts目录
- 执行```./ci -reset```
- 再执行```./ci -setup -release```

### 3、编译后的包位置
${oclint-home}/build/oclint-release <br>
![如图](../blogpic/oclint/oclint-release-location.png)


