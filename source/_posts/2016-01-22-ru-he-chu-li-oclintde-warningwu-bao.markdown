---
layout: post
title: "如何处理oclint的warning误报"
date: 2016-01-22 17:50:29 +0800
comments: true
categories: test-tools codeAnalyzer
tags: [oclint,warning误报]
keywords: oclint,静态扫描,warning误报
description: 讲解如何处理oclint扫描东西的误报
---
用过静态扫描工具的都知道，在扫描工程时存在误报，比如未使用的参数，但有时iOS的默认写法即如此，那怎么处理呢？</br>方法如下：
###一、在误报的行后面添加注释!OCLINT（推荐）
比如：
```
void a() {
    int unusedLocalVariable; //!OCLINT
}
```
但建议在注释里加下详细说明，为什么要忽略？</br>
推荐写法:
```
void a() {
    int unusedLocalVariable; //!OCLINT(the reason)
}
```
###二、添加注解
添加单条注解，忽略单条规则：
```
__attribute__((annotate("oclint:suppress[unused method parameter]")))
```
添加多条注解，忽略多条规则：
```
__attribute__((annotate("oclint:suppress[high cyclomatic complexity]"), annotate("oclint:suppress[high npath complexity]"), annotate("oclint:suppress[high ncss method]")))
```
忽略所有规则：
```
__attribute__((annotate("oclint:suppress")))
```
示例：
```
bool __attribute__((annotate("oclint:suppress"))) aMethod(int aParameter)
{
    // 忽略整个方法的所有规则的warning
    // like unused aParameter variable and empty if statement
    if (1) {}

    return true;
}

- (IBAction)turnoverValueChanged:
    (id) __attribute__((annotate("oclint:suppress[unused method parameter]"))) sender
    // 忽略sender可能未使用
{
    int i; // won't suppress this one
    [self calculateTurnover];
}

- (void)dismissAllViews:(id)currentView parentView:(id)parentView
   __attribute__((annotate("oclint:suppress")))
   // 忽略整个方法的所有规则的warning
{
    [self dismissTurnoverView];
    // plus 30+ lines of code of dismissing other views
}
```




