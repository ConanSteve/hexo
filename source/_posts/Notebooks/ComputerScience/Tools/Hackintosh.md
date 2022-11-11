---
title: 黑苹果安装教程
date: 2022-04-01 10:00:00
description: 个人的黑苹果安装教程，包括以下机型：惠普zhan66G1Pro、台式机技嘉Z97D3H+i56790K+GTX970Gaming
author: 陌上人如玉
tag: Mac
---

# 前言
本教程参考资料主要来源于[黑苹果星球](https://heipg.cn/)，目前推荐使用OpenCore安装。
安装的EFI文件有2种来源，一种是直接使用别人相似的配置（建议），另外一种是使用OC Gem-x自己生成。

  
# 工具下载地址
* [Hackintool](https://www.mfpud.com/tools/hackintool/)
* [opencore](https://macoshome.com/hackintosh/uefistart/2456.html#Down)
## OpenCore Configurator
* [OCC 黑苹果星球](https://heipg.cn/?cat=6&s=opencore++configurator)
* [OpenCore Configurator OCC](https://macoshome.com/hackintosh/htools/2100.html#Down)

## OC Gen-X
[OC Gen-X下载地址](https://www.mfpud.com/opencore/ocgenx/)

# OpenCore EFI文件生成

[一键生成黑苹果 OpenCore EFI 文件：OC.Gen-X](https://heipg.cn/tutorial/one-key-opencore-efi.html)

  
# 安装教程
  ## 网络恢复版
  [恢复版安装教程](https://heipg.cn/tutorial/install-macos-via-internet-recovery.html)

  1. 保证PC能联网，不管是有线还是无线都可以
  2. 将一块硬盘扇区全部删除，用DiskGenius在硬盘的最前端创建1个3G的ESP分区，并格式化。将系统恢复文件和EFI文件拷贝进去。
  3. 用EasyUEFI创建EFI引导，引导到第二部的ESP分区的路径/EFI/OC/opencore.efi文件，保存重启
  4. 进入BIOS，将第三部设置的引导设置为第一位。重启
  5. 安装盘名为`NONAME`
  > 默认是`NONAME`，如果要修改，需要在恢复镜像文件夹内添加文本文件，修改为需要显示的内容，然后将文本文件名修改为`.contentDetails`
  6. 其他正常安装。

  https://macoshome.com/hackintosh/hcourse/6103.html
  
  ## U盘刻录版教程
  
  
# 个人安装实例
  ## Z97D3H + i5 4690k + GTX970

  ![BIOS设置](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011445612.png)

  

  ## 惠普战66G1Pro双系统

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

  

## 修改主题
[教程](https://heipg.cn/tutorial/opencore-modern-picker.html)
* [霓虹ROG主题](https://heipg.cn/tutorial/opencore-070-rog-theme-neon.html)
* [元气少女主题](https://heipg.cn/apps/opencore-theme-pinkdream.html)

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

# CPU对比
![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202211021740545.png)

  # 系统优化
  
  [完美黑苹果](https://apple.sqlsec.com/7-%E5%AE%8C%E7%BE%8E%E9%BB%91%E6%9E%9C/7-1/)

  [mac OS 防止开机自动挂载磁盘/USB等外设 - 简书 (jianshu.com)](https://www.jianshu.com/p/526975ef197a)

  ## 启动参数
  不管是OCG还是黑苹果星球的配置文件，引导不了多数原因是启动参数的问题，启动参数在`NVRAM`中的`7C436110-AB2A-4BBB-A880-FE41995C9F82`中修改，以下是几个参数模板：
  * 内置主题可启动
  `-v keepsyms=1 debug=0x100 agdpmod=pikera -alcbeta alcid=1`
  * 黑苹果星球原版
  `-v debug=0x100 keepsyms=1`
  * 4690k黑苹果星球+内置主题-可启动版
  `-v debug=0x100 keepsyms=1 agdpmod=pikera -alcbeta alcid=1`
  * 4690k黑苹果星球+自定义主题-可启动版
  `-v debug=0x100 keepsyms=1 agdpmod=pikera -alcbeta alcid=1 npci=0x2000` 
  * 4690k江波配置
  `-v keepsyms=1 agdpmod=pikera -alcbeta alcid=1 npci=0x2000 igfxonln=1 -cdfon  -lilubetaall`
  ### 启动参数说明
  |启动参数|参数说明|备注|
  |---|---|---|
  | **-v** |用于打开跑码模式，方便排错|
  |-wegnoegpu|关闭外置GPU，笔记本无法驱动独显需要关闭独显的使用|
  |**debug=0x100**|打开用于发生严重错误（Kernel Panic）后禁止自动重启，将停留在出错位置，方便排错||
  |**keepsyms=1**|用于辅助上一个启动参数，可以对错误原因提供更多有用的信息||
  | nvda_drv=1|使用 Nvidia 显卡||
  | -no_compat_check |关闭兼容性检查||
  |**agdpmod=pikera**|用于解决 Navi 核心的显卡启动黑屏问题，如果你是 Polaris(RX400/RX500) 或 Vega(56/64) 显卡则无需此项|
  |**npci=0x2000**|X99、X299 平台以及部分 AMD 平台需要添加 npci=0x2000 或 npci=0x3000，当跑代码卡在 PCI Start Configuration 时使用|Z97D3H主板不开这个，使用`ResetNVRAMEntry.efi`和`ToggleSipEntry.efi`会出现无法启动的问题|
  |**alcid=11** |是 AppleALC.kext 用于驱动声卡的参数，演示机型板载 ALC1220 芯片，可使用 layout-id 11 驱动声卡，其它芯片可参考 [AppleALC.kext](https://heipg.cn/drivers?drivers=Audio) 提供的[解码器支持表单和驱动更新日志](https://heipg.cn/drivers/applealc-1-5-1.html#AppleALC-%E6%94%AF%E6%8C%81%E7%9A%84%E7%BC%96%E8%A7%A3%E7%A0%81%E5%99%A8)||
  
  ### AppleACL.kext相关启动参数
  |启动参数|参数说明|备注|
  |-|-|-|
  |alcid = layout|设置值layout-id||
  |-alcbeta|在不受支持的系统（通常是未发行或旧的系统）上启用AppleALC||
  |-alcoff|禁用自身||
  
  ### Z97D3H+4690K
  * 板载声卡：Realtek ALC 1150
  ![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202211101204787.png)
  
  
  


  ## 打补丁教程

  [【黑苹果系列】小白教程之DSD补丁篇 | 7分钟教你优雅定制最关键的OC补丁(clover通用) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/158786596)

  ## 补丁说明

  - SSDT-OC-XOSI.aml 操作系统补丁，能解决OC无法引导windows。
  - SSDT-plug.aml 加载CPU原生电源管理（开启节能四项），必须
  - [SSDT-EC-USBX](https://link.zhihu.com/?target=https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)（同SSDT-EC）：禁用EC（Embedded Controller）和修复USB充电问题，可选
  
  ## OpenCore无法引导windows
  将`booter-启动设置`里面的`SyncRuntimePermissions`勾上即可
![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204212014663.png)

## 快速更改SIP
打开config.plist文件，前往config – Misc – Security – AllowToggleSip 勾选保存

## 查看当前EFI版本

使用 Hackintool 工具，直接打开就能看到，如下图位置

Hackintool 下载：https://www.mfpud.com/tools/hackintool/

![](https://cdn.mfpud.com/static/2022/06/1654619962-9edd5ecd8c3a9e1.png)

## 仿冒ID
[6650xt](https://www.gaofumei.net/mac-os-x/11181.html)

## 使用USBToolBox定制USB驱动
* [黑果魏叔教程](http://www.imacosx.cn/6875.html)
* [黑苹果星球教程](https://heipg.cn/tutorial/customize-usb-port-windows.html)

## 关闭硬盘自动挂载
[MacOS下禁止开机自动挂载分区 [/etc/fstab]](https://blog.csdn.net/qq_38202733/article/details/109631753)
`sudo vim /etc/fstab`
`UUID=4B73513D-98E2-4C3E-84A8-773F3DE233D9 none ntfs rw,noauto`
  # Others

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

  # Reference