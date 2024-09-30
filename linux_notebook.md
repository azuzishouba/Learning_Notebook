# Linux笔记
## Linux简介
Linux是一种开源操作系统，它是由Linus Torvalds在1991年首次发布的。Linux的内核是其核心部分，负责管理硬件和软件之间的交互。由于其开源特性，用户可以自由修改和分发Linux的代码，这使得许多不同的Linux发行版（如Ubuntu、Fedora、Debian等）应运而生。
### Linux发行版
Linux发行版是基于Linux内核的操作系统版本，通常包含内核、系统工具和应用软件。每个发行版可能有不同的目标用户和特性，例如：

1. Ubuntu：用户友好，适合初学者，广泛用于桌面和服务器。
2. Fedora：强调最新技术，适合开发者和技术爱好者。
3. Debian：稳定性强，适合服务器环境，软件库丰富。
4. Arch Linux：灵活性高，适合高级用户，采用滚动更新模式。
### Linux系统启动过程
1. BIOS/UEFI：
  * 当计算机启动时，BIOS（基本输入输出系统）或UEFI（统一可扩展固件接口）首先进行自检，确保硬件正常运行。这一过程包括检查内存、硬盘和其他硬件组件。完成后，BIOS/UEFI会查找启动设备，通常是硬盘或USB驱动器。

2. 引导加载程序（Bootloader）：
  * 一旦BIOS/UEFI找到启动设备，引导加载程序（如GRUB）被加载到内存中。GRUB允许用户选择要启动的操作系统（如果有多个）并加载相应的内核。在此阶段，引导加载程序会读取配置文件，确定内核的位置和启动参数。

3. 加载内核：
    * 引导加载程序加载内核到内存，并初始化基本的硬件控制。内核会执行一系列初始化任务，包括检测和配置硬件设备（如硬盘、网络接口等）。接着，它会挂载根文件系统，通常是一个包含系统文件的分区。

4. 初始化进程（init）：
    * 一旦内核完成初始化，它会启动init进程（或systemd）。init是系统中的第一个用户空间进程，负责启动和管理其他进程。根据Linux的版本，可能会使用不同的初始化系统，例如SysVinit、Upstart或systemd。
      * 运行级别:
        >运行级别0：系统停机状态，系统默认运行级别不能设为0，否则不能正常启动

        >运行级别1：单用户模式（Single-user mode）：用于系统维护，只有超级用户可以登录，没有网络服务。

        >运行级别2：多用户模式（Multi-user mode without networking）：允许多个用户登录，但没有网络服务。

        >运行级别3：完整的多用户模式（Full multi-user mode）：允许多个用户登录，并且提供网络服务（通常是文本模式）。

        >运行级别4：未使用（Unused）：通常保留给用户自定义用途。

        >运行级别5：图形用户界面（Graphical mode）：与运行级别3类似，但启动图形用户界面（如X Window）。

        >运行级别6：重启（Reboot）：重新启动系统。

5. 启动服务：
    * init或systemd根据其配置文件（如/etc/inittab或/etc/systemd/system）启动系统服务。这些服务包括网络服务、登录管理器、图形界面等。systemd使用目标（targets）来管理不同的运行级别，使得服务的启动顺序更为高效。

6. 登录界面：
    * 系统启动完成后，用户会看到登录提示或图形用户界面，允许他们输入用户名和密码进行登录。一旦登录成功，用户会进入他们的桌面环境或命令行界面，开始使用系统。
## Linux的安装
1. 下载VMware:
   * https://ubuntu.com/download/desktop
2. 下载ubuntu ISO镜像：
   * https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Player
3. 启动VMware并创建新的虚拟机:
   * 选择下载好的Ubuntu ISO文件
4. 设置硬盘容量至少30GB，运行CPU核数4核，运行内存8GB
5. 按照默认安装软件
## 升级管理软件
* 通过应用商店管理软件
* Ubuntu可以用过synaptic package manager来管理
## COMMAND LINE
### 定位文件
* which (filename) 
查找文件的路径
  >which python
* whereis (filename) 查找二进制文件、源代码和手册页
  >whereis gcc
* grep "pattern" filename 命令用于在文件中搜索特定模式或字符串
>grep "error" file.txt

>ls -l | grep "txt"
  * | 表示前面命令的输出作为后面命令的输入，可以理解为执行两个命令
### 变更目录
* pwd 展示当前目录
*  

