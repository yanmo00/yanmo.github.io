---
title: "Android"
date: 2023-12-22T16:00:01+08:00
draft: false
tags:
  - Android
  - FE
categories:
  - 语言基础
  - Android
---

# 一、项目结构分析

### 1.Project 项目结构

##### 01 . gradle 和.idea

​ 自动生成的一些文件，不用手动编辑。

##### 02 . app

​ 项目中的代码、资源等内容

##### 03 . build

​ 在编译时自动生成的文件

##### 04 . gradle

​ 包含了 gradle wrapper 的配置文件，使用 gradle wrapper 的方式不需要提前将 gradle 下载好，而是会自动根据本地的缓存情况决定是否需要联网下载 gradle 。Andr oid Studio 默认就是启用 gradle wrapper 方式的，如果需要更改成离线模式，可以点击 Andr oid Studio 导航栏 →File→Settings→Build, Ex ecution,Deployment→Gradle ，进行配置更改。

##### 05 . gitignore

​ 这个文件是用来将指定的目录或文件排除在版本控制之外的

##### 06 . build.gradle

​ 这是项目全局的 gradle 构建脚本，通常这个文件中的内容是不需要修改的。稍后我们将会详细分析 gradle 构建脚本中的具体内容。

##### 07 . gradle.properties

​ 这个文件是全局的 gradle 配置文件，在这里配置的属性将会影响到项目中所有的 gradle 编译脚本。

##### 08 . gradlew 和 gradlew .bat

​ 这两个文件是用来在命令行界面中执行 gradle 命令的，其中 gradlew 是在 Linux 或 Mac 系统
中使用的，gradlew .bat 是在 Windows 系统中使用的。

##### 09 . HelloWorld.iml

​ iml 文件是所有 IntelliJ IDEA 项目都会自动生成的一个文件（Andr oid Studio 是基于 IntelliJIDEA 开发的），用于标识这是一个 IntelliJ IDEA 项目，我们不需要修改这个文件中的任何内容。

##### 10 . local.properties

​ 这个文件用于指定本机中的 Andr oid SDK 路径，通常内容是自动生成的，我们并不需要修改。除非你本机中的 Andr oid SDK 位置发生了变化，那么就将这个文件中的路径改成新的位置即可。

##### 11 . settings.gradle

​ 这个文件用于指定项目中所有引入的模块。由于 HelloWorld 项目中只有一个 app 模块，因此该文件中也就只引入了 app 这一个模块。通常情况下，模块的引入是自动完成的，需要我们手动修改这个文件的场景可能比较少。

### 2.app 目录下的结构

##### 01 . build

​ 这个目录和外层的 build 目录类似，也包含了一些在编译时自动生成的文件，不过它里面的内容会更加复杂，我们不需要过多关心。

##### 02 . libs

​ 如果你的项目中使用到了第三方 jar 包，就需要把这些 jar 包都放在 libs 目录下，放在这个目录下的 jar 包会被自动添加到项目的构建路径里。

##### 03 . androidTest

​ 此处是用来编写 Andr oid Test 测试用例的，可以对项目进行一些自动化测试。

##### 04 . java

​ 毫无疑问，java 目录是放置我们所有 Java 代码的地方（Kotlin 代码也放在这里），展开该目录，你将看到系统帮我们自动生成了一个 MainActivity 文件。

##### 05 . res

​ 这个目录下的内容就有点多了。简单点说，就是你在项目中使用到的所有图片、布局、字符串等资源都要存放在这个目录下。当然这个目录下还有很多子目录，**图片放在 drawable 目录下，布局放在 layout 目录下，字符串放在 values 目录下**，所以你不用担心会把整个 res 目录弄得乱糟糟的。

##### 06 . AndroidManifest.xml

​ 这是整个 Andr oid 项目的配置文件，你在程序中定义的所有四大组件都需要在这个文件里注册，另外还可以在这个文件中给应用程序添加权限声明。由于这个文件以后会经常用到，
第 1 章 开始启程，你的第一行 Android 代码 40
我们等用到的时候再做详细说明。

##### 07 . test

​ 此处是用来编写 Unit Test 测试用例的，是对项目进行自动化测试的另一种方式。

##### 08 .gitignore

​ 这个文件用于将 app 模块内指定的目录或文件排除在版本控制之外，作用和外层的.gitignor e 文件类似。

##### 09 . app.iml

​ IntelliJ IDEA 项目自动生成的文件，我们不需要关心或修改这个文件中的内容。

##### 10 . build.gradle

​ 这是 app 模块的 gradle 构建脚本，这个文件中会指定很多项目构建相关的配置，我们稍后将会详细分析 gradle 构建脚本中的具体内容。

##### 11 . proguard-rules.pro

​ 这个文件用于指定项目代码的混淆规则，当代码开发完成后打包成安装包文件，如果不希望代码被别人破解，通常会将代码进行混淆，从而让破解者难以阅读。

### 3.res 目录下的结构

##### 分类：

- **“drawable”** 开头的目录——图片
- **“mipmap”** 开头的目录——应用图标
- **“values”** 开头的目录——字符串、样式、颜色等配置
- **“layout”** 开头的目录——布局文件

##### 不同分辨率的版本

- xxx-hdpi 、xxx-xhdpi 、xxx-xxhdpi
- 理想状况下，程序运行的时候，会自动根据当前运行设备分辨率的高低选择加载哪个目录下的图片
- 一般放 drawable-xxhdpi，因为这是最主流的设备分辨率目录。

##### res 资源的引用方式

- 在代码中通过 R.string.app_name 可以获得该字符串的引用。
- 在 XML 中通过@string/app_name 可以获得该字符串的引用。

### 4.日志工具 Log

##### Log.v()

- 用于打印那些最为琐碎的、意义最小的日志信息。对应级别 verbose ，是 Android 日志里面级别最低的一种。

##### Log.d()

- 用于打印一些调试信息，这些信息对你调试程序和分析问题应该是有帮助的。对应级别 debug ，比 verbose 高一级。

##### Log.i()

- 用于打印一些比较重要的数据，这些数据应该是你非常想看到的、可以帮你分析用户行为的数据。对应级别 info ，比 debug 高一级。

##### Log.w()

- 用于打印一些警告信息，提示程序在这个地方可能会有潜在的风险，最好去修复一下这些出现警告的地方。对应级别 warn ，比 info 高一级。

##### Log.e()

- 用于打印程序中的错误信息，比如程序进入了 catch 语句中。当有错误信息打印出来的时候，一般代表你的程序出现严重问题了，必须尽快修复。对应级别 error ，比 warn 高一级。

```kotlin
## Log.d()方法中传入了两个参数：第一个参数是tag，一般传入当前的类名就好，主要用于对打印信息进行过滤；第二个参数是msg，即想要打印的具体内容。

Log.d("MainActivity", "onCreate execute")
```
