## 小天才电话手表刷机教程 — 基础篇
- 我们将为您简单的介绍小天才电话手表新机型的简单刷机以及玩法，如adb工具的使用，magisk的刷入等等。
- 我们会确保您看完此教程后能够对Android系统有一个最基本的认识，以及能够成功通过magisk root您的手表，并安装您需要的第三方软件。

# ADB
Android Debug Bridge，简称`adb`，在[android developer](https://developer.android.com/)的adb文档中是这么描述它的：
`adb`是一种多功能命令行工具，可让您与设备进行通信。该`adb`命令有助于各种设备操作，例如安装和调试应用程序。`adb`提供对 Unix shell 的访问，您可以使用它在设备上运行各种命令。它是一个客户端-服务器程序。

这听起来有些难以理解，因为您也没有必要去理解它，如果您对本文中的任何关键名词产生疑惑或兴趣，您都可以在搜索引擎中去搜索它，当然，我们会对其进行简单的解释：`adb`是一款在命令行中运行的，用于对Android设备进行调试的工具，并拥有比一般用户以及程序更高的权限，所以，我们可以使用它对Android设备进行最基本的调试操作。

而在小天才电话手表上启用它，您只需要这么做：
 - 打开拨号盘；
 - 输入`*#0769651#*`；
 - 点按打开adb调试选项。

其次是电脑上的Android SDK Platform-Tools的安装，此工具是 Android SDK 的组件。它包括与 Android 平台交互的工具，主要由`adb`和`fastboot`构成，如果您接触过Android开发，必然会使用到它，因为它包含在Android Studio等IDE中，当然，您可以独立下载，在下方选择对应的版本即可：
 - [Download SDK Platform-Tools for Windows](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
 - [Download SDK Platform-Tools for Mac](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)
 - [Download SDK Platform-Tools for Linux](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)

下载好后进行解压，放置到放置软件的目录后，设定环境变量即可。

随后，使用四点线连接设备到计算机，打开设备管理器，查看是否有连接到Android设备，或者打开终端，输入`adb devices`回车，查看是否有设备连接（如果有Android虚拟机正在运行，如wsa，我们推荐您将其关闭），如果您的电脑是win7或更老，我们推荐您检查您的电脑是否有安装USB驱动程序，或是升级至最新版本：
 - [下载 Google USB 驱动程序 ZIP 文件 (ZIP)](https://dl.google.com/android/repository/usb_driver_r13-windows.zip)

并进行安装，如果安装了驱动后仍然无法连接计算机，请按照以下顺序进行故障排查：
 1. 设备的adb调试是否启用；
 2. 连接电脑使用的线是否具有数据传输功能，即是否有`D+`，`D-`两个数据接口；
 3. 计算机的USB接口是否正常且电压达到标准，接口与数据线是否有积灰；
 4. 驱动程序是否正常且在最新版本；
 5. 是否有Android虚拟机或是其他会扰乱adb连接的软硬件正在运行；

若问题依然存在建议重启设备以及计算机。
因为小天才对于其操作系统的`adb`，`fastboot`等命令的阉割过于严重，命令的使用将在使用时讲解，详细可查询android developer以及命令行命令`adb help`。

# ROOT
在Unix以及类Unix系统，诸如Linux，Android系统下，系统的最高也是最底层的权限，即根权限，超级用户，就是`root`，因此，在折腾Android设备时，为了更高的权限，`root`是绕不开的，不过在Android中，为了用户的安全性，`root`是无法被简单获取的，因此，也诞生了给Android获取root权限的root管理器，常见的有SuperSU，[Magisk](https://github.com/topjohnwu/Magisk)和新兴的[KernelSU](https://kernelsu.org/)，而在本教程中我们使用目前反应性最广，社区生态最完备的Magisk进行`root`，Magisk的优点有：开源免费；使用简单；使用外部挂着的`/system`分区，不对系统本身造成影响；支持通过模块对设备进行修改；拥有完善的社区生态，拥有诸如Magisk Delta等社区改版。

使用Magisk进行root的方法很简单，这里教授简单的线刷方法：
 1. 在设备上安装Magisk Manager软件；
 2. 提取系统的`boot`分区，使用Magisk Manager对提取的`boot.img`镜像进行修补；
 3. 刷入修补后的`boot.img`镜像。

听起来这很简单，但是在小天才电话手表上实现较为困难，因为小天才将其系统中的`fastboot`命令进行了阉割，导致我们无法对设备进行简单的线刷，而是得使用更加底层的`9008`进行刷机。

# Qualcomm HS-USB QD-Loader 9008
Qualcomm Emergency Download mode，通常称为Qualcomm EDL mode，正式名称为Qualcomm HS-USB QD-Loader 9008，在国内被简称为`9008`是高通在片上系统的引导 ROM中实现的一项功能，可用于对设备的分区进行读写烧录。使用它，您首先需要为您的计算机安装Qualcomm HS-USB QD-Loader 9008 Driver，即9008驱动，以及最新版本的QFIL Tool，您可以在这里[下载](https://qfiltool.com/)到。

# 进行root（仅限Z6巅峰版及以后版本）
在一切都准备就绪后，我们推荐您重启计算机，以释放多余的内存，CPU占用和后天程序避免产生不必要的问题，随后，只需要进行一下操作即可：
 1. 下载[Magisk Manager 23.0](https://github.com/topjohnwu/Magisk/releases/download/v23.0/Magisk-v23.0.apk)，[设备分区表文件](https://github.com/ReX-iMoo-Team/imoo_Z6dfb_root/blob/main/prog_emmc_firehose_8937_ddr_hisen.mbn)，另外因为新机型拥有boot校验，之后在刷入时不可以将修补后的`boot.img`刷入`boot`分区，而是刷入恢复分区，即`recovery`分区，并使用`misc.bin`进行引导，所以还得下载修改过的[misc.bin文件](https://github.com/ReX-iMoo-Team/imoo_Z6dfb_root/blob/main/misc/misc.bin);
 2. 为设备安装Magisk，因为`adb`以及`pm`的命令被阉割，因此，如果您的设备未升级至最新版本，可以使用ReX iMoo Team的项目[iMoo Toolkit](https://github.com/ReX-iMoo-Team/iMoo-Toolkit)进行安装（当然，也可以手动安装），或是创建一个32位的Android虚拟机，并为其安装Magisk；
 3. 打开QFIL Tool，选择`flat build`，点击`Select Programmer`选择分区表文件`prog_emmc_firehose_8937_ddr_hisen.mbn`；
 4. 选择`Tools`，点击`Partition Manager`，并点击OK确认，此时手表会关机并进入黑屏的`9008`模式，请确保连接稳定；
 5. 在弹出的窗口中选择`boot`，右键并选择`Manage Partition Data`，并在弹出的窗口中选择`Read Data`；
 6. 依次关闭窗口，手表会自动重启，找到下方日志中提取到的路径，并将其中的镜像文件发送至使用的设备或是虚拟机；
 7. 打开设备或虚拟机上的Magisk Manager，并选择安装Magisk，点击选择修补一个文件（如果在手表上无法进行选择，推荐使用质感文件或mt管理器作为文件选择器），并选择传输过来的镜像文件，等待修补完成，将修补后的镜像文件发送至计算机；
 8. 重复3至4的步骤，并选择`recovery`，右键并选择`Manage Partition Data`，并在弹出的窗口中选择`Load Image`，随后选择修补后的`boot`镜像文件，等待刷入完成后，选择`misc`，并以相同的步骤刷入`misc.bin`即可，随后依次关闭窗口，手表自动开机，打开桌面上的Magisk Manager，在Magisk一栏显示有安装确认`root`成功。

## 鸣谢：
ReX iMoo Team 全体；
特别鸣谢：iMoo Toolkit开发者：Ling，冲之律者，wangzm5773；小天才电话手表高版本root方法发明者：早茶光

## 借物表：
[wiki](https://en.wikipedia.org/wiki/Wiki);
[android developer](https://developer.android.com/);
[Magisk](https://github.com/topjohnwu/Magisk);
[imoo Z6dfb root](https://github.com/ReX-iMoo-Team/imoo_Z6dfb_root)
