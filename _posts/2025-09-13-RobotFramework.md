---
layout: post
title:  "RobotFramework"
date:   2025-09-13 12:11:00 +0800
categories: 软件测试
tags: RF 软件测试  
author: PandHedge
mathjax: true
---

* content
{:toc}


## RobotFramework





### 一、RobotFramework(简称RF)的简介和特点

rf基于python开发的、可拓展的，以关键字驱动的自动化测试框架

**数据驱动**：把测试用例的数据放到excel\yaml里面，通过修改数据，来打倒控制测试用例的执行过程

**关键字驱动**:把项目中的一些业务逻辑或基本操作封装成一个个关键字，然后调用不同的关键字或关键字组合实现不同的业务逻辑

特点：

- 编写测试用例方便
- 自动生成html格式的测试报告（unittest:htmltestunner,pytest:allure）
- 自动很多类库，支持很多的拓展库
- 可以自定义关键字
- 支持非GUI运行，还可以和jenkins持续集成



### 二、搭建RF的环境

安装

```bash
pip3 install robotframework==3.1
```

生成快捷方式

```bash
pip3 install robotframework-ride
```



### 三、使用

项目-模块-子模块-测试套件-测试用例



**测试套件**：

​	导入外部文件

​	定义变量



### 四、RF类库和扩展库库

#### 1.标准库

测试库

集合库

时间库

截屏库

存储位置：

#### 2.扩展库（通过pip命令安装额外的库）

web自动化：SeleniumLibrary

```
pip install robotframework-seleniumLibrary
```

接口自动化测试：RequestsLibraby

```
pip install robotframework-requestsLibraby
```

app自动化测试:AppiumLibrary

```
pip install robotframework-appiumLibrary
```

### 五、基本使用



关键字不区分大小写

shift + ctrl +

|               |      |      |      |
| ------------- | ---- | ---- | ---- |
| 打印          |      |      |      |
| Log           |      |      |      |
| 定义变量      |      |      |      |
| ${a}          |      |      |      |
| 获取系统时间  |      |      |      |
|               |      |      |      |
| 字符串拼接    |      |      |      |
|               |      |      |      |
| 创建列表      |      |      |      |
|               |      |      |      |
| 字典关键字    |      |      |      |
|               |      |      |      |
| 获取字典的key |      |      |      |
|               |      |      |      |
|               |      |      |      |

