# OpenCore For X390 4G LTE OC 0.8.0

<div align="center">
<img src="https://img14.360buyimg.com/n0/jfs/t1/122699/10/10858/75075/5f4708e1Eb80b55c6/f276218d450b6840.jpg" width="350px">
</div>

# ThinkpadX390-Opencore-EFI

# 目录

- [介绍](#介绍)
- [下载](#下载)
- [声明](#声明)
- [ThinkPad X390 Hackintosh](#ThinkPadX390_4GLTE-OpenCore-Hackintosh)
  - [测试过的系统](#测试过的系统)
- [设备](#设备)
- [安装及DSDT说明](#安装及DSDT说明)
- [正常工作的部分](#正常工作的部分)
  - [详细的设备驱动情况](#详细的设备驱动情况)
- [已知的问题](#已知的问题)
- [推荐的BIOS配置](#推荐的BIOS配置)
- [补充](#补充)
- [更多帮助](#更多帮助)
- [疑问](#疑问)
- [鸣谢](#鸣谢)

## 介绍

**这包括一个EFI(Opencore)，它在Thinkpad-X390-4GLTE上工作完美**


1. 优化了config.plus部分设置，目前使用体验感觉比较完美。
2. 电源管理使用的 SMCBatteryManager.kext 
3. 所有kext部分全部更新到最新版本。
4. ACPI替换了部分通用SSDT-*.aml文件。
5. 添加了ThinkPad_ClickPad的aml文件，优化小红点和触控的使用体验，但不确定是不是负优化，欢迎你提供使用反馈。
6. 添加了OC的原生苹果主题资源，并默认设置为无选项 duang 声后开机。
7. 添加了PCI设备信息，现在可以在设备管理里查看到PCI硬件的信息了。
8. 键盘快捷键通过SSDT驱动，不用DSDT打补丁了。
9. OC升级到0.8.0了。

## 下载

git clone <https://github.com/abctel/ThinkPadX390_4GLTE-OpenCore.git>

## 声明

你的保修单现在无效了。如果你有任何顾虑，请在我的 EFI 取代你的 EFl 之前做一些研究。我不负责任何损失，包括但不限于内核恐慌，设备无法启动或不能正常工作，存储损坏或数据丢失，原子弹爆炸，第三次世界大战，谷歌和苹果都倒闭，等等

## ThinkPadX390_4GLTE-OpenCore-Hackintosh

可以完美地在ThinkPad X390上安装*Catalina/Big Sur*或者任何之前的版本，如*Mojave , High Sierra , Sierra , EI Captain , Yosemite , Mavericks ……*

### 测试过的系统

**Monterey**

- 12.0.0
- 12.3.1

**Catalina**

(以下版本如无法正常引导使用请切换到10.15.7分支下载)
- 10.15.2
- 10.15.3
- 10.15.4
- 10.15.5
- 10.15.6
- 10.15.7

**Big Sur**

- 11.0.1
- 11.1
- 11.2
- 11.2.1
- 11.2.2
- 11.2.3

## 设备

| 名称 | 细节 |
|:---|:---|
| Computer Model | ThinkPad X390 (39CD) |
| CPU | Intel Core i5-8265U |
| Mainboard |  Lenevo 20Q00039CD（I/O - 9D84 for mobile 8th Gen Intel Core processor family） |
| Displayer | Lenevo LEN4094 ( 13.3 inch  ) |
| Memory | DDR4 2667 Mhz. Onboard 8 GB |
| NVMe SSD | WDC PC SN720 SDBQNTY-500G-1001 (500G/SSD) |
| Integrated Graphics | Intel UHD Graphics 620 |
| Ethernet |  Intel(R) Ethernet Connection (6) I219-V |
| Sound Card | Realtek High Defination Audio@Intel Intel Smart Sound Technology Audio Controller (layoutid:11) |
| Wireless Card |  Intel(R) Wireless-AC 9560 160MHz |
| LTE 4G | |

## 安装及DSDT说明

从这个版本起，取消dsdt，所有补丁基于HotPatch进行修补，这样适用型可能更广，基本上8th CPU的笔记本都可以一试，尤其是ThinkPad系列的。

## 正常工作的部分

### 详细的设备驱动情况

#### CPU

功能正常。变频正常。

#### 电池

电池电量显示正常。（未测试睡眠时拔下充电器，电池是否准确，欢迎测试反馈）

#### 以太网

功能正常。（需要一个Dock）

#### 显卡

集成显卡的型号是`Intel UHD Graphics 620`，仿冒`Intel UHD Graphics 630 (Mobile)`
TYPE-C 与`Intel UHD Graphics 620` 连接，功能正常。支持`2K@60Hz` & `4K@30Hz` 。（可能正常，代码使用的是上个版本的，最近抽空测试一下）

#### 声卡

用AppleALC正常驱动`layout-id: 11`. 一切功能都正常。

#### 键盘

功能正常，

#### 硬盘

NVMe 功能正常并且开启了TRIM.

#### 蓝牙

功能正常。（不过intel网卡的蓝牙使用体验很一般啊，确实没有免驱的好用）

#### 触控板和小红点

功能正常。Trackpoint和ultranav也工作正常

#### 无线网卡

2.4G,5G功能部分正常.**感谢  [@zxystd's AirportItlwm](https://github.com/OpenIntelWireless/itlwm)**

#### 内置摄像头

通过USB内建成功，FaceTime和ipad测试使用正常。

#### 睡眠

睡眠完美支持。

#### Type-C

两个Type-C接口使用正常，雷电功能因没有设备，所以未测试。

#### 睡眠LED灯光

电源键和小红点呼吸灯可根据睡眠情况自动切换呼吸、常量模式。

#### 快捷键

- 睡眠快捷键正常（默认fn+4，因技术不精，还没搞明白如何调整为fn+F12对应键盘图标）
- 背光控制正常
- 音量控制正常

#### 背光状态

背光状态记录正常，睡眠前，唤醒后亮度保持一致。

## 已知的问题

- 隔空投送和接力无法正常工作
- 4GLTE 网卡 无法驱动。

## 推荐的BIOS配置

>在进入BIOS之前，请确保您已经禁用了Windows登录密码，因为在按照以下方式配置BIOS后，您可能无法在Windows上使用“PIN”登录。

- Security
  - Intel SGX: Software Controlled
- Boot
  - Boot Mode: UEFI Only

## 补充

### 声卡方面的疑问解答

如果你在从Windows启动到macOS后遇到了一些奇怪的问题(比如找不到音频设备)，你应该重启回到Windows，并进行冷重启(先关机再启动)回到macOS。在那之后你的音频设备应该回来了。

> 如果你在你的Hacintosh上使用带有Boot Camp模式的并行桌面，你不应该在macOS中直接重启
> 同样的原因。您应该在并行桌面中手动关闭Windows，然后重新启动macOS(先关闭再启动)。

注意⚠️：目前作者单MacOS系统使用中，这是上个版本遇到的问题和解决方法，请参考使用。

## 更多帮助

- 如需了解更多，请移步原作者的交流贴 [远景论坛]( http://bbs.pcbeta.com/viewthread-1852139-1-1.html)

## 疑问

- 如果你有任何问题，尽管在Github上提出来，我会尽量帮助你!
- 我们只接受在GitHub issues的bug报告.
  
## 鸣谢

- [Apple](https://www.apple.com) for [macOS](https://www.apple.com/macos)
- [@zxystd](https://github.com/zxystd) for developing [itlwm](https://github.com/OpenIntelWireless/itlwm)
- [@Acidanthera](https://github.com/acidanthera) for basic kexts.
- [@BAndysc](https://github.com/BAndysc) for [Trackpoint and UltraNavs drive](https://github.com/BAndysc/VoodooPS2/tree/master)
- [@SukkaW](https://github.com/SukkaW) for [Text and Templates](https://github.com/SukkaW/ThinkPad-E480-Hackintosh)
