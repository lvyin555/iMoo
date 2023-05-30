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
