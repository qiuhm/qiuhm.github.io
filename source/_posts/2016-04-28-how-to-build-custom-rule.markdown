---
layout: post
title: "本地开发oclint自定义规则"
date: 2016-04-28 18:39:31 +0800
comments: true
categories: 
---

### 开发前知识储备
- 1、[利用Scaffolding自动生成rule的模板文件](http://docs.oclint.org/en/stable/devel/scaffolding.html#creating-rules-with-scaffolding)
- 2、[学习clang的ast相关知识](http://clang.llvm.org/docs/IntroductionToTheClangAST.html)
- 3、[visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern)
- 4、[clang AST](http://docs.oclint.org/en/stable/devel/clang.html)
- 5、[学习libtool,oclint基于该工具生成语法树](http://clang.llvm.org/docs/LibTooling.html)

### 开始开发
- 1、使用scaffoldRule命令，快速创建rule
使用oclint-scripts目录下的scaffoldRule创建规则文件
如  ```scaffoldRule -t SourceCodeReader -c log -n customerRule -p 3 --test CustomerSample```
- 2、编写规则的逻辑代码

### 编译包，copy自定义规则到oclint的安装目录 
- [编译包的详细方法参照](http://qiuhm.github.io/blog/2016/04/28/how-to-build-oclint/)


