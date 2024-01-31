### Linux：安装软件

------

[TOC]

##### 01：软件包管理工具

- 一种用于管理计算机软件安装、更新、配置和移除的程序；
- 提供了**对软件包的集中管理，包括查找、下载、安装、升级和卸载软件**。这些工具还可以处理软件包之间的依赖关系，确保系统中的软件能够正确地运行。

###### linux 软件包管理工具

- **APT**（Advanced Package Tool）：一组用于管理Debian和其衍生版（如Ubuntu）软件包的高级工具，提供了用于安装、升级和移除软件包的命令。
- **RPM**：(Red Hat Package Manager)：是一种低级的软件包管理工具，可以用于安装、升级和删除软件包，但它不会自动解决软件包依赖关系，用于在基于 RPM 的Linux发行版（如Red Hat Enterprise Linux、Fedora、CentOS等）。
- **yum**：(Yellowdog Updater Modified)：是一个**基于 rpm 的高级包管理工具，它可以自动解决软件包依赖关系**，并允许从指定的软件仓库中安装、更新和删除软件包。因此，推荐在 Red Hat 系统中使用 yum 进行软件包的管理和安装。

###### macOS 软件包管理工具

- Homebrew：macOS 操作系统的软件包管理器，旨在简化安装、更新和管理开发工具、库和其他应用程序。用户可以通过命令行使用 Homebrew 轻松安装各种软件包，而无需手动下载、编译或处理依赖项。
- Homebrew 还提供了**一种机制来管理系统依赖项**，这对于开发人员和系统管理员来说尤为重要。

##### 02：apt

- 格式：  apt [options] [command] [package ...]
  - **options：**可选，选项包括 -h（帮助），-y（当安装过程提示选择全部为"yes"），-q（不显示安装的过程）等等；
  - **command：**要进行的操作；
  - **package**：安装的包名；
- 常用命令
  - 列出所有已安装的包：apt list --installed
  - 搜索：apt search <keyword>
  - 安装指定的软件命令：apt install <package_name>
  - 更新指定的软件命令：apt update <package_name>
  - 删除软件包命令：apt remove <package_name>
  - 显示软件包具体信息，例如：版本号，安装大小，依赖关系等等：apt show <package_name>
  - 清理不再使用的依赖和库文件: apt autoremove

##### 03：yum

- 格式：yum install package_name
- 常用命令 
  - 列出所有已安装软件包：yum list installed
  - 搜索：yum search keyword
  - 安装：yum install package_name
  - 更新：yum update 
  - 删除：yum remove package_name
  - 列出软件包信息：yum info package_name

##### 04：安装JDK

- 

##### 05：安装Tomcat

##### 06：安装MySQL