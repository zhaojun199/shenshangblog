---
title: react-native windows 环境搭建
author: 参商
date: 2019-12-26 11:33:00 +0800
categories: [react]
tags: [react-native]
---

## 平台
开发平台：  Windows

目标平台： iOS Android

## 安装依赖

### Node, Python2, JDK

Node 的版本必须大于等于 10

python 的版本必须为 2.x（不支持 3.x）

JDK 的版本必须是 1.8（目前不支持 1.9 及更高版本）

设置 npm 镜像（淘宝源）

> 不要使用 cnpm！cnpm 安装的模块路径比较奇怪，packager 不能正常识别！


``` 
nvm install 12.14.0
nvm use 12.14.0
``` 
python 2.7
``` 
https://www.python.org/downloads/release/python-2717/ 
``` 

java8：

``` 
https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html 

也可以直接在QQ电脑管家软件里面下载jdk1.8
``` 

### Yarn、React Native 的命令行工具（react-native-cli）

``` 
npm install -g yarn react-native-cli
``` 

### Android 开发环境

#### 安装 Android Studio
[http://www.android-studio.org/](http://www.android-studio.org/)

安装的时候一直下一步就行了

#### 安装SDK

**勾选以下组件**

- Android SDK
- Android SDK Platform
- Performance (Intel ® HAXM) (AMD 处理器看这里)
- Android Virtual Device

![](https://img2018.cnblogs.com/blog/1266852/201912/1266852-20191226211306657-470537725.png)

#### 安装 Android SDK
在 SDK Manager 中选择"SDK Platforms"选项卡，然后在右下角勾选"Show Package Details"。展开Android 9 (Pie)选项，确保勾选了下面这些组件（重申你必须使用稳定的翻墙工具，否则可能都看不到这个界面）：

Android SDK Platform 28
Intel x86 Atom_64 System Image（官方模拟器镜像文件，使用非官方模拟器不需要安装此组件）

![](https://img2018.cnblogs.com/blog/1266852/201912/1266852-20191226211338480-2093472751.png)

然后点击"SDK Tools"选项卡，同样勾中右下角的"Show Package Details"。展开"Android SDK Build-Tools"选项，确保选中了 React Native 所必须的28.0.3版本。你可以同时安装多个其他版本。

最后点击"Apply"来下载和安装这些组件。

#### 配置 ANDROID_HOME 环境变量
React Native 需要通过环境变量来了解你的 Android SDK 装在什么路径，从而正常进行编译。

打开控制面板 -> 系统和安全 -> 系统 -> 高级系统设置 -> 高级 -> 环境变量 -> 新建，创建一个名为ANDROID_HOME的环境变量（系统或用户变量均可），指向你的 Android SDK 所在的目录（具体的路径可能和下图不一致，请自行确认）：

![](https://img2018.cnblogs.com/blog/1266852/201912/1266852-20191226211426061-1279884595.png)

SDK 默认是安装在下面的目录：

``` 
c:\Users\你的用户名\AppData\Local\Android\Sdk 
``` 

你可以在 Android Studio 的"Preferences"菜单中查看 SDK 的真实路径，具体是`Appearance & Behavior → System Settings → Android SDK`。

#### 把 platform-tools 目录添加到环境变量 Path 中

打开控制面板 -> 系统和安全 -> 系统 -> 高级系统设置 -> 高级 -> 环境变量，选中Path变量，然后点击编辑。点击新建然后把 platform-tools 目录路径添加进去。

此目录的默认路径为：

``` 
c:\Users\你的用户名\AppData\Local\Android\Sdk\platform-tools 
``` 

### 创建新项目
使用 React Native 命令行工具来创建一个名为"rnTest"的新项目：

react-native init rnTest

### 准备 Android 设备

#### 使用 Android 模拟器
你可以使用 Android Studio 打开项目下的"android"目录，然后可以使用"AVD Manager"来查看可用的虚拟设备，它的图标看起来像下面这样：

![](https://img2018.cnblogs.com/blog/1266852/201912/1266852-20191226211506701-1403437204.png)

如果你刚刚才安装 Android Studio，那么可能需要先创建一个虚拟设备。点击"Create Virtual Device..."，然后选择所需的设备类型并点击"Next"，然后选择Pie API Level 28 image.

### 编译并运行 React Native 应用
#### 连接海马玩模拟器
下载海马玩模拟器

打开cmd，输入命令连接模拟器

``` 
打开cmd,输入：adb connect 127.0.0.1:26944。如下：

C:\Users\Administrator>adb connect 127.0.0.1:26944
connected to 127.0.0.1:26944 
``` 

确保你先运行了模拟器或者连接了真机，然后在你的项目目录中运行react-native run-android：

``` 
cd rnTest
react-native start
``` 

``` 
react-native run-android  
``` 

如果配置没有问题，你应该可以看到应用自动安装到设备上并开始运行。注意第一次运行时需要下载大量编译依赖，耗时可能数十分钟。此过程严重依赖稳定的翻墙工具，否则将频繁遭遇链接超时和断开，导致无法运行。

#### 查看console打印
``` 
react-native log-android
``` 