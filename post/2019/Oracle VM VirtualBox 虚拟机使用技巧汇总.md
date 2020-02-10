### 目录
- [VirtualBox 是什么](#1)
- [系统镜像下载](#2)
- [解决 VirtualBox 点击「安装增强功能」没有反应](#3)
- [VirtualBox 虚拟机/主机双向拖曳文件，共享粘贴板](#4)
<h3 id="1">VirtualBox 是什么</h3>

Oracle VirtualBox 是由德国 InnoTek 软件公司出品的虚拟机软件，现在则由甲骨文公司进行开发，是甲骨文公司xVM虚拟化平台技术的一部分[^1]。

VirtualBox 同时也是一开源软件，对于我来说软件轻量、功能够用，这便是是我选择  VirtualBox 主要原因。

<h3 id="2">系统镜像下载</h3>

Windows 系统：[下载](http://msdn.itellyou.cn/)
Ubuntu：[下载](https://ubuntu.com/download/desktop)
Linux Mint：[下载](https://linuxmint.com/download.php)
Deepin：[下载](https://www.deepin.org/download/)

<h3 id="3">解决 VirtualBox 点击「安装增强功能」没有反应</h3>

1. 设备→分配光驱→选择虚拟盘；
2. 在 VirtualBox 的安装路径下找到并打开`VBoxGuestAdditions.iso`，；
3. 在虚拟机中，打开文件管理器，找到CD驱动器，点击打开；
4. 可以找到以下三个应用程序：
	- VBoxWindowsAdditions.exe
	- VBoxWindowsAdditions-x86.exe
	- VBoxWindowsAdditions-amd64.exe
5.选择与虚拟机操作系统位数对应的程序安装，安装完成后需要重启一次虚拟机。

附：对于 x86,amd64 这些我也看得头疼，不是很理解这些东西。目前只有一个很粗略认知——凡是 x86 对应至 32 位系统，凡是提到 64 对应至 64 位系统。待后续有机会再深入了解以下这方面的知识。

下方为上述步骤的截图（4P）。

![VirtualBox 点击「安装增强功能」没有反应，步骤1](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213059.png)

![VirtualBox 点击「安装增强功能」没有反应，步骤2](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213505.png)

![VirtualBox 点击「安装增强功能」没有反应，步骤3](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213645.png)

![VirtualBox 点击「安装增强功能」没有反应，步骤4](https://cdn.jsdelivr.net/gh/joeyliu6/Blogger@master/static_files/iljw/img/large/20191101213850.png)

<h3 id="4">VirtualBox 虚拟机/主机双向拖曳文件，共享粘贴板</h3>
1. 安装增强功能；
2. 设备→拖放→双向；
3. 设备→共享粘贴板→双向；

----
1. 2019-11-01：
- 初稿
[^1]:[VirtualBox - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/VirtualBox#cite_note-1)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZXh0ZW5zaW9uczpcbiAgcHJlc2V0Oi
AnJ1xudGFnczogVmlydHVhbEJveFxuIiwiaGlzdG9yeSI6Wy0x
NDIwODMxMjgwXX0=
-->