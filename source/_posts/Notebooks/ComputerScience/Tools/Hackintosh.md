---
title: Hacintosh Tutorial
date: 2022-02-01 10:00:00
description: 个人的黑苹果安装教程，包括以下机型：惠普zhan66G1Pro、台式机技嘉Z97D3H+i56790K+GTX970Gaming
author: 陌上人如玉
tag: Mac
---

- # Vmware

  ## MacOS 11

  ```Plain%20Text
  smbios.reflectHost= "TRUE"
  hw.model = "MacBookPro16,1"
  board-id="Mac-E1008331FDC96864"
  ```

  [vm安装11.15教程](https://blog.csdn.net/wangchao_cn/article/details/109755360)

  [教程](https://heipg.cn/tutorial/basic-install-hackintosh-walkthrough.html)

  [这可能是对“小白”最友好的黑苹果安装教程（Catalina 10.15.5 安装记录）](https://www.jianshu.com/p/342b322e3841)

  [关于黑苹果的EFI该如何的配置和Config Configuration工具的使用](https://blog.csdn.net/Su_Yi/article/details/93773558)

  [黑苹果安装过程（10.13.617G7024）](https://www.jianshu.com/p/22b5e9db1780)

  [黑果小兵教程](https://blog.daliansky.net/macOS-BigSur-11.5.2-20G95-Release-version-with-OC-0.7.1-and-Clover-5138-and-PE-original-image.html#more)

  [黑果小兵镜像](https://blog.daliansky.net/categories/下载/)

  [系统下载](https://www.apple114.com/pages/macos/)

  [黑果小兵机型efi清单](https://blog.daliansky.net/Hackintosh-long-term-maintenance-model-checklist.html)

  镜像损坏

  ```shell
  ifconfig en0 down
  date 022208102015.20
  ```

  [如何确定英特尔®显卡支持的最大分辨率](https://www.intel.cn/content/www/cn/zh/support/articles/000023781/graphics.html)

  # [黑苹果星球](https://heipg.cn/)

  

  # OpenCore 文件生成

  [OC Gen-X下载](https://www.mfpud.com/opencore/ocgenx/)

  

  # [恢复版安装教程](https://heipg.cn/tutorial/install-macos-via-internet-recovery.html)

  1. 保证PC能联网，不管是有线还是无线都可以
  2. 将一块硬盘扇区全部删除，用DiskGenius在硬盘的最前端创建1个3G的ESP分区，并格式化。将系统恢复文件和EFI文件拷贝进去。
  3. 用EasyUEFI创建EFI引导，引导到第二部的ESP分区的路径/EFI/OC/opencore.efi文件，保存重启
  4. 进入BIOS，将第三部设置的引导设置为第一位。重启
  5. 安装盘名为`NONAME`
  6. 其他正常安装。

  https://macoshome.com/hackintosh/hcourse/6103.html

  # i5 4690k+GTX970

  ![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011445612.png)

  

  # 惠普战66G1Pro双系统

  1. 划分2个独立的磁盘，一个用DiskGenius创建ESP盘格式化，大约2G，另外一个用windows磁盘管理工具，创建一个盘，不要格式化。（[双系统磁盘创建](https://blog.csdn.net/weixin_43971764/article/details/106075438)）
  2. 将EFI文件和恢复版系统拷贝进ESP分区
  3. 用EasyEFI工具创建EFI引导
  4. 其他一样

  # OpenCore Configurator

  [下载地址](https://macoshome.com/hackintosh/htools/2100.html#Down)

  [版本说明](https://gitee.com/shuiyunxc/OpenCore-Configurator)

  [使用教程](https://macx.top/8780.html)

  [vmtools](http://softwareupdate.vmware.com/cds/vmw-desktop/fusion)

  ![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011445614.jpg)

  

  ## 无U盘恢复版教程

  1. 创建ESP分区，建议2G
  2. 将EFI和恢复版系统文件夹拷贝进ESP分区
  3. 启动安装，中间大概重启2-3次
  4. 安装完成
  5. 将EFI文件拷贝进系统盘的ESP分区

  ## 关闭啰嗦模式

  No2.关闭 -v 跑代码（关闭啰嗦模式）

  NVRAM-随机访问寄存器设置 --> 添加 --> UUID：7C436110-AB2A-4BBB-A880-FE41995C9F82

  查找键：`boot-args`

  删除值：`-v`

  ## 切换默认启动磁盘

  启动界面按`Ctrl`+`Enter`

  

  ## 声卡设置

  DeviceProperties-设备属性设置

  设备ID：`PciRoot(0x0)/Pci(0x1b,0x0)`必须存在，否则会无法识别耳机

  ## 显卡设置

  DeviceProperties-设备属性设置

  设备ID：`PciRoot(0x0)/Pci(0x2,0x0)`必须存在，否则会无法驱动显卡

  ## 添加UEFI引导项

  「注意」使用 Clover 引导时，启动文件可选择 BOOTX64.efi 也可以选择 CLOVERX64.efi；但使用 OpenCore 引导时，启动文件必须选择 BOOTx64.efi，否则会造成莫名其妙的问题，切记切记！

  # 系统优化

  [mac OS 防止开机自动挂载磁盘/USB等外设 - 简书 (jianshu.com)](https://www.jianshu.com/p/526975ef197a)

  ## 启动参数说明

  - -wegnoegpu 关闭外置GPU

  ## 打补丁教程

  [【黑苹果系列】小白教程之DSD补丁篇 | 7分钟教你优雅定制最关键的OC补丁(clover通用) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/158786596)

  ## 补丁说明

  - SSDT-OC-XOSI.aml 操作系统补丁，能解决OC无法引导windows。
  - SSDT-plug.aml 加载CPU原生电源管理（开启节能四项），必须
  - [SSDT-EC-USBX](https://link.zhihu.com/?target=https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)（同SSDT-EC）：禁用EC（Embedded Controller）和修复USB充电问题，可选