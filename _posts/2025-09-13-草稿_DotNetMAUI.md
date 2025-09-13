---
layout: post
title:  ".Net MAUI"
date:   2025-09-13 12:11:00 +0800
categories: 后端
tags: .Net 
author: PandHedge
mathjax: true
---

* content
{:toc}


# 使用 .NET MAUI 生成移动应用和桌面应用

.NET MAUI 是一种多平台框架，用于使用 C# 和 **XAML** (Extensible Application Markup Language) 创建本机桌面和移动应用。 借助 .NET MAUI（多平台应用程序用户界面），可设计能够在 Windows、Android、iOS、iPadOS 和 macOS 上运行的移动应用。

## 描述 .NET MAUI 体系结构

.NET MAUI（多平台应用程序用户界面）的目的是简化多平台应用开发。 使用 .NET MAUI，可以使用单个项目创建多平台应用，但可以根据需要添加特定于平台的源代码和资源。 .NET MAUI 的主要目的是使你能够在单个代码库中实现尽可能多的应用程序逻辑和 UI 布局。

## 什么是 .NET MAUI 技术堆栈？

.NET 提供了一系列特定于平台的框架，用于创建应用：.NET for Android、.NET for iOS（和 iPadOS）、.NET for Mac 和 WinUI 3（使用 Windows 应用 SDK）。 这些框架都具有访问同一个 .NET 基类库 (BCL) 的权限。 该库提供了创建和管理资源，以及从代码中抽象出基础设备的详细信息的功能。 BCL 依赖于 .NET 运行时来为代码提供执行环境。 Mono，一种 .NET 运行时的开源实现，可实现 Android、iOS（以及 iPadOS）和 macOS 环境。 在 Windows 上，Win32 起到相同的作用，只是它针对 Windows 平台进行了优化。

![示意图显示 .NET MAUI 技术堆栈和实现平台特定功能的方式。](https://learn.microsoft.com/zh-cn/training/dot-net-maui/build-mobile-and-desktop-apps/media/2-architecture.png)

## .NET MAUI 的工作原理是什么？

.NET MAUI 从 UI 元素的逻辑说明中抽象出该元素的实现。 可以使用 XAML (Extensible Application Markup Language) 描述 UI，这是一种基于 XML 的平台中性语言。

![示意图显示 .NET MAUI 如何将 XAML 控件映射到本机控件。此图展现了 .NET MAUI 控件实现了每个本机处理程序也会实现的接口。](https://learn.microsoft.com/zh-cn/training/dot-net-maui/build-mobile-and-desktop-apps/media/2-button-handler.png)

.NET MAUI 始终为目标设备生成本机代码，因此你可以获得最佳性能。还可以根据偏好使用 C# 代码动态创建 UI。 此方法使你可以根据环境修改布局。 例如，如果用户没有适当的授权级别，你可能不希望显示某些控件

借助 .NET MAUI，可以轻松访问按钮等常用控件。 还可同样轻松地访问其他常用控件（如文本输入字段、标签和日期选取器）。 但是，各个控件仍不足以成为可用于创建丰富应用的良好平台。 .NET MAUI 还提供：

- 用于设计页的精心布局引擎。
- 用于创建丰富导航类型的多种页类型，如抽屉。
- 对数据绑定的支持，以便实现更简洁且可维护性更高的开发模式。
- 创建自定义处理程序，以增强 UI 元素的显示方式的能力。
- 对本机 API 的直接访问，以及与 UI 分离的移动应用和桌面应用的许多常见需求的抽象。 概要库使应用能够访问 GPS、加速计、电池和网络状态等内容。 通过此库，还可以使用在移动开发中常见的数十种传感器和服务。

# 在 Visual Studio 中创建 .NET MAUI 项目

## .NET MAUI 项目结构和应用程序启动

项目内容包括以下项：

- App.xaml。 此文件定义应用在 XAML (Extensible Application Markup Language) 布局中使用的应用程序资源。 默认资源位于 `Resources` 文件夹中，并为每个 .NET MAUI 内置控件定义应用范围内的颜色和默认样式。 在此处，你会看到将合并在一起的两个资源字典：

```xaml
<?xml version = "1.0" encoding = "UTF-8" ?>
<Application xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MyMauiApp"
             x:Class="MyMauiApp.App">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="Resources/Colors.xaml" />
                <ResourceDictionary Source="Resources/Styles.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

- App.xaml.cs。 此文件是 App.xaml 文件的代码隐藏文件。 它定义 App 类。 此类表示运行时的应用程序。 该类创建一个初始窗口并将其分配给 `MainPage` 属性；此属性确定应用程序开始运行时显示哪个页面。 此外，此类使你能够替代常见的平台中性应用程序生命周期事件处理程序。 事件包括 `OnStart`、`OnResume` 和 `OnSleep`。 这些处理程序定义为 `Application` 基类的成员。 以下代码显示了默认模板的示例，以及替代这些事件的能力：

```xaml
public partial class App : Application
{
    public App()
    {
        InitializeComponent(); // 初始化XAML中定义的组件
    }

    // 创建应用的主窗口
    protected override Window CreateWindow(IActivationState? activationState)
    {
        return new Window(new AppShell()); // 使用AppShell作为主页面
    }

    // 应用生命周期事件
    protected override void OnStart()
    {
        base.OnStart(); // 调用基类实现
        // 可在此添加启动逻辑
    }

    protected override void OnResume()
    {
        base.OnResume(); // 调用基类实现
        // 可在此添加恢复逻辑
    }

    protected override void OnSleep()
    {
        base.OnSleep(); // 调用基类实现
        // 可在此添加休眠逻辑
    }
}
```

- MainPage.xaml。 此文件包含用户界面定义。 MAUI 应用模板生成的示例应用包括两个标签、一个按钮和一个图像。 这些控件是使用包含在 `ScrollView` 中的 `VerticalStackLayout` 排列的。 `VerticalStackLayout` 元素可垂直排列控件（堆叠显示），而 `ScrollView` 提供滚动条，当视图太大而无法在设备上显示时可使用该滚动条。 你打算将此文件的内容替换为自己的 UI 布局。 如果有多页应用，还可以定义更多 XAML 页面。

  ```xaml
  <?xml version="1.0" encoding="utf-8" ?>
  <ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
              xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
              x:Class="MyMauiApp.MainPage">
  
      <ScrollView>
          <VerticalStackLayout
              Padding="30,0"
              Spacing="25">
              <Image
                  Source="dotnet_bot.png"
                  HeightRequest="185"
                  Aspect="AspectFit"
                  SemanticProperties.Description="dot net bot in a hovercraft number nine" />
  
              <Label
                  Text="Hello, World!"
                  Style="{StaticResource Headline}"
                  SemanticProperties.HeadingLevel="Level1" />
  
              <Label
                  Text="Welcome to &#10;.NET Multi-platform App UI"
                  Style="{StaticResource SubHeadline}"
                  SemanticProperties.HeadingLevel="Level2"
                  SemanticProperties.Description="Welcome to dot net Multi platform App U I" />
  
              <Button
                  x:Name="CounterBtn"
                  Text="Click me" 
                  SemanticProperties.Hint="Counts the number of times you click"
                  Clicked="OnCounterClicked"
                  HorizontalOptions="Fill" />
          </VerticalStackLayout>
      </ScrollView>
  
  </ContentPage>
  ```

  
