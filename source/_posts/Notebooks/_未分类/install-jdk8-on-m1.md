---
link: https://www.winsonlo.com/it/howto/zulu-jdk8-on-m1/
title: 如何在苹果M1芯片 (Apple Silicon) 上安装 JDK 环境 - Winson LO
description: M1 (Apple Silicon) 使用全新的系统架构，截至2021年8月只有 Zulu JDK 适配了 M1 芯片。甲骨文 (Oracle) 的 JDK 尚未针对苹果 M1 芯片进行适配。我们可以选择 Zulu JDK 来以原生的方式在 M1 芯片的电脑上运行 Java。
keywords: M1 (Apple Silicon)
author: Winson Lo
date: 2021-03-09T09:30:00.000Z
publisher: Winson LO
stats: paragraph=27 sentences=10, words=182
---
【 **最后更新于2021年8月12日**】

M1 使用全新的系统架构，如果你正在使用搭载 M1 芯片的 Macbook 或 Mac mini 电脑，你一定会困惑如何解决 Java 开发环境的问题。截止2021年8月，甲骨文 (Oracle) 的 JDK 尚未针对苹果 M1 芯片进行适配。 因此如果将甲骨文 JDK 安装到 M1 芯片的 Mac 电脑上，Mac OS 将会使用 Rosetta 2 对其进行转译运行，导致生产力性能大幅下跌，同时开发过程中还可能会遇到兼容性问题。

如果想以原生的方式在 M1 芯片的电脑上运行 Java，我们可以选择使用 Azul Zulu 的 Java JDK 来解决改问题。

Zulu JDK 支持的 Java 版本有：8，9，10，11，12，13，14，15。

本次安装我们将选择较为通用的 JDK 8 来搭建环境。

本教程所使用 Mac 之配置详情如下：

* Mac mini ( M1, 2020 )

* 16 GB 内存

* 512 GB 存储内存

* macOS Big Sur 11.2.1

![mac-mini-config.png (586×313) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/mac-mini-config.png?x86153)

## 从 Zulu JDK 官方网站下载 JDK 安装包

```
Java Version: 对应 Java 版本，如：Java 8 (LTS)
Operating Systems: 选择 macOS
Architecture: 选择 ARM 64-bit
Java Package: JDK
```

![zulu-jdk8-download-selection.png (1473×663) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/08/zulu-jdk8-download-selection.png)

本次我将选择 Java 8 (LTS) 的 "8u282b08Zulu: 8.52.0.23" 版本，同时以 .dmg 安装包的方式安装以获得更加便捷的安装体验。

你可[点击这里](https://cdn.azul.com/zulu/bin/zulu8.52.0.23-ca-jdk8.0.282-macosx_x64.dmg)直接下载。 _（链接对应 JDK 版本号: 8u282b08Zulu: 8.52.0.23，格式为 dmg 安装包，如需最新版本或其他格式的安装方式，请直接前往官方下载页面下载。）_

***注意：**请选择 ARM 64-bit(ARMv8) 版本的安装包，切勿选择 x86 64-bit 版本，否则所安装的 JDK 环境后续运行时，Mac 将调用 Rosetta 2 将其转译，使其运行速度变得极为缓慢，性能大幅度下跌。

![image-28.png (1197×354) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-28.png)

## 运行 Zulu JDK 8 安装包

下载完毕后，你将得到一个 Zulu JDK 的安装包，双击以打开并运行它。安装包打开后，双击右边的按钮。

![image-29.png (600×509) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-29.png?x86153)

直接点击「继续」以进入下一步

![image-30.png (620×444) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-30.png?x86153)

选择你希望安装 JDK 的硬盘，通常就是你默认的 Mac 系统盘。然后点击「继续」以进入下一步。

继续点击「安装」，确认将 Zulu JDK 8 安装到 Mac 上。

![image-31.png (620×444) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-31.png?x86153)

点击「安装」后，你需要输入你 Mac 的密码或使用 Apple Watch 以授权安装器将 Zulu JDK 8 安装到你的 Mac 上。

![image-32.png (446×126) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-32.png?x86153)

授权完成后，安装器将会自动将 Zulu JDK 8 安装到你的 Mac 上。

## 大功告成

安装器结束安装后，你将会见到「安装成功」的提示页面。此时，前往 Mac 的终端，并输入：

```bash
java -version
```

执行命令后，当你看到如下输出，则证明 Zulu JDK 8 已成功安装在你的 Mac 上。

![image-38.png (654×371) (winsonlo.com)](https://www.winsonlo.com/wp-content/uploads/2021/03/image-38.png?x86153)

安装完 Zulu JDK 8 后，你可以在搭载 M1 芯片的 Mac 上搭建并部署相关开发环境。

## 开发环境的搭建

欢迎前往查看 M1 (Apple Silicon) 开发环境部署的教程。

[《如何在苹果M1芯片 (Apple Silicon) 上安装 Apache Netbeans 12 以搭建 Web 开发环境》](https://www.winsonlo.com/it/howto/apache-netbeans-12-on-m1/)

## JDR 环境的安装

Azul zulu 同时提供可运行在 M1 芯片上 JDR，安装方法与安装 JDK 相似，前往[下载页面](https://www.azul.com/downloads/?package=jre)选择对应版本的安装包即可。
