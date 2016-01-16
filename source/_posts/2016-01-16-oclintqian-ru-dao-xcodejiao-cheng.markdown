---
layout: post
title: "oclint嵌入到xcode教程"
date: 2016-01-16 12:01:27 +0800
comments: true
categories: 测试工具
---
前一篇讲了oclint的安装及配置，现在要将oclint运用到实际的项目中，平时iOS开发和测试跟xcode打交道最多，so如何将oclint运用到xcode IDE中呢？
###环境准备
1、oclint已安装配置<br>
2、xcode已安装<br>
3、xcode commandLine已安装
###开始嵌入xcode
1、在工程中新建一个target(比如取名为OCLint)，类型为Aggregate<br>
![新建类型为Aggregate的target](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/oclint/newTarget.png)<br>
2、在该target->Build Phases里新建脚本<br>
![新建script](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/oclint/newPhase.png)<br>
3、编辑脚本如下<br>


```
source ~/.bash_profile

echo "******** start check the oclint ********"
hash oclint &> /dev/null
if [ $? -eq 1 ]; then
echo >&2 "oclint not found, analyzing stopped"
exit 1
fi
echo "******** end check the oclint ********"
echo "******** start clean the environment ********"
cd ${SRCROOT}
rm -rf **/compile_commands.json
rm -rf **/oclint.xml
xctool -scheme ${PROJECT_NAME} clean
echo "******** end clean the environment ********"

echo "******** start building ********"
xctool \
-project ${PROJECT_NAME}.xcodeproj  \
-scheme ${PROJECT_NAME} \
-reporter json-compilation-database:compile_commands.json \
build
echo "******** end building ********"

echo "******** start analyzing ********"
oclint-json-compilation-database -- -report-type xcode
echo "******** end analyzing ********"
```
4、切换scheme到刚才新建的这个target，按快捷键（command+B），开始编译<br>
![扫描出的警告](https://raw.githubusercontent.com/qiuhm/Resource/master/blogpic/oclint/warning.png)<br>
###附录
[https://github.com/qiuhm/OCLintDemo](OCLintDemo)

