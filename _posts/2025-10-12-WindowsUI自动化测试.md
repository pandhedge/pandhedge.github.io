---
layout: post
title:  "windowsUI自动化测试框架"
date:   2025-10-12 20:18:00 +0800
categories: 软件测试
tags: 软件测试 python  
author: PandHedge
mathjax: true
---
## 一、前言

### 1.起因

### 2.项目要求

- 平台:windows
- 主要要求
  - 完成:windowsUI自动化测试框架预言和搭建
  - 满足
  - 达到
  - 特质
  - 时间

### 3.研制过程

#### 3.1技术选型

### 4.研制成果

#### 4.1框架

`UIAutomation + Python + pytest + Allure  + loguru + Pillow`

| 模块名称       | 核心定位                 | 主要作用                                                                 |
|----------------|--------------------------|--------------------------------------------------------------------------|
| Python         | 核心开发语言             | 提供基础语法支持与丰富库生态，作为所有模块的运行载体，支撑自动化流程开发 |
| UIAutomation   | Windows UI自动化测试库   | 识别Windows平台UI元素（按钮、输入框等），实现点击、输入、控件属性获取等自动化操作 |
| pytest         | 自动化测试执行框架       | 简化测试用例编写，支持参数化、Fixtures、用例分组，批量执行用例并自动断言结果 |
| Allure         | 可视化测试报告生成工具   | 生成美观、详细的测试报告，展示用例状态、执行步骤、日志、截图，支持趋势分析 |
| loguru         | 轻量日志记录库           | 简化日志配置（无需复杂setup），支持控制台/文件输出、日志格式化、分级记录，便于问题定位 |
| Pillow         | Python图像处理库         | 处理图像（如截图裁剪、格式转换、像素验证、添加文字），常用于自动化测试中的截图对比与结果留存 |

#### 4.2代码展示

#### 4.3运行效果

## 二、项目介绍

### 1.测试对象

### 2.技术栈

```yaml
# 核心测试框架与报告
pytest==8.4.1
allure-pytest==2.15.0
# 日志与配置
loguru==0.7.3
configparser==7.2.0  # 配置文件解析
# 数据处理与请求
requests==2.32.4     # HTTP请求处理
openpyxl==3.1.5      # Excel文件读写
# 自动化相关
uiautomation==2.0.29  # UI自动化控制
Pillow==11.3.0        # 图像处理（截图等）
pyautogui
Smtplib				  # 邮件服务
os					  # 系统模块
```

### 3.项目框架说明

#### 文件结构

```bash
Automated_WindowsGUITest_demo
├── .idea\               # IDEA项目配置文件
├── .pytest_cache\       # pytest缓存文件
├── .venv\               # Python虚拟环境
├── common\              # 公共模块目录
│   ├── __init__.py      # 包初始化文件
│   ├── baseInfo.py      # 基础信息和登录模块
│   ├── logOut.py        # 日志输出模块
│   ├── reportOut.py     # 报告生成模块
│   ├── screenShot.py    # 截图功能模块
│   └── sendMain.py      # 邮件发送模块
├── file\                # 测试文件目录
│   ├── test_allure.py   # Allure测试示例
│   └── test_notepad.py  # 记事本测试示例
├── log\                 # 日志存储目录
├── page\                # 页面对象目录
│   └── toolbar.py       # 工具栏页面对象
├── report\              # 报告存储目录
├── requirements.txt     # 项目依赖文件
├── screenshot\          # 截图存储目录
└── testcase\            # 测试用例目录
│   └── test_toorbar.py  # 工具栏测试用例
└── main.py              # 主函数入口
     
```

#### 文件说明
| 文件路径                  | 文件名称         | 功能说明                                                         |
|---------------------------|------------------|------------------------------------------------------------------|
| main.py                   | 主程序入口       | 项目的主要执行入口，负责初始化日志、运行测试用例和生成报告         |
| common/baseInfo.py        | 基础信息模块     | 封装应用程序登录、退出等基础操作                                 |
| common/logOut.py          | 日志输出模块     | 配置和管理项目的日志系统，提供统一的日志记录功能                   |
| common/reportOut.py       | 报告生成模块     | 集成pytest和Allure，负责执行测试用例并生成HTML测试报告             |
| common/screenShot.py      | 截图功能模块     | 提供测试过程中的截图功能，用于保存测试证据                         |
| common/sendMain.py        | 邮件发送模块     | 负责测试报告的邮件发送功能                                       |
| page/toolbar.py           | 工具栏页面对象   | 封装应用程序工具栏的UI元素和操作方法                             |
| testcase/test_toolbar.py  | 工具栏测试用例   | 针对工具栏功能编写的自动化测试用例                               |
| file/test_notepad.py      | 记事本测试示例   | 记事本应用的测试示例脚本                                         |
| file/test_allure.py       | Allure测试示例   | Allure报告功能的测试示例脚本                                     |
| requirements.txt          | 项目依赖文件     | 记录项目所需的第三方库及其版本                                   |

![主要文件及函数分析](C:\Users\lin\Downloads\github\Typora\img\主要文件及函数分析.png)



#### 项目实现流程
1. 初始化阶段 ：
   - main.py中的run_case()函数启动程序
   - logOut.py配置全局日志系统
2. 测试执行阶段 ：
   - reportOut.py中的report_out()调用pytest执行testcase目录下的测试用例
   - test_toorbar.py中的测试用例通过Toolbar类操作应用界面
   - Toolbar类通过baseInfo.py中的InitInfor类获取应用窗口和执行登录
3. 报告生成阶段 ：
   - reportOut.py生成Allure测试报告
   - 自动压缩报告为ZIP文件
   - 可选自动打开报告在浏览器中查看
4. 通知阶段 ：
   
   - main.py调用send_main()函数发送邮件，附件为测试报告


## 三、项目展示





## 四、经验分享

### 用例设计